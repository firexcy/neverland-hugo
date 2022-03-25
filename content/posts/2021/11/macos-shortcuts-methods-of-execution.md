---
title: "[Preview] 条条大路通罗马：细数 macOS 版「快捷指令」的运行方式"
date: 2021-11-26
tags:
  - "macOS"
  - "shortcuts"
  - "automation"
  - "tutorial"
---

**Note:** This article was published as a member-exclusive post for [SSPAI Prime](https://sspai.com/prime), which you may find [here](https://sspai.com/prime/story/macos-shortcuts-methods-of-execution); the content below is a selected preview thereof. Please consider subscribing to SSPAI Prime if you find content like this helpful. Thanks for your support.

快捷指令的加入拓宽了 macOS 自动化的疆域。但对于任何自动化方案而言，一个基本的评价标准是**运行是否方便**——只有「随叫随到」的自动化才是有用的。

好消息是，macOS 上快捷指令的运行方式相比 iOS 有增无减，不仅可以融入 Dock 图标、菜单栏等 macOS 专有的界面，而且还能与 AppleScript、终端命令等传统自动化途径打通。

本文的目的，就是结合实例，整理这些运行方式的设置方法和适用场景，帮助读者将快捷指令安置到最合适的位置。

## 最方便随手取用——通过菜单栏、Dock 与快捷键运行

菜单栏、Dock 与快捷键的共同特征是「无处不在」，因此都适合用来运行那些**工具性、辅助性**的快捷指令。不过，由于它们的位置、醒目程度和触发方式不同，具体分工又各有所长。

### 菜单栏

菜单栏的特点是视觉上相对低调，因此更适合那些**在使用其他应用过程中顺手调用的「小工具」类快捷指令**。

要让快捷指令显示在菜单栏上，方法是在编辑界面侧边栏点击「设置」图标，然后选择「在菜单栏中固定」。或者，也可以在「快捷指令」app 的主窗口，将要加入菜单栏的快捷指令拖拽到左侧边栏「菜单栏」智能文件夹中。

这样，菜单栏中就会出现一个快捷指令图标，点击后即可从下拉菜单中选择要运行的快捷指令。

![197cec2d-919c-47c7-9718-ee9f9c97beba.png?v=49b8f212e024aaa1123691c5372d950c](https://cdn.sspai.com/2021/12/02/article/6170c51895dec729b249d3a47167e415?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

[ Intermediate content is omitted from this preview ]

### Dock

与菜单栏相比，程序坞（Dock）也具有始终显示的特点，但视觉上更加突出，因此更适合那些**具有独立功能**的快捷指令。

要让快捷指令显示在 Dock 上，方法是在「快捷指令」app 的主窗口（注意不是编辑窗口）找到并选中要添加的快捷指令，然后在菜单栏点击「文件」>「添加到程序坞」。

![8c895d9c-da8a-4373-ba32-8ba6d71e5ada.png?v=46658df779ea8bb0bf0b912b768e9273](https://cdn.sspai.com/2021/12/02/article/d6094c2e85a63ca756dbc5d77a155b8e?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

[ Intermediate content is omitted from this preview ]

### 快捷键

快捷键支持的好处无需多解释：可以在任何界面闭着眼睛直达目标；这对于那些**追求运行效率**的快捷指令再合适不过。

要给快捷指令设置快捷键，编辑界面侧边栏点击「添加键盘快捷键」按钮，然后按下要设置的快捷键。（如果要删除快捷键，点击现有的快捷键字样后按 Delete 即可。）

[ Intermediate content is omitted from this preview ]

## 最方便队友助攻——通过「服务」菜单或「快速操作」菜单运行

[ Intermediate content is omitted from this preview ]

要让快捷指令在「服务」或「快速操作」菜单等位置出现，方法是在编辑界面侧边栏点击「设置」图标，然后分别选中「服务菜单」或「作为快速操作使用」选项即可。（在配备了触控栏的 Mac 上，启用了「作为快速操作」的快捷指令还会同时显示在「自定触控栏」的可选项中。）

[ Intermediate content is omitted from this preview ]

## 最方便高玩混搭——通过 URL Scheme、AppleScript 和终端命令运行

行文至此，尽管介绍的快捷指令运行方式已经很多，但都没有跳出快捷指令本身的框架。这对于自动化玩家来说尚显不足——他们的要求是自动化工具间**相互打通**。这就要用到 URL Scheme、AppleScript 和终端命令了。

### URL Scheme

URL Scheme 是在 iOS 上被发扬光大的自动化方式；虽然这多少是 iOS 封闭环境下的被迫选择，但它的确具有简单、直观的优点。iOS 版的快捷指令（和前身 Workflow）本就以对 URL Scheme 的友好而著称，macOS 版也继承了这个优点，并且用法基本相同。

使用 URL Scheme 运行快捷指令的基本语法是：

```
shortcuts://run-shortcut?name=[名称]&input=[输入类型]&text=[输入文本]
```

[ Intermediate content is omitted from this preview ]

**怎样用将运行结果传出快捷指令？** 与在 iOS 上类似，用 URL Scheme 运行快捷指令时，可以使用 [X-Callback-URL](https://support.apple.com/zh-cn/guide/shortcuts/apdcd7f20a6f/ios) 中的 `x-success` 等参数，将快捷指令的输出传递给其他 app；在此不赘述。

### **AppleScript**

[ Intermediate content is omitted from this preview ]

通过 AppleScript 执行快捷指令的基本语法是：

```
tell application "Shortcuts Events"
    run the shortcut named "[快捷指令名称]"
end tell
```

此外，还可以将 AppleScript 中的文本、变量等作为快捷指令的输入，在运行时传递给快捷指令，其语法是：

```
tell application "Shortcuts"
    run the shortcut named "[快捷指令名称]" with input [输入内容]
end tell
```

[ Intermediate content is omitted from this preview ]

**怎样将运行结果传出快捷指令？** 如果快捷指令的输出结果是文本，那么可以直接将其赋给一个 AppleScript 变量，然后在脚本中继续使用。

[ Intermediate content is omitted from this preview ]

如果输出结果不是文本，或者有更复杂的需求，则可以使用 macOS 版快捷指令内置的「Run AppleScript」步骤。该步骤可以将自身的输入值、任意变量或剪贴板内容作为 `input` 变量传递给一段 AppleScript 脚本，然后在脚本内部读取 `input` 变量的值（或者其中的某一项，例如 `(item 1 of input)`）即可。

### **终端命令**

[ Intermediate content is omitted from this preview ]

通过 `shortcuts` 命令运行快捷指令的基本语法是：

```
shortcuts run [快捷指令名称]
```

[ Intermediate content is omitted from this preview ]

**怎样将运行结果传出快捷指令？** 如果快捷指令的输出结果是文本，那么可以直接使用管道符号传递给其他终端命令继续处理。

[ Intermediate content is omitted from this preview ]

如果输出结果不是文本，或者有更复杂的需求，则可以使用 macOS 版快捷指令内置的「Run Shell Script」步骤。该步骤可以将自身的输入值、任意变量或剪贴板内容作为 `STDIN` 或参数传递回终端。
