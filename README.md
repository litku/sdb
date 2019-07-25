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
