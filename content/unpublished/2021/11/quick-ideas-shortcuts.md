---
title: "快捷指令搭配提醒事项，打造 iOS 和 macOS 的「闪念胶囊」"
date: 2021-11-22
draft: true
tags:
  - "iOS"
  - "shortcuts"
  - "tutorial"
---

**Note:** This article was published as a member-exclusive post for [SSPAI Prime](https://sspai.com/prime), which you may find [here](https://sspai.com/prime/story/quick-ideas-shortcuts); the content below is a selected preview thereof. Please consider subscribing to SSPAI Prime if you find content like this helpful. Thanks for your support.

## 使用场景

「闪念胶囊」是 Android 手机上一类常见的实用功能，它可以从任意界面快捷唤出，通过键盘或语音记录用户当前想法，并以某种样式固定显示在屏幕上，方便事后回忆。在注意力资源稀缺的当下，这样的功能颇有意义。

遗憾的是，iOS 上并没有内置这个功能，第三方 app 也因为权限的限制无法完美提供类似功能。不过，借助快捷指令和「提醒事项」app 的通知和同步能力，模拟出类似的效果是可能的。

## 使用方法

首先，请[下载](https://www.icloud.com/shortcuts/7cded151e9b34c5c872bc2a431facf33)我做好的快捷指令。

该快捷指令可以直接运行，也可以接受分享菜单的输入。直接运行时，会要求输入「闪念」内容；通过分享菜单运行时，会直接将传入的内容作为「闪念」。

你还可以直接说「Hey Siri, Quick Idea」（或者你修改后的快捷指令名称），将屏幕上的内容捕获为「闪念」（例如 Safari 网页链接）。

![](https://cdn.sspai.com/2021/11/21/article/46a6b324b4324ffc82769d3fba7a5b1c?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

记录下来的闪念会**立即在通知中心和锁屏界面固定显示**。iCloud 同步设备（包括 iPhone、iPad、Mac 和 Apple Watch）上会**立即同步出现的固定通知**。

闪念内容则存储在「提醒事项」中名为「Ideas」的列表中（如果没有可以新建一个，或者自己换成其他的列表）。

![](https://cdn.sspai.com/2021/11/21/article/24b48675a75d279d4990f129d25e6444?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

几个设置技巧：

下载后，建议先点击右上角的「设置」按钮，将其添加到 iOS 主屏幕（或者为其设置一个桌面小组件），以便快速运行。同时，建议将「Ideas」列表按截止日期倒序排列时间排列，并为该列表创建一个桌面小组件，从而让「闪念」的先来后到一目了然。

![](https://cdn.sspai.com/2021/11/21/article/e05788190dd540e96042120ef2a98372?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

如果希望随时唤出，还可以通过「设置」>「辅助功能」>「触控」>「轻点背面」将其**绑定到连敲 iPhone 背面的手势上**。

此外，得益于 macOS 现已支持快捷指令，我为它设置了在 macOS 的菜单栏上显示，可以**通过快捷指令的菜单栏图标快速运行**。

![](https://cdn.sspai.com/2021/11/21/article/f069d3fc7ac7c4c2237a32737c413a3a?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

## 步骤解析

这个快捷指令的构成极其简单，只有两个步骤，甚至装不满一个屏幕：

![](https://cdn.sspai.com/2021/11/21/article/bb7c05785eeddca1514204f050553b07?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

第一步，快捷指令试图从获得从分享菜单获取输入；如果没有输入，则要求用户输入文本。

第二步，快捷指令在「Ideas」列表中新建一条提醒事项，其标题即为上一步获取的输入，**过期时间为当前时间点**。

这样做的目的有二：让任务立刻处于「已到期」状态，从而弹出通知；以及让到期时间间接扮演「时间戳」的角色，方便事后回忆。（理论上当然也可以把这些信息写在附注里——事实上 GoodTask 这类基于提醒事项的第三方 app 就采用类似思路——但终究比不上到期时间的醒目。）

第三步？没有第三步了。

事实上，这个快捷指令的重点不在于步骤，而在于**充分「压榨」系统内置服务的特权**。它对闪念胶囊的模拟效果是基于如下事实：

-   提醒事项是为数不多在 Apple 设备中普遍内置、可以通过 iCloud 近乎实时地同步的功能。
-   提醒事项的通知默认是「时间敏感」的；这类通知以「黏着」形态显示，会一直在通知区域等待用户操作或移除，从而间接实现闪念胶囊所需的醒目效果。
-   快捷指令具有繁多的触发方式（包括「敲后背」的辅助功能手势），并通过 [`NSUserActivity`](https://developer.apple.com/documentation/foundation/nsuseractivity) 获取当前 app 的活动内容。

## 讨论和延伸

如果希望维护几种不同类型的「闪念胶囊清单」，你可以将本快捷指令复制多份，分别绑定到不同的「提醒事项」列表中。不过经验上看，「闪念」的价值就在于不假思索，有时一个念头记住还是忘掉就在几秒之间；因此，或许将分类问题放到事后整理阶考虑，更符合这个技巧的初衷。

你可能注意到，本快捷指令没有像它试图效仿的原版「闪念胶囊」那样，默认接受语音输入。这是有意为之的选择，是为了更好的灵活度。原因在于在当下的 iOS 和 watchOS 上，文本输入切换到听写输入都只要点一下麦克风按钮（watchOS 上还可以直接切换到手写）；而反过来则没有这么快捷。此外，对很多人来说，对着屏幕自言自语仍然不是什么自在的动作。因此，我还是选择了文本输入优先。

本文还意在说明，我们有时会倾向于以步骤的复杂程度评判一个快捷指令是否「高级」或「有用」，但事实并非如此。快捷指令的设计需要考虑步骤和使用场景的互动。如果能结合需求充分挖掘系统自带功能，类似本文介绍的这种「简陋」到不像话的快捷指令，也能发挥非常实用的功能。
