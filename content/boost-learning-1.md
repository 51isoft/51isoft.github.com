Title: Boost学习日志1
Date: 2013-04-09 23:32:17
Tags: boost, C++11
Category: Blogs
Slug: boost-learning-1
Author: 51isoft
Summary: Boost学习日志：前一段买了《Boost程序库完全开发指南》，今天真正开始阅读这本大部头了……

前一段买了《Boost程序库完全开发指南》，今天真正开始阅读这本大部头了。我用的环境是OS X 10.8.3 + Netbeans 7.3 + G++ 4.8/CLang++ 4.1，微微有些奇葩……

### 配置环境

首先安装Homebrew，因为我懒得自己编译……而且我一直觉得如果有别人编译好了的，而你又没有什么奇葩需求的话，没有什么必要去自行编译……Homebrew的安装方式就不赘述了。

然后执行`brew install boost`，就搞定了boost安装，安装目录在`/usr/local/Cellar/boost`。

接下来是可选步骤了：安装G++ 4.8。先`brew tap homebrew/versions`，接下来`brew install gcc48`。（吐槽下，编译真慢……）

然后在Netbeans的C/C++选项卡里面添加一个工具集合，设置下CLang或者G++4.8，然后新建工程，在工程属性里面，加入编译选项：`-std=c++0x`，并且添加动态链接库。

然后应该就搞定了，嗯。。。


### 学习笔记

今天学习了下第二章关于时间和日期的那部分，表示boost的日期类真是各种碉堡啊。。。。虽然表示的时间范围没有Java那么Bug吧，但是基本功能还是够用了。
另外，写timer真是方便极了，精神上通过ptime和time_duration就可以搞掂，最后取一下total_milliseconds就行了（PS：这家伙居然还可以搞到纳秒……）

另外，每用一个东西都有极大的可能要使用一个新的命名空间，所以要么就是`using namespace`写一坨，要么就是各种`XXX::YYY`了，当然还可以`#define`……

再有，在学习过程中，扫了一眼Boost官网，发现了很多奇奇怪怪的强大东西，例如[这个](http://www.boost.org/doc/libs/1_53_0/libs/geometry/doc/html/geometry/reference/algorithms.html)，完爆我ACM期间使用的几何库啊有木有……
求重心（2D、3D）、凸包、判相交、判覆盖、算周长……真是什么都有啊……不过可能还是比Java的几何库少点？（没用过，不了解呃……）

最后说点C++11吧，表示for+auto看起来真爽……但是估计短时间内在我们这种渣渣学校是没有老师会教C++11吧？Boost也有自己的foreach，但是目前我还不知道有什么特点，
所以还没有使用过。Lambda算子、函数编程什么的目前处于完全不会的状态，但是看很多人都说函数式编程效率高、大势所趋什么的，压力十分十分大……

### 幻想（？）

唉，先按部就班的学习Boost吧。再列下一些希望能在下学期开学前起码做到会用的技术：Node.js、Python、Android基本开发。应该不算想的太多吧……