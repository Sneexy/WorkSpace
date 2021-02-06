# mysql workbench使用
## 前期准备
[Mac安装mysql](https://www.jianshu.com/p/199492627ccc)

下载安装mysql workbench：官网下载，8.0.21版本可以，22和23可能会崩溃

[MySQL Workbench连接MySQL失败](https://www.dazhuanlan.com/2019/10/17/5da801d1dbed7/)：可能是mysql服务没安装或没打开

[workbench图标是灰色，代码不能运行](https://www.cda.cn/discuss/post/details/5f15968bf8aa1b450e8381fd)：重连服务

## 使用workbench
MySQL Workbench的功能使用——功能界面：分为三个主要功能模块：Sql Development(Sql开发 相当于Sql2000中的查询分析器), Data Modeling(数据库建模), Server Administration(服务器管理 相当于Sql2000中的企业管理器)

：很全面的数据库操作（Sql Development部分）

[使用 forward-engineer（正向引擎） 将模型生成为MySQL 数据库](https://wenku.baidu.com/view/dc83b71027d3240c8547ef69.html)

向其中添加表格数据：[MySQL 8.0 Workbench 插入数据方法](https://blog.csdn.net/xiaofengfeng20/article/details/89887157)：在表上右键选择 Select Rows - Limit 1000。输入要插入的数据，点击Apply插入成功。

[MySQL WorkBench 如何运行sql文件](https://www.jianshu.com/p/0621648c57fa)

以下是一些报错的情况的解决：

warning 3719，不需要改，改成utf8MB4也会报另一个类似的warning：

```sql
Warning: (3719, “‘utf8’ is currently an alias for the character set UTF8MB3, which will be replaced by UTF8MB4 in a future release. Please consider using UTF8MB4 in order to be unambiguous.”)
```

[Mysql Workbench 同步model时 VISIBLE 错误问题](https://blog.csdn.net/asdfsadfasdfsa/article/details/84777682)

运行sql文件报错，原因： 已经打开了该sql script ；解决方法：关闭打开的文件 ，再 run script：

```sql
Error calling Python module function in MySQL Workbench
```

