## 【阅读笔记】《Deep Multimodal Clustering with Cross Reconstruction》
题目中译：具有交叉重构深度多模态聚类

## ●Abstract

-   question作者想解决什么问题？
提取共同特征至关重要。但是，由于忽略了不同模态的数据在**特征空间中共享相似分布**的事实，大多数工作并未完全挖掘模态间的分布关系，最终导致了无法接受的共同特征。
-   method作者通过什么理论/模型来解决这个问题？
    提出了一种采用**交叉重构**的深度多模态聚类方法，该方法首先关注于一种无监督的多模态特征提取，然后对这些提取的**特征进行聚类**。提出的交叉重建旨在在不同形态之间建立潜在的联系，从而有效减少特征空间中的分布差异。
-   answer作者给出的答案是什么？
    有效减少特征空间中的分布差异。理论分析表明，交叉重构减少了多模态特征分布的Wasserstein距离[^1]。实验结果表明，有了明显的改进。
    [^1]:衡量两个分布相似程度的指标，[Wasserstein距离学习笔记-知乎](https://zhuanlan.zhihu.com/p/84617531)，2019主流的分布距离度量依然是KL散度，这是由于KL散度的计算方式简单，计算成本较Wasserstein低

## ●Instruction

-   why作者为什么研究这个课题
对于深度多模态聚类，最常用的方法是通过使用多个深度神经网络（DNN）并在这些公共特征上进行聚类，从不同的模态中提取公共特征。分为3类：
	- 基于AE（自动编码器）：共同特征√ 通用特征分布的相似性×
	- 基于CDM（深度玻尔兹曼机）：不同模式的联合表示√ 计算成本×
	- 基于DCCA（深度规范相关分析）：相关特征√ （不同形式数据包含不同数值特征时，可能无明显相关性）概率分析×（导致分布差异难以监测）
-   how当前研究到了哪一阶段
    
    以无监督方式提取多模式数据的共同特征，着重于多模式聚类，并减少了特征空间中不同模式的分布差异。
    - 首先，我们应用变分信息瓶颈（VIB）从不同的模式中提取特征，最小化原始数据和提取的特征之间的互信息。
    - 使用交叉重构构造方法从不同模态提取特征，可以有效减少不同形态在特征空间中的分布差异
    - 第三，我们使用融合层将提取的特征融合到通用特征。
    - 最后，我们使用聚类算法对通用特征进行聚类。
-   what作者基于什么样的假设（看不懂最后去查）
    

## ●Conclusion

-   优点
    有效地减少了分布差异
-   缺点
    

## ●Table & Method

 1.   数据来源
    6个多模态数据集：Digits, CNN, AwA, Cal101, LUse-21, Scene-15
 2.   重要指标
    ACC，NMI，purity
 3.   模型步骤+ 每个步骤得出的结论
DMCR有两个阶段。
![](https://media.springernature.com/original/springer-static/image/chp%3A10.1007%2F978-3-030-47426-3_24/MediaObjects/492449_1_En_24_Fig1_HTML.png)
		- 在第一阶段，我们使用VIB和交叉重构从不同模态中提取特征，以约束编码器，从而确保不同模态中提取的特征共享相似的分布。
		
			E1和D1是用于第一模态的编码器和解码器，E2和D2是用于第二模态的编码器和解码器。 z1和z2是从x1和x2提取的特征，$\widehat{x}$是通过z重构的数据
		- 在图1的第二阶段，融合层将特征从不同的模态融合到通用特征，z*是通用特征




