---
title: 关于CSS display的多种用法
subtitle: The display keyword usages summary
date: 2016-08-28 21:30:02
tags: CSS3
header-img: /img/post_display.jpg
comments: True
---
## 前言
相信很多人对css中display的用法有很多的confuse，特别是block, inline, inline-block，甚至还有CSS3最新的flex。你可能有这个感觉：  

<img src="/img/frustrated.jpg" width="300em" />
 
没关系，现在我来帮大家梳理下这几个值的用法和特性

## display: block
>	将元素显示成块级元素  

最典型的block元素就是常见的div了，块级元素有以下特点：

-  总是在新行开始（一个block元素占满一行，除非使用了float）
-  默认的宽度是容器的100%
-  可以指定宽高，若指定了宽度，其仍然会占满一行（剩余的部分用margin填满），这个时候如果给它设置 *margin: auto* 便可以让此块级元素居中显示，请[参考示例](http://codepen.io/hejiaji/pen/QEZqxw)
-  Block元素只能被嵌套在block元素内
-  常见的块级元素有 DIV, FORM, TABLE, P, PRE, H1~H6, DL, OL, UL 等

## display: inline
> 将元素显示成行内元素

这类元素和它们的名字很搭，行内元素，允许和其他元素在一行里😄，行内元素的特点是：

-  不能包含块级元素
-  不会独占一行，可以和别的元素“分享”整行
-  不能给其设置宽高，它的宽高由它的children决定
-  能够给 margin 和 padding 指定 *left* 和 *right*，但是对 *top* 和 *bottom* 无效
-  常见的内联元素有 SPAN, A, STRONG, EM, LABEL, INPUT, SELECT, TEXTAREA, IMG 等。 
-  *inline元素一般无法自己实现居中效果，可在外层添加一个块级元素，用块级元素的特性居中*

## display: inline-block
> 将元素显示为内联元素

这个命名很奇怪，又是inline，又是block的，很让人疑惑，其实它就是二者的杂交，继承了二者的一部分特点，但是其本质上还是一个inline元素（毕竟inline在前面嘛），这类元素的特点是：

-  它并不会独占一行，但是它是一个块级元素
-  可以给它设定宽度和高度
-  支持 margin 和 padding 的所有属性

## *display: flex
> flex属性是CSS3引进的新特性，个人认为其非常强大，但是有所有新特性的硬伤：兼容性问题，
 
如果要支持低版本浏览器的话，使用这个属性可能会有些头疼，但是对于高版本的浏览器来说，flex真的太强大了，它可以帮你非常简单的控制子元素的排列，而不需要对子元素做任何操作，这里只对其中做个大概介绍和讲解一下其居中的用法：

```
display: flex;     
align-items: center;     
justify-content: center;
```
其中 **align-items：center** 是指让子元素在垂直方向居中，而 **justify-content：center** 是指让子元素在水平方向居中，具体用法请[参考示例](http://codepen.io/hejiaji/pen/grVvAj)

## 后话
看到这里相信大家对display最常见的几个用法已经很熟悉了！再附上一张图来对这三种display有一个更直观的概念：![display](/img/display-special.png)
另外貌似IE的老版本是不认识inline-block这个属性了，不过anyway，who cares about IE？