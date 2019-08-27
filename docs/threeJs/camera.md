
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


## 透视摄像机参数

THREE.PerspectiveCamera(fov, aspect, near, far) 具有 4 个参数，具体解释如下：

  | 参数        | 描述           |
  | ------------- |:-------------|
  | fov      | fov 表示视场，即摄像机能看到的视野。比如，人类有接近 180 度的视场，而有些鸟类有接近 360 度的视场。但是由于计算机不能完全显示我们能够所看到的景象，所以一般会选择一块较小的区域。对于游戏而言，视场大小通常为 60 ~ 90 度。推荐默认值为：50 |
  | aspect      | 指定渲染结果的横向尺寸和纵向尺寸的比值。在我们的示例中，由于使用窗口作为输出界面，所有使用的是窗口的长宽比。推荐默认值：window.innerWidth / window.innerHeight      |
  | near | 指定从距离摄像机多近的距离开始渲染。推荐默认值：0.1      |
  | far | 指定摄像机从它所处的位置开始能看到多远。若过小，那么场景中的远处不会被渲染；若过大，可能会影响性能。推荐默认值：1000      |


[可参考文章](https://blog.csdn.net/qq_31976161/article/details/84166746)
