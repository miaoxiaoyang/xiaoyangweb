阮一峰的网络日志 » 首页 » 档案
搜索 
上一篇：ES6 的功能侦测库 
下一篇：Flex 布局教程：实
分类： 开发者手册
Flex 布局教程：语法篇
作者： 阮一峰

日期： 2015年7月10日

感谢 腾讯课堂NEXT学院 赞助本站，腾讯官方的前端培训 正在招生中。

腾讯课堂 NEXT 学院

网页布局（layout）是 CSS 的一个重点应用。


布局的传统解决方案，基于盒状模型，依赖 display 属性 + position属性 + float属性。它对于那些特殊布局非常不方便，比如，垂直居中就不容易实现。


2009年，W3C 提出了一种新的方案----Flex 布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持，这意味着，现在就能很安全地使用这项功能。


Flex 布局将成为未来布局的首选方案。本文介绍它的语法，下一篇文章给出常见布局的 Flex 写法。网友 JailBreak 为本文的所有示例制作了 Demo，也可以参考。

以下内容主要参考了下面两篇文章：A Complete Guide to Flexbox 和 A Visual Guide to CSS3 Flexbox Properties。

一、Flex 布局是什么？
Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。

任何一个容器都可以指定为 Flex 布局。

.box{
  display: flex;
}
行内元素也可以使用 Flex 布局。

.box{
  display: inline-flex;
}

Webkit 内核的浏览器，必须加上-webkit前缀。

.box{
  display: -webkit-flex; /* Safari */
  display: flex;
}
注意，设为 Flex 布局以后，子元素的float、clear和vertical-align属性将失效。

二、基本概念
采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。


容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；交叉轴的开始位置叫做cross start，结束位置叫做cross end。

项目默认沿主轴排列。单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。

三、容器的属性
以下6个属性设置在容器上。

flex-wrap
flex-flow
justify-content
align-items
align-content
3.1 flex-direction属性
flex-direction属性决定主轴的方向（即项目的排列方向）。

.box {
  flex-direction: row | row-reverse | column | column-reverse;
}


它可能有4个值。

row（默认值）：主轴为水平方向，起点在左端。
row-reverse：主轴为水平方向，起点在右端。
column：主轴为垂直方向，起点在上沿。
column-reverse：主轴为垂直方向，起点在下沿。

@row(默认值)：主轴为水平方向，起点在左端。
@row-reverse: 主轴为水平方向，起点在右端。
@column:主轴为垂直方向，起点在上沿。
@column-reverse: 主轴为垂直方向，起点在下沿。

3.2 flex-wrap属性
默认情况下，项目都排在一条线（又称"轴线"）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。

.box{
  flex-wrap: nowrap | wrap | wrap-reverse;
}
它可能取三个值。

（1）nowrap（默认）：不换行。



（2）wrap：换行，第一行在上方。



（3）wrap-reverse：换行，第一行在下方。

@3.2 flex-wrap属性：默认情况下，项目都排在一条线上，属性为：1,nowrap(默认) 不换行 2,wrap 换行 3, wrap-reverse:换行，第一行在下方


3.3 flex-flow
flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。


.box {
  flex-flow: <flex-direction> || <flex-wrap>;
}
3.4 justify-content属性
justify-content属性定义了项目在主轴上的对齐方式。


.box {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}


它可能取5个值，具体对齐方式与轴的方向有关。下面假设主轴为从左到右。

flex-start（默认值）：左对齐
flex-end：右对齐
center： 居中
space-between：两端对齐，项目之间的间隔都相等。
space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

@justify-content  项目在主轴上的对齐方式
1.flex-start 左对齐 2.flex-end:右对齐 3.center:居中 4.space-between:两端对齐，项目之间的间隔都相等。5,space-around：每个项目两侧的间隔相等，所以，项目之间的间隔比项目与边框的间隔大一倍。


3.5 align-items属性
align-items属性定义项目在交叉轴上如何对齐。

.box {
  align-items: flex-start | flex-end | center | baseline | stretch;
}


它可能取5个值。具体的对齐方式与交叉轴的方向有关，下面假设交叉轴从上到下。

flex-start：交叉轴的起点对齐。
flex-end：交叉轴的终点对齐。
center：交叉轴的中点对齐。
baseline: 项目的第一行文字的基线对齐。
stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
3.6 align-content属性
align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。


.box {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}


该属性可能取6个值。

flex-start：与交叉轴的起点对齐。
flex-end：与交叉轴的终点对齐。
center：与交叉轴的中点对齐。
space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
stretch（默认值）：轴线占满整个交叉轴。
四、项目的属性
以下6个属性设置在项目上。

order
flex-grow
flex-shrink
flex-basis
flex
align-self
4.1 order属性
order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。


.item {
  order: <integer>;
}


4.2 flex-grow属性
flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。


.item {
  flex-grow: <number>; /* default 0 */
}


如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

4.3 flex-shrink属性
flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。


.item {
  flex-shrink: <number>; /* default 1 */
}


如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。

负值对该属性无效。

4.4 flex-basis属性
flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。


.item {
  flex-basis: <length> | auto; /* default auto */
}
它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。

4.5 flex属性
flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。


.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

4.6 align-self属性
align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。


.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}


该属性可能取6个值，除了auto，其他都与align-items属性完全一致。

（完）

文档信息
版权声明：自由转载-非商用-非衍生-保持署名（创意共享3.0许可证）
发表日期： 2015年7月10日
Teambition：研发管理工具 
Teambition

CODING：企业级软件研发协作平台 
Coding

相关文章
2019.04.09: OAuth 2.0 的四种方式
上一篇文章介绍了 OAuth 2.0 是一种授权机制，主要用来颁发令牌（token）。本文接着介绍颁发令牌的实务操作。
2019.04.04: OAuth 2.0 的一个简单解释
OAuth 2.0 是目前最流行的授权机制，用来授权第三方应用，获取用户数据。
2019.03.25: Grid 布局教程
一、概述 网格布局（Grid）是最强大的 CSS 布局方案。
2019.03.16: 普通人的网页配色方案
网页需要配色。一种好看、易用、符合心意的配色，是很不容易的，尤其在没有设计师时。
广告（购买广告位）
API 调试和文档生成利器

="ApiPost"
React 框架课程

="B.Match"
留言（196条）
云墨雪 说：

坐个沙发, ie10的普及率还有待观望啊..

2015年7月10日 13:04 | # | 引用

王永起 说：

四、容器的属性，应该是“项目的属性”吧？

2015年7月10日 13:10 | # | 引用

阮一峰 说：

@王永起，

谢谢指出，已经改正。

2015年7月10日 13:19 | # | 引用

一月31 说：

好文章，简单明了。

2015年7月10日 14:58 | # | 引用

Henry 说：

听说博主是搞经济出身的，居然没有一篇经济类的文章，真想问博主炒股不？

2015年7月10日 15:04 | # | 引用

chshouyu 说：

现在介绍有点晚了吧-_-#

2015年7月10日 15:08 | # | 引用

Overtrue 说：

赞，终于在您这儿看明白了，谢谢！

2015年7月10日 16:26 | # | 引用

chenjia404 说：

谢谢分享，新的开发技术，使我们开发者越来越方便了。

2015年7月10日 17:31 | # | 引用

shikelong 说：

flex布局除了响应不同页面之外，还有什么优点呢？

2015年7月10日 18:14 | # | 引用

KevinSu 说：

简单明了，配图很赞！

2015年7月10日 19:24 | # | 引用

liaotonglang 说：

看标题还以为是讲编译器，兴冲冲点进来。不过并不失望，最近做课程设计正好需要这个。博主配图好漂亮。

2015年7月11日 11:31 | # | 引用

Soli 说：

属性名字起的很别扭哈。

2015年7月11日 22:48 | # | 引用

imskull 说：

多谢，很不错的文章，一直都用Polymer预定义的flex排版（"layout horizontal center"这样），看完才知道原来flex还有其它这些功能。

2015年7月11日 23:50 | # | 引用

張旭 说：

wow! 這傢伙太實用了!
grid layout framework 不知道是否會重寫了

2015年7月13日 14:13 | # | 引用

WINE 说：

长见识了

2015年7月15日 09:48 | # | 引用

temp 说：

进了阿里，写文章不精致了。

2015年7月15日 10:37 | # | 引用

大个 说：

阮大神啊，flex-basis，这个属性的作用是优先级高于width的width吗？它除了设置宽度的作用还有什么用处？（宽度指的是水平方向，如果是垂直方向就是height了）。

2015年7月20日 16:56 | # | 引用

longfei 说：

阮老师，那个item的flex-grow属性，我写了个demo
CSS:
body{margin:0;}
ul,li{margin:0; padding:0;}
li{list-style-type:none;}
#list{border:2px solid gold; height:500px; display:flex; flex-direction:row;}
#list li{font-family:"microsoft yahei"; font-size:50px; background:#C00; color:#fff; margin:2px; flex-grow:1;}
#list li:nth-child(2){flex-grow:2;}

<ul id="list">
<li>test1</li>
<li>test2</li>
<li>test3</li>
</ul>
结果第2个li所占的宽度并不是其它li的2倍，为什么呢？比其它两个要大，但不足2倍。

2015年7月22日 11:50 | # | 引用

夜幕下的猫 说：

写的非常好！我用来弄我的 zhihu-daily-reader 布局了，嘿嘿！

2015年7月22日 15:52 | # | 引用

阮一峰 说：

@longfei:

flex-basis都设为0，因为flex-grow定义的是，剩余空间分配的比例关系。

2015年7月22日 16:06 | # | 引用

victor 说：

兼容性是大问题！

2015年8月 6日 14:32 | # | 引用

coffce 说：

Nice！看了这篇文后我写了个基于flex的栅格布局库 flex-layout
https://github.com/Coffcer/flex-layout

2015年8月17日 09:49 | # | 引用

dubbo 说：

有了这个以后可以真正的告别table了。

2015年8月21日 07:41 | # | 引用

夜愿 说：

阮老师，align-items：flex-start和align-items:flex:end 的图弄反了

2015年8月26日 14:00 | # | 引用

第二梦 说：

您发表的每篇文章,都是那么的善于理解,一目了然,看着很轻松并且感觉学到了知识;非常感觉,看了您的很多文章觉得不评论支持一下过意不去.

2015年9月21日 01:34 | # | 引用

广州哈哥 说：

阮老师，您好，我是0基础开始学习flex,今天看了你的这篇博文，发现有个地方好像你给弄反了。就是justify-content和align-items这两个属性。我试过了，其实，前者是设置项目在交叉轴上的对齐方式的，而后者是设置项目在主轴上的对齐方式的。

2015年9月23日 22:10 | # | 引用

六翼 说：

引用阮一峰的发言：
@longfei:

flex-basis都设为0，因为flex-grow定义的是，剩余空间分配的比例关系。

那请问不设为0的时候它是多少呢？看您的原文里是“auto”，但这个auto是怎么计算的？

2015年9月24日 09:58 | # | 引用

ixoixo 说：

能不能好好解释下flex-grow flex-shrink flex-basis的用法，网上的各种解释感觉都不好理解

2015年10月 9日 23:07 | # | 引用

年华果腹 说：

想学习flex的相关知识，找了几篇文章大概看了一下，觉得都不满意，突然在google上发现文章后面带有阮老师标识的文章，于是默默把其他的几篇文章的tab都关了

2015年10月30日 13:20 | # | 引用

phc 说：

引用广州哈哥的发言：
阮老师，您好，我是0基础开始学习flex,今天看了你的这篇博文，发现有个地方好像你给弄反了。就是justify-content和align-items这两个属性。我试过了，其实，前者是设置项目在交叉轴上的对齐方式的，而后者是设置项目在主轴上的对齐方式的。

我不知道自己理解的对不对，但是我觉得主轴的话也就是项目的排布方向，加入是水平排布，那么交叉轴即是垂直方向的，设置align-items:stretch；的话确实是在垂直方向上拉伸的，那align-itmes就是设置交叉轴的吧

2015年11月 5日 17:34 | # | 引用

大海的子民 说：

如果我把子元素按照固定像素来分配，是否可以（就是替换现在的float布局），还是子元素用width吗？

2015年11月 5日 21:32 | # | 引用

Jasmine 说：

很好用的布局，学习了！

2015年11月11日 15:19 | # | 引用

Citrus 说：

多次过来学习，非常感谢。

2015年12月12日 12:31 | # | 引用

professorz 说：

flex-direction 图片顺序和文字顺序是不是不一样呀。

2015年12月12日 17:35 | # | 引用

ppYoung 说：

原来是css-tricks上的文章翻译过来的，为什么不做说明
传送门：https://css-tricks.com/snippets/css/a-guide-to-flexbox/

2015年12月22日 11:37 | # | 引用

巫婆 说：

我每次写项目的时候也考虑过用flex布局，但是有的手机上显示不谦容。我到现在都不知道该怎么解决。

2015年12月30日 17:51 | # | 引用

wcg 说：

@mixin flex(){
display: -webkit-box; /* OLD - iOS 6-, Safari 3.1-6 */
display: -moz-box; /* OLD - Firefox 19- (buggy but mostly works) */
display: -ms-flexbox; /* TWEENER - IE 10 */
display: -webkit-flex; /* NEW - Chrome */
display: flex; /* NEW, Spec - Opera 12.1, Firefox 20+ */
}
body{
@include flex();
flex: 1;
justify-content: center;
align-items: center;
flex-direction: column;
}
#main{
@include flex();
height: 400px;
width: 1200px;
background-color: red;
}
div #main 并不会居中

2015年12月31日 15:42 | # | 引用

lomin 说：

想问一下，微信的内置浏览器是不是不支持这个属性啊。。我写了一个。在电脑上用chrome浏览器有用。在微信上没用了

2016年1月 7日 10:04 | # | 引用

wing-kai 说：

引用lomin的发言：
想问一下，微信的内置浏览器是不是不支持这个属性啊。。我写了一个。在电脑上用chrome浏览器有用。在微信上没用了

微信的话用display: box

2016年1月 9日 13:01 | # | 引用

littelbowl 说：

感谢科普，跟着demo学习下来很有收获。

2016年1月11日 15:20 | # | 引用

小天312 说：

移动端的兼容应该没有什么大问题了吧。可以在团队开发时候推广了吧？

2016年1月25日 17:37 | # | 引用

Silvers · Rayleigh 说：

引用longfei的发言：
阮老师，那个item的flex-grow属性，我写了个demo
CSS:
body{margin:0;}
ul,li{margin:0; padding:0;}
li{list-style-type:none;}
#list{border:2px solid gold; height:500px; display:flex; flex-direction:row;}
#list li{font-family:"microsoft yahei"; font-size:50px; background:#C00; color:#fff; margin:2px; flex-grow:1;}
#list li:nth-child(2){flex-grow:2;}

<ul id="list">
<li>test1</li>
<li>test2</li>
<li>test3</li>
</ul>
结果第2个li所占的宽度并不是其它li的2倍，为什么呢？比其它两个要大，但不足2倍。

这里是你理解错了，3个 li 平分下来每个是1/3。
你想实现的2个相等，1个宽度是其他2个的两倍实际上就是4个 li 平分，其中2个合并成1个，所以每个 li 是1/4，也就是#list li:nth-child(2){flex-grow:3;}

2016年1月30日 16:28 | # | 引用

Silvers · Rayleigh 说：

引用巫婆的发言：
我每次写项目的时候也考虑过用flex布局，但是有的手机上显示不谦容。我到现在都不知道该怎么解决。

不兼容可以用 display:box 试试看

2016年1月30日 16:29 | # | 引用

村小闹 说：

引用广州哈哥的发言：
阮老师，您好，我是0基础开始学习flex,今天看了你的这篇博文，发现有个地方好像你给弄反了。就是justify-content和align-items这两个属性。我试过了，其实，前者是设置项目在交叉轴上的对齐方式的，而后者是设置项目在主轴上的对齐方式的。

是你自己弄错了好吧~

2016年2月 1日 15:29 | # | 引用

无双 说：

http://flexboxin5.com/
博士哥与我本科生一站

2016年2月28日 16:13 | # | 引用

jingsam 说：

3.1 节关于 flex-direction 的部分，代码和图不是一一对应的。

2016年3月 3日 14:12 | # | 引用

大果子 说：

我就看看能不能发表成功

2016年3月 4日 10:46 | # | 引用

cc 说：

flex-wrap: wrap;
在微信内置浏览器中无效！

2016年3月19日 12:25 | # | 引用

cc 说：

引用cc的发言：
flex-wrap: wrap;
在微信内置浏览器中无效！


autoprefixer({browsers: ['last 10 version']})
这样都无效！

2016年3月19日 12:26 | # | 引用

cc 说：

引用cc的发言：

autoprefixer({browsers: ['last 10 version']})
这样都无效！

换个写法吧，历史的倒退！shit!

2016年3月19日 12:27 | # | 引用

SHUSHU 说：

谢谢老师讲解，之前的一些困惑现在看明白了

2016年3月25日 13:55 | # | 引用

杨继坤 说：

厉害

2016年4月 7日 17:03 | # | 引用

yanhaijing 说：

棒棒的

2016年4月 9日 18:46 | # | 引用

wlq 说：

阮老师，item翻译成项目感觉怪怪的，没有直接用item好理解点

2016年4月12日 10:56 | # | 引用

麦当真 说：

一峰老师，我简直不能更加感激您，也非常崇拜您。哇唔，我猜您已经将技术看作是艺术了吧！！！现在好多程序员生活都比较枯燥（我猜他们和我一样，嘻嘻）（每天都很忙，技术更新快，提升自己的技术还要完成项目），灵魂也很干涸（因为很忙，所以太少的时间感受生活，去吸取技术之外的东西来滋养我们的灵魂）。然而每次看您的博文，我就感觉自己经历了一场与艺术的邂逅，不仅学习了知识，还让我得以短暂的放松，让我的心灵经历了一次奇妙的旅行，然后再元气满满，整装继续上路。非常感谢您的分享，您无私的指引，以及心灵的关怀。

2016年4月14日 11:14 | # | 引用

MZ 说：

引用阮一峰的发言：
@longfei:

flex-basis都设为0，因为flex-grow定义的是，剩余空间分配的比例关系。

flex-basis设为0，那项目的初始大小是多大？

2016年4月27日 20:21 | # | 引用

善心法西斯 说：

很清楚，一目了然

2016年4月28日 23:58 | # | 引用

曾胜荣 说：

请问flex在任何浏览器都能用吗，有没有兼容性的问题

2016年5月11日 00:28 | # | 引用

赖俊杰 说：

老师的文章写得总是那么易懂

2016年5月13日 17:07 | # | 引用

林明哲 说：

图片很好！点赞。flex在安卓原生开发上也有了支持库。https://github.com/google/flexbox-layout

2016年5月16日 16:55 | # | 引用

Christopher 说：

前端自学者受用了，谢谢！

2016年5月16日 23:12 | # | 引用

walle 说：

好的老师不仅要学会知识，还要讲得通俗易懂，阮老师就是这样的老师

2016年5月19日 15:24 | # | 引用

react-native-android 说：

flex-direction这个属性的默认值是row吗？这样的话是不是默认情况下，item就是横向排列了。但是。我在做的过程中发现，如果不写flex-direction属性的话，item是竖向排列的

2016年5月26日 10:46 | # | 引用

laoyur 说：

还是没看明白align-content跟justify-content的区别 :(

2016年6月 7日 20:17 | # | 引用

落雨收柴 说：

老师，怎样使用flex布局使得两个组件的一部分重叠

2016年6月27日 17:39 | # | 引用

石海伟 说：

引用longfei的发言：
阮老师，那个item的flex-grow属性，我写了个demo
CSS:
body{margin:0;}
ul,li{margin:0; padding:0;}
li{list-style-type:none;}
#list{border:2px solid gold; height:500px; display:flex; flex-direction:row;}
#list li{font-family:"microsoft yahei"; font-size:50px; background:#C00; color:#fff; margin:2px; flex-grow:1;}
#list li:nth-child(2){flex-grow:2;}

<ul id="list">
<li>test1</li>
<li>test2</li>
<li>test3</li>
</ul>
结果第2个li所占的宽度并不是其它li的2倍，为什么呢？比其它两个要大，但不足2倍。

好像是按多余空间算的

2016年6月28日 15:57 | # | 引用

两仪 说：

玉峰老师的博客真写的通熟易懂 点赞一个

2016年6月28日 23:24 | # | 引用

卓 说：

引用石海伟的发言：
好像是按多余空间算的

一共有三个li元素，flex-grow:2即当前元素宽度为 父元素的2/3 并不是其他元素的两倍

2016年6月29日 16:08 | # | 引用

卓 说：

引用longfei的发言：
阮老师，那个item的flex-grow属性，我写了个demo
CSS:
body{margin:0;}
ul,li{margin:0; padding:0;}
li{list-style-type:none;}
#list{border:2px solid gold; height:500px; display:flex; flex-direction:row;}
#list li{font-family:"microsoft yahei"; font-size:50px; background:#C00; color:#fff; margin:2px; flex-grow:1;}
#list li:nth-child(2){flex-grow:2;}

<ul id="list">
<li>test1</li>
<li>test2</li>
<li>test3</li>
</ul>
结果第2个li所占的宽度并不是其它li的2倍，为什么呢？比其它两个要大，但不足2倍。

一共有三个li元素，flex-grow:2即当前元素宽度为 父元素的2/3 并不是其他元素的两倍

2016年6月29日 16:09 | # | 引用

Mr.Luo 说：

默认好像是flex-wrap: wrap;

2016年7月 1日 16:17 | # | 引用

卓 说：

请问: 针对此属性 justify-content: space-between 3个元素为一行排列，最后多余的两个多余的元素如何让它靠左排布，事实上是左右排布了，表面看就是中间空了个元素，请看demo

1 2 3 4 5
.container {width: 400px;display: flex;justify-content: space-between;flex-flow: row wrap;
}

span {width: 110px;background-color: #f60;border-radius: 5px;margin-top: 10px;padding: 10px;
}
2016年7月 5日 10:47 | # | 引用

卓 说：

引用卓的发言：
请问: 针对此属性 justify-content: space-between 3个元素为一行排列，最后多余的两个多余的元素如何让它靠左排布，事实上是左右排布了，表面看就是中间空了个元素，请看demo


1
2
3
4
5


.container {width: 400px;display: flex;justify-content: space-between;flex-flow: row wrap;
}

span {width: 110px;background-color: #f60;border-radius: 5px;margin-top: 10px;padding: 10px;
}


2016年7月 5日 10:49 | # | 引用

键盘侠 说：

我只想说这个css3的新属性flex局势一个巨坑，谁用谁知道。安卓低端机完全不支持

2016年7月 9日 17:16 | # | 引用

Yac 说：

目前发现一个问题，和@卓貌似是一个问题：
父元素：justify-content: space-between
在每排3个元素一共5个元素情况下，第五个元素怎么实现居中？
现在的效果是第1、2、3元素正常，4元素居左，5元素居右

2016年7月10日 03:19 | # | 引用

肖德华 说：

UC浏览器设置flex：1；盒子里面加入文字 弹性盒子会被撑开要怎么解决，其他浏览器都是正常的

2016年7月10日 17:10 | # | 引用

zw 说：

不得不说，看了半天外文网站， 不如看十分钟阮大师的。

2016年7月13日 16:42 | # | 引用

liangwang 说：

"Webkit内核的浏览器，必须加上-webkit前缀。“， 我测试了下safari和chrome，都不需要的。

2016年7月14日 10:34 | # | 引用

liangwang 说：

问下，支付宝是否已经有页面部署了flex的布局？ 似乎各大浏览器，除了chrome支持的都不是特别好，比如IE8就，FireFox46之前的，Safari9.1之前的都不支持

2016年7月14日 10:46 | # | 引用

孟泰德 说：

引用liangwang的发言：
"Webkit内核的浏览器，必须加上-webkit前缀。“， 我测试了下safari和chrome，都不需要的。

在ios8及以下的版本中就需要了

2016年7月19日 13:12 | # | 引用

vec 说：

太好了，总算是弄明白了，谢谢博主！

2016年8月 5日 00:18 | # | 引用

前端小菜 说：

怎么用flex实现footer一直存在在屏幕下方 不随滚动消失

2016年8月 5日 10:51 | # | 引用

zhishaofei3 说：

引用Silvers · Rayleigh的发言：
这里是你理解错了，3个 li 平分下来每个是1/3。
你想实现的2个相等，1个宽度是其他2个的两倍实际上就是4个 li 平分，其中2个合并成1个，所以每个 li 是1/4，也就是#list li:nth-child(2){flex-grow:3;}


3也不行吧？

2016年8月 5日 13:11 | # | 引用

zhishaofei3 说：

引用longfei的发言：
阮老师，那个item的flex-grow属性，我写了个demo
CSS:
body{margin:0;}
ul,li{margin:0; padding:0;}
li{list-style-type:none;}
#list{border:2px solid gold; height:500px; display:flex; flex-direction:row;}
#list li{font-family:"microsoft yahei"; font-size:50px; background:#C00; color:#fff; margin:2px; flex-grow:1;}
#list li:nth-child(2){flex-grow:2;}

<ul id="list">
<li>test1</li>
<li>test2</li>
<li>test3</li>
</ul>
结果第2个li所占的宽度并不是其它li的2倍，为什么呢？比其它两个要大，但不足2倍。

是按剩余空间算的，因为你里面有文字，所以刨去了文字宽度，你去掉文字就好了

2016年8月 5日 14:08 | # | 引用

zousjun 说：

引用zhishaofei3的发言：
是按剩余空间算的，因为你里面有文字，所以刨去了文字宽度，你去掉文字就好了

这里是必须先除去每个元素实际占有的大小之后，然后按照你设置的比例来分配空间，h

还有默认空间应该是flex-grow： 1，而不是flex-grow： 0；

<ul id="list">
  <li>test1</li>
  <li>test2</li>
  <li>test3</li>
</ul>
body{margin:0;}
	ul,li{ margin:0; padding:0;}
	li{ list-style-type:none;}
	#list{ border:2px solid gold; height:500px; display:flex; flex-direction:row;}
	#list li {
		width: 120px;
	}
	#list li{font-family:"microsoft yahei"; font-size:50px; background:#C00; color:#fff; margin:2px; flex-grow:1;}
	#list li:nth-child(2){flex-grow:2;}
	#list li:nth-child(3){
		flex-grow: 0;
	}
你可以比较一下两段代码的不同

2016年8月17日 18:27 | # | 引用

微风 说：

苹果手机的IOS8系统不支持flex布局，有什么好方法吗？

2016年8月25日 16:48 | # | 引用

小汤 说：

不错，容易明白，大神就是大神

2016年9月 9日 15:15 | # | 引用

felbry 说：

今天实践过程中发现了一个理解误区，就是刚开始把justify-content误认为是指定水平对齐方式（其实针对的是主轴），而align-items是指定垂直对齐方式。而指定主轴需要用到flex-direction(默认为水平)。不过后来想想，假使指定主轴为竖直的话，那主轴和交叉轴是不是就是一样了？还有那个align-content说的是针对多根轴线，是不是就意味着如果主轴指定为column，就是主轴和交叉轴一样是一根线了，如果主轴为默认，那么当主轴和交叉轴的对齐方式一样的话，直接用一个align-content属性就ok了？

2016年9月14日 15:44 | # | 引用

lavender 说：

很明了，很直观，感谢博主~

2016年10月 8日 14:25 | # | 引用

家兴 说：

flex-direction: row | row-reverse | column | column-reverse;

这部分的描述和下面的配图，容易误导一些新手哈

可能会造成 row = 下图第一个 依次的顺序

2016年10月10日 11:11 | # | 引用

张宝 说：

“四、项目的属性”这个标题的字体小了，之前同种标题都是,应该是H2

2016年10月31日 12:40 | # | 引用

cnwhy 说：

在我测试中有这样的感觉,还请指正
1.当主轴设置的是水平方向时(row,row-reverse)方向还和容器的dir属有关; 
flex-direction 的方向是相对dir设置的方向来设置的.

2.交叉轴的方向(默认和主轴换行的方向一至),flex-wrap: wrap-reverse; 会改变交叉轴的方向

demo: http://sandbox.runjs.cn/show/zkqimsj5


2016年11月 1日 18:17 | # | 引用

良心的荒野开拓者 说：

引用phc的发言：
我不知道自己理解的对不对，但是我觉得主轴的话也就是项目的排布方向，加入是水平排布，那么交叉轴即是垂直方向的，设置align-items:stretch；的话确实是在垂直方向上拉伸的，那align-itmes就是设置交叉轴的吧

2016年11月11日 14:37 | # | 引用

LeoHsia 说：

真的非常感谢！解决了从入行以来一直面临的垂直居中的大问题，在很多应用场景中可以实现。虽然负面性还有待发掘，真的是非常感谢博主！！！

2016年12月 5日 22:45 | # | 引用

螃蟹 说：

感谢阮老师无私教诲

2016年12月13日 10:36 | # | 引用

Cody Constant 说：

以前一直对flex模糊不清，终于决定攻破它，打开了好几篇教程，看完阮老师的后，彻底会用啦！谢谢您

2016年12月17日 15:24 | # | 引用

dfb 说：

我有个等高布局不懂，就是左边有一张1000多px高的图片，右边为文字区域。

怎么让其当右边文字区域的高度小于浏览器高度时，左边的图片高度为浏览器高度，
当右边文字区域的高度大于浏览器高度时，则左边的图片的高度为右边文字区域的高度？

要求是：不用js控制，还有不能把左边的图片当背景图来使用

2016年12月23日 09:51 | # | 引用

flowplay 说：

flex-grow, flex-shrink,flex-basis可能不好理解，补充下，这里指的空间是主轴空间，是水平的还是垂直的，依flex-direction而定

2016年12月26日 21:47 | # | 引用

vinceok 说：

引用zhishaofei3的发言：
是按剩余空间算的，因为你里面有文字，所以刨去了文字宽度，你去掉文字就好了

引用Silvers · Rayleigh的发言：
这里是你理解错了，3个 li 平分下来每个是1/3。
你想实现的2个相等，1个宽度是其他2个的两倍实际上就是4个 li 平分，其中2个合并成1个，所以每个 li 是1/4，也就是#list li:nth-child(2){flex-grow:3;}

你说的很对，博主没有说清楚

2017年1月 6日 10:40 | # | 引用

炉石不传说 说：

引用chshouyu的发言：
现在介绍有点晚了吧-_-#

不晚，我就是刚刚来学习的，因为小程序出来了，学习一下布局

2017年1月 9日 14:25 | # | 引用

The One 说：

引用Silvers · Rayleigh的发言：
这里是你理解错了，3个 li 平分下来每个是1/3。
你想实现的2个相等，1个宽度是其他2个的两倍实际上就是4个 li 平分，其中2个合并成1个，所以每个 li 是1/4，也就是#list li:nth-child(2){flex-grow:3;}

flex-grow分的是剩余的空间你要看你内容之外的空间

2017年1月10日 10:44 | # | 引用

lightbee 说：

引用广州哈哥的发言：
阮老师，您好，我是0基础开始学习flex,今天看了你的这篇博文，发现有个地方好像你给弄反了。就是justify-content和align-items这两个属性。我试过了，其实，前者是设置项目在交叉轴上的对齐方式的，而后者是设置项目在主轴上的对齐方式的。

没有错啊，你再试试看，或者是你理解错了吧。
2017年1月26日 00:03 | # | 引用

ReedSUN 说：

阮老师，在align-content属性中，您说 `align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。` 一开始我没太看明白，后来才发现这里说的应该是多行的对齐方式。我觉得在这里用行代替轴线更容易解释整个属性。

2017年2月 9日 00:53 | # | 引用

Sherry 说：

四、项目的属性 应该是h2标签吧，现在用的是h3标签

2017年2月13日 11:04 | # | 引用

我叫春 说：

使用align-content属性，如何定义多轴？
求html代码，或者align-content的Demo

2017年2月17日 09:54 | # | 引用

雨辰 说：

这篇是我看到讲得最好的一篇

2017年2月17日 14:44 | # | 引用

lihsai0 说：

尝试了一下flex+单行省略号，发现盒子被撑开好多。

2017年2月17日 22:44 | # | 引用

艺米 说：

您好，我试了一下align-content，将其设置成stretch，并不会把每行拉伸，填满容器高度。而是在每行下面留有相同高度的空白。能否确认一下？

2017年2月21日 18:59 | # | 引用

前段之路 说：

非常好~讲的清楚明白

2017年2月22日 11:43 | # | 引用

冬天 说：

每次看到您的内容， 我嘴里默默来了一个句 阮大神~~~

2017年2月22日 14:33 | # | 引用

全栈攻城狮 说：

每个例子都照着敲了一遍，真赞。敲完之后，对flex布局了解的也就差不多了。谢谢阮大神，如果不是你，我还困在MDN的文档里，犯糊涂呢。哈哈哈

2017年2月22日 15:47 | # | 引用

夏目比丘 说：

谢谢阮老师，您传授给我们的知识让我们收获很多

2017年3月 8日 18:07 | # | 引用

youkelike 说：

"多根轴线的对齐方式" 是不是指出现了多行item的情况，每行一根轴线，多行item就有多根轴线？

2017年3月12日 18:04 | # | 引用

liaokai 说：

浏览这篇文章就是一次赏心悦目的浏览体验，配图清爽明了，真希望我以后看到的文章都有这么好的浏览体验

2017年3月27日 11:23 | # | 引用

JoKer 说：

我测试加入了 align-items: flex-start; 子标签加入了align-self: flex-end; 惊人的发现 在不同的浏览器 flex-end 和flex-start 效果不一样 这要如何解决？我放在谷歌和Edege里 效果居然上下相反

2017年4月 1日 17:17 | # | 引用

leon 说：

老师写的文章真的很清晰，期待您的续作。

2017年4月 4日 15:53 | # | 引用

Rachel 说：

老师的文章和配图很赞！

2017年4月12日 16:08 | # | 引用

王骞 说：

总结的真好，条理清晰，便于理解和记忆。真是个有思想的人

2017年4月14日 16:47 | # | 引用

leon 说：

仔细过了一遍真的很方便.

2017年5月 1日 22:30 | # | 引用

牧羊人 说：

有事没事就逛阮老师的博客，受益匪浅。

2017年5月10日 09:04 | # | 引用

京川啟继FE 说：

一讲就懂，很棒，超棒，非常棒；
哪怕有些玩家吐槽进了阿里文章变得不精致了；这篇文章也远比网上泛滥的各种云里雾里的资料有用得多。
感谢大大的分享√

2017年5月16日 19:58 | # | 引用

JailBreak 说：

将文章中提及的布局 全部实现了一遍，源码：

https://github.com/JailBreakC/flex-box-demo

2017年5月23日 14:27 | # | 引用

nollyup 说：

非常好的文章，详细明了

2017年5月23日 17:03 | # | 引用

阮一峰 说：

@JailBreak：

赞！ 我要把它加到教程里面。

2017年5月24日 07:29 | # | 引用

Zen 说：

我也来做点贡献，看完阮一峰老师的教学文章，临时做了个 flex 布局动态测试的 demo，支持 flex 所有的属性测试，希望能对大家有所帮助

演示地址 : https://ihuangmx.gitbooks.io/front-demo/content/zen-flex-demo.html#flex-布局在线测试

源码：https://github.com/ihuangmx/zen-flex-online

2017年5月25日 17:16 | # | 引用

JailBreak 说：

@阮一峰：

哈哈，多谢阮老师！

2017年6月 1日 16:08 | # | 引用

laiqi 说：

阮一峰老师的教学文章真的太棒了，感谢有您，指路明灯

2017年6月 1日 18:34 | # | 引用

xxx 说：

实现过之后发现 3.1 flex-direction属性 中的图中的效果和下面的文字描述顺序就不一致

2017年6月 8日 15:13 | # | 引用

柏运送 说：

阮老师，flex布局，左边自适应，右边固定宽，但当页面缩小到一定比例后，左边不在自适应了，而是右边变小了，sapn的宽度好像不能一直按照70%的比例缩小下去



DOM3 event textInput

body{
padding:0;
margin:0;
font-size:0;
}
.box{
display: flex;
}
.d1{
flex:1;
border:1px solid blue;
margin-right:15px;
}
.d2{
width:300px;
border:1px solid red;
min-height:100vh;
}
.span{
display: inline-block;
width:70%;
border:1px solid red;
overflow: hidden;
white-space: nowrap;
text-overflow:ellipsis;
font-size:12px;
}





Loommodi cumque us repellendus unde veritatis? Beatae doloribus 





2017年6月 8日 23:56 | # | 引用

Alex Zou 说：

3.1 flex-direction属性

样式中 属性 和 下面示意图 中的顺序 不一致。 有阅读误导。

图中顺序 对应为：
flex-direction: column-reverse | column | row | row-reverse;

2017年6月12日 17:51 | # | 引用

小小柴 说：

阮大神我发现flex-basis这个属性好像并不是主轴所占空间，如果我将主轴方向定为垂直排列flex-direction: column;再给他定义flex-basis的属性，结果我发现只有水平方向的大小在变，垂直方向无效果

2017年6月14日 15:28 | # | 引用

去去去 说：

看完以后，加深了印象

2017年6月14日 17:59 | # | 引用

老姚 说：

谢谢您的教程
整整两年了 即使到现在依然是非常好的react-native中文入门教程
2017年7月17日 14:13 | # | 引用

Msea 说：

真心感谢 阮一峰同学

2017年7月26日 21:03 | # | 引用

Lulin 说：

引用小小柴的发言：
阮大神我发现flex-basis这个属性好像并不是主轴所占空间，如果我将主轴方向定为垂直排列flex-direction: column;再给他定义flex-basis的属性，结果我发现只有水平方向的大小在变，垂直方向无效果

主轴就是水平方向的啊，垂直方向的叫做交叉轴。

2017年7月27日 16:31 | # | 引用

Better 说：

设为 Flex 布局以后，子元素的float属性没有失效呀。。。

2017年7月31日 11:08 | # | 引用

Better 说：

我自己看错了。。。[允悲]，设为 Flex 布局以后，子元素的float、clear和vertical-align属性将失效是OK的。

2017年7月31日 11:13 | # | 引用

cshenger 说：

我发现这个文章的亮点现在在评论区了，从15年的7月到17年的7月，整整跨了两年！！！

2017年8月16日 11:09 | # | 引用

今晚打老虎 说：

处于转型阶段的我，第一次看到这么详细的介绍，对于我来说就是雪中送炭啊！！！

2017年9月 7日 17:26 | # | 引用

薛定谔的猫 说：

引用cshenger的发言：
我发现这个文章的亮点现在在评论区了，从15年的7月到17年的7月，整整跨了两年！！！

不要大惊小怪，阮大师的文章一向如此，两年并不算多
2017年9月13日 11:23 | # | 引用

korea 说：

flex-direction这块配图顺序是不是还可以优化？容易误导人

2017年9月18日 11:42 | # | 引用

ellen 说：

vue里面使用justify-content：flex-end 无效

2017年9月18日 17:40 | # | 引用

杨 说：

纠正一下。当align-items : baseline的时候，子元素的vertical-align是有效的

2017年9月21日 23:19 | # | 引用

薯条君与番茄酱 说：

大爱 太实用的

2017年9月22日 12:02 | # | 引用

一条不会发电的鳗鱼 说：

引用longfei的发言：
阮老师，那个item的flex-grow属性，我写了个demo
CSS:
body{margin:0;}
ul,li{margin:0; padding:0;}
li{list-style-type:none;}
#list{border:2px solid gold; height:500px; display:flex; flex-direction:row;}
#list li{font-family:"microsoft yahei"; font-size:50px; background:#C00; color:#fff; margin:2px; flex-grow:1;}
#list li:nth-child(2){flex-grow:2;}

<ul id="list">
<li>test1</li>
<li>test2</li>
<li>test3</li>
</ul>
结果第2个li所占的宽度并不是其它li的2倍，为什么呢？比其它两个要大，但不足2倍。

引用zhishaofei3的发言：
是按剩余空间算的，因为你里面有文字，所以刨去了文字宽度，你去掉文字就好了

zhishaofei3 说得对，确实是文字影响了item的宽度；
如果要修改的话，考虑到 longfei的代码里面 现在只是修改了flex-grow而剩余两个用的是默认值（也就是flex-shrink:1;flex-basis:auto;）。
可以根据 阮老师写的“建议优先使用flex这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。”，把代码修改成
#list li{flex:1;}
#list li:nth-child(2){flex:2;}
这样显示出来就和没有文字的时候一样是两倍，不会因为文字影响了宽度；

2017年9月26日 16:10 | # | 引用

xbup 说：

想问一个问题
如果我拥有一个高为500px的容器
并flex-direction:row，flex-wrap:warp
添加两个项目宽均为100%
那么这两个项目会均分高,为什么
即使我没有指定他们的高度

2017年10月14日 17:43 | # | 引用

xbup 说：

引用xbup的发言：
想问一个问题
如果我拥有一个高为500px的容器
并flex-direction:row，flex-wrap:warp
添加两个项目宽均为100%
那么这两个项目会均分高,为什么
即使我没有指定他们的高度

经验证，flex-grow自动默认到了1

2017年10月14日 18:03 | # | 引用

xbup 说：

引用xbup的发言：
经验证，flex-grow自动默认到了1

即使不设置100%也会如此啊。。。。。。。。。。

2017年10月14日 18:11 | # | 引用

destiny 说：

阮老师，我做demo时，发现flex-wrap会把交叉轴的方向都改变了，垂直方向flex-start本来是顶部，变成了底部

2017年10月16日 15:33 | # | 引用

nissa 说：

引用Silvers · Rayleigh的发言：
这里是你理解错了，3个 li 平分下来每个是1/3。
你想实现的2个相等，1个宽度是其他2个的两倍实际上就是4个 li 平分，其中2个合并成1个，所以每个 li 是1/4，也就是#list li:nth-child(2){flex-grow:3;}


这个分配还是不完全 等比1：2：3的

2017年11月 9日 13:44 | # | 引用

Mr_yuan 说：

css挂掉了啊。。页面变形了

2017年11月14日 11:39 | # | 引用

红烧肉 说：

align-content 这个东西的解释有问题，应该是多行，而不是多轴

2017年11月20日 15:46 | # | 引用

上善若水2324 说：

为什么不把您的文章整理成书籍呢？期待中

2017年11月29日 14:42 | # | 引用

随旭东 说：

flex-direction配图不走心啊

2017年11月29日 15:49 | # | 引用

好人 说：

居然不知道flex还有这么多属性,写的很好,虽然有人吐槽说什么进了阿里文章写得不如以前精致,不知道还要怎么精致,自己写不出来,还好意思吐槽别人的文章,有本事写个精简的,把链接发出来,不然就别指责别人,我也是长见识了

2017年12月11日 15:45 | # | 引用

文里 说：

很好，非常受用。之前看 css-tricks 的教程看得一头雾水，在这篇文章里理清了很多概念，卡住的一些问题也得到了解决。十分感谢博主。

2017年12月18日 19:23 | # | 引用

断水流 说：

文章写的很不错，配图很给力，简单明了。我看了很多阮老师的文章，有点不敢相信，感觉好像什么都会一样，学Python看得到教程，学前端出看得到教程，而且都还讲得挺不错。

2017年12月21日 15:06 | # | 引用

EmmanuelAgui 说：

引用小小柴的发言：
阮大神我发现flex-basis这个属性好像并不是主轴所占空间，如果我将主轴方向定为垂直排列flex-direction: column;再给他定义flex-basis的属性，结果我发现只有水平方向的大小在变，垂直方向无效果

flex-direction这个属性是容器container的属性，你外层容器设置flex-direction:column（此时主轴就是垂直方向）,在项目item里面设置flex-basis属性为不同值，这样主轴（即垂直方向）所占的大小就会变化。

2017年12月22日 14:34 | # | 引用

hanzichi 说：

也做了个直观的 demo，感谢阮老师 https://hanzichi.github.io/2017/flex/index.html

2017年12月24日 14:44 | # | 引用

石丽丽 说：

在谷歌中，item的align-self 并不是居中在父亲的中间的。

2018年1月13日 13:58 | # | 引用

JohnnyWu 说：

引用石丽丽的发言：
在谷歌中，item的align-self 并不是居中在父亲的中间的。

容器的justify-content设置成space-between

2018年1月22日 11:26 | # | 引用

小西 说：

此文大赞！看一次就明白了，作者大才，才能这样简洁就把知识讲得这样透彻。

2018年1月24日 17:43 | # | 引用

tenyiyi 说：

厉害了 16年看了一遍，今天再看一遍

2018年1月31日 14:36 | # | 引用

Limengke 说：

反复看了几次了，很少用，所以老记不住

2018年2月 5日 13:49 | # | 引用

1080 说：

@Silvers · Rayleigh：

回答有毛病吧，flex-grow分的是剩余的空间，你的字体大小50px的大小本身就占了空间，应该把这个空间除去再分

2018年2月 7日 11:12 | # | 引用

Airmole 说：

今天做微信小程序的时候要做一个png图标+说明文字的分享的按钮，结果分享图标始终无法和文字在一条水平线上对齐，就是用了flex布局（display: flex; flex-direction: row; align-items: center;），结果分享图标确实是和文字在一条水平线线上了。但是却把button按钮撑的特别大，根本没了按钮的样子。。。

2018年2月14日 20:00 | # | 引用

f'd'f 说：

一峰老师，我简直不能更加感激您，也非常崇拜您。哇唔，我猜您已经将技术看作是艺术了吧！！！现在好多程序员生活都比较枯燥（我猜他们和我一样，嘻嘻）（每天都很忙，技术更新快，提升自己的技术还要完成项目），灵魂也很干涸（因为很忙，所以太少的时间感受生活，去吸取技术之外的东西来滋养我们的灵魂）。然而每次看您的博文，我就感觉自己经历了一场与艺术的邂逅，不仅学习了知识，还让我得以短暂的放松，让我的心灵经历了一次奇妙的旅行，然后再元气满满，整装继续上路。非常感谢您的分享，您无私的指引，以及心灵的关怀。

2018年2月27日 18:00 | # | 引用

刘朋朋 说：

引用云墨雪的发言：
坐个沙发, ie10的普及率还有待观望啊..

IE低版本是毒瘤啊

2018年3月 9日 10:10 | # | 引用

符永盛 说：

研习完真想给峰哥点赞，可以没有这个功能~~真心感谢峰哥分享的知识^v^

2018年3月11日 10:30 | # | 引用

九月 说：

看了一遍评论，有些错误，好像一直没改正。

2018年3月23日 16:39 | # | 引用

李成 说：

阮大大，您在属性align-content处有地方解释有点模糊，应该是在交叉轴方向上有多行时，align-content属性能作用；原文大意也是如此：“This aligns a flex container's lines within when there is extra space in the cross-axis, similar to how justify-content aligns individual items within the main-axis.”

https://css-tricks.com/snippets/css/a-guide-to-flexbox/

2018年4月 3日 00:30 | # | 引用

feng 说：

flex弹性布局 田字格布局怎么做？
2018年4月 9日 13:55 | # | 引用

CodeDeer 说：

做了一个可交互的演示站flexbox演示站
初学者可以看一下快速帮助理解
https://xluos.github.io/demo/flexbox/

2018年4月10日 23:20 | # | 引用

none 说：

MDN上找到的一个示例网站：http://the-echoplex.net/flexyboxes

2018年4月23日 17:01 | # | 引用

王平 说：

4.6 align-self属性
align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

最后一句：“如果没有父元素”，应该是如果父元素没有设置 align-items 属性的意思吧

2018年4月28日 14:55 | # | 引用

黄仔辉 说：

感谢 您对前端初学者的贡献，Flex知识点整理的非常好，我原本以为我很熟了，结果一看，查漏补缺了，感谢！
另外 页面的排版 很舒服，让我想看下去的冲动，如果排版不行的话，我大概瞄一眼就没耐心看下去了。

2018年5月 9日 11:12 | # | 引用

xiaokeke 说：

别吹过头了，图基本就是照搬国外网站的。https://css-tricks.com/snippets/css/a-guide-to-flexbox/#flexbox-background

2018年6月18日 12:04 | # | 引用

漫长。 说：

不错，以前用得稀里糊涂，看完您的文章之后，有了总体把握。

2018年7月 4日 09:05 | # | 引用

yang 说：

不错看了学的很清晰

2018年7月14日 09:45 | # | 引用

Ada.H 说：

main axis, cross axis. 主轴水平，交叉轴垂直，这个是在flex-direction: row;的前提下定义的吧

2018年7月24日 15:09 | # | 引用

dmm 说：

justify-content取值还可以是space-evenly，上面没有提到
https://css-tricks.com/snippets/css/a-guide-to-flexbox/#article-header-id-6

2018年7月25日 13:50 | # | 引用

小A 说：

flex布局高度问题怎么解决

2018年8月 4日 15:01 | # | 引用

李文磊 说：

align-content:space-between; 配图不对，误导我很久

2018年8月21日 13:28 | # | 引用

????天涯 说：

子div设置 flex-grow 后，如果没有内容是正确的，如果设置了内容，布局就变掉了，请问是怎么回事？

2018年9月 4日 18:48 | # | 引用

荣先森 说：

感谢，文章加配图看懂了，怎么提高自己的js编写能力，看别人代码还好，但是一到自己写，，，，，就不知道了

2018年9月12日 11:41 | # | 引用

李杨 说：

align-content这个定义多根轴线的说法有误，这个主要是针对定义了wrap或wrap-reverse属性的父容器垂直布局，从形意理解上来说它和 justify-content正好是一个横竖布局的对应关系。

2018年10月10日 15:28 | # | 引用

韦得 说：

为什么在PHP文件中不支持flex横向布局呢？

2018年11月 9日 06:13 | # | 引用

Ron 说：

做了一年左右纯前端，flex布局入门就是看您的博客。今天再次看到，想起忘了给您说声谢谢了。


thx。

2018年11月26日 17:30 | # | 引用

herbert 说：

flex-direction 对应的图列是否反了，row 应该是从左往右的箭头

2018年12月11日 16:39 | # | 引用

weiyinfu 说：

建议顶部加一个阅读进度条，因为目前评论太多了，右侧进度条根本无法反应实际进度。
实现很简单，就加一个fixed div，让它的背景色为特定颜色，捕捉滚动条滚动事件，更新div的宽度。

2019年1月 7日 14:27 | # | 引用

xxyangyoulin 说：

网站搞一个目录看着就更方便了。

2019年1月25日 21:06 | # | 引用

bokerr 说：

虽然存在小瑕疵，但是不得不佩服讲得非常的有结构，认真拜读完收益良多。

2019年3月 6日 23:13 | # | 引用

Gavin 说：

非常棒的讲解！受益匪浅~

2019年3月17日 08:21 | # | 引用

王宏亮 说：

如何让item主动换行呢？比如我希望4个一行。

2019年3月27日 17:15 | # | 引用

徐凌波 说：

突然读到下面这里的后一句不明白了。
“align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。”
‘如果项目只有一根轴线’？ 这个怎么理解。
再开始的时候我们介绍说。‘容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）’。并没介绍容器里面项目也有轴线。求解。

2019年3月27日 19:27 | # | 引用

痴人的梦 说：

引用徐凌波的发言：
突然读到下面这里的后一句不明白了。
“align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。”
‘如果项目只有一根轴线’？ 这个怎么理解。
再开始的时候我们介绍说。‘容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）’。并没介绍容器里面项目也有轴线。求解。

多个轴线既：一个容器内多个flex容器
2019年3月29日 15:19 | # | 引用

刘骏佳 说：

我有一个问题 flex:1 这种写法 不是 省略后两项吧 flex:1 ≠ flex-grow:1吧

2019年4月 4日 21:52 | # | 引用

我要发表看法
您的留言 （HTML标签部分可用）


您的大名：

 «-必填

电子邮件：

 «-必填，不公开

个人网址：

 «-我信任你，不会填写广告链接

记住个人信息？

 «- 点击按钮

2019 © 联系方式 | 邮件订阅