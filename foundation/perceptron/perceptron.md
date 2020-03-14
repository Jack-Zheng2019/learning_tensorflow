# 多层感知机

## 一、隐藏层

多层感知机在单层神经网络的基础上引入了一到多个隐藏层（hidden layer）。隐藏层位于输入层和输出层之间。图1展示了一个多层感知机的神经网络图，它含有一个隐藏层，该层中有5个隐藏单元。

![image](../image/3.8_mlp.svg)

<div align=center>图1  带有隐藏层的多层感知机</div>

虽然神经网络引入了隐藏层，却依然等价于一个单层神经网络：其中输出层权重参数为WhWo，偏差参数为bhWo+bo。不难发现，即便再添加更多的隐藏层，以上设计依然只能与仅含输出层的单层神经网络等价。

## 二、激活函数

上述问题的根源在于全连接层只是对数据做仿射变换（affine transformation），而多个仿射变换的叠加仍然是一个仿射变换。解决问题的一个方法是引入非线性变换，例如对隐藏变量使用按元素运算的非线性函数进行变换，然后再作为下一个全连接层的输入。这个非线性函数被称为激活函数（activation function）。下面我们介绍几个常用的激活函数。

### 1、ReLU函数

ReLU（rectified linear unit）函数提供了一个很简单的非线性变换。给定元素x，该函数定义为

ReLU(x)=max(x,0).

可以看出，ReLU函数只保留正数元素，并将负数元素清零。

![image](../image/3.8_relu.png)

显然，当输入为负数时，ReLU函数的导数为0；当输入为正数时，ReLU函数的导数为1。尽管输入为0时ReLU函数不可导，但是我们可以取此处的导数为0。

### 2、sigmoid函数

sigmoid函数可以将元素的值变换到0和1之间：

sigmoid(x)=1/(1+exp(−x))

sigmoid函数在早期的神经网络中较为普遍，但它目前逐渐被更简单的ReLU函数取代。

依据链式法则，sigmoid函数的导数

sigmoid′(x)=sigmoid(x)(1−sigmoid(x)).

当输入为0时，sigmoid函数的导数达到最大值0.25；当输入越偏离0时，sigmoid函数的导数越接近0。

![image](../image/3.8_sigmoid.png)

### 3、tanh函数

tanh（双曲正切）函数可以将元素的值变换到-1和1之间：

tanh(x)=(1−exp(−2x))/(1+exp(−2x))

当输入接近0时，tanh函数接近线性变换。虽然该函数的形状和sigmoid函数的形状很像，但tanh函数在坐标系的原点上对称。

依据链式法则，tanh函数的导数

tanh′(x)=1−tanh2(x).

下面绘制了tanh函数的导数。当输入为0时，tanh函数的导数达到最大值1；当输入越偏离0时，tanh函数的导数越接近0。

## 三、多层感知机

多层感知机就是含有至少一个隐藏层的由全连接层组成的神经网络，且每个隐藏层的输出通过激活函数进行变换。多层感知机的层数和各隐藏层中隐藏单元个数都是超参数。

在分类问题中，我们可以对输出做softmax运算，并使用softmax回归中的交叉熵损失函数。 在回归问题中，我们将输出层的输出个数设为1，并将输出，直接提供给线性回归中使用的平方损失函数。

## 四、多层感知机的从零开始实现

## 五、 多层感知机的简洁实现