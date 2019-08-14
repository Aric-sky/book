
## 相机
作为场景中人眼的角色，决定场景中模型的远近、高度角度等参数

threeJS提供正投影相机、透视相机、立体相机等多种相机模式，现实常用的为前两种
正投影相机（OrthographicCamera）

```
  new THREE.OrthographicCamera( left, right, top, bottom, near, far )
```
分别设置相机的左边界，右边界，上边界，下边界，远面，近面
左/右边界：左右边界渲染范围，超出部分不做渲染处理
上/下边界：上下边界渲染范围，超出部分不做渲染处理
近面：基于相机所在位置开始渲染
远面：基于相机位置，一直渲染场景到远面，后面的部分不做渲染处理

![](https://img.alicdn.com/tfs/TB1lnTqbrj1gK0jSZFuXXcrHpXa-800-432.jpg)

## 透视相机（PerspectiveCamera）

```
  new THREE.PerspectiveCamera( fov, aspect, near, far )
```
分别设置相机的视场角度，长宽比，近面，远面
视场：从相机位置看到的部分场景，就如人类有180度视场，某些昆虫却拥有360度视场。
长宽比：水平视场和垂直视场之间的比例
近面：从距离相机多远的距离开始渲染场景（近面越小，离相机越近）
远面：相机可以看到最远的距离（过低只看到部分场景，过高则影响模型渲染）

![](https://img.alicdn.com/tfs/TB1HrjnbpY7gK0jSZKzXXaikpXa-800-386.jpg)
