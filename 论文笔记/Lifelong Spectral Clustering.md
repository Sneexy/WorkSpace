# 论文笔记：《Lifelong Spectral Clustering》
## 目录

 1. 论文信息
 2. 个人总结
 3. 谱聚类
 4. 论文做了什么（Abstract）
 5. 公式解读

## 论文信息
题目：Lifelong Spectral Clustering ，终身谱聚类

作者：[Gan Sun](https://arxiv.org/search/cs?searchtype=author&query=Sun%2C+G), [Yang Cong](https://arxiv.org/search/cs?searchtype=author&query=Cong%2C+Y), [Qianqian Wang](https://arxiv.org/search/cs?searchtype=author&query=Wang%2C+Q), [Jun Li](https://arxiv.org/search/cs?searchtype=author&query=Li%2C+J), [Yun Fu](https://arxiv.org/search/cs?searchtype=author&query=Fu%2C+Y)

论文链接：https://arxiv.org/abs/1911.11908v1

## 个人总结
本论文基于两篇论文，对谱聚类的目标函数拆分成矩阵相乘相加的形式，然后这些矩阵分为3类，第一类是任务样本直接相关的矩阵，第二类是多个任务共享的矩阵，第三个是其他。这篇论文中的第二类矩阵有两个，灵感来自两篇论文。

终身学习体现在，多个任务共享的矩阵要保存下来，每一个新的任务加入时，可以加快聚类速度，然后更新共享的矩阵；多个任务的整体目标函数为多个任务目标函数的平均值，一个任务的目标函数为F的话，多个就为$\frac{1}{m}\sum F$。

## 谱聚类
刚开始被“拉普拉斯矩阵”吓到了，看上去很高级的样子，其实并没有那么难。只推荐两个博客：
 - 原理和Python手写代码：[谱聚类（Spectral Clustering）原理及Python实现](https://blog.csdn.net/songbinxu/article/details/80838865)
 - Python调库：[用scikit-learn学习谱聚类](https://www.cnblogs.com/pinard/p/6235920.html)
 我个人对这两篇博客的笔记在：[github链接](https://github.com/Sneexy/WorkSpace/blob/4cf8e86b4994f8628abb1abe084c912cc7923823/DailyRecord/20-11-19.md#python%E5%9F%BA%E7%A1%80) 的“谱聚类”部分

## 论文做了什么（Abstract）
在本文中，我们旨在探讨终身机器学习框架中的频谱聚类问题，即**终身谱聚类（$L^2SC$，Lifelong Spectral Clustering）**。它的目标是通过有选择地从知识库中转移以前积累的经验，为新的谱聚类任务有效地学习一个模型。

具体来说，$L^2SC$的**知识库包含两个组件**：1）**正交基础库**：在每对任务中的集群中捕获潜在的聚类中心； 2）**特征嵌入库**：嵌入在多个相关任务之间共享的特征流形信息。

随着新的谱聚类任务的到来，$L^2SC$首先从基础库和特征库两者中转移知识以获得编码矩阵，然后随着时间的推移重新定义库的基础，以最大程度地提高所有聚类任务的性能。同时，推导了通用的**更新公式**来交替更新基础库和特征库。

## 公式解读
### The Proposed L2SC Model 提出模型
-   公式（1）：L是拉普拉斯矩阵（输入矩阵-度矩阵），D是用来归一化的，得到$W_N^t$
-   公式（2）：$K^t$是$W^t$没有N的约束的公式，就是标准化后的拉普拉斯矩阵，$F^t$是$K^t$的特征分解后的最优聚类分配矩阵（其实还是用来给后续K-means之类的分类用）
-   公式（3）：$F^t=E^tB$（论文引用中的公式），代入公式2，求平均$\frac{1}{m}\sum 目标函数$，得到公式3
-   公式（4）：引用了新的论文公式，得到图联合聚类的目标函数。公式（3）没有考虑多任务间的公共特征嵌入转移，这个公式考虑了多任务间的关系，这个是基于图的联合聚类（co-clustering）来控制和实现任务间知识转移（又是一个求平均（$\frac{1}{m}\sum 目标函数$））。L是group联合约束下的特征嵌入库（跟拉普拉斯矩阵一个符号，但不是同一个）
-   公式（5）：$\widehat{X}=D_1XD_2$,，解释公式（4）一个变量的
-   公式（6）：公式（3）和（4）得到公式（6）（公式3和4的$E^tB$是相同的），公式里的变量为$E^t,B,L$,由任务样本直接决定的是$\widehat{X},K^t$，$K^t$根据公式（2）可知是当前样本矩阵$X$的标准化后的拉普拉斯矩阵。多个任务间通过共享$B$和$L$实现常识共享。

### Model Optimization 模型优化
第m个任务下：
 - 公式（7）：固定L和B更新E，因为LB是多个任务共享的，在当前任务的目标函数max时，固定L，B，更新$E^m$
 - 公式（10）是固定L和$\{{E^t}\}_{t=1}^m$，更新B
 - 公式（14）是固定B和$\{{E^t}\}_{t=1}^m$，更新L
 - 公式（15）的$\Theta$就是公式（14）等效衍生出来的
 算法模型的主体部分就是L，B，$E^m$，$\Theta$四个值的更新，每个任务到来执行一次迭代，迭代到收敛为止。
