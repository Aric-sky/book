> 自适应屏幕（窗口）大小

```
  window.addEventListener('resize', onResize, false)

  function onResize () {
      // 设置透视摄像机的长宽比
      camera.aspect = window.innerWidth / window.innerHeight
      // 摄像机的 position 和 target 是自动更新的，而 fov、aspect、near、far 的修改则需要重新计算投影矩阵（projection matrix）
      camera.updateProjectionMatrix()
      // 设置渲染器输出的 canvas 的大小
      renderer.setSize(window.innerWidth, window.innerHeight)
  }
```








