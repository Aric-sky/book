## JavaScript 性能监测器 stats.js

stats.js 为开发者提供了易用的性能监测功能，它目前支持四种模式：

- 帧率
- 每帧的渲染时间
- 内存占用量
- 用户自定义

![](https://img.alicdn.com/tfs/TB1APV8doT1gK0jSZFhXXaAtVXa-667-103.jpg)


### stats.js 介绍

1. stats.js 是一个 Three.js 开发的辅助库，这个库同样也是 Three.js 作者开发的。
2. stats.js 主要用于检测动画运行时的帧数。
3. GitHub 主页地址：https://github.com/mrdoob/stats.js

### 使用步骤

1. 首先在页面的 `<head>` 标签中引入这个辅助库。

```
  <script src="https://cdnjs.cloudflare.com/ajax/libs/stats.js/r16/Stats.min.js"></script>
```

2. 然后在网页上添加 `<div>` 元素，用于显示统计图形。

```
  <div id="Stats-output"></div>
```

3. 接着初始化统计对象，并将该对象添加到 `<div>` 元素中。这里要注意 setMode() 方法参数：

  - 设置为 0：检测的是画面每秒传输帧数（fps）
  - 设置为 1：检测每帧的渲染时间

4. 为了能够统计 stats 对象画面何时被重新渲染，我们还需要在重新渲染时调用 stats.update() 方法。


### 完整代码

```
  <!DOCTYPE html>
  <html>
  <head>
      <meta charset="utf-8">
      <title>demo</title>
      <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/three.js/109/three.min.js"></script>
      <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/stats.js/r16/Stats.min.js"></script>
      <style>
          body {
              margin: 0;
              overflow: hidden;
          }
      </style>
  </head>
  <body>
  
  <!-- 用于显示统计图形 -->
  <div id="Stats-output"></div>
  
  <!-- 作为Three.js渲染器输出元素 -->
  <div id="WebGL-output"></div>
  
  <!-- 第一个 Three.js 样例代码 -->
  <script type="text/javascript">
  
      //网页加载完毕后会被调用
      function init() {
  
          //初始化统计对象
          var stats = initStats();
  
          //创建一个场景（场景是一个容器，用于保存、跟踪所要渲染的物体和使用的光源）
          var scene = new THREE.Scene();
  
          //创建一个摄像机对象（摄像机决定了能够在场景里看到什么）
          var camera = new THREE.PerspectiveCamera(45,
            window.innerWidth / window.innerHeight, 0.1, 1000);
  
          //设置摄像机的位置，并让其指向场景的中心（0,0,0）
          camera.position.x = -30;
          camera.position.y = 40;
          camera.position.z = 30;
          camera.lookAt(scene.position);
  
          //创建一个WebGL渲染器并设置其大小
          var renderer = new THREE.WebGLRenderer();
          renderer.setClearColor(new THREE.Color(0xEEEEEE));
          renderer.setSize(window.innerWidth, window.innerHeight);
  
          //创建一个立方体
          var cubeGeometry = new THREE.BoxGeometry(4, 4, 4);
          //将线框（wireframe）属性设置为true，这样物体就不会被渲染为实物物体
          var cubeMaterial = new THREE.MeshLambertMaterial({color: 0xff0000});
          var cube = new THREE.Mesh(cubeGeometry, cubeMaterial);
          cube.castShadow = true;
  
          //设置立方体的位置
          cube.position.x = -4;
          cube.position.y = 3;
          cube.position.z = 0;
  
          //将立方体添加到场景中
          scene.add(cube);
  
          //创建点光源
          var spotLight = new THREE.SpotLight(0xffffff);
          spotLight.position.set(-40, 60, -10);
          spotLight.castShadow = true;
          scene.add(spotLight);
  
          //将渲染的结果输出到指定页面元素中
          document.getElementById("WebGL-output").appendChild(renderer.domElement);
  
          //渲染场景
          renderScene();
  
          //渲染场景
          function renderScene() {
              //通知stats画面已被重新渲染了
              stats.update();
              //选装立方体
              cube.rotation.x += 0.02;
              cube.rotation.y += 0.02;
              cube.rotation.z += 0.02;
  
              //通过requestAnimationFrame方法在特定时间间隔重新渲染场景
              requestAnimationFrame(renderScene);
              //渲染场景
              renderer.render(scene, camera);
          }
  
          //初始化统计对象
          function initStats() {
              var stats = new Stats();
              //设置统计模式
              stats.setMode(0); // 0: fps, 1: ms
              //统计信息显示在左上角
              stats.domElement.style.position = 'absolute';
              stats.domElement.style.left = '0px';
              stats.domElement.style.top = '0px';
              //将统计对象添加到对应的<div>元素中
              document.getElementById("Stats-output").appendChild(stats.domElement);
              return stats;
          }
      }
  
      //确保init方法在网页加载完毕后被调用
      window.onload = init;
  </script>
  </body>
  </html>

```










