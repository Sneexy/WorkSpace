##  论文笔记：《Guided Policy Search for Sequential Multitask Learning》

题目：序列多任务学习的引导策略搜索（Sequential有时序/序列两种翻译，总之是表示任务是不同时到达的）

心得：终身学习的重心是任务一个一个地到来，在终身多任务学习中，“多任务”已经有些失去其在“多任务学习”中的意义。

亮点：将lifelong应用到GPS上解决实际问题

## ●Abstract

-   question作者想解决什么问题？
    **强化学习中的策略搜索**是一种在参数空间中直接与环境交互的实用方法，通常处理局部最优和实时样本收集的难题。一种很有前途的算法，称为引导策略搜索(GPS，**guided policy search**)，能够处理使用以轨迹为中心的方法训练样本的挑战。它还可以提供渐近局部收敛的保证。然而，在目前的形式下，GPS算法**不能在序列多任务学习场景**中运行。这是由于它的批处理风格的训练要求，其中所有的训练样本都是在学习过程开始时集体提供的。因此，算法的适应性在实时应用中受到阻碍，在实时应用中，训练样本或任务可以随机到达。
-   method作者通过什么理论/模型来解决这个问题？
    本文采用最近提出的一种**终身学习方法和弹性加权法，对GPS方法进行了改进**。具体来说，费舍尔（Fisher）信息是用来传授以前所学任务中的知识的。该算法被称为序列多任务学习GPS（sequential multitask learning in GPS，**SMT-GPS**），它能够在连续多任务学习环境下工作，并保证策略的连续学习，而不会发生灾难性遗忘。
-   answer作者给出的答案是什么？
    实验证明了新算法在学习控制策略以处理连续到达的训练样本方面的**有效性**，提供了与传统的、基于批处理的GPS算法**相当的性能**。综上所述，该算法被认为是实时RL和机器人学研究领域的一个**新的基准**（好大的口气哦）

## ●Instruction

-   why作者为什么研究这个课题
    **强化学习**是人工智能的核心组成部分，它为机器人社区提供了一个框架和一套工具，用于设计复杂且难以工程化的行为来与现实世界交互。换句话说，它使机器人作为代理，能够通过试错学习自主寻求最佳行为。此外，通常使用一个**目标函数**来描述学习任务及其相关反馈，而不是明确地导出这个未解决问题的解决方案。
		
	作为目标函数的一种特定形式，逆向物流中的代理人试图使**长期回报最大化**，以获得执行任务的最佳行为。从学习过程中获得的原始经验中估计预期的长期回报，需要使用传统方法，如动态规划和时间差异学习。然而，它们不能满足在机器人领域中特别遇到的**高维连续状态和动作空间**的要求。
		
	**直接策略搜索**方法可以有效地处理高维系统，而具有数百个参数的复杂策略经常对此类方法提出挑战，需要许多样本。还可能陷入局部最优。
	
	然而，目前的GPS方案只能针对不同的任务以批处理模式来训练策略，而且众所周知，这种方案难以应对增量数据处理的挑战，特别是在机器人应用中。具体来说，如果所有的训练任务都是按顺序进行的，而不是在早期训练期间集体提供的，GPS方法将不起作用。
-   how当前研究到了哪一阶段
    引导策略搜索方法引入**轨迹优化**来缓解样本效率问题，为其远离局部最优。该方法主要利用以轨迹为中心的优化来生成合适的样本，并**引导学习过程**来训练复杂的高维策略。

	目标是从数据序列中逐步建立一个预测模型，而不会出现灾难性的遗忘。通过开发和修改最近开发的EWC算法[26]，我们建议**结合Fisher信息**(FI)，以保护对以前的任务很重要的权重，同时学习手头的新任务。在某种程度上，这也克服了我们提出的顺序多任务学习方法中的灾难性遗忘。

	总之，本文的主要贡献是一个基于GPS的框架的新公式，及其算法实现，称为SMT-GPS。该算法能够有效地利用连续任务信息，使智能体能够在不忘记先前学习的任务的情况下，逐步完成新的任务。这是通过学习两个动力系统的控制策略来证明的，具体来说，就是上摆和插钉任务（upward swinging pendulum and peg insertion tasks.）（ps.作者你到底说不说得清楚当前研究了什么啊）
-   what作者基于什么样的假设（看不懂最后去查）
    GPS (SMT-GPS)中的顺序多任务学习问题也被认为是终身学习的一部分[21]，[22]，因为代理的目标是添加新的任务知识，同时在任务之间传递知识。

## ●Conclusion

-   优点
    实现了基于GPS的SMT-GPS，可以应对序列任务了。能够解决灾难性遗忘的问题。
-   缺点
    

## ●Table & Method

-   数据来源
    使用提出的贴片全球定位系统算法来学习图2和3所示的两个动态系统的控制策略，具体来说，一个钟摆向上摆动，一个插钉环境。
-   重要指标
	  -  a)克服灾难性遗忘：动力系统
	  -  b)顺序多任务学习能力：末端执行器位置和目标位置之间的距离、动作成本和插钉成功率。
	  - c)费希尔信息（Fister Information，FI，描述了每个任务参数的估计后验概率的准确性）分析: 分析了保留先前信息的具体影响
-   模型步骤 + 每个步骤得出的结论
![](Guided%20Policy%20Search%20for%20Sequential%E9%A1%BA%E5%BA%8F%E5%A4%9A%E4%BB%BB%E5%8A%A1%E5%AD%A6%E4%B9%A0%E7%9A%84%E5%BC%95%E5%AF%BC%E7%AD%96%E7%95%A5%E6%90%9C%E7%B4%A2_md_files/image1.png?v=1&type=image)
![](Guided%20Policy%20Search%20for%20Sequential%E9%A1%BA%E5%BA%8F%E5%A4%9A%E4%BB%BB%E5%8A%A1%E5%AD%A6%E4%B9%A0%E7%9A%84%E5%BC%95%E5%AF%BC%E7%AD%96%E7%95%A5%E6%90%9C%E7%B4%A2_md_files/image2.png?v=1&type=image)

SMT-GPS-两层for循环：

    for 条件m=1 to M
	   	for迭代k属于1,…,K
	   		生成样本Di
	   		使用Di拟合线性-高斯动态pi
	   		优化本地策略
	   		通过运行pi收集“成功样本”，并记录为Dm
	   		利用Dm优化全局政策

