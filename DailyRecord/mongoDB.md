MongoDB stores data records as BSON documents.

What is BSON? BSON is a binary representation of JSON documents.

用键值对表示。

集合中的文档不需要遵循相同的结构。例：

<img src="/Users/sneexy/Library/Application Support/typora-user-images/image-20210206210044178.png" alt="image-20210206210044178" style="zoom:30%;" />

数据类型：

<img src="/Users/sneexy/Library/Application Support/typora-user-images/image-20210206210241723.png" alt="image-20210206210241723" style="zoom:30%;" />

嵌入式文档：同json

CRUD（创建、读取、更新、删除）操作

如果要删除集合中的所有文档，最好删除集合。•为什么？•与“删除所有文档”相比，“删除收集”的速度要快得多

有关联的collection的两种设计方式：

<img src="/Users/sneexy/Library/Application Support/typora-user-images/image-20210207102344452.png" alt="image-20210207102344452" style="zoom:30%;" />

设计中的选择：

- 参考式比嵌入式慢
- 当内容很多的时候，嵌入式需要存储太多
- 混合方法？•在用户文档中保留最近的tweet，以便在用户页面上即时访问•保留来自tweet集合的引用•在请求时提供更多tweet•搜索tweet与用户集合分离
- <img src="/Users/sneexy/Library/Application Support/typora-user-images/image-20210207103356270.png" alt="image-20210207103356270" style="zoom:30%;" />



