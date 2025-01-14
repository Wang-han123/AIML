# 第一章学习笔记
* * * 
## 神经网络的基本工作原理
> 神经网络的一个重要特性是它能够从环境中学习,并把学习的结果分布存储于网络的突触连接中。  
## 神经元细胞的数学模型
- 输入 input：是外界输入信号，一般是一个训练数据样本的多个属性，   一个神经元可以有多个输入。
- 输出 output：一个神经元只能有一个输出。
- 权重 weights： 是每个输入信号的权重值， 一个神经元的w的数量和输入的数量一致。 
- 偏移 bias：b是临界值。    
- 激活函数 activation：求和之后，神经细胞已经处于兴奋状态了，已经决定要向下一个神经元传递信号了，但是要传递多强烈的信号，要由激活函数来确定。
**回归/拟合 Regression/fitting**
- **分类 Classification**
### 激活函数的作用  
如果不用激活函数，每一层输出都是上层输入的线性函数，无论神经网络有多少层，输出都是输入的线性组合，这种情况就是最原始的感知机。  
如果使用的话，激活函数给神经元引入了非线性因素，使得神经网络可以任意逼近任何非线性函数，这样神经网络就可以应用到众多的非线性模型中。
## 为什么需要深度神经网络与深度学习
通常我们把三层以上的网络称为深度神经网络。两层的神经网络虽然强大，但可能只能完成二维空间上的一些拟合与分类的事情。如果对于图片、语音、文字序列些复杂的事情，就需要更复杂的网络来理解和处理。第一个方式是增加每一层中神经元的数量，但这是线性的，不够有效。另外一个方式是增加层的数量，每一层都处理不同的事情。
1. 卷积神经网络 CNN (Convolutional Neural Networks)

对于图像类的机器学习问题，最有效的就是卷积神经网络。
2. 循环神经网络 RNN (Recurrent Neural Networks)

对于语言类的机器学习问题，最有效的就是循环神经网络。
函数的导数，沿梯度最小方向将误差回传，修正前向计算公式中的各个权重值；
#### 损失函数
##### 1.损失函数的概念

损失函数的作用：
损失函数的作用，就是计算神经网络每次迭代的前向计算结果与真实值的差距，从而指导下一步的训练向正确的方向进行。

损失函数的使用：
1.用随机值初始化前向计算公式的参数；
2.代入样本，计算输出的预测值；
3.用损失函数计算预测值和标签值（真实值）的误差；
4.根据损失函数的导数，沿梯度最小方向将误差回传，修正前向计算公式中的各个权重值；
5.goto 2, 直到损失函数值达到一个满意的值就停止迭代。


##### 2.机器学习常用损失函数
绝对值损失函数
铰链/折页损失函数或最大边界损失函数
对数损失函数，又叫交叉熵损失函数
均方差损失函数
指数损失函数

##### 3.损失函数图像理解
用二维函数图像理解单变量对损失函数的影响
用等高线图理解双变量对损失函数影响

##### 4.神经网络中常用的损失函数
1.均方差函数，主要用于回归
2.交叉熵函数，主要用于分类
二者都是非负函数，极值在底部，用梯度下降法可以求解。

##### 5.均方差函数
工作原理
实际案例

##### 6.损失函数的可视化
损失函数值的3D示意图
损失函数值的2D示意图

##### 7.交叉熵损失函数
交叉熵的由来：
信息量
熵
相对熵(KL散度)
交叉
熵

##### 8.二分类问题交叉熵
##### 9.多分类问题交叉熵
## 梯度下降

### 1 从自然现象中理解梯度下降

在大多数文章中，都以“一个人被困在山上，需要迅速下到谷底”来举例，这个人会“寻找当前所处位置最陡峭的地方向下走”。这个例子中忽略了安全因素，这个人不可能沿着最陡峭的方向走，要考虑坡度。

在自然界中，梯度下降的最好例子，就是泉水下山的过程：

1. 水受重力影响，会在当前位置，沿着最陡峭的方向流动，有时会形成瀑布（梯度下降）；
2. 水流下山的路径不是唯一的，在同一个地点，有可能有多个位置具有同样的陡峭程度，而造成了分流（可以得到多个解）；
3. 遇到坑洼地区，有可能形成湖泊，而终止下山过程（不能得到全局最优解，而是局部最优解）。

### 2 梯度下降的数学理解

梯度下降的数学公式：

$$\theta_{n+1} = \theta_{n} - \eta \cdot \nabla J(\theta) \tag{1}$$

根据公式(1)，迭代公式：

$$x_{n+1} = x_{n} - \eta \cdot \nabla J(x)= x_{n} - \eta \cdot 2x$$

假设终止条件为 $J(x)<0.01$，迭代过程是：
```
x=0.480000, y=0.230400
x=0.192000, y=0.036864
x=0.076800, y=0.005898
x=0.030720, y=0.000944
```

上面的过程如图2-10所示。

<img src="https://aiedugithub4a2.blob.core.windows.net/a2-images/Images/2/gd_single_variable.png" ch="500" />
### 3 双变量的梯度下降

假设一个双变量函数：

$$J(x,y) = x^2 + \sin^2(y)$$

我们的目的是找到该函数的最小值，于是计算其微分：

$${\partial{J(x,y)} \over \partial{x}} = 2x$$
$${\partial{J(x,y)} \over \partial{y}} = 2 \sin y \cos y$$

假设初始位置为：

$$(x_0,y_0)=(3,1)$$

假设学习率：

$$\eta = 0.1$$

根据公式(1)，迭代过程是的计算公式：
$$(x_{n+1},y_{n+1}) = (x_n,y_n) - \eta \cdot \nabla J(x,y)$$
$$ = (x_n,y_n) - \eta \cdot (2x,2 \cdot \sin y \cdot \cos y) \tag{1}$$

根据公式(1)，假设终止条件为 $J(x,y)<0.01$，迭代过程如表2-3所示。

表2-3 双变量梯度下降的迭代过程

|迭代次数|x|y|J(x,y)|
|---|---|---|---|
|1|3|1|9.708073|
|2|2.4|0.909070|6.382415|
|...|...|...|...|
|15|0.105553|0.063481|0.015166|
|16|0.084442|0.050819|0.009711|

迭代16次后，$J(x,y)$ 的值为 $0.009711$，满足小于 $0.01$ 的条件，停止迭代。

上面的过程如表2-4所示，由于是双变量，所以需要用三维图来解释。请注意看两张图中间那条隐隐的黑色线，表示梯度下降的过程，从红色的高地一直沿着坡度向下走，直到蓝色的洼地。

表2-4 在三维空间内的梯度下降过程

|观察角度1|观察角度2|
|--|--|
|<img src="https://aiedugithub4a2.blob.core.windows.net/a2-images\Images\2\gd_double_variable.png">|<img src="https://aiedugithub4a2.blob.core.windows.net/a2-images\Images\2\gd_double_variable2.png">|

### 4 学习率η的选择

在公式表达时，学习率被表示为$\eta$。在代码里，我们把学习率定义为`learning_rate`，或者`eta`。针对上面的例子，试验不同的学习率对迭代情况的影响，如表2-5所示。

表2-5 不同学习率对迭代情况的影响

|学习率|迭代路线图|说明|
|---|---|---|
|1.0|<img src="https://aiedugithub4a2.blob.core.windows.net/a2-images/Images/2/gd100.png" width="500" height="150"/>|学习率太大，迭代的情况很糟糕，在一条水平线上跳来跳去，永远也不能下降。|
|0.8|<img src="https://aiedugithub4a2.blob.core.windows.net/a2-images/Images/2/gd080.png" width="400"/>|学习率大，会有这种左右跳跃的情况发生，这不利于神经网络的训练。|
|0.4|<img src="https://aiedugithub4a2.blob.core.windows.net/a2-images/Images/2/gd040.png" width="400"/>|学习率合适，损失值会从单侧下降，4步以后基本接近了理想值。|
|0.1|<img src="https://aiedugithub4a2.blob.core.windows.net/a2-images/Images/2/gd010.png" width="400"/>|学习率较小，损失值会从单侧下降，但下降速度非常慢，10步了还没有到达理想状态。|
### 总结与心得体会
通过本节课的学习，我学习了什么是神经网络，了解了神经网络的基本工作原理，知道了神经元细胞的数学模型，了解了神经网络的训练过程和神经网络中的矩形运算，还有学习了神经网络的主要功能有回归拟合和分类，单层的神经网络能够模拟一条二维平面上的直线，从而可以完成线性分割任务。