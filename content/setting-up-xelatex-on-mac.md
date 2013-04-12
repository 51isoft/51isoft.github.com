Title: 在Mac上配置TeX环境以及中文支持
Date: 2013-04-12 19:43:39
Tags: XeLaTeX, Mac, resume
Category: Blogs
Slug: setting-up-xelatex-on-mac
Author: 51isoft

为了找工作做准备，找了个TeX的简历模板，然后猛然发现，我这台Mac上还没装TeX（其实吧……我也不会TeX……）……之前一直觉得对于全新手来说，折腾TeX的中文支持还是很疼的，
不过为了装装X，还是决定搞一下了……

### 准备工作

MacTeX下载地址：[https://www.tug.org/mactex/downloading.html](https://www.tug.org/mactex/downloading.html)

### 配置

1.  下载完成之后（TeX真TMD大啊），双击MacTeX.pkg进行安装。

2.  在TeX文件文件头，使用如下代码：

    <code>
    \documentclass[UTF8,nofonts]{ctexart}<br>
    \setCJKmainfont[BoldFont={Heiti SC},ItalicFont={STKaiti}]{STSong}
    </code>

    例子：

    <code>
    \documentclass[UTF8,nofonts]{ctexart}<br>
    \setCJKmainfont[BoldFont={Heiti SC},ItalicFont={STKaiti}]{STSong}<br>
    \begin{document}<br>
    我是汉字啊！<br>
    \end{document}<br>
    </code>

3.  用TeXworks打开.tex文件，选择XeLaTeX生成PDF文件，嗯，然后你就可以看到成品了。

4.  如果字体提示不对，那么请在终端里面使用`fc-list`命令查看你的系统有的字体，然后替换`setCJKmainfont`部分的字体。

### 其他

我的简历可以在我的Github上看到，求各大公司包养啊！！！嗯，看起来MacTeX的中文也不是那么难搞嘛……