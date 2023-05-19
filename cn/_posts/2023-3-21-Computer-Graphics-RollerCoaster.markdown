---
lng_pair: MS_2_CG_2
title: 基于OpenGL的过山车渲染
author: 张靖祥
category: 课程项目
tags: [Graphics, C/C++]
img: ":MS_2_CG_2/demo.gif"
date: 2023-3-01 00:00:00
---

### 过山车渲染项目

<!-- outline-start -->这是计算机图形学课程的第二个作业。 在这个项目中，我将通过 OpenGL 渲染过山车。输入为是一组点的坐标，我会使用样条插值来创建过山车的轨道，并使用 OpenGL 进行渲染。<!-- outline-end -->

成果展示：

![demo](:MS_2_CG_2/demo.gif){:data-align="center"}


项目配置环境

- Windows系统

- visual studio 2017或更高版本

第三方库：

- GLUT： 用于窗口创建
- GLEW：用于OpenGL核心库
- GLM：OpenGL数学运算库
- jpeg：图像输入输出

项目特色：

- 使用B样条曲线，在间断点达到2阶连续
- 通过样条曲线来构建轨道
- 使用物理模拟来控制过山车的速度
- 渲染轨道阴影
- 渲染天空盒

键盘与鼠标控制：

- 拖动鼠标：
  - 拖动鼠标左键：模型沿 x、y 轴旋转
  - 拖动鼠标中键：模型沿 z 轴旋转
- Control + 拖动鼠标：
  - Control + 拖动鼠标左键：模型沿 x、y 轴平移
  - Control + 拖动鼠标中键: 模型沿 z 轴平移
- Shift + 拖动鼠标：
  - Shift + 拖动鼠标左键：模型沿 x、y 轴缩放
  - Shift + 拖动鼠标中键: 模型沿 z 轴缩放
- 键盘按键：
  - 数字键 1： 静态模式，在这个模式中你将会看到过山车轨道模型
  - 数字键 2： 过山车模式，在这个模式中你将会驾驶过山车
  - 数字键 3： 切换渲染风格，一共有3个渲染风格：
    - 彩色模式：轨道顶点的颜色取决于顶点的方向
    - Phong 模型渲染: 使用 Phong 模型渲染轨道
    - Phong 模型 + 纹理渲染: 最终的完整版渲染模型

如何使用？

1. 点击 rollerCoaster.sln 运行项目
2. demonstration 文件夹展示了渲染结果
3. release 文件夹包含了项目编译后的版本。运行此文件，你需要提供 1 个额外参数，即高度图的路径。你也可以点击 render.bat 来运行演示用例
4. Bin文件夹包含了visual studio的输出。请注意项目运行需要用到 glew32.dll 与 freeglut.dll，所以你需要确保这两个文件在项目输出的目录中

点击[此次](https://github.com/Jingxiang-Zhang/RollerCoasterRender)获取项目源代码。


---

技术细节：

### 1. 样条曲线的方向

在相机在过山车上移动时，除了样条曲线各个顶点的位置外，我们还需要知道样条曲线的切线和法线。这里我将相机放在样条的位置上，面向位置 + 切线方向，并使用法线作为向上向量。 具体为：LookAt(position.x, position.y, position.z, position.x + tangent.x, position.y + tangent.y, position.z + tangent.z, normal.x, normal.y, normal.z);

通过使用 Sloan 算法，渲染结果有以下两方面的问题：

1. 算法选取任意向量 V 作为初始状态。然而，该算法的结果依赖于初始状态，也就是说这个算法是一个随机算法，我们需要一个确定的算法。

2. 在轨道上移动时，镜头前的赛道有坡度，看起来不够真实。

![1.1](:MS_2_CG_2/1.1.png){:data-align="center"}

比如我们上面有这样一条轨道，我们要骑在轨道上方，也就是说法线应该指向上。但是 Sloan 的算法无法得到这样的结果。

所以，我是这样做的：

![1.2](:MS_2_CG_2/1.2.png){:data-align="center"}

假设P1的切线为v1，P1的下一个顶点的切线为v2。 P1 的 binormal 应为 b1 = v1 × v2。 P1 的法线应为 n1 = v1 × b1。

![1.3](:MS_2_CG_2/1.3.png){:data-align="center"}

直到这里，您可能会注意到法线总是指向凹陷区域的外侧，上面的样条显示了这个方法是如何失败的，法线会在凹凸部分的连接处突然翻转。所以，我们需要检查并翻转法线，我通过以下算法实现的：

```pseudocode
for normal in normal_list:
	if previous_normal * normal < 0:  // the joint position
		normal = - normal // then flip the normal
	previous_normal = normal
```

![1.4](:MS_2_CG_2/1.4.png){:data-align="center"}



### 2. 轨道顶点与如何处理轨道样条曲线的接缝

下面的黑线是样条曲线，绿线是轨迹的顶点，轨迹是根据样条曲线的法线和 binomial 线生成的。

![2.1](:MS_2_CG_2/2.1.png){:data-align="center"}

但请注意，为了计算样条顶点的法线，我使用了 2 个连续切线的叉积，相当于 3 个顶点位置。 3个连续的顶点位置可以确定一个二次函数。 为了使二次函数在关节处平滑，样条至少需要 C2 连续。

当使用 C1 连续的 Catmull Rom 样条曲线时，我得到以下轨迹，关节位置拼接错误。

![2.2](:MS_2_CG_2/2.2.png){:data-align="center"}

这个问题可以用C2连续样条来解决，这里我使用 B 样条曲线。唯一的问题是 B 样条没有通过我们提供的顶点。在这里，natural 样条可以解决这个问题，但由于它有很多复杂的计算，本项目没有使用。

![2.3](:MS_2_CG_2/2.3.png){:data-align="center"}



### 3. 生成均匀间隔的样条曲线

课程提到了递归细分算法以生成匀速样条，但是由于函数调用，使用递归算法很慢。这里我想通过使用基于栈的算法来改进这个算法。 您可以查看 rollerCoaster.cpp 文件中的 splineInterpolationRS 函数中的代码。 这是我如何使用堆栈生成匀速样条的伪代码：

```c++
start_point = fun(0) // calculate the start point position when u = 0
spline_list.push_back(start_point) // spline_list store all the vertex of the spline
stack<pair<float, float>> subdivision_tree // the stack structure tree
subdivision_tree.push({0, 1}) // push the initial line segment
while (!subdivision_tree.empty()) {
first_u, second_u = subdivision_tree.top()
subdivision_tree.pop() // get the top item
	first_point = fun(first_u); second_point = fun(second_u); 
	if distance(first_point, second_point) < threshold: // push into the list
		spline_list.push_back(second_point)
	else:
		middle_u = (first_u + second_u) / 2
		subdivision_tree.push({middle_u, second_u})
		subdivision_tree.push({first_u, middle_u })

```

我以goodRide.sp为例，生成B样条。首先，我使用 BF 算法，每两个点插值 50 个顶点。 然后，我使用上面提到的匀速算法，选择 0.1 作为阈值。 这是我从我创建的两条样条曲线中得到的统计数据：

1. BF 算法

- 总计生成 4500 条线段

- 总长度：154.481

- 平均长度：0.0686584

- 长度标准差：0.0200213

- 最大长度：0.196158

- 最小长度：0.0253739

2. 均匀间隔算法

- 总计生成 4363 条线段

- 总长度：154.48

- 平均长度：0.0707974

- 长度标准差：0.0103522

- 最大长度：0.099981

- 最小长度：0.0497747

从我得到的标准差，我们可以发现匀速算法生成的样条更加均匀。


### 4. 渲染天空盒

我使用的天空盒纹理来自 Unity 标准资源库。天空盒的前、后、左、右、上、下共6张图片。您需要将图像放在正确的位置，图像也可能水平翻转。 首先，我确定了向上的图像，然后将其余图像一张一张地放置并测试正确的顺序和位置。

于是我得到了：

![4.1](:MS_2_CG_2/4.1.png){:data-align="center"}

天空盒中有黑色部分。 我检查了我编写的所有代码，没有发现任何错误发生，然后我注意到透视投影函数可能有问题。我把我的天空盒放在 x, y, z = -1000 和 1000 中，巧合的是，透视投影是：

```c++
matrix.Perspective(54.0f, (float)w / (float)h, 0.01f, 1000.0f);
```

在这种情况下，视野不能超过 1000。 因此，我将上述的 far 参数更改为 2000.0f，从而解决了问题。

另外，我根据天空盒太阳的位置调整光源位置，让它看起来更真实。 但是图像的边界也有接缝，我使用以下设置来解决这个问题（下右图）。

```c++
glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_CLAMP_TO_EDGE);
```

![4.2](:MS_2_CG_2/4.2.png){:data-align="center"}



### 5. 基于物理模拟的位置更新

您可以查看 rollerCoaster::matrixMode_ride() 函数以获取更多信息 

简而言之，我使用了如下的方法：

1. 初始化变量。 设置当前相机状态（位置、法线、切线），找到样条轨迹的最大和最小高度，根据轨迹的高度计算重力势能。 我们必须让相机能够通过最大高度位置，所以初始能量必须大于总重力势能。

2. 每次更新相机位置时，先计算速度。 然后根据速度和 FPS（frame per second）计算更新距离。

3. 计算当前位置到下一个顶点位置的距离。如果此距离小于更新距离（见下图），则意味着下一个位置必须在 p1 之后。 然后从更新距离中减去这个距离，并设置当前位置等于 p1。 重复第 3 步，直到当前位置到下一个顶点位置的距离小于更新距离。

![5.1](:MS_2_CG_2/5.1.png){:data-align="center"}

4. 现在从当前位置到下一个顶点位置的距离大于更新距离，我们站在p2（上图）。 根据当前位置与下一个顶点位置的比值计算出下一个位置，并将相机放在该位置。

您可以通过运行程序来查看该内容


### 6. 渲染阴影时遇到的问题与解决办法

##### 6.1 阴影是完全黑暗的，看起来不真实。

即使我设置了 ` c = vec4(0.0f, 0.0f, 0.0f, 0.5f);`， 阴影仍然是完全黑的。

![6.1](:MS_2_CG_2/6.1.png){:data-align="center"}

解决方案是，我需要在我的程序中启用 alpha 通道混合。

```c++
glEnable(GL_BLEND); // enable blending
glBlendFunc(GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA); // set blend function
```

##### 6.2 Z-缓冲区竞争

![6.2](:MS_2_CG_2/6.2.png){:data-align="center"}

该问题可以通过 4 步法解决：

```c++
// 1. Set depth buffer to read-only, draw surface
glDepthMask(GL_FALSE);
drawGroundTexture();
// 2. Set depth buffer to read-write, draw shadow
glDepthMask(GL_TRUE);
drawShadow();
// 3. Set color buffer to read-only, draw surface again
GLboolean colorMask[4];
glGetBooleanv(GL_COLOR_WRITEMASK, colorMask); // save current color mask
glColorMask(GL_FALSE, GL_FALSE, GL_FALSE, GL_FALSE);
drawGroundTexture();
// 4. Set color buffer to read-write
glColorMask(colorMask[0], colorMask[1], colorMask[2], colorMask[3]);
```

最终，我得到了以下的结果（我更换了一张背景纹理）

![6.3](:MS_2_CG_2/6.3.png){:data-align="center"}

