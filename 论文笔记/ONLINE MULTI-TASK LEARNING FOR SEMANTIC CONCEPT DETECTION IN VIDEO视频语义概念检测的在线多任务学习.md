##  论文笔记：《ONLINE MULTI-TASK LEARNING FOR SEMANTIC CONCEPT DETECTION IN VIDEO》视频语义概念检测的在线多任务学习

亮点：ELLA算法的：L-知识共享基础矩阵，迭代更新L和L的列向量化（矩阵分解）的结果。本文的亮点，添加了基于标签的约束，该约束考虑了概念的相关性。使用SVM而非逻辑回归作为base learner。

## ●Abstract

-   question作者想解决什么问题？
    扩展了高效终身学习算法(ELLA)
      *[ELLA]:Efficient Lifelong Learning Algorithm，E. Eaton and P . L. Ruvolo, “Ella: An efficient lifelong learning algorithm,” inProc. of the 30th Int. Conf. on Machine Learning (ICML-13), S. Dasgupta and D.Mcallester, Eds. 2013, vol. 28, pp. 507–515, JMLR Workshop
-   method作者通过什么理论/模型来解决这个问题？
    - 我们使用**二次规划**来解决 ELLA 的目标函数，而不是解决套索问题
    - b)我们添加了一个新的**基于标签的约束**，该约束考虑了概念的相关性，	
    - c)我们使用**线性SVMs**作为基础learner，而不是逻辑回归。
    
-   answer作者给出的答案是什么？
    比该问题中常用的单任务学习方法和原 ELLA 算法都有所改进

## ●Instruction

-   why作者为什么研究这个课题
    **视频中的语义概念检测**指的是基于预定义的概念列表(例如，“汽车”、“跑步”)将一个或多个语义概念分配给视频片段(例如，视频关键帧)的任务
    
    对此的典型过程是视频最初被分割成有意义的片段，称为镜头；每个镜头可以由一个或多个特征关键帧来表示；并且，从关键帧或整个镜头中提取几个特征。然后，对于每个目标概念，训练一个监督学习分类器来解决**二元分类**问题(即，决定概念的存在与否)。独立训练概念检测器是一个单任务学习(STL)过程，其中**每个任务涉及识别一个概念**。STL**忽略了概念组可以相关**的事实。
-   how当前研究到了哪一阶段
    开发了一个视频概念检测的终身MTL（Multi-task learning）算法，称为带标签约束的高效终身学习算法。

	以以下方式扩展了现有的ELLA[2]:a)我们使用二次规划来求解ELLA的目标函数，b)我们添加了一个考虑概念相关性的新的基于标签的约束，以及c)我们用线性支持向量机(SVM)和逻辑回归(LR)来实例化ELLA。
-   what作者基于什么样的假设（看不懂最后去查）
    一些任务可能不相关（GO-MTL算法，ELLA算法是GO-MTL的在线版本）

## ●Conclusion

-   优点
    大量的实验揭示了学习许多任务模型(每个概念一个)之间的关系以及可以从基本事实注释中获取的概念相关性的有用性
-   缺点
    

## ●Table & Method

-   数据来源
    TRECVID 2013 SIN（2013年夏季奥林匹克运动会自行车比赛，互联网存档视频）
-   重要指标
    MXinfAP（mean extended inferred average precision，平均扩展推断平均精度，平均精度的近似值）
-   模型步骤 + 每个步骤得出的结论
	- 我们在ELLA的模型上添加了一个新的基于标签的约束，以包含我们可以从基本事实注释中获得的概念之间成对相关的统计信息。
![](ONLINE%20MULTI-TASK%20LEARNING%20FOR%20SEMANTIC%20CONCEPT%20DETECTION%20IN%20VIDEO%E8%A7%86%E9%A2%91%E8%AF%AD%E4%B9%89%E6%A6%82%E5%BF%B5%E6%A3%80%E6%B5%8B%E7%9A%84%E5%9C%A8%E7%BA%BF%E5%A4%9A%E4%BB%BB%E5%8A%A1%E5%AD%A6%E4%B9%A0_md_files/image.png?v=1&type=image)
	
	- 公式（1）：在每次迭代中，ELLA_LC接收任务t的训练数据(X(t) new，y(t) new)。如果这是任务t第一次出现，则ELLA_LC使用基础学习器(Alg)仅从任务t的训练数据计算模型参数w(t)和Hessian H(t)。H(t)是在w(t)上评估的损失函数L的Hessian（海森）函数。
	- 公式（2）：随后，使用相关信息和共享基L来计算特定任务权重向量s(t)。
	- 公式（3-5）：最后，ELLA_LC通过考虑Eq的增量更新来更新基础L以纳入新知识。L-知识共享基础矩阵，列向量化$L=A^{-1}b$
