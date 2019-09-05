# LitkuSDB Core

试灯宝核心。

## API

### Litku.Version

```javascript
coonsole.log(Litku.Version); // 0.0.1
```

### Litku.Extend()

无使用说明。

### Litku.Create(options) => renderer

同步创建渲染器实例。`options` 参数配置，请阅读 <a href="#options">options 参数列表</a>。

```javascript
// 创建渲染实例
const renderer = LitkuSDB.Create(options);

// 销毁实例
renderer.destroy();
renderer = null;
```

### Litku.CreateAsync(options, callback) => void

异步创建渲染器实例。`options` 参数配置，请阅读 <a href="#options">options 参数列表</a>。

```javascript
LitkuSDB.CreateAsync(options, function(err, renderer) {
  if (err) {
    return;
  }

  // 销毁实例
  renderer.destroy();
  renderer = null;
});
```

### renderer.updateLamp(options, callback) => void

这个操作：

- 不更新场景
- 不更新环境光
- 不更新光通量
- 不更新色温

只会更新灯具 ies 数据。

```javascript
// 创建渲染实例
const renderer = LitkuSDB.Create(__full_options__);
const callback = (err) => {
  closeLoading();
  if (err) {
    // TODO 更新失败
    return;
  }
  // TODO 更新成功
};

// 方式一：只有灯具id，内部先拉取灯具数据，再更新灯具
showLoading();
renderer.updateLamp(
  {
    load: true,
    product: {
      pid: '5d22ebc5badc4d69887117cf', // product id
      mid: '', // option product model id
    },
  },
  callback,
);

// 方式二：已知灯具数据，直接更新灯具
showLoading();
renderer.updateLamp(
  {
    load: false,
    product: {
      // 详细内容，请阅读 options 参数列表
      name: '产品名称',
      ambient_light: 30,
      angle: '15',
      ies: {
        15: {
          beam_angle: '15',
          cct: 3000,
          dat: 'http://cdn.lightank.com/ies/dat/5d36a999b802f200d87799aa_15.dat',
          ies: 'http://cdn.lightank.com/files/2019/0723/813181de10d342b2652fe41a76fe960da8e1f7da.ies',
          intensity: 500,
          power: 7,
        },
        38: {
          beam_angle: '38',
          cct: 4000,
          dat: 'http://cdn.lightank.com/ies/dat/5d36a999b802f200d87799aa_38.dat',
          ies: 'http://cdn.lightank.com/files/2019/0723/5d2f471e73fc0cee899762b5d42786f1533c8ed7.ies',
          intensity: 725,
          power: 7,
        },
      },
      scene: 1,
      thumbnail: 'http://1t.click/G9N',
      url: 'http://1t.click/G9S',
    },
  },
  callback,
);
```

<span id="options"></span>

## options 参数列表

```javascript
let options = {
  container: document.querySelector('#sdb-container-wrapper'), // canvas and ctrl container, default document.body
  scene: 1, // 强制使用场景1。若同时指定，以 scene 为准。
  load: true, // 是否远程加载product数据。远程加载时只提供 product:{pid:'', [mid:'']}
  // light product 数据
  product: {
    // 如果load=false，不需要传递下面的参数；如果load=true，需要传递下面的参数
    pid: '5d22ebc5badc4d69887117cf', // product id
    mid: '', // option product model id

    // 如果load=false，需要传递下面的参数；如果load=true，不需要传递下面的参数
    name: '产品名称', // product name
    ambient_light: 30, // 环境光照度, number
    angle: '15', // 默认光束角，原定位beam_angle，现修改为angle。代码同时兼容beam_angle与angle。
    // 灯具产品的ies数据
    ies: {
      15: {
        beam_angle: '15',
        cct: 3000, // 请确保这个参数为数值类型
        dat: 'http://cdn.lightank.com/ies/dat/5d36a999b802f200d87799aa_15.dat',
        ies: 'http://cdn.lightank.com/files/2019/0723/813181de10d342b2652fe41a76fe960da8e1f7da.ies',
        intensity: 500, // 请确保这个参数为数值类型
        power: 7,
      },
      38: {
        beam_angle: '38',
        cct: 4000,
        dat: 'http://cdn.lightank.com/ies/dat/5d36a999b802f200d87799aa_38.dat',
        ies: 'http://cdn.lightank.com/files/2019/0723/5d2f471e73fc0cee899762b5d42786f1533c8ed7.ies',
        intensity: 725,
        power: 7,
      },
    },
    scene: 1, // 默认场景编号
    thumbnail: 'http://1t.click/G9N', // 产品缩略图链接
    url: 'http://1t.click/G9S', // 灯具产品详情页链接
  },
  // control panel config (GUI config)
  ctrl: {
    visible: true, // 是否显示控制面板，PC,平板端时默认显示，手机端时默认不显示
    stats: false, // 是否显示FPS，默认不显示，可通过控制面板开关操作显示与隐藏
    changeLampButton: true, // 是否展示更换灯具按钮

    fullScreenButton: true, // 是否显示全屏按钮
    fullScreen: false, // 是否全屏显示，默认不全屏
    moveButton: true, // 是否显示移动按钮
    move: true, // 是否允许部件移动
    rotateButton: true, // 是否显示旋转按钮
    rotate: true, // 是否允许部件旋转
    scaleButton: true, // 是否显示部件缩放按钮
    scale: true, // 是否允许部件缩放
    viewButton: true, // 是否显示视角切换按钮
    view: 'perspective|side|top|front', // 视角, 默认 perspective(透视角)

    screenshotButton: true, // 是否显示截图按钮
    feedbackButton: true, // 是否显示截图按钮
  },
  onClick: function(targetType, optionData) {
    // targetType => 点击元素的类型
    // optionData => 部分类型会传递数据
    // 类型列表：
    // changeLamp|changeScene
    // fullScreen|move|rotate|scale|
    // perspectiveView|sideView|topView|frontView|
    // screenShot|feedback|
    // toggleControl|closeControl|
    // resetLights|resetItems
  },
  onError: function(code, error) {
    // code  => 错误代码
    // error => 错误对象实例
    // × 1 => 入口参数错误，不符合参数规范
    // √ 2 => 获取灯具数据失败，在loadLampData方法判断
    // √ 3 => 灯具数据错误，不包含正确的IES数据，在init方法判断
  },
};
```

## 使用示例

- 已知灯具数据，直接渲染：`examples/sync.html`
- 异步加载灯具数据，再执行渲染：`examples/async.html`
