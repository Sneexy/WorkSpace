代码属于论文：Li X , Chandrasekaran S N , Huan J . Lifelong multi-task multi-view learning using latent spaces[C]// 2017 IEEE International Conference on Big Data (Big Data). IEEE, 2017.

[matlab中的param是什么意思？](https://zhidao.baidu.com/question/328374271033391845.html)：param是输入参数的集合。

[Matlab之zeros](https://www.cnblogs.com/ywl925/archive/2013/03/26/2982890.html)：创建全0数组用，参数为矩阵大小和精度

[cell](https://ww2.mathworks.cn/help/matlab/ref/cell.html)：元胞数组，元胞数组通常包含文本列表、文本和数字的组合或者不同大小的数值数组。通过将索引括在圆括号 `()` 中可以引用元胞集。使用花括号 `{}` 进行索引来访问元胞的内容。`cell(2,3)` 返回一个 2×3 元胞数组。

[size](https://ww2.mathworks.cn/help/matlab/ref/size.html)：`sz = size(A)` 返回一个行向量，其元素是 `A` 的相应维度的长度。如果 `A` 是一个 3×4 矩阵，则 `size(A)` 返回向量 `[3 4]`，`szdim = size(A,dim)` 返回维度 `dim` 的长度

代码里两层for循环，b和v，和代码里不匹配

[eye](https://ww2.mathworks.cn/help/matlab/ref/eye.html)：单位矩阵

[一些MATLAB的编程规范总结1.0版](https://blog.csdn.net/brcucejiang/article/details/53313911)



计算中后续用不到的量用～表示。

```matlab
if (isNew(views, viewID))            
	[u,~,~]=svd(Theta{viewID, taskID});
	L{viewID,1}=u(:, 1:k); 
```
