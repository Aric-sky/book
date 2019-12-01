## 材质

创建几何体时通过指定几何体的顶点和三角形的面确定了几何体的形状，另外还需要给几何体添加皮肤才能实现物体的效果，材质就像物体的皮肤，决定了物体的质感。常见的材质有如下几种：

![材质类型](https://img.alicdn.com/tfs/TB1xqfEoxn1gK0jSZKPXXXvUXXa-634-470.png)

- 基础材质：以简单着色方式来绘制几何体的材质，不受光照影响。
- 深度材质：按深度绘制几何体的材质。深度基于相机远近端面，离近端面越近就越白，离远端面越近就越黑。
- 法向量材质：把法向量映射到RGB颜色的材质。
- Lambert材质：是一种需要光源的材质，非光泽表面的材质，没有镜面高光，适用于石膏等表面粗糙的物体。
- Phong材质：也是一种需要光源的材质，具有镜面高光的光泽表面的材质，适用于金属、漆面等反光的物体。
- 材质捕获：使用存储了光照和反射等信息的贴图，然后利用法线方向进行采样。优点是可以用很低的消耗来实现很多特殊风格的效果；缺点是仅对于固定相机视角的情况较好。

下图是使用不同贴图实现的效果：

![贴图效果](https://img.alicdn.com/tfs/TB1S_vBopY7gK0jSZKzXXaikpXa-809-391.png)


## 材质类型

Mesh 好比一个包装工，它将『可视化的材质』粘合在一个『数学世界里的几何体』上，形成一个『可添加到场景的对象』。
当然，创建的材质和几何体可以多次使用（若需要）。而且，包装工不止一种，还有 Points（点集）、Line（线/虚线） 等。

```
function init () {
    // 获取浏览器窗口的宽高，后续会用
    var width = window.innerWidth
    var height = window.innerHeight

    // 创建一个场景
    var scene = new THREE.Scene()

    // 创建一个具有透视效果的摄像机
    var camera = new THREE.PerspectiveCamera(45, width / height, 0.1, 800)

    // 设置摄像机位置，并将其朝向场景中心
    camera.position.x = 20
    camera.position.y = 10
    camera.position.z = 30
    camera.lookAt(scene.position)

    // 创建一个 WebGL 渲染器，Three.js 还提供 <canvas>, <svg>, CSS3D 渲染器。
    var renderer = new THREE.WebGLRenderer({
      antialias: true // 开启抗齿锯效果
    })

    // 设置渲染器的清除颜色（即背景色）和尺寸
    renderer.setClearColor(0xffffff)
    renderer.setSize(width, height)

    // 创建一个聚光灯，并将其设置恰当位置后添加到场景中
    var spotLight = new THREE.SpotLight(0xffffff)
    spotLight.position.set(10, 50, 20)
    scene.add(spotLight)

    // 创建一个长宽高为 4 的立方体
    var cubeGeometry = new THREE.BoxGeometry(4, 4, 4)

    // 创建点集（Points）材质
    var cubePointMaterial = new THREE.PointsMaterial({
      color: 0xff0000,
      size: 0.4
    })

    // 创建线（Line）材质
    var cubeLineMaterial = new THREE.LineBasicMaterial({
      color: 0x00ff00
    })

    // 创建 Lambert 材质：会对场景中的光源作出反应，但表现为暗淡，而不光亮。
    var cubePlaneMaterial = new THREE.MeshLambertMaterial({
      color: 0x0000ff,
    })

    // 立方体的多种表现形式：点集、线、面
    var pointCube = new THREE.Points(cubeGeometry, cubePointMaterial)
    var lineCube = new THREE.Line(cubeGeometry, cubeLineMaterial)
    var meshCube = new THREE.Mesh(new THREE.BoxGeometry(4, 4, 4), cubePlaneMaterial)

    pointCube.position.set(-8, 0, 0)
    meshCube.position.set(8, 0, 0)
    
    // 一次性向场景添加三种表现形式
    scene.add(pointCube, lineCube, meshCube)

    // 将渲染器的输出（此处是 canvas 元素）插入到 body
    document.body.appendChild(renderer.domElement)

    // 渲染，即摄像机拍下此刻的场景
    renderer.render(scene, camera)
}

```