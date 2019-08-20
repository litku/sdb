# LitkuSDB Core

试灯宝核心。

## API

<!-- ## Litku.Version -->
<details><summary><b>Litku.Version</b></summary><div>

```javascript
coonsole.log(Litku.Version); // 0.0.1
```

</div></details>

<!-- ## Litku.Create(options) -->
<details><summary><b>Litku.Create(options)</b></summary><p>
    
`options` 参数配置，请阅读 <a href="#options">options参数列表</a>。

```javascript
// 创建渲染实例
const renderer = LitkuSDB.Create(options);

// 销毁实例
renderer.destroy();
renderer = null;
```

</p></details>

<!-- ## Litku.Extend() -->
<details><summary><b>Litku.Extend()</b></summary><p>

无使用说明。

</p></details>

<!-- ## options 参数列表 -->
<h2 id="options">options 参数列表</h2>

```javascript
let options = {
  container: document.querySelector('#sdb-container-wrapper'), // canvas and ctrl container, default document.body
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
    scene: 1, // 默认场景编号
    thumbnail: 'http://1t.click/G9N', // 产品缩略图链接
    url: 'http://1t.click/G9S', // 灯具产品详情页链接
  },
  // control panel config (GUI config)
  ctrl: {
    visible: true, // 是否显示控制面板，PC,平板端时默认显示，手机端时默认不显示
    stats: false, // 是否显示FPS，默认不显示，可通过控制面板开关操作显示与隐藏

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
  onClick: function(targetType) {
    // 点击元素的类型 targetType: 
    // changeLamp|
    // fullScreen|move|rotate|scale|
    // perspectiveView|sideView|topView|frontView|
    // screenShot|feedback|
    // toggleControl|closeControl|
  },
};
```

## 使用示例

- 已知灯具数据，直接渲染：`examples/sync.html`
- 异步加载灯具数据，再执行渲染：`examples/async.html`
