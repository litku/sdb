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
<h2 id="options"><code>options</code> 参数列表</h2>

```javascript
let options = {
  container: document.querySelector('#sdb-container-wrapper'), // canvas and ctrl container, default document.body
  load: true, // 是否远程加载product数据。远程加载时需提供product:{pid:'', [mid:'']}
  // light product
  product: {
    pid: '5d22ebc5badc4d69887117cf', // product id
    mid: '', // option product model id
    name: '产品名称', // product name
    url: null, // 产品官网链接
    scene: 1, // 场景编号
    ambient_light: 30, // 环境光照度, number
    beam_angle: 15, // 产品型号光束角或默认光束角，如果load true，不要传递这个参数
    // product ies，如果load true，不需要传递这个参数
    ies: {
        15: {
            cct: 3000,
            power: 7,
            intensity: 500,
            beam_angle: "15",
            ies: "http://cdn.lightank.com/files/2019/0723/813181de10d342b2652fe41a76fe960da8e1f7da.ies",
            dat: "http://cdn.lightank.com/ies/dat/5d36a999b802f200d87799aa_15.dat"
        },
        38: {
            cct: 4000,
            power: 7,
            intensity: 725,
            beam_angle: "38",
            ies: "http://cdn.lightank.com/files/2019/0723/5d2f471e73fc0cee899762b5d42786f1533c8ed7.ies",
            dat: "http://cdn.lightank.com/ies/dat/5d36a999b802f200d87799aa_38.dat"
        }
    },
  },
  fullScreenButton: true, // 是否显示全屏按钮
  fullScreen: false, // 是否全屏显示，默认不全屏
  rotateButton: true, // 是否显示旋转按钮
  rotate: true, // 是否允许部件旋转
  zoomButton: true, // 是否显示绽放按钮
  zoom: true, // 是否允许绽放
  viewButton: true, // 是否显示视角切换按钮
  view: 'perspective|front|side|top', // 视角, 默认 perspective(透视角)
  moveButton: true, // 是否显示移动按钮
  move: true, // 是否允许部件移动
  screenShot: true, // 是否显示截图按钮
  // control panel config (GUI config)
  ctrl: {
    visible: true, // 是否显示控制面板，PC,平板端时默认显示，手机端时默认不显示
    stats: false, // 是否显示FPS，默认不显示，可通过控制面板开关操作显示与隐藏
  },
};
```

## 使用示例

- 已知灯具数据，直接渲染：`examples/sync.html`
- 异步加载灯具数据，再执行渲染：`examples/async.html`
