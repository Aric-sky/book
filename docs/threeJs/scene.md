### 场景
scene是场景作为实体代入必要的背景，它是承载所有模型的容器，它允许渲染模型和位置;
里面能放置对象（Objects）、灯光（Lights）、摄像机（Cameras）等。

### 创建场景：

```
  new THREE.Scene()

```

### 场景的属性：

```
fog（雾）：
创建fog：
1. fog(color:int, near:float, far:float)
color：雾的颜色。
near：开始应用雾的最小距离。活动相机中小于“近”单位的对象不会受到雾的影响。默认为1。
far：雾停止计算和应用的最大距离。远离活动摄像机的物体不会受到雾的影响。默认为1000。

2. FogExp2(color:int, density:float)
color：
density：定义雾的浓度变化速率。默认0.00025。
fog的属性：
name：

fog的方法：
.clone()：拷贝雾。
.toJson():以json格式回雾的数据。
.overrideMaterial：
如果不为空，它将强制场景中的所有内容都用该材质渲染。默认值为空。
.autoUpdate：Boolean
默认值为真。如果设置，渲染器将检查每一帧场景及其对象是否需要矩阵更新。否则，你必须自己维护场景中的所有矩阵。
.background：Object
如果不为空，设置渲染场景时使用的背景，并且总是首先渲染。可以设置为设置透明颜色的颜色、覆盖画布的纹理或立方体纹理。默认值为空。
```

### 场景的方法

.toJson(): 以json格式返回场景的数据。



