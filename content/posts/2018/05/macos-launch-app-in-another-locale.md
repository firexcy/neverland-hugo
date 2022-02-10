---
title: "如何临时修改 macOS 应用程序的显示语言"
date: "2018-05-13"
categories: 
  - "post"
tags: 
  - "macos"
  - "tips"
---

一般情况下，应用程序的界面语言会和系统语言保持一致。但有些时候，我们也会希望临时换用一种不同的界面语言。例如，一些程序的中文翻译词不达意，有必要参考英文界面来确定功能的准确含义；又如，一些网页会强制按照浏览器语言显示不同版本，因此必须通过切换浏览器语言来控制网页语言。

问题是，并不是所有的应用程序都提供了切换界面语言的选项。事实上，大多数 macOS 的内建应用都没有这样的设置。如果每次遇到这种需求都去临时改变系统语言，未免过于耗时和麻烦。

这个问题可以通过终端命令来解决。macOS 允许在运行应用程序时向其传递特定参数，其中，**`-AppleLanguages`** 参数就是用来控制应用程序的语言的。例如：

```
# 以简体中文界面启动 Safari 浏览器
$ open -a /Applications/Safari.app --args -AppleLanguages '(zh-CN)' 

# 以英文界面启动 Pages
$ open -a /Applications/Pages.app --args -AppleLanguages '(en)'
```

如果想以其他语言启动某个应用程序，只需要修改上述命令最后的地区代码。其他一些常用的代码包括繁体中文（`zh-TW`）、日文（`ja`）、法文（`fr`）、德文（`de`）等。

**要知道一个应用都支持哪些界面语言**，可以在 Finder 中找到该应用，点击右键选择 **显示包内容**，然后查看 `/Contents/Resources` 目录下以 `.lproj` 结尾的语言文件目录；`.lproj` 之前的部分就是各语言对应的地区代码。

![Safari 的语言文件目录](https://cl.ly/rWgk/Screen%20Shot%202018-05-12%20at%208.17.46%20PM.png)

当然，更快捷的方法还是使用终端命令。例如：

```
# 查看 Ulysses 支持的界面语言
$ ls /Applications/Ulysses.app/Contents/Resources | grep lproj
> Base.lproj
> de.lproj
> en.lproj
> …
```

## 为应用程序的特定语言创建快捷方式

**如果需要比较频繁地用不同语言显示某个应用**，那么可以为其创建一个快捷方式。

方法是：打开系统内建的「脚本编辑器」应用，新建一个文档，在命令栏输入：

```
do shell script "open -a [应用程序路径] --args -AppleLanguages '([要显示的语言])'"
```

点击 **文件** > **导出**，起一个易认的名字（例如「Safari CN」），并将「文件格式」选为「脚本」，然后将其导出到 Applications 文件夹。

![用脚本编辑器为特定语言创建快捷方式](https://cl.ly/rXBR/script-applelanguages.png)

这样，就可以直接从 Launchpad 以特定语言启动这一应用了。

Alfred 或 LaunchBar 用户可以用该原理制作动作来实现同样效果，在此不赘。

## 默认以特定语言启动应用程序

最后，**如果希望始终以某种与系统设置不同的语言启动特定应用**，可以用 `defaults write` 命令来修改其默认设置。具体语法是：

```
$ defaults write [应用的 Bundle ID] AppleLanguages '([要默认显示的语言])'
```

例如：

```
# 默认以简体中文打开「文本编辑」应用
$ defaults write com.apple.TextEdit AppleLanguages '(zh-CN)'
```

其中，应用的 Bundle ID 可以通过运行 `mdls -name kMDItemCFBundleIdentifier [应用程序路径]` 来查找。例如：

```
# Chrome 浏览器的 Bundle ID
$ mdls -name kMDItemCFBundleIdentifier /Applications/Google\ Chrome.app
> kMDItemCFBundleIdentifier = "com.google.Chrome"
```

如果不再需要固定应用程序的显示语言，在终端运行：

```
$ defaults delete [应用的 Bundle ID] AppleLanguages
```

即可解除上述默认语言设置。

\-- NORMAL --
