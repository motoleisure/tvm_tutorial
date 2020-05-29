- [Translate from here](https://tvm.apache.org/2020/05/20/bring-your-own-datatypes)
- May 20, 2020 • Gus Smith

- 在本篇blog中，我们介绍了“带入你自己的数据类型框架”，就是在TVM中定义你自己的数据类型。

## Introduction
- 当我们设计加速算子时，其中一个很重要的决策就是我们在硬件中如何近似表示实数。这个问题有一个长期的工业标准的解决方案： the IEEE 754 floating-point standard.
但是，
