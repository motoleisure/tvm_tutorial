- [Translate from here](https://tvm.apache.org/2020/05/20/bring-your-own-datatypes)
- May 20, 2020 • Gus Smith

- 在本篇blog中，我们介绍了“带入你自己的数据类型框架”，就是在TVM中定义你自己的数据类型。

## Introduction
- 当我们设计加速算子时，其中一个很重要的决策就是我们在硬件中如何近似表示实数。这个问题有一个长期的工业标准的解决方案： the IEEE 754 floating-point standard. 但是，当我们尝试创建高度专业化的设计来压缩大多数的硬件时，使用IEEE 754 floats真的有效吗？ 如果我们知道我们工作负载的数值需求，我们就能创建一个较小的，快速的或者更加节能的数据类型呢？答案是肯定的！研究者们已经开始在学术和工业的加速设计上做了一些新的数据类型的实验。譬如，谷歌的TPU利用了**bfloat**类型：一个单精度被截到16个bits的IEEE float。由于大多数的深度学习框架中的数值需求定义的相对松弛， 这样的截断通常对模型的精度不做影响，另一方面却可以减少了模型大小的一半。

- 在研究人员开始为数据类型来创建硬件的时候，他们最先要确定的就是他们关心的工作负载中数据类型的表现数值。这常常关乎第一次创建的软件仿真的数据类型（譬如，[Berkeley SoftFloat](http://www.jhauser.us/arithmetic/SoftFloat.html)或者[libposit](https://github.com/cjdelisle/libposit)）,然后直接在工作负载中修改数据类型，去观察不同数据类型的不同表现。 或者更好的是直接把数据类型和编译器整合在一起，这样很多不同的工作负载都可以用这个数据类型来进行编译。这两种做法都是冗长的，而后一种由于给定现代编译器的size和complexity而变得难以操作。Github上的一个[例子](https://github.com/xman/tensorflow) 展示了在tensorflow中修改**posit**数据类型。结果是237个commits，增加了接近6000行代码和修改了超过200个文件，才能加入一个数据类型。这样的工作量对很多研究者来说是非常高的。

- 
