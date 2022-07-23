---
title: "条条大路通罗马：细数 macOS 版「快捷指令」的运行方式"
date: 2022-11-26
draft: true
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

## **最方便随手取用——通过菜单栏、Dock 与快捷键运行**

菜单栏、Dock 与快捷键的共同特征是「无处不在」，因此都适合用来运行那些**工具性、辅助性**的快捷指令。不过，由于它们的位置、醒目程度和触发方式不同，具体分工又各有所长。

### **菜单栏**

菜单栏的特点是视觉上相对低调，因此更适合那些**在使用其他应用过程中顺手调用的「小工具」类快捷指令**。

要让快捷指令显示在菜单栏上，方法是在编辑界面侧边栏点击「设置」图标，然后选择「在菜单栏中固定」。或者，也可以在「快捷指令」app 的主窗口，将要加入菜单栏的快捷指令拖拽到左侧边栏「菜单栏」智能文件夹中。

这样，菜单栏中就会出现一个快捷指令图标，点击后即可从下拉菜单中选择要运行的快捷指令。

![197cec2d-919c-47c7-9718-ee9f9c97beba.png?v=49b8f212e024aaa1123691c5372d950c](https://cdn.sspai.com/2021/12/02/article/6170c51895dec729b249d3a47167e415?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

例如，下图是一个用于将网页打印为 PDF 的简单快捷指令「Print Webpage」（[下载](https://www.icloud.com/shortcuts/4d640a845e11428d81381f77ef97186e)）。运行后，系统从输入中读取 URL（如果没有输入则从剪贴板获取），获取其中的网页内容，然后生成 PDF 并通过「快速查看」窗口显示。通过上面的方法启用菜单栏图标后，就很方便在浏览网页时随手取用。

![b9079f03-24de-48a2-a7e8-72ad87d8d7ab.png?v=0bdb41727e3c781be068b631504f8c47](https://cdn.sspai.com/2021/12/02/article/8f774d306882760b87003b10f0bd93db?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

### **Dock**

与菜单栏相比，程序坞（Dock）也具有始终显示的特点，但视觉上更加突出，因此更适合那些**具有独立功能**的快捷指令。

要让快捷指令显示在 Dock 上，方法是在「快捷指令」app 的主窗口（注意不是编辑窗口）找到并选中要添加的快捷指令，然后在菜单栏点击「文件」>「添加到程序坞」。

![8c895d9c-da8a-4373-ba32-8ba6d71e5ada.png?v=46658df779ea8bb0bf0b912b768e9273](https://cdn.sspai.com/2021/12/02/article/d6094c2e85a63ca756dbc5d77a155b8e?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

例如，macOS Monterey 大幅强化了内置的密码管理功能，并在「系统偏好设置」中专设了一个「密码」面板；但如果每次都手动打开，仍然显得麻烦。对此，我们可以用下图所示的快捷指令（[下载](https://www.icloud.com/shortcuts/3f22f723466c4764a6861c726d2b0cfd)）直达「密码」设置面板。

![b0e09861-40df-4147-a7b2-b31c0de5edb0.png?v=d2f5a5034626ba8cfbcfc072874d6cf0](https://cdn.sspai.com/2021/12/02/article/7e1d9ebe97fd80271460983d69c88d28?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

然后，用上述方法为其指定一个 Dock 图标。这样，就仿佛获得了一个独立的密码管理 app 一样。

![adae6cd7-9d15-4fe0-a164-8ed507f06b24.png?v=7be039ad9e751ddb9d34788c88ad7fe2](https://cdn.sspai.com/2021/12/02/article/8ee4cea6a305fbc48d67bcf07501030b?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

### **快捷键**

快捷键支持的好处无需多解释：可以在任何界面闭着眼睛直达目标；这对于那些**追求运行效率**的快捷指令再合适不过。

要给快捷指令设置快捷键，编辑界面侧边栏点击「添加键盘快捷键」按钮，然后按下要设置的快捷键。（如果要删除快捷键，点击现有的快捷键字样后按 Delete 即可。）

例如，之前文章介绍的[仿「闪念胶囊」快捷指令](https://sspai.com/prime/story/quick-ideas-shortcuts)——用于即时记录想法并生成提醒事项——就很适合安排一个快捷键。这样，可以在想法闪现时以最快的速度记录下来。

## **最方便队友助攻——通过「服务」菜单或「快速操作」菜单运行**

[**「服务」**](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/SysServices/introduction.html#//apple_ref/doc/uid/10000101-SW1)（Services）是 macOS 传统的跨应用自动化功能，通过右键菜单（或菜单栏中的应用名称菜单）下的「服务」子菜单访问，其作用是调用另一个应用来处理当前应用中的被选中内容。例如，调用 Safari 搜索 Pages 中的选中文本，调用「邮件」app 发送 Finder 中的选中文件等。

[**「快速操作」**](https://support.apple.com/zh-cn/guide/automator/aut73234890a/mac)（Quick Actions）加入于 2018 年的 macOS Mojave，可以看作「服务」的现代版。由于「快速操作」会以直观的图标形式显示在 Finder 的预览窗格（和已经过气的触控栏）中，因此特别适合针对文件的自动化流程，例如合并多个 PDF 文件、批量旋转图片等。

在过去，用户编写「服务」和「快速操作」的主要途径是上手门槛较高的「自动操作」（Automator）app。现在，快捷指令也同样可以「服务」和「快速操作」菜单中安家了。

要让快捷指令在「服务」或「快速操作」菜单等位置出现，方法是在编辑界面侧边栏点击「设置」图标，然后分别选中「服务菜单」或「作为快速操作使用」选项即可。（在配备了触控栏的 Mac 上，启用了「作为快速操作」的快捷指令还会同时显示在「自定触控栏」的可选项中。）

例如，为上面提到的「Print Webpage」快捷指令启用「服务菜单」选项后，就可以在 Safari 中选中任意链接，通过右键菜单中的「服务」>「Print Webpage」将链接网页打印为 PDF 文档。

![ea5b35a7-7c18-4252-b963-442d11b5a0f0.png?v=47fc2f53e52ff88d0f2ada20a0f6b85f](https://cdn.sspai.com/2021/12/02/article/af4927426408d34f1f88e7be9b630ab9?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

又如，下图所示的快捷指令「Count Items」（[下载](https://www.icloud.com/shortcuts/62a4fd164b4a4becb35977d03ec6e80a)）会递归地（即考虑所有子文件夹）计算指定文件夹中的文件数量。

![c9ee9217-2b14-4992-b5c3-1cae817febb7.png?v=342b64a6ae82c58f7f9cfad57a269f64](https://cdn.sspai.com/2021/12/02/article/c768fe796d6d53f887d6df8e56eec95a?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

将其加入「快速操作」后，就可以一键得知那些深如兔穴的文件夹里，究竟有多少文件了。

![7456e5de-3543-4af7-bb70-c0ae19e72176.png?v=9fac7c6a59babd2bc8bc934349d41466](https://cdn.sspai.com/2021/12/02/article/26bb6378e3c100c4f2d7861a9a6512e4?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

## **最方便高玩混搭——通过 URL Scheme、AppleScript 和终端命令运行**

行文至此，尽管介绍的快捷指令运行方式已经很多，但都没有跳出快捷指令本身的框架。这对于自动化玩家来说尚显不足——他们的要求是自动化工具间**相互打通**。这就要用到 URL Scheme、AppleScript 和终端命令了。

### **URL Scheme**

URL Scheme 是在 iOS 上被发扬光大的自动化方式；虽然这多少是 iOS 封闭环境下的被迫选择，但它的确具有简单、直观的优点。iOS 版的快捷指令（和前身 Workflow）本就以对 URL Scheme 的友好而著称，macOS 版也继承了这个优点，并且用法基本相同。

使用 URL Scheme 运行快捷指令的基本语法是：

```
shortcuts://run-shortcut?name=[名称]&input=[输入类型]&text=[输入文本]
```

其中：

- `name`：要运行快捷指令的名称，注意如果含有空格等特殊字符，需要转为 [URL 编码](https://zh.wikipedia.org/zh-hans/%E7%99%BE%E5%88%86%E5%8F%B7%E7%BC%96%E7%A0%81)
- `input`：一个可选参数，如果值为 `text`，则可以将特定文本（通过 `text` 参数指定）传给快捷指令作为输入；如过值为 `clipboard`，则将剪贴板内容传给快捷指令。（但根据我的测试，截至 macOS 12.0.1，传入剪贴板的功能**在 macOS 上似乎无法正常使用**，仅在 iOS 上能成功。）
- `text`：在 `input` 设为 `text` 时有效，记录要传给快捷指令的文本输入内容，同样需要 URL 编码格式。

例如，对于前面举例的「Print Webpage」快捷指令，运行下列 URL：

```
shortcuts://run-shortcut?name=Print%20Webpage&input=text&text=https://sspai.com
```

将调用该快捷指令，获取少数派主页内容生成 PDF。

**怎样用将运行结果传出快捷指令？** 与在 iOS 上类似，用 URL Scheme 运行快捷指令时，可以使用 [X-Callback-URL](https://support.apple.com/zh-cn/guide/shortcuts/apdcd7f20a6f/ios) 中的 `x-success` 等参数，将快捷指令的输出传递给其他 app；在此不赘述。

### **AppleScript**

在快捷指令到来前，AppleScript 是 macOS 上唯一的「正统」自动化方式。尽管近年来颇有成为明日黄花之势，但凭借其强大功能和广泛支持，AppleScript 的地位短期内预计还不会被快捷指令取代。

不少读者可能已经知道，macOS 版快捷指令中有一个「执行 AppleScript」步骤，可以将 AppleScript 脚本作为快捷指令的一个步骤运行。但反过来的整合也是行得通的——可以通过 AppleScript 执行快捷指令。这特别适合用来在其他自动化辅助工具中调用快捷指令（例如[这个 Keyboard Maestro 动作](https://forum.keyboardmaestro.com/t/shortcuts-picker-for-macos-monterey/24292)）。

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

值得注意：第一个例子中的应用程序对象是「Shortcuts Events」，而第二个例子中的对象是「Shortcuts」。这两者都可以用来运行快捷指令，但区别在于，如果希望快捷指令**只在后台运行**，而不唤起「快捷指令」app，那么应该使用「Shortcuts Events」；否则，应该使用「Shortcuts」。特殊地，如果快捷指令具有交互界面（例如要求输入、从菜单中选择等），则必须使用「Shortcuts」来运行，否则会报错。

如果想进一步了解 AppleScript 运行快捷指令的功能和用法，可以打开内置的「脚本编辑器」（Script Editor）app，点击「文件」>「打开词典」菜单，然后找到「快捷指令」并双击。

**怎样将运行结果传出快捷指令？** 如果快捷指令的输出结果是文本，那么可以直接将其赋给一个 AppleScript 变量，然后在脚本中继续使用。例如，下图展示了一个用快捷指令替换文本，然后用 AppleScript 弹窗显示替换结果的简单例子。

![21dd2e43-88be-465a-b8db-b3ccbde88940.png?v=fb77dc7bd1a7a0ac648144623942d282](https://cdn.sspai.com/2021/12/02/article/90c60bf7327d168422b8570d1bd01c64?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

如果输出结果不是文本，或者有更复杂的需求，则可以使用 macOS 版快捷指令内置的「Run AppleScript」步骤。该步骤可以将自身的输入值、任意变量或剪贴板内容作为 `input` 变量传递给一段 AppleScript 脚本，然后在脚本内部读取 `input` 变量的值（或者其中的某一项，例如 `(item 1 of input)`）即可。

### **终端命令**

作为具有 Unix 血统的操作系统，终端也是很多 macOS 自动化操作的常用渠道；不给快捷指令一个命令行入口大概是说不过去的。

的确，macOS Monterey 新增了一个内置的 `shortcuts` 命令（位于 `/usr/bin/shortcuts`），其功能正是帮助用户通过终端控制快捷指令。这特别适合习惯使用终端环境的用户，或者与终端下的其他工具配合使用。

通过 `shortcuts` 命令运行快捷指令的基本语法是：

```
shortcuts run [快捷指令名称]
```

注意快捷指令名称如果包含空格，需要在外侧包裹引号，例如 `shortcuts run "Print Webpage"`。

此外，终端环境的一大优势就是可以使用管道（pipe）将不同命令的输入输出串联起来。对此，快捷指令在终端下运行时同样可以接受其他命令的输入：

- 如果不附加任何选项，直接将输入作为参数传递给 `shortcuts run`，那么输入将被视为**纯文本**。
- 如果附加 `--input-path`（缩写为 `-i`）选项，那么输入将被视为**文件路径**；此时，还可以进一步通过 `--output-path`（缩写为 `-o`）选项指定输出路径。

例如，将网址作为文本输入给「Print Webpage」快捷指令，以输出相应网页的 PDF：

```
echo "https://sspai.com" | shortcuts run "Print Webpage"
```

又如，将当前目录下所有文件名以「Screen Shot」开头的截图输入给「Combine PDF」快捷指令，以输出合并后的 PDF：

```
find . -name "Screen Shot*"" -print0 | xargs -0 -I{} shortcuts run "Combine PDF" -i {} -o combined.pdf
```

最后，`shortcuts` 命令除了可以通过 `run` 子命令运行快捷指令外，还有其他多种子命令；比较实用的包括：

- `shortcuts view [快捷指令名称]`：启动「快捷指令」App 并编辑指定的快捷指令
- `shortcuts list`：列举所有快捷指令。`shortcuts list --folders` 则可以列举所有快捷指令文件夹

要了解更多功能和选项，可以运行 `man shortcuts` 来查阅手册。

**怎样将运行结果传出快捷指令？** 如果快捷指令的输出结果是文本，那么可以直接使用管道符号传递给其他终端命令继续处理。例如，下图展示了一个用快捷指令替换文本，然后传递给 `cat` 命令显示替换结果的简单例子。

![771797f6-cfa6-4d3d-a0e8-2b7b5e038fe3.png?v=6f8dee0e7617b8a15bb959e6feda3296](https://cdn.sspai.com/2021/12/02/article/e2f8ba52b506d1122ab42773e9b1c758?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

如果输出结果不是文本，或者有更复杂的需求，则可以使用 macOS 版快捷指令内置的「Run Shell Script」步骤。该步骤可以将自身的输入值、任意变量或剪贴板内容作为 `STDIN` 或参数传递回终端。
