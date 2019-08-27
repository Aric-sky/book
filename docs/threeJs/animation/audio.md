我们从文档目录中竟然发现有 Audio 音频对象，为什么 Three.js 不是游戏引擎，却带个音频组件呢？原来这个音频也是 3D 的，它会受到摄像机的距离影响：

声源离摄像机的距离决定着声音的大小。
声源在摄像机左右侧的位置分别决定着左右扬声器声音的大小。
我们可以到 [官方案例](https://threejs.org/examples/#misc_animation_authoring) 亲自体验一下 Audio 的效果。