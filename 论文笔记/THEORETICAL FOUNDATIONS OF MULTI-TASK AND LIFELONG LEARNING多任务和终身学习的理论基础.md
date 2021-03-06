##  论文笔记：《THEORETICAL FOUNDATIONS OF MULTI-TASK AND LIFELONG LEARNING》

中译：多任务和终身学习的理论基础

总结：论文是一篇哲学博士学位要求的一部分的论文。很长，暂时只选读一部分。先看了Multi-task Learning和Lifelong Learning部分的Conclusion，和Future directions。

任务顺序对learner表现确实有影响，但是真到终身学习的话应该没有选择的余地了。

## Multi-task Learning
在本章中，我们讨论了在多任务学习中使用的任务相关性的各种假设。特别地，我们已经表明，先前的旨在学习线性特征变换的表示转移的结果可以扩展到核学习。由定理5给出的所得结果表明，每当所考虑的 **核族的伪维数**是有限的时，对来自几个相关学习任务的数据的访问降低了**学习核**的每个任务的样本复杂度。在参数传递的情况下，我们已经表明**顺序处理任务比联合处理任务更有效** 。定理6和7捕捉 **任务顺序对学习者平均表现的影响** ，并可用于导出算法，该算法能够仅基于训练数据自动确定有利的任务顺序。我们以线性预测为例说明了这一过程，并在两个真实图像数据集上展示了所得到的SeqMT和MultiSeqMT方法的有效性。最后，在第3.3节中，我们讨论了 **主动任务选择框架** :对标准多任务场景的修改，最初所有感兴趣的任务仅由未标记的数据表示，学习者能够选择任务的子集来请求标记。定理8和9为两种域适应方法提供了对该框架的分析，并且可以用于以有原则的方式选择标记哪些任务。我们已经在两个数据集上说明了所得到的一个终端服务系统和一个终端服务系统的性能。

**伪维数**：是VC维的扩展，用于非二元函数中的实数函数。相当于分成多少个维度可以将原来的数据合理划分。[参考](https://www.jiqizhixin.com/graph/technologies/e766aa0d-af15-480a-9ce9-b6357442330e)

**求解最好任务顺序**的算法：Algorithm 1 Sequential Learning of Multiple Tasks

> 等式(3.11)的右边只包含可计算的量:平均经验误差和每项任务的先验和后验之间的库尔巴克-莱博发散之和。此外，它还取决于处理任务的顺序π，因为每个任务的先验π(t)取决于任务π(1)。。。，π(t1),之前已经求解过。因此，(3.11)的右边可以看作是π阶的质量度量，通过最小化它，可以得到一个非常适合基于给定训练数据求解任务的阶。此外，因为不等式对所有可能的**任务顺序**都是一致的，所以它的保证也适用于最终的、学习的数据相关的顺序。（PDF P29）

## Lifelong Learning

讨论了终身学习的情景，它可以被看作是多任务学习的延伸，它有一个额外的不确定性来源，这是因为学习者不知道他将来会遇到什么任务。

在第4.2节中，我们讨论了一个更具挑战性的终身学习流模型，它对任务生成过程不做任何假设。
 
 定理10导致了标准经验风险最小化方法的多任务一般化。然而，在实践中，自治代理似乎不太可能保留所有这些信息。因此，显然需要一种替代的终身学习流模型，该模型(1)为每个观察到的任务提供保证，(2)不对任务生成过程做出分布假设，以及(3)只需要存储对先前任务的紧凑描述，例如，只存储相应的学习假设。

Balcan等人[11]最近提供了流式模式下终身学习的第一个分析，其中作者专注于学习线性分类器的情况。他们提出了一种迭代算法，该算法维护一组从以前的任务中学习到的基本预测值。**对于每个新任务，它首先尝试在基本预测范围内学习它，如果失败，则学习一个新的线性预测，然后将其添加到基本集合中。** 在任务共享低维表示的假设下，作者证明了与单独解决每个任务相比，所提出的方法导致样本复杂度的降低。然而，他们的分析也依赖于假设所有任务的边际分布是各向同性的对数凹分布，并且这是否可以扩展到其他类型的分布是一个公开的问题。

通过假设基本类别H是线性的，并用线性组合代替加权多数票，可以从[11]中获得定义。然而，这种替代导致了所使用的复杂性度量的性质的显著差异。在线性预测器及其线性组合的情况下，序列的小维度是对经常使用的任务预测器位于低维度子空间的假设的放松。此外，**任务的顺序并不重要，对任务进行洗牌不会增加序列的维数。相比之下，对于加权多数票，任务的顺序至关重要。** 事实上，根据任务的排序方式，同一组任务可能具有不同的维度。

## Future directions
所有迁移学习方法的关键方面，包括多任务和终身学习，是对预测任务之间相关性的假设。因此，重要的是识别和探索不同类型的关联性，使信息传递有益。大多数迁移方法集中于学习“好的”表示，其中表示的质量通过其近似能力和简单性来衡量。这种假设不仅用于线性分类器，如3.1节中所讨论的，还用于神经网络[52]，其中共享表示采用深度架构的共享层的形式。然而，这不是唯一的选择。人们也可以把一个好的表示看作是一个导致每项任务“容易”学习的表示，即快速学习。在这种情况下，人们可以使用已被证明能导致更快收敛速度的分布“精确”的度量，如概率李普希茨[95]，作为学习表示的质量度量。在[3]中探索了一种定义任务关联性的完全不同的方法。在那里，作者考虑使用深度神经网络来学习几个任务，假设使感兴趣的任务**相似的**不是网络的结构，而是**优化过程**，并且所提出的方法旨在推断用于训练对应于不同任务的神经网络的最佳梯度步长更新。可能**更普遍的问题是，现有的多任务和终身学习模式是否相关**。特别是，多任务学习几乎总是被定义为这样一种设置，其中学习者被给予一组用于几个任务的注释训练集，并且**目标是最小化所有任务的平均预期误差**。然而，正如在第3.3节中所讨论的，在某些情况下，并非所有感兴趣的任务都有标记数据可用。或者，正如[65]中指出的，平均性能可能不是人们应该关心的。终身学习是一个定义更不明确的领域，因此**确定信息传递可能有益的情景非常重要**。据推测，迁移学习的所有这些方面都取决于应用领域。因此，将更多的注意力放在机器学习实践者考虑的建模问题上是很重要的。
