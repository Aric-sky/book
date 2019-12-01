## 纹理

在生活中纯色的物体还是比较少的，更多的是有凹凸不平的纹路或图案的物体，要用Three.JS实现这些物体的效果，就需要使用到纹理贴图。3D世界的纹理是由图片组成的，将纹理添加在材质上以一定的规则映射到几何体上，几何体就有了带纹理的皮肤。

## 普通纹理贴图

![地图](https://img.alicdn.com/tfs/TB1PadyoKL2gK0jSZPhXXahvXXa-827-265.png)


在这个示例中使用上图左侧的地球纹理，在球形几何体上进行贴图就能制作出一个地球。
代码如下：

```
/* 创建地球 */
function createGeom() {
    // 球体
    var geom = new THREE.SphereGeometry(1, 64, 64);
    // 纹理
    var loader = new THREE.TextureLoader();
    var texture = loader.load('./earth.jpg');
    // 材质
    var material = new THREE.MeshLambertMaterial({
        map: texture
    });
    var earth = new THREE.Mesh(geom, material);
    return earth;
}
```

## 反面贴图实现全景视图

![反面贴图实现全景视图](https://img.alicdn.com/tfs/TB12wpzoSf2gK0jSZFPXXXsopXa-645-160.png)

这个例子是通过在球形几何体的反面进行纹理贴图实现的全景视图，实现原理是这样的：创建一个球体构成一个球形的空间，把相机放在球体的中心，相机就像在一个球形的房间中，在球体的里面（也就是反面）贴上图片，通过改变相机拍摄的方向，就能看到全景视图了。

材质默认是在几何体的正面进行贴图的，如果想要在反面贴图，需要在创建材质的时候设置side参数的值为THREE.BackSide，代码如下：

```
/* 创建反面贴图的球形 */
// 球体
var geom = new THREE.SphereGeometry(500, 64, 64);
// 纹理
var loader = new THREE.TextureLoader();
var texture = loader.load('./panorama.jpg');
// 材质
var material = new THREE.MeshBasicMaterial({
    map: texture,
    side: THREE.BackSide
});
var panorama = new THREE.Mesh(geom, material);
```

## 凹凸纹理贴图

![凹凸纹理](https://img.alicdn.com/tfs/TB1B64yoUT1gK0jSZFrXXcNCXXa-510-311.png)

凹凸纹理利用黑色和白色值映射到与光照相关的感知深度，不会影响对象的几何形状，只影响光照，用于光敏材质（Lambert材质和Phong材质）。

如果只用上图左上角的砖墙图片进行贴图的话，就像一张墙纸贴在上面，视觉效果很差，为了增强立体感，可以使用上图左下角的凹凸纹理，给物体增加凹凸不平的效果。

凹凸纹理贴图使用方式的代码如下：

```
// 纹理加载器
var loader = new THREE.TextureLoader();
// 纹理
var texture = loader.load( './stone.jpg');
// 凹凸纹理
var bumpTexture = loader.load( './stone-bump.jpg');
// 材质
var material =  new THREE.MeshPhongMaterial( {
    map: texture,
    bumpMap: bumpTexture
} );
```

## 法线纹理贴图

![法线纹理](https://img.alicdn.com/tfs/TB1kSXwoFY7gK0jSZKzXXaikpXa-514-316.png)

法线纹理也是通过影响光照实现凹凸不平视觉效果的，并不会影响物体的几何形状，用于光敏材质（Lambert材质和Phong材质）。上图左下角的法线纹理图片的RGB值会影响每个像素片段的曲面法线，从而改变物体的光照效果。

使用方式的代码如下：

```
// 纹理
var texture = loader.load( './metal.jpg');
// 法线纹理
var normalTexture = loader.load( './metal-normal.jpg');
var material =  new THREE.MeshPhongMaterial( {
    map: texture,
    normalMap: normalTexture
} );
```

## 环境贴图

![环境贴图](https://img.alicdn.com/tfs/TB1oQpyoRv0gK0jSZKbXXbK2FXa-781-448.png)

环境贴图是将当前环境作为纹理进行贴图，能够模拟镜面的反光效果。在进行环境贴图时需要使用立方相机在当前场景中进行拍摄，从而获得当前环境的纹理。立方相机在拍摄环境纹理时，为避免反光效果的小球出现在环境纹理的画面上，需要将小球设为不可见。

环境贴图的主要代码如下：

```
/* 立方相机 */
var cubeCamera = new THREE.CubeCamera( 1, 10000, 128 );
/* 材质 */
var material = new THREE.MeshBasicMaterial( {
    envMap: cubeCamera.renderTarget.texture
});
/* 镜面反光的球体 */
var geom = new THREE.SphereBufferGeometry( 10, 32, 16 );
var ball = new THREE.Mesh( geom, material );
// 将立方相机添加到球体
ball.add( cubeCamera );
scene.add( ball );

// 立方相机生成环境纹理前将反光小球隐藏
ball.visible = false;
// 更新立方相机，生成环境纹理
cubeCamera.update( renderer, scene );
balls.visible = true;

// 渲染
renderer.render(scene, camera);

```

## 加载外部3D模型

Three.JS已经内置了很多常用的几何体，如：球体、立方体、圆柱体等等，但是在实际使用中往往需要用到一些特殊形状的几何体，这时可以使用3D建模软件制作出3D模型，导出obj、json、gltf等格式的文件，然后再加载到Three.JS渲染出效果。

![3D模型](https://img.alicdn.com/tfs/TB1uF8yoKL2gK0jSZPhXXahvXXa-418-552.png)

上图的椅子是在3D制图软件绘制出来的，chair.mtl是导出的材质文件，chair.obj是导出的几何体文件，使用材质加载器加载材质文件，加载完成后得到材质对象，给几何体加载器设置材质，加载后得到几何体对象，然后再创建场景、光源、摄像机、渲染器等进行渲染，这样就等得到如图的效果。主要的代码如下


```
// .mtl材质文件加载器
var mtlLoader = new THREE.MTLLoader();
// .obj几何体文件加载器
var objLoader = new THREE.OBJLoader();

mtlLoader.load('./chair.mtl', function (materials) {
    objLoader.setMaterials(materials)
        .load('./chair.obj', function (obj) {
            scene.add(obj);
            …
        });
});
```


