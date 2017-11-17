# 背景
Udacity深度学习纳米学位第一个实战项目，构建一个神经网络，并用该网络预测每日自行车租客人数。

# 项目内容
项目中的数据是预先准备好的，并且训练所需的代码也有一部分已经写好。需要自己实现的主要是：

- sigmoid 激活函数

以及正向传播中的：
- 隐藏层输入
- 隐藏层输出
- 输出层输入
- 网络输出

和反向传播中的：
- 输出误差
- 更新权重

# Lessons learned
我花了大概2天的时间完成了这个项目，走了不少弯路。现在回顾一下，感觉有一些需要注意的地方，总结如下，也许对您有用。

## 理论与公式
Udacity提供了视频与网页介绍了梯度下降反向传播的原理，包括了公式的具体推导过程。**请不要为了节省时间而忽视这部分内容**。最好自己亲手推导一下，这样在后续写代码的时候能够做到心里有数。否则可能会被error, error term等术语困扰。

## 矩阵运算
自己动手画一下神经网络的结构，把各个节点、输入、权重的连线都画出来，手动写写输出的表达式，然后将表达式用矩阵相乘的方式写出来，这样可以避免后期写代码时候的矩阵维度匹配问题。

## 模型特质
共享单车模型的输出于之前的网络结构不同，它的最后一层并不是要输出概率，因此输出层的激活函数不是`sigmoid`函数。忽视这一点会造成误差计算的错误。

# 总结
最后，学习不能着急，要扎实。看到群里的小伙伴们有用几个小时就完成项目一的时候感觉很着急。然而基础不牢固就去做项目正好验证了一句老话“欲速则不达”。稳扎稳打才是适合我的学习方法。

---

# Review内容

经过Udacity的review，需要改进的地方有两点：
- 隐藏层单元个数
- 学习速率

## 更新前参数与结果
### 参数
```
iterations = 5000
learning_rate = 0.1
hidden_nodes = 128
```
### 结果
Training loss: 0.230 ... Validation loss: 0.408

![result_orig-1](https://yinguobing.com/content/images/2017/11/result_orig-1.jpg)

更新前的隐藏层单元个数选了128，这个节点数太多了。另外learning_rate选了0.1，比较小。这两个因素综合在一起导致需优化参数太多。即使迭代数为5000，loss的值依旧在0.4左右。

## 更新后的参数与结果
### 参数
```
iterations = 3000
learning_rate = 0.8
hidden_nodes = 14
```
### 结果
Progress: 100.0% ... Training loss: 0.064 ... Validation loss: 0.155

![result_review](https://yinguobing.com/content/images/2017/11/result_review.jpg)

更新后的参数极大的减小了隐藏层的节点数，增大了学习率，并且获得0.155的loss，比之前的小了很多。迭代次数也减小到了3000。迭代后期error基本上处于极小幅度的跳动，因此迭代次数理论上可以更少。

更新后的参数参考了reviewer的建议。

## 附加思考
测试数据采用了11日到31日的数据，仔细观察你会发现21日后的单车租用数量整体比之前低了好多。虽然新的参数获得了更低的loss，但是从结果的图像来看，隐藏层节点数更多的网络在21日后的预测更加准确。看起来对于复杂的数据规律，复杂的模型还是有一定应用的潜力。