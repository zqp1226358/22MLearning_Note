## CNN卷积神经网络

### 一、CNN的设计原理

- Receptive Field 不需要看整张图片，神经元只看图片的一小部分
- Parameter Sharing 同样的pattern可以出现在图片的不同地方，所以神经元之间可以共用参数，对Filter而言，一个Filter扫过整张图片，这个就是Convolutional Layer
- 对像素下采样不会改变物体

#### Spatial transformer

平移不变性、尺度不变性、旋转不变性

spatial transformer就是为了克服CNN的旋转、缩放不变性的缺点

Interpolation 采用插值法将离散问题变成连续问题



### 二、为什么用了验证集还是overfitting



### 三、鱼与熊掌可以兼得的机器学习

