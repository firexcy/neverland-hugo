---
title: "用快捷指令将 Safari 标签页导出为文本链接"
date: 2022-03-02
tags:
  - "macOS"
  - "iOS"
  - "tutorial"
---

**Note:** This article was published as a member-exclusive post for [SSPAI Prime](https://sspai.com/prime), which you may find [here](https://sspai.com/prime/story/safari-export-link); the content below is a selected preview thereof. Please consider subscribing to SSPAI Prime if you find content like this helpful. Thanks for your support.

「标签页组」是 Safari 15 新增的重要功能，除了整理归组之外，还可以通过「复制链接」导出组内所有页面的链接。这对于备份和分享都非常方便。但 Safari 所能导出的只是富文本格式的链接，但很多场景下都是无法粘贴、或者不方便处理的。本文将指导制作一个快捷指令来搭配使用，导出的链接变为更方便处理的 Markdown 或纯文本格式。

## 使用场景

**「标签页组」**是 Safari 15 新增的重要功能，为 Safari 补齐了相比于 Chrome 和 Firefox 的一项短板。标签页组可以将主题相关的标签页整合起来；例如，将工作中常用的内网办公系统页面整理为「工作」标签组；将为了写论文而检索资料用到的页面整理为「论文」标签组；等等。这大大减少了标签栏的负担，也是患有「标签囤积症」用户的救星。

![](https://cdn.sspai.com/2022/03/02/article/782e424fb358d370a44e1bea734bebc0?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

Safari 标签页组

除了整理归组之外，标签页组还有很多额外的辅助功能。其中最实用的一项莫过于**「复制链接」**，即可以导出组内所有页面的链接。这对于备份和分享都非常方便。

稍显遗憾的是，Safari 所能导出的只是**富文本**格式的链接，但很多场景下——例如 Markdown 笔记软件、聊天软件输入框，这样的链接都是无法粘贴、或者不方便处理的。

![](https://cdn.sspai.com/2022/03/02/c18e4c7312d7c731e1923e60ba0639dc.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

直接复制得到的富文本链接

因此，我们不妨用一个快捷指令来搭配使用，**将 Safari 导出的链接变为更方便处理的 Markdown 或纯文本格式**。这就是本文要实现的目的。

**注：** 你可以通过 Apple 的支持文章来进一步了解标签组功能在 [iPhone](https://support.apple.com/zh-cn/guide/iphone/iph3028ebf68/ios)、[iPad](https://support.apple.com/zh-cn/guide/ipad/ipada3308ec5/ipados) 和 [Mac](https://support.apple.com/zh-cn/guide/safari/ibrwa2d73908/mac) 上的功能和使用方法。

## 使用方法

本文方法构建的快捷指令（[下载](https://www.icloud.com/shortcuts/6ff72928dc084420a4d2facf63546b49)）同时适用于 iOS 和 macOS。

**第一步** 通过 Safari 的复制链接功能获得原始链接。具体而言：

**在 iOS 上：**

1. 点击 Safari 工具栏最右侧的标签页按钮，然后点击底部的「\[标签数\] 个标签」字样，展开标签组菜单（对于 iPad，则点击 Safari 工具栏左侧的侧边栏开关，打开工具栏，即可看到标签组）；
2. 长按要导出链接的标签组（或者 「\[标签数\] 个标签」字样来导出未分组的标签），然后选择「复制链接」。

![](https://cdn.sspai.com/2022/03/02/617f75b408ac4c6557fa70138cbf6c3b.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

**在 Mac 上：**

1. 点击 Safari 左侧的侧边栏开关，打开侧边栏，即可看到标签组；
2. 右键点击要导出链接的标签组（或者 「\[标签数\] 个标签」字样来导出未分组的标签），然后选择「复制链接」。

![](https://cdn.sspai.com/2022/03/02/f5ad8b5d00ff6777cb45c54ba1bbde97.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

**第二步** 运行本快捷指令后，会弹出一个菜单显示剪贴板中已复制的标签页列表。如果有不想包含在导出结果中的网址，可以取消其勾选。

**第三步** 从菜单中选择要导出的格式（Markdown 列表或纯文本列表），到其他应用中粘贴即可。

![](https://cdn.sspai.com/2022/03/02/91d8115e3253d1d29b66a87697168e41.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

## 步骤解析

本快捷指令主要用到了**菜单**、**列表**和**循环**等功能。

开头的几个步骤中，我们首先从剪贴板获取了原始链接，然后串接到一个「列表」步骤，让用户从中选择要导出的项目。这里，「多选」和「默认全选」两个选项非常有用。

![](https://cdn.sspai.com/2022/03/02/0dbb4d984a572b3eafa3de1dacfd532c.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

然后，我们使用「菜单」步骤构建一个菜单，让用户从 Markdown 和纯文本这两种常见格式中选择。

以选择 Markdown 格式为例。由于从上一步传来的是一个列表，我们使用一个「循环」步骤来依次处理其中的每一个项目——富文本格式的链接。然后，我们用「文本」步骤构造一段文本，其内容是 Markdown 语法下的链接列表格式：

```
- [ <链接标题> ]( <链接地址> )
```

要获取上述格式中的链接标题，首先将光标放在方框 `[ ]` 之间，从键盘上方选择「重复项目」（在 Mac 上，则在方框之间点击右键，选择「插入变量」 >「重复项目」）。

然后，点击刚才插入的重复项目，选择其类型为「URL」，以及要获取其「名称」（即网页标题）。

![](https://cdn.sspai.com/2022/03/02/5368742d0c4cd7e3aed0d8f87c4428a0.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

获取链接地址的步骤与之完全一致，只是最后一步选择获取的是「URL」。

这样，就完成了单条 Markdown 格式链接的构建。我们串接一个「添加到变量」步骤，将每条循环结果都放进 `output` 变量。这样循环结束后，`output` 变量就是一个包含了所有标签页对应的 Markdown 格式链接的集合。

![](https://cdn.sspai.com/2022/03/02/7eda40a527995d6da44b0c3d2fcef3b7.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

类似地，我们对选择纯文本格式时的步骤做类似设置。唯一的区别在于「文本」步骤的模板现在是：

```
<链接标题> <链接地址>
```

这里，别忘了善用快捷指令的「复制」步骤功能，即在这些多次用到的上长按（macOS 上则点击右键，还可以按住 Shift 键点选多个步骤）、选择「复制」，快速克隆出相同的步骤。

最后，我们获取包含了文本链接的集合的 output 变量，串接一个「合并文本」步骤，分隔符选择「新行」（即每行一条链接），输出给「复制到剪贴板」步骤即可。

![](https://cdn.sspai.com/2022/03/02/ceb20463672b07496e10f3dfe7af9806.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

你可以将这个快捷指令 [添加到 iOS 桌面](https://support.apple.com/zh-cn/guide/shortcuts/apd735880972/ios)、[主屏幕小组件](https://support.apple.com/zh-cn/guide/shortcuts/apd029b36d05/ios)，或 [macOS 菜单栏](https://support.apple.com/zh-cn/guide/shortcuts-mac/apd163eb9f95/5.0/mac/12.0) 方便调用。
