# threeJS基础
基础介绍

在进行进一步的three组装前，我们必须掌握threeJS的基本知识及原理
传统三维图像制作中，开发人员需要使用OpenGL（Open Graphics Library）图形程序接口进行开发，从而在 PC、工作站、超级计算机等硬件设备上实现高性能、极具冲击力的高视觉表现力图形处理软件的开发。openGL并不适合直接在浏览器端运行，因此在OpenGL基础上，webGL通过统一的、标准的、跨平台的OpenGL接口，这种绘图技术标准允许把JavaScript和OpenGL ES 2.0结合在一起，通过增加OpenGL ES 2.0的一个JavaScript绑定，webGL可以为HTML5 Canvas提供硬件三维加速渲染，这样Web开发人员就可以借助系统显卡来在浏览器里更流畅地展示三维场景和模型了，还能创建复杂的导航和数据视觉化。

threeJS是一个webgl为基础的库，对webGL的3D渲染工具方法与渲染循环封装的js库，省去与繁琐底层接口的交互，通过threeJS就可以快速生成三维模型

![](https://img.alicdn.com/tfs/TB1orYpbAL0gK0jSZFtXXXQCXXa-714-360.jpg)


因此，要创建模型，我们需要场景（scene）、相机(camera)和渲染器(renderer)三样东西，他们是图形渲染得重要部分



