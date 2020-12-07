## 【阅读笔记】《Deep Partial Multi-View Learning》
题目中译：深度局部多视图学习

## ●Abstract

-   question作者想解决什么问题？
    由于很难对不同视图之间的复杂关联进行建模，尤其是在缺少视图的情况下，它仍然具有挑战性。
-   method作者通过什么理论/模型来解决这个问题？
    提出了一个称为跨部分多视图网络（CPM-Nets）的新颖框架，旨在全面，灵活地利用多个部分视图。】
    为了**完整性**，通过模仿数据传输将学习潜在多视图表示的任务专门转换为退化（**degradation**）过程，从而可以隐式实现不同视图之间一致性和互补性之间的最佳折衷。配备了**对抗策略**，我们的模型可以稳定地估算缺失的视图，将每个视图的所有视图中的信息编码为潜在的表示形式，以进一步提高完整性。此外，引入了**非参数分类损失**以生成结构化表示并防止过度拟合，这使该算法在缺少视点的情况下具有广阔的前景。
    *[CPM-Nets]:Cross Partial Multi-View Networks
-   answer作者给出的答案是什么？
    大量实验结果验证了在分类，表示学习和数据插补等现有技术水平上的有效性

## ●Instruction

-   why作者为什么研究这个课题
    不同的观点可以相互补充，从而最终提高性能。不幸的是，不同视图之间未知而复杂的**相关性**通常会破坏模型中不同模式的集成。**缺失数据**进一步加剧了建模难度。。
-   how当前研究到了哪一阶段
	我们主张将重点放在部分多视图表示学习的完整性和灵活性上。
    提出了一种新颖的深度局部多视图学习算法，即交叉局部多视图网络（CPM-Nets），该模型将来自不同视图的信息全面编码为潜在的表示形式。
    得益于对抗策略，归因得到进一步稳定，这反过来又提高了潜在表示。
-   what作者基于什么样的假设（看不懂最后去查）
    在实际应用中，多视图数据通常不完整

## ●Conclusion

-   优点
    灵活性，学习到的表示结构良好，鲁棒性
-   缺点
    

## ●Table & Method

-   数据来源
    Handwritten，Animal，CUB，3Sources-complete，Football，Politics，ADNI，3Sources-partial
-   重要指标
    对于所有方法，使用五重交叉验证来调参。运行10次取平均值。
    和监督的算法比：missing rate： η =$\frac{\sum_v M_v}{V\times N}$，$M_v$表示在没有v-th视图的样本数，Accuracy
    和非监督的算法比：（1）归因性能：根据归一化均方根误差（NRMSE）评估插补性能。（2）聚类性能：ACC和NMI
-   模型步骤 + 每个步骤得出的结论
	**监督学习**：
	![](Deep%20Partial%20Multi-View%20Learning%E6%B7%B1%E5%BA%A6%E5%B1%80%E9%83%A8%E5%A4%9A%E8%A7%86%E5%9B%BE%E5%AD%A6%E4%B9%A0_md_files/image1.png?v=1&type=image)
	- 对v个视图分别：梯度下降更新网络参数$\Theta$
	- 对n个样本分别：梯度下降更新潜在表示$h_n$
![](Deep%20Partial%20Multi-View%20Learning%E6%B7%B1%E5%BA%A6%E5%B1%80%E9%83%A8%E5%A4%9A%E8%A7%86%E5%9B%BE%E5%AD%A6%E4%B9%A0_md_files/image2.png?v=1&type=image)

	**非监督学习**：
	
	结合对抗策略（CPM-GAN）进行的潜在表示学习和缺失数据归因相互促进
![](Deep%20Partial%20Multi-View%20Learning%E6%B7%B1%E5%BA%A6%E5%B1%80%E9%83%A8%E5%A4%9A%E8%A7%86%E5%9B%BE%E5%AD%A6%E4%B9%A0_md_files/image3.png?v=1&type=image)
	- 对v个视图分别：梯度下降更新鉴别参数$\Theta_d^{(v)}$
	- 对v个视图分别：梯度下降更新生成器参数$\Theta_g^{(v)}$
	- 对n个样本分别：梯度下降更新潜在表示$h_n$
![](Deep%20Partial%20Multi-View%20Learning%E6%B7%B1%E5%BA%A6%E5%B1%80%E9%83%A8%E5%A4%9A%E8%A7%86%E5%9B%BE%E5%AD%A6%E4%B9%A0_md_files/image4.png?v=1&type=image)
