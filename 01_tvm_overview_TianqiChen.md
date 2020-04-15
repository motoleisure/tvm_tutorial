- [TVM Tutorial](https://sampl.cs.washington.edu/tvmfcrc/)
- [Slides-Overview of TVM](https://drive.google.com/file/d/1_j1dqKZG6Vfedwpzgz4XLD-YWS0e33ve/view)

## Problem: Run deep learning everywhere
- ![Problem](asserts/problem-run-dl-everywhere.png)
- For now, how I start to work on this problem ?
  - We need Machine Learning Reseacher, System Researcher and Computer Architect to work together.
  - ![key problems](asserts/key_problems.png)
  - **It's so resource-comsuming!!! So we propose TVM **
  
## 分析现状  
- 现在的模型训练和模型部署的硬件之间存在非常大的gap。
  - ![deploy dl model everywhere](asserts/01-deploy-dl-model-everywhere.png)
- 我们现在能做到的，目前支持大多数的是英伟达的显卡。
  - ![existing dl model ](asserts/01-existing-dl-framworks.png)
- 现在的方案存在的困难
  - ![problem](asserts/01-existing-dl-frameworks-problem.png)
  - 上层框架中的算子是数据图数据，我们要在底层的GPU中对上层的算子，如二维卷积进行加速优化，这样才能加速上层模型的训练。每增加一个新的算子，我们都要在底层的GPU中实现一个对应的加速操作。然而，当我们希望泡在不同的硬件上，如开发板或者手机等边缘设备，我们需要对应的工程师进行对接新的加速实现。这是和等的麻烦啊。
  - ![limitation of existing approach](asserts/01-limitations-of-existing-approcach.png)
  
- Current System]
  - 现时的做法是我们先优化底层的系统层，然后令系统层赋予我们的机器学习层来优化。这是一个单向的过程，每次我们改变了机器学习算法，那么我们都得重新优化底层的系统来适应。那么，我们提出了这样的问题，我们可不可以直接利用机器学习算法来优化底层的系统呢？如果我们能完成这样的工作，那么底层系统和机器学习算法就会变成一个双向的过程，变成了一个相辅相成的关系。
  - ![current learning system](asserts/01-current-learning-systems.png)

  - ![learning-based learning system](asserts/01-learning-based-learning-systems.png)

## 解决方案：TVM 
- Why ?
  - How to build intelligent systems with learning
  - End-to-end learning-based learning system stack
- Core idea, 能让计算机完成的任务绝不丢给人来做。
  - TVM是一个基于学习的学习系统，那它学习的是什么呢？它学习的就是上层框架和底层硬件之间的加速实现操作(一下蓝色部分)。
  - ![](asserts/01-tvm-lls-01.png)
  - ![](asserts/01-tvm-lls-03.png)
  
