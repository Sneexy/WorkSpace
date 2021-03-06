##  论文笔记：《Online Multi-Task Learning based on K-SVD》
中译：基于支持向量机的在线多任务学习

总结：基于K-SVD算法，首先将其应用到多任务学习，然后通过算法上的改变应用到终身学习。输入分布不相似的时候，增量更新共享矩阵L。保存了L，因此极大减少了时间复杂度。

疑惑：算法的“在线”是什么意思：[DailyRecord/20-12-11.md](https://github.com/Sneexy/WorkSpace/blob/6e66af1ec3cd61560888162babe601a1815807a5/DailyRecord/20-12-11.md)

## ●Abstract

-   question作者想解决什么问题？
    提出了一种基于K-奇异值分解的高效在线算法，用于学习多个连续任务。
-   method作者通过什么理论/模型来解决这个问题？
    我们首先导出一种基于K-SVD算法的批处理多任务学习方法，然后扩展批处理算法，在终身学习环境中在线训练模型。

	提出的方法提供了一个终身学习的替代公式，支持任务和特征相似矩阵。
-   answer作者给出的答案是什么？
    更低的计算复杂度，同时保持几乎相同的性能
    

## ●Instruction
为了促进任务模型之间的知识传递，MTL算法使用的一种常见技术是学习和维护潜在模型组件的共享存储库；每个任务模型都是这些潜在组件的加权组合。
-   why作者为什么研究这个课题
    ELLA（是作者之前的论文提出的）采用几种简化方法来消除支持在线学习的昂贵优化，同时最小化对最终任务模型性能的不利影响。最值得注意的是，ELLA要求每个模型一旦被学习，就基于潜在组件的固定权重。这可能会对性能产生不利影响，因为**不允许任务模型调整单个潜在组件的权重**，因为这些组件由于额外的训练而变得更加精细。
    [^碎碎念]:（好家伙，在以前的Conclusion写这些缺点了吗，自我批判呀）
-   how当前研究到了哪一阶段
    我们研究了一种基于K-SVD算法的在线多任务学习的替代方案，与ELLA相比，该方案**降低了计算复杂度**，为连续任务的快速学习提供了更好的支持。这个K-SVD公式还消除了ELLA的一个简化，使任务模型能够在学习过程中灵活地调整它们在模型组件上的**权重**。

	在批**处理MTL设置中调整K-SVD来学习任务模型**，产生了一种新的算法，我们称之为MTL-SVD。然后，我们修改批量MTL-SVD算法，使其**在线运行**，使其适用于终身学习设置。
-   what作者基于什么样的假设（看不懂最后去查）
    

## ●Conclusion

-   优点
    将Aharon等人(2006)的方法调整到终身学习环境需要几个关键的创新，包括:(1)用**广义奇异值分解替换原始算法中的奇异值分解步骤**，以及(2)当新的任务数据被呈现给算法时，**选择性地更新模型**的组件。在数据的输入**分布相似**的问题上表现良好。

	对于输入**分布不相似**的领域，我们展示了一种混合方法(在该方法中，我们将ELLA-SVD更新与另一个称为ELLA增量的有效更新步骤交织在一起)表现稳健。
-   缺点
    

## ●Table & Method

-   数据来源
    一个使用合成数据，另三个使用真实数据： (1) 综合回归任务，(2)学生考试成绩预测，(3)从雷达图像中检测地雷，(4)面部表情识别[^译]

	[^译]: (1) synthetic regression tasks, (2) student exam score prediction, (3) land mine detection from radar images, and (4) facial expression recognition
-   重要指标
    使用ROC下面积 (area under the ROC, AROC)作为分类任务的准确性指标，使用负均方根(negative root mean-squaredr，-MSE)作为回归任务的指标。
-   模型步骤 + 每个步骤得出的结论
	**The K-SVD Algorithm**：稀疏编码学习字典的K-SVD算法，这是我们的方法的基础。
	- Step1：给定L，优化S
	- Step2：优化字典元素及其对应的非零系数![](Online%20Multi-Task%20Learning%20based%20on%20K-SVD%E5%9F%BA%E4%BA%8E%E6%94%AF%E6%8C%81%E5%90%91%E9%87%8F%E6%9C%BA%E7%9A%84%E5%9C%A8%E7%BA%BF%E5%A4%9A%E4%BB%BB%E5%8A%A1%E5%AD%A6%E4%B9%A0_md_files/image1.png?v=1&type=image)
	
	**Multi-Task Learning Using K-SVD**基于支持向量机的多任务学习
	- 通过单任务学习计算(θ(t)，D(t))（θ(t)是第t个任务的参数向量）（这两个变量用来计算L）
	- 循环运行直到收敛：（1）根据L更新S（2）优化字典元素
	
	**Lifelong Learning Using K-SVD**基于支持向量机的终身学习
	- 当接收任务t的训练数据时，等式12中的更新(用于更新s(t)的值)仅针对任务t执行
	- 等式9、5和6中的更新仅在对应于s(t)的非零条目的列的子集上执行(即，我们仅更新用于构建当前任务的模型的潜在基向量)(s(t)是系数向量，θ(t)=L·s(t)，L是k个任务的潜在模型组件库，在多个任务中共享，让LJ指示要优化的L的特定列。）。
	- K-SVD算法的两个步骤直到收敛才重复，而是每批新的训练数据只执行一次。
	- 终身学习图例![](Online%20Multi-Task%20Learning%20based%20on%20K-SVD%E5%9F%BA%E4%BA%8E%E6%94%AF%E6%8C%81%E5%90%91%E9%87%8F%E6%9C%BA%E7%9A%84%E5%9C%A8%E7%BA%BF%E5%A4%9A%E4%BB%BB%E5%8A%A1%E5%AD%A6%E4%B9%A0_md_files/image2.png?v=1&type=image)

	 拓展：**ELLA增量**：当接收到新任务的数据时，它会独立更新L的每一列。
