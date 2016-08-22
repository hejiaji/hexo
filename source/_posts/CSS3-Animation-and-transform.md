---
title: CSS3中两种动画表现形势的优劣
subtitle: The differences between transition/transform and animation in CSS3
header-img: /img/post-css-difference.jpg
date: 2016-08-19 15:33:16
tags: CSS3
---
# 前言
众所周知，CSS3的其中一个令人兴奋的较大改变便是加入了动画效果，没错！不用JQuery或其他第三方库，单单几行CSS代码，就可以写出一些非常棒的动画页面。目前， 各大浏览器厂商已经逐渐兼容这些CSS3语法，所以使用它你不用过多考虑兼容性问题。

CSS3动画相关的几个属性：transition transform animation; 中文翻译过来是过渡，转化和动画。

[transform](http://www.w3schools.com/cssref/css3_pr_transform.asp)主要是用于应用于一个元素2D或者是3D的变化，如旋转，放大，移动等等。但是单只是它这一个属性是没法做出一个动画效果的，所以它必须要跟[transition](http://www.w3schools.com/cssref/css3_pr_transition.asp)配合使用，就会变得很平滑，所以这两兄弟经常一起出现。[animation](http://www.w3schools.com/css/css3_animations.asp)自成一派，最早安家于Safari浏览器，其于关键字 **@keyframe** 配合使用，效果非常强大

# transform和transition
选择将这两者放在一起讲的原因是这两者就像是豆浆和油条，两者一起使用才最是最佳搭配。

**transform**的基本语法如下：

```
transform: none|transform-functions|initial|inherit;
```
值为none的话就表示没有transform，一般transform-functions包含了[translate](http://www.w3schools.com/cssref/playit.asp?filename=playcss_transform_translate)，[scale](http://www.w3schools.com/cssref/playit.asp?filename=playcss_transform_scale)，[rotate](http://www.w3schools.com/cssref/playit.asp?filename=playcss_transform_rotate)等等。也就是对元素的形状，位置等因素进行改变。

**trasition**元素实际上是4个元素的简写（速记）模式
> transition-property : //过渡的性质，比如transition-property:background 就是指background参与这个过渡       
> transition-duration: //过渡的持续时间    
> transition-delay: //延迟过渡时间     
> transition-timing-function: //指定过渡类型，有ease | linear | ease-in | ease-out | ease-in-out | cubic-bezier

具体事例可以参考一下w3school的 [example](http://www.w3schools.com/cssref/tryit.asp?filename=trycss3_transition)。

两者相互搭配的效果可以参考[示例](https://codepen.io/hejiaji/pen/bZJQOj)

```
transition: transform 1s ease-in-out;
```
以上代码将transition和transform接合起来，另由于浏览器兼容问题，最好加上以下代码以便兼容主流浏览器

```
-webkit-transition: transform 1s ease-in-out;
```

# animation
animation可以让一个元素渐渐的的从一个style变成另一个style，你可以想改变任意个CSS属性，**任意次数**，要用CSS3 anmation，你必须为动画声明对应的 keyframes。

keyframes的基本使用方式如下：

```
@keyframes example {
    from {background-color: red;}
    to {background-color: yellow;}
}
```
该keyframes的规则指定背景色从红变黄，参考[示例](https://codepen.io/hejiaji/pen/VjNVNb)  
另外，在示例中，div css代码如下:

```
div {
    width: 100px;
    height: 100px;
    background-color: red;
    animation-name: example;
    animation-duration: 4s;
}
```
其中animation-name对应了我们的 @keyframes 的名字，animation-duration 指定了过渡的持续时间，类似于transition-duration。

# 不同点

-	transform + transition的应用场景一般是给定起始style和最终style，transition控制动画平滑的程度，animation不仅仅可以控制始末style，它还可以指定中间过程如下：

	```
	@keyframes example {
	   10% { transform: rotate(90deg); -webkit-transform: rotate(90deg) }
	   50%, 60% { transform: rotate(180deg); -webkit-transform: rotate(180deg) }
	   90% { transform: rotate(90deg); -webkit-transform: rotate(90deg) }
	   100% { transform: rotate(90deg); -webkit-transform: rotate(90deg) }
	}
	```
请参考具体[示例](https://codepen.io/hejiaji/pen/LkvrPx)
-	transfrom + transition并不支持重复动画，而animation一个属性就可以办到
	> animation-iteration-count: infinite;
	
	请查看Infinite animation[示例](http://codepen.io/hejiaji/pen/QEPzWY)

#	总结
总体来说，animation比transform + transition强大一点点，具体使用哪个要视具体需求而定。   
目前大部分主流浏览器都已经兼容以上几个属性，但是为了兼容安卓系统保险起见最好加上-webkit-keyframes, 用animation的时候也加上-webkit-animation，如果觉得每次都要这么写太麻烦的话可以用例如sass中的mixin功能帮助我们减少代码，关于这部分内容我我会在之后写一篇博文详细描述。
