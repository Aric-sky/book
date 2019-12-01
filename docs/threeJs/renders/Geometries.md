### 几何体
计算机内的3D世界是由点组成，两个点能够组成一条直线，三个不在一条直线上的点就能够组成一个三角形面，无数三角形面就能够组成各种形状的几何体。

![正方体](https://img.alicdn.com/tfs/TB1bQbxoqL7gK0jSZFBXXXZZpXa-418-376.png)

以创建一个简单的立方体为例，创建简单的立方体需要添加8个顶点和12个三角形的面，创建顶点时需要指定顶点在坐标系中的位置，添加面的时候需要指定构成面的三个顶点的序号，第一个添加的顶点序号为0，第二个添加的顶点序号为1…

创建立方体的代码如下：

```
var geometry = new THREE.Geometry();

// 添加8个顶点
geometry.vertices.push(new THREE.Vector3(1, 1, 1));
geometry.vertices.push(new THREE.Vector3(1, 1, -1));
geometry.vertices.push(new THREE.Vector3(1, -1, 1));
geometry.vertices.push(new THREE.Vector3(1, -1, -1));
geometry.vertices.push(new THREE.Vector3(-1, 1, -1));
geometry.vertices.push(new THREE.Vector3(-1, 1, 1));
geometry.vertices.push(new THREE.Vector3(-1, -1, -1));
geometry.vertices.push(new THREE.Vector3(-1, -1, 1));

// 添加12个三角形的面
geometry.faces.push(new THREE.Face3(0, 2, 1));
geometry.faces.push(new THREE.Face3(2, 3, 1));
geometry.faces.push(new THREE.Face3(4, 6, 5));
geometry.faces.push(new THREE.Face3(6, 7, 5));
geometry.faces.push(new THREE.Face3(4, 5, 1));
geometry.faces.push(new THREE.Face3(5, 0, 1));
geometry.faces.push(new THREE.Face3(7, 6, 2));
geometry.faces.push(new THREE.Face3(6, 3, 2));
geometry.faces.push(new THREE.Face3(5, 7, 0));
geometry.faces.push(new THREE.Face3(7, 2, 0));
geometry.faces.push(new THREE.Face3(1, 3, 4));
geometry.faces.push(new THREE.Face3(3, 6, 4));
```

### 图形类型
> 目前 Three.js 一共提供了 22 个 Geometry，除了 EdgesGeometry、ExtrudeGeometry、TextGeometry、WireframeGeometry，上面涵盖 18 个，它们分别是底层的 planeGeometry 和以下 17 种（顺序与上述案例一一对应，下同）：


| BoxGeometry（长方体）| CircleGeometry（圆形）| ConeGeometry（圆锥体）| CylinderGeometry（圆柱体）|
| ------------------ | -------------------- | ------------------- | ------------------- |
| DodecahedronGeometry（十二面体）| IcosahedronGeometry（二十面体）| LatheGeometry（让任意曲线绕 y 轴旋转生成一个形状，如花瓶）| OctahedronGeometry（八面体）|
| ParametricGeometry（根据参数生成形状）| PolyhedronGeometry（多面体）| RingGeometry（环形）|ShapeGeometry（二维形状）|
| SphereGeometry（球体）| TetrahedronGeometry（四面体）| TorusGeometry（圆环体）| TorusKnotGeometry（换面纽结体）|
| TubeGeometry（管道）| \ | \ | \ |


剩余的 TextGeometry、EdgesGeometry、WireframeGeometry、ExtrudeGeometry 我们单独拿出来解释：

| / | TextGeometry | / |
| ------------------ | -------------------- | ------------------- |
| EdgesGeometry | WireframeGeometry | ExtrudeGeometry |

如案例所示，EdgesGeometry 和 WireframeGeometry 更多地可能作为辅助功能去查看几何体的边和线框（三角形图元）。

ExtrudeGeometry 则是按照指定参数将一个二维图形沿 z 轴拉伸出一个三维图形。

TextGeometry 则需要从外部加载特定格式的字体文件（可在 typeface.js 网站上进行转换）进行渲染，其内部依然使用 ExtrudeGeometry 对字体进行拉伸，从而形成三维字体。另外，该类字体的本质是一系列类似 SVG 的指令。所以，字体越简单（如直线越多），就越容易被正确渲染。

以上就是目前 Three.js 提供的几何体，当然，这些几何体的形状也不仅于此，通过改变参数即能生成更多种类的形状，如 THREE.CircleGeometry 可生成扇形。

另外，通过 console.log 查看任意一个 geometry 对象可发现，在 Three.js 中的几何体基本上是三维空间中的点集（即顶点）和这些顶点连接起来的面组成的。以立方体为例（widthSegments、heightSegments、depthSegments 均为 1 时）：

一个立方体有 8 个顶点，每个顶点通过 x、y 和 z 坐标来定义。
一个立方体有 6 个面，而每个面都包含两个由 3 个顶点组成的三角形。
对于 Three.js 提供的几何体，我们不需要自己定义这些几何体的顶点和面，只需提供 API 指定的参数即可（如长方体的长宽高）。当然，你仍然可以通过定义顶点和面来创建自定义的几何体。如：

```
  var vertices = [
      new THREE.Vector3(1, 3, 1),
      new THREE.Vector3(1, 3, -1),
      new THREE.Vector3(1, -1, 1),
      new THREE.Vector3(1, -1, -1),
      new THREE.Vector3(-1, 3, -1),
      new THREE.Vector3(-1, 3, 1),
      new THREE.Vector3(-1, -1, -1),
      new THREE.Vector3(-1, -1, 1)
  ]

  var faces = [
      new THREE.Face3(0, 2, 1),
      new THREE.Face3(2, 3, 1),
      new THREE.Face3(4, 6, 5),
      new THREE.Face3(6, 7, 5),
      new THREE.Face3(4, 5, 1),
      new THREE.Face3(5, 0, 1),
      new THREE.Face3(7, 6, 2),
      new THREE.Face3(6, 3, 2),
      new THREE.Face3(5, 7, 0),
      new THREE.Face3(7, 2, 0),
      new THREE.Face3(1, 3, 4),
      new THREE.Face3(3, 6, 4)
  ]

  var geometry = new THREE.Geometry()
  geometry.vertices = vertices
  geometry.faces = faces
  geomtry.computeFaceNormals()
```

上述代码需要注意的点有：

- 正面和反面
> 创建面时顶点的顺序，因为顶点顺序决定了某个面是面向摄像机还是背向摄像机。顶点的顺序是逆时针则是面向摄像机，反之则是背向摄像机。
出于性能的考虑，Three.js 认为几何体在整个生命周期都不会更改。若出现更改（如某顶点的位置），则需要告诉 geometry 对象的顶点需要更新 geometry.verticesNeedUpdate = true。更多关于需要主动设置变量来开启更新的事项，可查看官方文档的 [How to update things](https://threejs.org/docs/index.html#manual/en/introduction/How-to-update-things)。



Three.js 提供的 18 个几何体：
```
function init () {
    // 获取浏览器窗口的宽高，后续会用
    var width = window.innerWidth
    var height = window.innerHeight

    // 创建一个场景
    var scene = new THREE.Scene()

    // 创建一个具有透视效果的摄像机
    var camera = new THREE.PerspectiveCamera(45, width / height, 0.1, 1000)
    // var camera = new THREE.OrthographicCamera(width / - 10, width / 10, height / 10, height / -10, 1, 1000)

    // 设置摄像机位置，并将其朝向场景中心
    camera.position.set(0, 125, 125)
    camera.lookAt(new THREE.Vector3(0,0,0))

    // 创建一个 WebGL 渲染器，Three.js 还提供 <canvas>, <svg>, CSS3D 渲染器。
    var renderer = new THREE.WebGLRenderer({
      antialias: true // 开启抗齿锯
    })

    // 设置渲染器的清除颜色（即背景色）和尺寸
    renderer.setClearColor(0xffffff)
    renderer.setSize(width, height)

    // 将渲染器的输出（此处是 canvas 元素）插入到 body
    document.body.appendChild(renderer.domElement)

    // 添加环境光，提亮整个场景
    var ambientLight = new THREE.AmbientLight(0x777777)
    scene.add(ambientLight)

    // 添加聚光灯（可产生投影的光）
    var spotLight = new THREE.SpotLight(0xffffff)
    spotLight.position.set(-40, 40, 50)
    scene.add(spotLight)

    var cameraY = 45
    function render () {
      // 渲染，即摄像机拍下此刻的场景
      renderer.render(scene, camera)
      
      // 各个网格（mesh）绕自身中心的 y 轴自转
      if (meshs.length > 0) {
        for (var i = 0; i < meshs.length; i++) {
          meshs[i].rotation.y += 0.01
        }
      }

      requestAnimationFrame(render)
    }

    // 创建一个平面 PlaneGeometry(width, height, widthSegments, heightSegments)
    var planeGeometry = new THREE.PlaneGeometry(120, 140, 1, 1)

    // 创建 Lambert 材质：会对场景中的光源作出反应，但表现为暗淡，而不光亮。
    var planeMaterial = new THREE.MeshLambertMaterial({
      color: 0xffffff
    })
    var plane = new THREE.Mesh(planeGeometry, planeMaterial)

    // 以自身中心为旋转轴，绕 x 轴顺时针旋转 45 度
    plane.rotation.x = -0.5 * Math.PI
    plane.position.set(0, -4, 0)

    scene.add(plane)

    var meshs = addGeometries()
    render()
    
    // 初始化摄像机插件（用于拖拽旋转摄像机，产生交互效果）
    var orbitControls = new THREE.OrbitControls(camera)
    orbitControls.autoRotate = true

    function addGeometries () {
      var geoms = []
      var meshs = []
      // 共 22 个形状，除了 EdgesGeometry、ExtrudeGeometry、TextGeometry、WireframeGeometry，下面涵盖 17 个（PlaneGeometry在上面）
      // Box 长方体
      geoms.push(new THREE.BoxGeometry(8, 8, 8))

      // Circle 圆形
      geoms.push(new THREE.CircleGeometry(8, 32))

      // Cone 圆锥体
      geoms.push(new THREE.ConeGeometry( 8, 20, 32 ))

      // Cylinder 圆柱体
      geoms.push(new THREE.CylinderGeometry(5, 5, 20, 32))

      // Dodecahedron 十二面体
      geoms.push(new THREE.DodecahedronGeometry(8))

      // Icosahedron 二十面体
      geoms.push(new THREE.IcosahedronGeometry(8))

      // Lathe 让任意曲线绕 y 轴旋转生成一个形状，如花瓶
      var lathePoints = [];
      for ( var i = 0; i < 10; i ++ ) {
        lathePoints.push( new THREE.Vector2( Math.sin( i * 0.2 ) * 5 + 2.5, ( i - 5 ) * 2 ) );
      }
      geoms.push(new THREE.LatheGeometry( lathePoints ))

      // Octahedron 八面体
      geoms.push(new THREE.OctahedronGeometry(8))

      // Parametric：根据参数生成形状，THREE.ParametricGeometries.klein 是 ParametricGeometries.js 库提供
      geoms.push(new THREE.ParametricGeometry(THREE.ParametricGeometries.klein, 10, 10))

      var verticesOfCube = [
          -1,-1,-1,    1,-1,-1,    1, 1,-1,    -1, 1,-1,
          -1,-1, 1,    1,-1, 1,    1, 1, 1,    -1, 1, 1,
      ]

      var indicesOfFaces = [
          2,1,0,    0,3,2,
          0,4,7,    7,3,0,
          0,1,5,    5,4,0,
          1,2,6,    6,5,1,
          2,3,7,    7,6,2,
          4,5,6,    6,7,4
      ]

      // Polyhedron 多面体
      geoms.push(new THREE.PolyhedronGeometry( verticesOfCube, indicesOfFaces, 8, 1 ))

      // Ring 环形
      geoms.push(new THREE.RingGeometry( 3, 8, 16 ))

      // Shape 二维形状(心形)
      var x = 0, y = 0;
      var heartShape = new THREE.Shape();

      heartShape.moveTo( x + 5, y + 5 );
      heartShape.bezierCurveTo( x + 5, y + 5, x + 4, y, x, y );
      heartShape.bezierCurveTo( x - 6, y, x - 6, y + 7,x - 6, y + 7 );
      heartShape.bezierCurveTo( x - 6, y + 11, x - 3, y + 15.4, x + 5, y + 19 );
      heartShape.bezierCurveTo( x + 12, y + 15.4, x + 16, y + 11, x + 16, y + 7 );
      heartShape.bezierCurveTo( x + 16, y + 7, x + 16, y, x + 10, y );
      heartShape.bezierCurveTo( x + 7, y, x + 5, y + 5, x + 5, y + 5 );

      geoms.push(new THREE.ShapeGeometry( heartShape ))

      // Sphere 球体
      geoms.push(new THREE.SphereGeometry( 8, 24, 24 ))

      // Tetrahedron 四面体
      geoms.push(new THREE.TetrahedronGeometry(8))

      // Torus 圆环体
      geoms.push(new THREE.TorusGeometry( 6, 2, 16, 100 ))

      // TorusKnot 环面纽结体
      geoms.push(new THREE.TorusKnotGeometry( 6, 2, 100, 16 ))

      // Tube 管道
      var points = [];
      for (var i = 0; i < 5; i++) {
          var randomX = -10 + Math.round(Math.random() * 20);
          var randomY = -7 + Math.round(Math.random() * 20);
          var randomZ = -10 + Math.round(Math.random() * 20);

          points.push(new THREE.Vector3(randomX, randomY, randomZ));
      }

      geoms.push(new THREE.TubeGeometry(new THREE.CatmullRomCurve3(points), 20, 2, 8, false))

      // 为几何体添加材质
      var j = 0
      for (var i = 0; i < geoms.length; i++) {
        var cubeMaterial = new THREE.MeshLambertMaterial({
          wireframe: true,
          color: Math.random() * 0xffffff
        })

        var materials = [
          new THREE.MeshLambertMaterial({
            color: Math.random() * 0xffffff,
            flatShading: THREE.FlatShading,
            side: THREE.DoubleSide
          }),
          new THREE.MeshBasicMaterial({
            color: 0x000000,
            wireframe: true
          })
        ]

        var mesh = THREE.SceneUtils.createMultiMaterialObject(geoms[i], materials)

        meshs.push(mesh)

        mesh.position.x = -36 + ((i % 4) * 24);
        mesh.position.y = 4;
        mesh.position.z = -36 + (j * 24);

        if ((i + 1) % 4 == 0) {
          j++
        }
        scene.add(mesh)
      }
      console.log(meshs.length)

      return meshs
    }
```