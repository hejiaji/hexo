---
title: 「译」在finder中打开iTerm?
subtitle: Open iTerm here
date: 2018-05-07 11:57:46
tags: 译
---

>    本文翻译自[原文](http://azaleasays.com/2017/09/21/mac-os-x-open-iterm-here/)

#  作用

很多时候我们都想直接从当前finder目录中直接打开iTerm, 你觉得直接右键打开是不是很酷？！如图：
<img src="/img/post/finder_iTerm_1.png" />

### 第一步

打开 **Automator**

### 第二步

**File** - **New** - **Service**

顶上的第一个下拉框选择 **files or folders**, 第二个下拉框选择 **Finder.app**

双击或者从左边拖动 **Run Shell Script** 到右边，然后输入以下代码

```ruby
if [[ -d $1 ]]; then
    open -a iTerm $1
elif [[ -f $1 ]]; then
    parentdir="$(dirname "$1")"
    open -a iTerm $parentdir
fi
```

如图：
<img src="/img/post/finder_iTerm_2.png" />

### 第三步

**File** - **Save** - 保存service名为 **Open iTerm Here**


如果你之后需要对它进行修改，它的位置在 **~/Library/Services**

现在你已经可以尝试下新功能啦！



