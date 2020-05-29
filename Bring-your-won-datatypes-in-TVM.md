- [Translate from here](https://tvm.apache.org/2020/05/20/bring-your-own-datatypes)
- May 20, 2020 • Gus Smith

- 在本篇blog中，我们介绍了“带入你自己的数据类型框架”，就是在TVM中定义你自己的数据类型。

## Introduction
- 当我们设计加速算子时，其中一个很重要的决策就是我们在硬件中如何近似表示实数。这个问题有一个长期的工业标准的解决方案： the IEEE 754 floating-point standard. 但是，当我们尝试创建高度专业化的设计来压缩大多数的硬件时，使用IEEE 754 floats真的有效吗？ 如果我们知道我们工作负载的数值需求，我们就能创建一个较小的，快速的或者更加节能的数据类型呢？答案是肯定的！
