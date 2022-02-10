---
title: "用 Calibre 命令行优化 Kindle 电子书字体"
date: "2018-04-02"
categories: 
  - "post"
tags: 
  - "ereader"
  - "kindle"
  - "tips"
---

## 1\. 需求分析与解决思路

排版问题一直是 Kindle 的顽疾，而其在字体选用方面的不作为又特为尤甚。因此，更换字体一直是 Kindle 用户折腾的主要动力之一。早先，这一需求经常通过越狱并替换系统字体来实现。但随着 Kindle 越狱难度的加大，加上替换文件容易导致的诸多故障，尝试这种方法的成本已经越来越高了。

另外一种更为方便和安全的方式，则是利用 Calibre 这一强大的管理、编辑工具对电子书进行处理，在其中嵌入自定义字体。但直接应用这种方法得到的排版效果其实也并不完善，因为 Calibre 一次只能嵌入一个字体文件，在显示粗体和西文部分时，就会出现字体缺失或效果不佳的问题（很多中文字体附带的西文质量是十分平庸的）。

实际上，对于常见的中西文混排电子书，实现较为完善的排版效果至少需要两款字体、共计六个字体文件（中文常规体和粗体，西文常规体和粗体、及各自对应的斜体）。这在 Calibre 的图形界面上并不容易实现。但利用 Calibre 完善的命令行支持，则不仅能最大限度地实现字体嵌入的自定义，还能与其他效率工具结合，达到自动化、可复用的效果。

下图是原电子书的显示效果、使用 Calibre 直接嵌入字体的效果、以及嵌入多种字体效果的对比。请特别注意西文和粗体、斜体的显示效果。

![](https://cl.ly/qZIB/Untitled.png)

本文的目的，即在于说明如何利用 Calibre 的命令行支持，通过在电子书中嵌入自定义的 CSS 和字体文件，以实现更完善的排版效果。

![本文方法原理图示](https://cl.ly/qYud/iPad.png)

## 2\. 前期准备和字体选择

要使用本文方法修改电子书文件，需要提前准备的条件有：

1. 安装 [Calibre](https://calibre-ebook.com)；
2. 待修改的电子书文件（如果该电子书是从商店购买，则需要先行移除其 DRM 保护）；
3. 将需要嵌入的中西文字体文件（`.ttf` 或 `.otf`，不支持 `.ttc`）放在同一文件夹中（例如 `~/Documents/KindleFonts`）。

字体的推荐并非本文重点，且中文互联网上已有不少较为完善的讨论（例如[这篇](https://wzyboy.im/post/736.html)和[这篇](https://www.douban.com/note/557634901/)）。至于免费字体的推荐和获取，则可参看我[之前的文章](https://sspai.com/post/42889)。这里只提出几点建议供读者参考：

- 衬线体/宋体总体上更适合长文阅读（前提是分辨率足够高，但这对较新的 Kindle 不是问题）；
- 中文和西文字体在风格和粗细程度上应当尽量接近；
- 电子墨水屏的显示效果看起来偏淡，因此尽量选择略粗的字体；
- 嵌入的字体以够用为原则，不要数量过多或体积过大，否则容易导致 Kindle 无法打开或死机；
- 从尊重版权角度出发，请始终注意电子书和字体的正规来源，并且**不要传播**修改后的文件。

例如，如果从获取和使用最为便利的开源字体中选择，IBM 推出的 IBM Plex Serif 和 Adobe/Google 制作的思源宋体就是一组较为协调的搭配。但考虑到电子书屏幕的上述显示特点以及两种字体的字重差异，比起直接选用思源宋体常规体和粗体，更好的做法是以其 Medium 字重（比 Regular 稍粗一些）作为常规体、以 Heavy 字重作为粗体。下文也将以这一组合为例进行演示。(🔗 你可以[下载](https://cl.ly/qaRn/KindleFonts.zip)我准备好的这两种字体进行尝试。)

![IBM Plex Serif 搭配思源宋体](https://cl.ly/qVCi/iPad.png)

## 3\. CSS 的编写

Kindle 等阅读器读取和显示电子书的原理和浏览器显示网页几乎是一样的，都是以 html 文件为内容载体，而通过 CSS 来决定颜色、字体、排版等显示特性。为了让 Kindle 在显示时能正确调用嵌入的字体，就要同时嵌入相对应的 CSS，用于说明使用了哪些字体、分别应当在什么地方使用。

例如，如果准备嵌入上文提及的 IBM Plex Serif 配思源宋体的组合，并让中文字体加粗一档，所用到的 CSS 应如下图所示（已经放在上文提供字体压缩包中的 `KindleFonts.css` 内）：

![](https://cl.ly/qbCs/iPad%20Copy.png)

可以看到，这段 CSS 主要分为两大部分：

首先，用 `@font-face` 来声明将要嵌入的字体文件的各项属性（上图第 1—36 行）。这本不是必须的（因为字体文件本身已经记载了这些信息），但当需要改变字体原有的属性时（如将较粗字体当作常规体来用），就要借助 `@font-face` 来进行修改。这里拿出上面代码中涉及中文粗体的部分来具体说明：

```
@font-face {
    font-family: "Source Han Serif";
    font-style: normal;
    font-weight: normal;
    src: url(SourceHanSerifCN-Medium.otf);
}
```

上面这段代码的作用是将名为 `SourceHanSerifSC-Medium.otf` 的字体文件重新定义为「Source Han Serif」家族中的常规体。其中：

- `font-family`：字体家族名称，可以任意填写，易于识别即可；
- `font-style`：字体样式，取值为 `normal`（常规体）或 `italic`（斜体）；
- `font-weight`：字重，取值为 `normal`（常规体）或 `bold`（粗体）；
- `src`：字体文件的路径，此处填写字体文件名即可。

每有一个要嵌入的字体文件，都要配以对应的一段 `@font-face` 代码。

接着，用 CSS 选择器「告诉」Kindle 在哪些地方使用嵌入的字体（上图第 36 行以下）。在 `font-family` 属性中列举字体时要注意顺序，**把西文字体放在中文字体之前**；否则，Kindle 在显示时就会调用中文字体自带的西文，这不符合我们的目的。

最后，将写好的代码保存为一个 `.css` 文件（例如 `~/Documents/KindleFonts/KindleFonts.css`），记下其路径备用。

## 4\. 命令的构建

完成上述准备后，就可以着手构建用来嵌入字体的终端命令了。该命令的结构如下：

```
$ /Applications/calibre.app/Contents/MacOS/ebook-convert 原始电子书文件路径 ~/Desktop/temp.htmlz --extra-css "$(cat 自定义CSS文件路径 | tr '\n','\t' ' ')" \
&& zip -urj0 ~/Desktop/temp.htmlz 字体所在文件夹路径 \
&& /Applications/calibre.app/Contents/MacOS/ebook-convert ~/Desktop/output.htmlz ~/Desktop/output.azw3 --language zh-Hans \
&& rm ~/Desktop/temp.htmlz
```

其中，`原始电子书文件路径`、`自定义 CSS 文件路径`和`字体所在文件夹路径`在上面的步骤中都已经准备好，填入对应位置即可。

**注：**如果你不确定文件路径的写法，可以将其拖入终端窗口来显示（macOS），或点击右键选择「属性」（Windows）来查看。

一个填写完整的命令如下图所示（🔗 [下载](https://cl.ly/qb8g/Embed%20with%20custom%20fonts.sh)）：

![](https://cl.ly/qaLH/carbon%20(7).png)

对该命令中其余部分的解释如下：

- `/Applications/calibre.app/Contents/MacOS/ebook-convert`：Calibre 格式转换模块的路径。在 macOS 上，该可执行文件位于 Calibre 的 `.app` 包中。在 Windows 和 Linux 上，该文件可在 Calibre 的安装目录中找到。此命令的基本用法为 `ebook-convert 原始文件 目标文件.目标格式 [-参数]`
- `--extra-css "$(cat 自定义CSS文件路径 | tr '\n','\t' ' ')"`：去除 CSS 文件中的换行和 tab（为了符合终端命令的语法要求）并嵌入到电子书中。
- `temp.htmlz`：上述思路中用于「中转」的电子书文件。`htmlz` 格式本质上就是一个 zip 压缩包，内容是电子书中的资源文件。
- `zip -urj0`：将自定义字体文件夹中的文件（`-rj`）更新到（`-u`）用于中转的 `htmlz` 格式电子书中，且不压缩其大小（`-0`）；
- `output.azw3`：最终生成的 Kindle 电子书文件，本命令中将其放在桌面。如果你使用非 Kindle 阅读器，也可以将其后缀名改为 `.epub` 以生成 ePub 格式的电子书。
- `--language zh-Hans`：指定电子书语言，这影响到 Kindle 中字体菜单中提供的选项。如果你是用本文方法转换英文电子书，不要使用该参数。
- `rm ~/Desktop/temp.htmlz`：删除用于中转的`htmlz` 格式电子书。

执行命令并稍等片刻，即可在桌面看到输出的 `output.azw3` 文件。这就是嵌入了字体的电子书。将其拷贝到 Kindle 设备上后，在字体菜单中选择新出现的「出版方字体」选项，即可看到效果。

![在 Kindle 字体菜单中选择「出版方字体」](https://cl.ly/qYcx/Amazon%20Kindle%20Paperwhite%20Mockup.png)

## 5\. 延伸应用

在实际使用中，如果每次都要根据上述步骤重新编写一次命令，未免显得麻烦。其实，由于想要嵌入的字体一般相对固定，每次操作中需要改变的只有电子书文件的路径而已。为此，只需将原命令中的电子书路径改为变量 `"$1"`，就可以将其当作一段 shell 脚本，放在各类效率工具中反复利用。

例如，你可以用 Automator 将其变为一个服务项，从而通过在电子书上点击右键直接调用（🔗 [下载](https://cl.ly/qaX3/Embed%20with%20Custom%20Fonts.workflow.zip)）：

![](https://cl.ly/qaUa/Image%202018-04-01%20at%2010.45.02%20PM.png)

或者，可以将其制作成 LaunchBar 动作，通过快捷键调用（🔗 [下载](https://cl.ly/qath/Kindle%20Fonts%20Embedder.lbaction.zip)）：

![](https://cl.ly/qZgy/08.png)

顺带提及，本方法的幕后主角 `ebook-convert` 是一个极其强大的命令，可以实现 Calibre 图形界面的一切格式转换选项。你可以参阅其[文档](https://manual.calibre-ebook.com/generated/en/ebook-convert.htm)来进一步定制出适合自己需求的命令。

\-- NORMAL --
