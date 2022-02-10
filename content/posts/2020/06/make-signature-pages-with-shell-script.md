---
title: "用 Shell 脚本制作签字页"
date: "2020-06-17"
categories: 
  - "post"
tags: 
  - "automation"
  - "pdf"
---

在我目前的工作中，一项常见但繁琐的任务就是制作文件的「签字页」。具体而言，这项任务包含如下步骤：

1. 将 Word 格式的交易文件导出为 PDF 格式；
2. 逐页提取 PDF 版中的签字页部分；
3. 将单页签字页按照类似于 `合同名称_SigPage_01_签署方名称.pdf` 的格式重命名。

![「签字页」](https://p178.p0.n0.cdn.getcloudapp.com/items/8Lu7PdbE/sigpage_eg.png?v=7788fcec612983304f82e5ce43c1a258)

「签字页」

这些步骤本身都毫无难度，但逐个操作下来仍然麻烦且易错。特别是对于那些文件数量和签署方数量都动辄十几二十个的大型交易，制作签字页对体力、眼力和脑力都是挑战。

显然，这就给通过自动化来「偷懒」创造了很强的动机。

上述步骤中，第 1 步是最容易通过工具来省事的：有大把的图形界面软件（例如 Acrobat、WPS 等）可以批量将 Word 文件转换为 PDF，只要一股脑地选中需要转换的原始文件，等待转换完成即可。如果偏好使用命令行，还可以使用 [`docx2pdf`](https://github.com/AlJohri/docx2pdf)（Windows 和 macOS 通用）、[`DocTo`](https://github.com/tobya/DocTo)、[`OfficeToPDF`](https://github.com/cognidox/OfficeToPDF)（只适用于 Windows）等工具进一步方便批量操作。

但之后的两个步骤——分割页面和重命名——才是最耗费精力、却又不太可能找到现成的工具的。

之前，我虽然一直有 DIY 一个自动化方案的想法，但总是因为时间有限和自己懒等原因未能实现。但在今天又一次被制作签字页的任务羞辱之后，我终于决心长痛不如短痛，花了一个下午把这个想法付诸实践，而成果就是下面这段（简陋难看的）shell 脚本 `[sigpgs.sh](https://pastebin.com/eCP0b41r)`：

![](https://p178.p0.n0.cdn.getcloudapp.com/items/6qu2e0E2/script.png?v=b42c31eaa5ff742cd51ee63bd7277947)

根据我的设计，这个脚本在运行时需要输入 3 个参数：

1. 要被拆分的 PDF 文件；
2. 一个包含所有签署方名称的文本文件，每个签署方一行，以空行结尾；
3. PDF 文件中签字页的起始页码。

例如：

1. 当前目录有一个名为 `Shareholders Agreement.pdf` 的文件需要制作签字页；
2. 该协议有 10 个签署方，列举在 `signatories.txt` 文件中；
3. 签字页从第 26 页开始。

那么，则执行：

```
$ ./sigpgs.sh 'Shareholders Agreement.pdf' signatories.txt 26
```

稍等片刻，就能在生成的 Shareholders Agreement 文件夹下看到分割好并且自动编号和命名的 10 张签字页：

![](https://p178.p0.n0.cdn.getcloudapp.com/items/BluO5pG4/output.png?v=617da0f64c7bcbdf1e12894cf470d30a)

* * *

下面简单介绍一下这段脚本的思路。整体而言，这段脚本分为三个部分：

**第一部分**（第 3–7 行）

该部分用于读取输入并准备好之后会用到的几个变量，其中：

- `$label` 变量是之后在签字页文件名中插入的文本，我这里用的是「SigPage」，也可以根据内部习惯改成中文的「签字页」等。
- `$npg` 变量通过计算签署方名单的行数，得知有多少个签署方；再结合输入的签字页起始页码（`$spg` 变量），就得到了签字页在原始 PDF 中的页码范围（从第 `$spg` 至第 `$epg` 页）。
- `$filename` 变量存放原始 PDF 的文件名以便后续操作。这里，`basename` 命令后面的第二个参数的作用是将文件名中的扩展名部分去除，得到不含 `.pdf` 的文件名。

**第二部分**（第 9–12 行）

该部分用于从原始 PDF 中提取签字页部分并分割为单页文件。

首先，用 `mkdir` 在原始 PDF 所在目录下创建一个同名文件夹，用于存放之后分割好的签字页。

接着就是最关键的提取和分割 PDF 步骤（第 12 行）。这里用到了一个功能非常齐全的命令行 PDF 处理工具 [`qpdf`](http://qpdf.sourceforge.net/files/qpdf-manual.html)（可以通过 Homebrew 安装：`$ brew install qpdf`）。

命令中的关键部分解释如下：

- `--split-pages`：该选项用于将 PDF 文件拆分成单页；如果想拆分成每 2 页一组的文件，则可以使用 `--split-pages=2`。
- `--pages`：该选项用于指定页码范围，其后接的第一个参数是输入文件，这里的句点 `.` 表示与整条命令的输入文件（即原始 PDF 文件）相同；第二个参数是页码范围，也就是我们上面通过起始页码和签署方数量计算得到的 `$spg-$epg`。
- `./"$filename"/_%d`：这是输出文件的路径，路径中的 `%d` 会在实际输出时被替换为编号；如果编号数超过两位数，个位数编号前会被追加 `0`（`01`、`02`、…、`10`）。由于后面的步骤还要重命名，这里暂时没有追加扩展名 `.pdf`。

**第三部分**（第 14–29 行）

该部分用于将上面分割好的文件重命名为我们需要的格式。

这里整体使用了一个 `while` 循环，通过 `read` 命令逐行从签署方名单（最后的 `< "$2"`）中读取签署方名称，进而将其拼合到最终的文件名中。（之前要求签署方名单最后以空行结尾，是因为 `read` 命令以换行符 `\n` 为各条记录的分隔符；因此，如果最后一个签署方之后没有空行，它就不会被纳入循环。）

在每次循环中，`$c` 变量起计数和编号作用，反映当前处理的是第几个签署方。（第 20–25 行的 `if` 循环用于处理上面提到的 `qpdf` 编号格式问题，即编号数超过两位数时在个位数编号前追加 `0`。）

接着，第 27 行的 `mv` 命令找到对应序号的签字页，将其名称改为 `$newname` 变量指定的格式：`原始文件名_SigPage_编号_签署方名称.pdf`。

最后，第 28 行的 `echo` 命令提示最终输出的文件名。

* * *

在此基础上，如果想把这个脚本做成独立应用程序的形式以方便运行，只要用内建的 Automator 应用简单包装一下即可。

你可以[下载](https://p178.p0.n0.cdn.getcloudapp.com/items/wbuW7r4X/SigPgMaker.zip?v=a5f7eeb62f68aacf0c53bf4737a5f486v)我打包好的 App Bundle。它的核心，就是下图中最后的 Run Shell Script 步骤，其内容原封不动地照搬了上面写好的 `sigpgs.sh` 脚本。图中上部还有几个要求选择或输入的步骤，作用都是引导用户提供脚本运行所需的变量（即原始 PDF 文件、签署方名单和签字页起始页码）。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/qGuKNg8o/automator.png?v=410fa814191c222c25cad9ede5f18e1f)

最后有两个值得提示的地方：

1. 在 Run Shell Script 步骤的选项中，要将「Pass input」改为「as argument」，即将输入作为脚本的参数。这样，之前通过连续 3 个 Get Value of Variable 步骤串联起来的参数就能像通过终端直接运行时那样，依次被传入到脚本中。
2. 填写的脚本开头要加入一行 `export PATH=/usr/local/bin:$PATH`。这是因为 Automator 在运行脚本时默认不会读取 `/usr/local/bin` 下的程序，而这是 Homebrew 安装软件包的位置。如果不加入这一行，Automator 会因为找不到该处的 `qpdf` 而报错（Command not found）。
