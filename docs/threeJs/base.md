# threeJS基础
## 基础介绍

在进行进一步的three组装前，我们必须掌握threeJS的基本知识及原理
传统三维图像制作中，开发人员需要使用OpenGL（Open Graphics Library）图形程序接口进行开发，从而在 PC、工作站、超级计算机等硬件设备上实现高性能、极具冲击力的高视觉表现力图形处理软件的开发。openGL并不适合直接在浏览器端运行，因此在OpenGL基础上，webGL通过统一的、标准的、跨平台的OpenGL接口，这种绘图技术标准允许把JavaScript和OpenGL ES 2.0结合在一起，通过增加OpenGL ES 2.0的一个JavaScript绑定，webGL可以为HTML5 Canvas提供硬件三维加速渲染，这样Web开发人员就可以借助系统显卡来在浏览器里更流畅地展示三维场景和模型了，还能创建复杂的导航和数据视觉化。

threeJS是一个webgl为基础的库，对webGL的3D渲染工具方法与渲染循环封装的js库，省去与繁琐底层接口的交互，通过threeJS就可以快速生成三维模型

![](https://img.alicdn.com/tfs/TB1orYpbAL0gK0jSZFtXXXQCXXa-714-360.jpg)


因此，要创建模型，我们需要场景（scene）、相机(camera)和渲染器(renderer)三样东西，他们是图形渲染得重要部分。

![](https://img.alicdn.com/tfs/TB1TtpvdoD1gK0jSZFGXXbd3FXa-1000-588.jpg)


## 坐标系

Three.js 的坐标系是遵循右手坐标系，如下图：

![右手坐标系](https://img.alicdn.com/tfs/TB1iQpwdeH2gK0jSZJnXXaT1FXa-255-220.jpg)

> 坐标系的原点在画布中心（canvas.width / 2, canvas.height / 2）。我们可以通过 Three.js 提供的 THREE.AxisHelper() 辅助方法将坐标系可视化。

```
  // 创建坐标轴（RGB颜色 分别代表 XYZ轴）
  var axisHelper = new THREE.AxisHelper(6)

  // 将立方体网格加入到场景中
  scene.add(axisHelper)
```

## demo

```
  // 引入 Three.js 库
  <script src="https://unpkg.com/three"></script>

  function init () {
      // 获取浏览器窗口的宽高，后续会用
      var width = window.innerWidth
      var height = window.innerHeight

      // 创建一个场景
      var scene = new THREE.Scene()

      // 创建一个具有透视效果的摄像机
      var camera = new THREE.PerspectiveCamera(45, width / height, 0.1, 800)

      // 设置摄像机位置，并将其朝向场景中心
      camera.position.x = 10
      camera.position.y = 10
      camera.position.z = 30
      camera.lookAt(scene.position)

      // 创建一个 WebGL 渲染器，Three.js 还提供 <canvas>, <svg>, CSS3D 渲染器。
      var renderer = new THREE.WebGLRenderer()

      // 设置渲染器的清除颜色（即背景色）和尺寸。
      // 若想用 body 作为背景，则可以不设置 clearColor，然后在创建渲染器时设置 alpha: true，即 new THREE.WebGLRenderer({ alpha: true })
      renderer.setClearColor(0xffffff)
      renderer.setSize(width, height)

      // 创建一个长宽高均为 4 个单位长度的立方体（几何体）
      var cubeGeometry = new THREE.BoxGeometry(4, 4, 4)

      // 创建材质（该材质不受光源影响）
      var cubeMaterial = new THREE.MeshBasicMaterial({
          color: 0xff0000
      })

      // 创建一个立方体网格（mesh）：将材质包裹在几何体上
      var cube = new THREE.Mesh(cubeGeometry, cubeMaterial)

      // 设置网格的位置
      cube.position.x = 0
      cube.position.y = -2
      cube.position.z = 0

      // 将立方体网格加入到场景中
      scene.add(cube)

      // 将渲染器的输出（此处是 canvas 元素）插入到 body 中
      document.body.appendChild(renderer.domElement)

      // 渲染，即摄像机拍下此刻的场景
      renderer.render(scene, camera)
  }
  init()

```

