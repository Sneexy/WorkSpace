# 目录

- [仓库收藏](#仓库收藏)
- [设计模式](#设计模式)
- [Android](#Android)
- [Java](#Java)
- [Kotlin](#Kotlin)
- [软件](#软件)
  - [Android Studio](#Android_Studio)
  - [Xcode（for iOS）](#Xcode_for_iOS)
  - [git](#git)
  - [Ubuntu](#Ubuntu)
  - [Code diff](#Code diff)
  - [其他软件/工具](#其他软件_工具)



# 仓库收藏

- [huihut/interview: 📚 C/C++ 技术面试基础知识总结，包括语言、程序库、数据结构、算法、系统、网络、链接装载库等知识及面试经验、招聘、内推等信息](https://github.com/huihut/interview)



# 设计模式

- [设计模式 | 菜鸟教程 (runoob.com)](https://www.runoob.com/design-pattern/design-pattern-tutorial.html)
  - [单例模式](https://www.runoob.com/design-pattern/singleton-pattern.html)
  - [工厂模式](https://www.runoob.com/design-pattern/factory-pattern.html)

- [理解 泳道图、时序图、流程图、状态图、协作图](https://www.cnblogs.com/Mark-blog/p/10435351.html)



# Android

- Webview
  - [网页优化之WebView预加载_china_2014的博客-CSDN博客](https://blog.csdn.net/china_2014/article/details/111319421)：这个博客里的实现方式为，在主线程预先创建一个单例的cacheWebView，在进入页面时如果已有cacheWebView就赋值给当前webView
  - webview [Android WebView系列（一）WebView的基本使用](https://www.taodudu.cc/news/show-381018.html)（包括setting详细，生命周期） 
  - [7.5.1 WebView(网页视图)基本用法](https://www.runoob.com/w3cnote/android-tutorial-webview.html) 
  - 什么是WebView？ 
    答：Android内置webkit内核的高性能浏览器,而WebView则是在这个基础上进行封装后的一个 控件,WebView直译网页视图,我们可以简单的看作一个可以嵌套到界面上的一个浏览器控件 
  - [WebView全面解析](https://www.jianshu.com/p/3e0136c9e748)
- [[Junit\] 测试方法执行顺序 - androidme - 博客园](https://www.cnblogs.com/androidme/p/3540680.html)
- [ViewTreeObserver](https://developer.android.com/reference/kotlin/android/view/ViewTreeObserver)
  - OnPreDrawListener、OnPreDraw()函数和OnDrawListener()函数的listener都在此文件夹里。listener集合的加减有addOnPreDrawListener和removeOnPreDrawListener。 

- recyclerView的回收和复用 
  - [Android基础知识-RecyclerView的复用和回收机制_笨鸟的专栏-CSDN博客_android recyclerview 复用](https://blog.csdn.net/u010577768/article/details/102835040) 
  - 缓存
    - mCachedViews 一级缓存：ViewHolder数据还在，只有原来的position可用，不需要重新绑定数据；
    - RecycledViewPool 二级缓存：ViewHolder数据重置，需要重新绑定数据 

  - 复用流程： 
    - 2级缓存 mCachedViews 取 > 1级缓存 RecycledViewPool 取 > Adapter.onCreateViewHolder() 

  - 回收流程： 
    - 遍历移除屏幕的 View，从 View的 LayoutParams 中取出**ViewHolder**，塞入 2级缓存**mCachedViews**
    - 如果 mCachedViews 满了（容量2），则 mCachedViews 移除第一个，用来放要回收的 ViewHolder 
    - 如果 RecycledViewPool 对应 viewType 的 List 没满（容量5），则从 mCachedViews 移除的 ViewHolder 放入**RecycledViewPool**。

- RecyclerView里放置多个view
  - Demo的制作：
    -  [使用 RecyclerView 创建动态列表  |  Android 开发者  |  Android Developers](#kotlin) 
    - [RecyclerView的使用（一）：基本使用](https://www.jianshu.com/p/7a7d9301b2f1) 
    - https://github.com/wangzailfm/RvAdapterForKotlin 
    - [Android开发实践七:一个界面显示多个layout或view_zcc9618的博客-CSDN博客_android 多个界面](https://blog.csdn.net/zcc9618/article/details/80632320) 
    - [Android RecyclerView-segmentfaul](https://segmentfault.com/a/1190000013314654) 
  - 扩展-ScrollView，addView 
    - [让你的布局滚动起来—ScrollView](https://segmentfault.com/a/1190000020157255)
    - [Android ViewGroup 中 addView 方法使用详解_G的博客-CSDN博客](https://blog.csdn.net/qq_37381177/article/details/111592575) 
    - [Android动态添加View之addView的用法 - 新感觉 - 博客园](https://www.cnblogs.com/xgjblog/p/14048402.html)



# Java

- [同步锁synchronized](https://www.cnblogs.com/weibanggang/p/9470718.html)
- listener
  - [Android的Listener用法 - JJ_S - 博客园](https://www.cnblogs.com/vivian187/p/12789950.html) 
  - 函数和listener的调用顺序：[listener的执行先后问题 - @si - 博客园](https://www.cnblogs.com/withasi/archive/2012/05/03/2481031.html)，函数先，listener后
- [java中的 getInstance() 的理解](https://blog.csdn.net/qq_26293573/article/details/78184844)，在单例模式中使用，获取一个static实例。
- [Java 到底是值传递还是引用传递？ - Hollis的回答 - 知乎](https://www.zhihu.com/question/31203609/answer/576030121)
- JSON
  - [JSON put ,accumulate,element 区别 - 掘金](https://juejin.cn/post/6844903903922749447) 
  - [com.alibaba.fastjson和org.json遍历获取key - zipon - 博客园](https://www.cnblogs.com/zipon/p/7399505.html) 使用法2，java遍历json 
- [Java定时任务的三种实现方式](https://www.jb51.net/article/155453.htm),Timer() 
- Java map时key不存在，会返回null，[Kotlin集合类型之Map、MutableMap](https://blog.csdn.net/alfredkao/article/details/106950050)
- [JAVA中final关键字的作用 - 虎啸千峰 - 博客园](https://www.cnblogs.com/chhyan-dream/p/10685878.html)
- [Java 使用 throw 抛出异常](https://blog.csdn.net/weixin_43819113/article/details/91468459)
- 线程休眠
  - [Thread.Sleep线程休眠](https://blog.csdn.net/song854601134/article/details/111290759)：表示接下来多少毫秒此进程/线程不参与抢占CPU的竞争 
  - [为什么在用Thread.sleep()总在加try{}catch(){}语句?-CSDN论坛](https://bbs.csdn.net/topics/110081671)：因为sleep本身会跑抛出异常。 
- 设置函数参数默认值（JAVA不能设置默认参数
  - [java 能为方法参数设置默认参数吗](https://zhidao.baidu.com/question/383805542.html)
  - [java通过函数的重载来实现函数参数默认值_WZH577的博客-CSDN博客](https://blog.csdn.net/WZH577/article/details/101604622)



# Kotlin

- [Kotlin入门篇之--HelloWord_QJay.Dev-CSDN博客](https://blog.csdn.net/qJay_Dev/article/details/50812954)（目前和Java兼容，可以互相引用）
- [Kotlin 教程 - 菜鸟教程](https://www.runoob.com/kotlin/kotlin-tutorial.html)（优点：简洁安全，谷歌从2017开发Android用Kotlin） 
  - 基础语法差不多
  - 类和对象：属性（getter 和 setter，主构造器，次构造函数，抽象类abstract，嵌套类，内部类inner，匿名内部类，类的修饰符） 
  - 继承，接口（定义格式不一定定义操作） 
  - 扩展（Kotlin可以为一个类扩展一个新功能，但是不必继承该类或使用设计模式）数据类和密封类（枚举的延伸，可以不止一种数据类型） 
  - 范型 
  - 枚举 
  - 对象表达式和对象声明（实现创建一个对某个类做了轻微改动的类的对象，且不需要去声明一个新的子类） 
  - 委托（软件设计模式中的一项基本技巧。在委托模式中，有两个对象参与处理同一个请求，接受请求的对象将请求委托给另一个对象来处理。Kotlin 通过关键字 by 直接实现委托。） 
- kt的问号：定义变量时，可在变量后添加“?”表示此变量可为空



# 内核

- JAVA相关
  - [技术随笔之谈架构中Glue机制设计](https://zhuanlan.zhihu.com/p/160169235) 
  - Java垃圾回收：[图解Java 垃圾回收机制](https://blog.csdn.net/justloveyou_/article/details/71216049)，[Java性能优化之JVM GC（垃圾回收机制）](https://zhuanlan.zhihu.com/p/25539690) 
  - Java反射[Java高级篇（四）——反射](https://www.cnblogs.com/adamjwh/p/9683705.html)，[详解 Java 类加载与反射（笔记）](https://blog.csdn.net/weixin_44544465/article/details/108092733) 
  - Java JNI：[java jni简介](https://blog.csdn.net/xdw1985829/article/details/6900178)，[Java JNI的使用基础](https://www.cnblogs.com/zenny-chen/archive/2012/06/15/2550114.html)，[Java 之JNI基础篇(一)](https://arcticfox.blog.csdn.net/article/details/79053061)（JNI编写流程-图），[Java 之JNI基础篇(二)](https://arcticfox.blog.csdn.net/article/details/79080462) 
  - 
  - 



# 软件

<a id="Android_Studio"></a>

## Android Studio

- [Android Studio查看测试覆盖率并生成测试报告_Thik叮当-CSDN博客](https://blog.csdn.net/huiling815/article/details/53312127)

- [如何在Android Studio中进行android单元测试和UI测试](https://www.jianshu.com/p/27a1f932b56c)，函数前添加“@Test”，选择需要测试的类，在文件内右键run。提示“Success Operation succeeded”后打开手机上安装的APP，开始测试，打开后不要后续操作。 

- For Mac

  - 快捷键

    - 格式化代码快捷键：选中 command+option+L 
    - 最近文件 ：command+e
    - 全局搜索：control+shift+f
    - [修改快捷键](https://jingyan.baidu.com/article/27fa7326a15dd346f8271f9c.html )

  - Android studio打开两个项目就非常卡。解决办法：手动设置运行内存：[Mac中Android Studio使用内存调整方法_fenglolo的博客-CSDN博客](https://blog.csdn.net/fenglolo/article/details/108406986)，[android studio 运行非常卡的解决办法_以后的今天的博客-CSDN博客](https://blog.csdn.net/change987654321/article/details/53085332)

  - [Android Studio的调试](#startdebug) 

  - ```
    > Failed to install the following Android SDK packages as some licences have not been accepted. 
    build-tools;28.0.3 Android SDK Build-Tools 28.0.3 
    platforms;android-29 Android SDK Platform 29 
    ```

    在Android Studio里，导航栏"Android Studio"->"Appearance &Behavior"->"System setting"->"Android SDK"，找不到的勾选一下下方的"Show Package Details"。就可以安装上面两个版本

  - app的运行：因为x86的问题，在MacBook上不能运行，将手机用usb连上MacBook打开调试模式，就可以在Android Studio里点击run运行了。 

<a id="Xcode_for_iOS"></a>

## Xcode（for iOS）

- xcode代码格式化：[Mac] xcode 代码自动排序／对齐快捷键 command A ，之后 control ＋ i 
- 项目第一次运行，报错时，运行pod install [pod install 的历程 - #甜甜8023 - 博客园](https://www.cnblogs.com/kaola8023/p/12072380.html)

## git

- Git 教程 | 菜鸟教程](https://www.runoob.com/git)

- 拉取代码

  - 扩充交换分区大小：git config --global http.postBuffer 100000000000（100G） 
  - [Git命令自动补全(mac)](https://www.jianshu.com/p/7130a5c11d42) 
  - 安装Java8（cask好像不支持了）brew install adoptopenjdk8 
  - 安装gradle：brew install gradle(安装了7.0) 
  - brew search XX寻找近似名称的安装包
  - 安装ADB（Android debug bridge）（1.0.41） 
  - 需要加--no-depth（避免拉取的仓库过大）

- [git - 拉取远程代码并且不覆盖本地修改的代码](https://blog.csdn.net/liaofengji/article/details/104892687)（git stash）

- 查看git add了的内容git diff --cached 

- 撤销git add [git 如何取消add操作](https://www.cnblogs.com/chenxi188/p/13663814.html)，常用git reset HEAD

- [git删除本地分支和删除远程分支 - 李勇888 - 博客园](https://www.cnblogs.com/liyong888/p/9822410.html) 

- git 强制切换到某个分支：git checkout -f 0.3.1.280112352415 

- git自动补全 

  - [git命令自动补全 - KinwingHU - 博客园](https://www.cnblogs.com/kinwing/p/11670577.html) 
  - [git自动补全:WARNING: this script is deprecated, please see git-completion.zsh](https://blog.csdn.net/qq_39251759/article/details/110003061) 

- 安装 

  -  [LINUX 上GIT默认安装路径_qq_33450226的博客-CSDN博客](https://blog.csdn.net/qq_33450226/article/details/79826036) 
  -  安装失败，用这个成功了https://zhidao.baidu.com/question/1822494459915869828.html

- 卸载git [mac下卸载Git-阿里云开发者社区](https://developer.aliyun.com/article/577279)

- [git 拉取指定的远程分支(三种方式) - 走看看](http://t.zoukankan.com/miangao-p-12580041.html)

- [git commit之后，想撤销commit](https://www.cnblogs.com/lfxiao/p/9378763.html)：git reset --soft HEAD^

- git放弃修改，强制覆盖本地代码： 

  ```
  git fetch --all
  git reset --hard origin/branch_name 
  （git pull）git branch --set-upstream-to=origin/remote_branch_name local_branch_name
  ```

- checkout -b中，chekout是切换分支，-b是在无此分支的时候创建分支 

## Ubuntu

- [homebrew | 镜像站使用帮助 | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirror.tuna.tsinghua.edu.cn/help/homebrew/) 
- [ubuntu下su: Authentication failure的解决办法(su和su - root的区别)_cjmcp的专栏-CSDN博客](https://blog.csdn.net/cjmcp/article/details/17655187) 
- 创建新用户： sudo adduser xxx [Linux 添加管理员用户_深兰之家-CSDN博客_linux创建管理员用户](https://blog.csdn.net/leem1986/article/details/78048099) 
- vim
  - vim： :wq! //按【:wq!】 强制保存后离开 
  - 复制剪切粘贴：https://cloud.tencent.com/developer/article/1626821 
- [Getting Clear read only status on Webstorm 8](https://stackoverflow.com/questions/25396984/getting-clear-read-only-status-on-webstorm-8)：read only时，修改文件夹权限 



## Code diff

- [Diff文本比较 - 站长工具](http://tool.chinaz.com/tools/diff/)

<a id="其他软件_工具"></a>

## 其他软件/工具

- [JSON在线解析及格式化验证 - JSON.cn](https://www.json.cn/json/jsononline.html) 
- Vscode官网下载直接安装，插件：[vs code 安装（mac）](https://www.jianshu.com/p/0bc70f94b36a) 
- [有道网页翻译](#/?url=https://google.github.io/styleguide/javaguide.html&from=auto&to=auto&type=1)- Google Java Style Guide 
- H5：w3schools: [HTML](https://www.w3schools.com/html/default.asp), [CSS](https://www.w3schools.com/css/default.asp), [Javascript](https://www.w3schools.com/js/default.asp). 

