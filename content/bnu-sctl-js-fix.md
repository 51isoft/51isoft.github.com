Title: 北师大本科教务系统JS修正
Date: 2013-04-16 00:05:14
Tags: BNU, sctl, js, jQuery
Category: Blogs
Slug: bnu-sctl-js-fix
Author: 51isoft

读本科的时候就对学校教务系统不能在Chrome下使用这件事情感到十分的不爽，一直想修正一下这个问题，但拖到本科毕业都没搞……研究生之后发现，
和现在使用的系统相比，本科那套系统真是太智能了，可惜我不用了……研二闲下来之后，前些日子终于决定开始搞一下这个问题了～～

### 问题描述

[北师大本科教务系统](http://sctl.bnu.edu.cn/jwmis/)在Chrome下是不能切换系统的TAB（JS脚本错误），所以没法进入到登录界面。然后即使直接从登陆FRAME的URL进行登陆，
也无法正常跳转到系统的界面。

### 解决
为了方便，直接就JS注入好了，而CHROME下JS注入最方便的就是写扩展了，主界面的JS错误不会影响注入JS执行。

#### TAB切换问题
在主页上，每一个Tab连接都有个onclick事件：`onclick=ToLink(this)`。然而在ToLink函数中，有这么个错误：
`Uncaught TypeError: Cannot read property 'length' of undefined `。直接导致CHROME无法正确的加载TAB页面，解决方法也很直接，替换掉他的ONCLICK事件，
我的做法比较粗暴：
<code>
<pre>
$("span[onclick='ToLink(this)']").click(function(){
    var vHref=$(this).attr("value");
    if(vHref.length<18) return false;
    $("iframe[name='frmHomeShow']").attr("src",vHref);
    event.preventDefault();
});
$("span[onclick='ToLink(this)']").removeAttr("onclick");
</pre>
</code>

貌似没啥难度哈……


#### 登陆问题
简单的来说，就是在那个诡异的界面，登陆完之后，就会一直卡在加载权限数据这一个奇葩的状态下。当你再次刷新的时候他却提示你已登录……另外点击图片也没法刷新验证码。
原因还是各种js错误，比如`Uncaught SyntaxError: Unexpected token . `

对于验证码刷新，还是没什么难度：

<code>
<pre>
$("#imgCode").removeAttr("onclick").click(function() {
    var dt = new Date();
    this.src="../sys/ValidateCode.aspx?t="+dt.getMilliseconds();
});
</pre>
</code>

而对于登陆跳转，我找了半天愣是没找到原来的JS在什么鬼地方…………只能采取奇奇怪怪的方法了，最后写出了如下代码……

<code>
<pre>
if ($("#divLogNote").text()=="正在加载权限数据...") window.top.location.href="../MAINFRM.aspx";
if (window.location.pathname.toLowerCase()=="/jwmis/_data/index_LoginNote.aspx".toLowerCase()) window.top.location.href="../MAINFRM.aspx";
</pre>
</code>

奇葩的解决了这个问题……

#### 存在的Bug
目前各种弹出窗口的显示都有问题，各种白板，即使我已经修复了URL链接问题，介于看的人应该不多，先不折腾他了……


### 其他
咳咳，这货已经可以再Web store上下载到了，地址在[这里](https://chrome.google.com/webstore/detail/%E5%8C%97%E5%B8%88%E5%A4%A7%E6%95%99%E5%8A%A1%E7%B3%BB%E7%BB%9Fjs%E4%BF%AE%E6%AD%A3/ffkgjadiejddlbljnapiafglhgkhbpck)。
截图什么的懒得搞了……

以后想起什么有趣的功能（比如GPA计算什么的）可能会更新更新……
