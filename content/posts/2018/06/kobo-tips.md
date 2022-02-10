---
title: "Kobo 系统使用和修改综述"
date: "2018-06-15"
categories: 
  - "post"
tags: 
  - "ereader"
  - "kobo"
---

## 激活

- Kobo 首次开机需要联机登录账号来激活。
    - Kobo 的激活服务器在中国大陆无法访问，需要连接可以正常访问互联网的电脑，使用 Kobo Desktop 客户端来激活。
    - 大量指南提出通过向 `.kobo` 目录拷贝其他用户已激活设备中的 `KoboReader.sqlite` 文件来绕过激活，原理是该文件中的 user 表中存储了用户登录信息。显然，这是极其错误的做法。
- 登出账号会抹掉 Kobo 上的内容，并且需要重新激活。
    - Kobo 的登出操作实质上是对一系列目录执行 `rm -rf` 命令，其中包括上述 `.kobo` 目录。

## 系统与修改

- 与 Kindle 等阅读器类似，Kobo 的系统软件是一个高度定制化的 Linux。
    - USB 模式下的根目录挂载在 Kobo 系统的 `/mnt/onboard/` 下。
    - 根目录下的 .kobo 目录存储了 Kobo 系统对外暴露的重要配置文件。
- Kobo 系统软件的桌面环境称为 Nickel。
- Kobo 系统默认停用了截图功能。若要启用，需要手动编辑 USB 目录下的 `.kobo/Kobo/Kobo eReader.conf`，并在其中的 `[FeatureSettings]` 段后加入 `Screenshots=true`，然后就可以通过按电源键来截图。电源键的原始功能在删除这条配置前会失效。
- 系统升级可以通过设备自动下载或 Kobo Desktop 软件进行。
    - 在国内网络环境下，最快捷的方法是直接[下载](https://geek1011.github.io/KoboStuff/kobofirmware.html)对应版本升级包，将其中所有文件解压到 /.kobo 目录，然后弹出 Kobo 磁盘。设备会自动开始升级。
    - 事实上，Kobo 系统会在检测到 /.kobo 目录下的任何 KoboRoot.tgz 文件时，自动重启并将其中文件拷贝或替换到系统分区中。因此，可以通过自制 KoboUpdate.tgz 文件来达到修改系统文件的目的。
    - 像早期的 Kindle 一样，Kobo 升级时不检查升级包版本是否大于当前系统版本，即可以任意降级到[偏好的版本](https://www.mobileread.com/forums/showthread.php?t=296325)。
    - Settings > Device information > Factory Reset 会将系统版本回滚到出厂版本。
- 民间对 Kobo 系统的主要修改（patching）工具来自 MobileRead 论坛上的 [GeoffR](https://www.mobileread.com/forums/search.php?searchid=13202668)。
    - 该 patching 工具为[版本特定](https://www.mobileread.com/forums/showthread.php?t=260100)，每次升级系统需要等待放出针对该版本的 patching 工具，重新修改。
    - 工具的原理是：修改升级包中的 /usr/local/Kobo 中的配置文件，并将经修改的文件重新打包成升级包，然后通过 Kobo 的升级机制替换到系统中。
    - 工具的使用方法是：将对应版本的原版升级包（.zip 文件）拷贝到 patching 工具中的 $systemVersion\_source 目录下，然后用文本编辑器打开同目录下几个 .patch 文件，根据其中注释部分的提示修改文件内容来启用希望作出的修改。完成后，运行 $systemVersion.sh 脚本，获得 $systemVersion\_target 目录下的 KoboRoot.tgz 文件；用手动更新系统的方式安装该文件。
    - 用户 [oren64](https://www.mobileread.com/forums/search.php?searchid=13202739) 额外提供了基于 GeoffR 方法的大量修改脚本，例如修改主屏幕布局。
- Kobo 安装 [KOReader](https://github.com/koreader/koreader) 非常简单。
    - 与很多在其他嵌入系统上运行自制软件类似，在 Kobo 上运行 KOReader 需要两步：安装一个启动器（launcher），和安装 KOReader 本身。
    - 目前民间流行的启动器是 [KSM (Kobo Start Menu) 09](https://www.mobileread.com/forums/showthread.php?t=293804)，其同样通过引导系统安装一个自制的升级包来安装，并且通过在原生桌面环境 Nickel 下浏览特殊的自制图片来启动（非常类似 PSP 3000 下运行 Prometheus 自制系统，表明原理应该同样是利用内存溢出。）
    - 安装 KSM 后，系统每次启动会首先进入到 KSM 菜单；同时，当检测到存在 /.kobo/KoboRoot.tgz 文件时，KSM 也会首先接管系统引导并询问是否安装该升级包。
    - 安装 KSM 后，将 KOReader 安装包拷贝到根目录下的 `.add` 目录中，然后即可在 KSM 菜单中启动 KOReader。
- MobileRead 论坛上的一个帖子[列举了](https://www.mobileread.com/forums/showthread.php?t=217160)其他对系统的各种修改。

## 字体与字典

- Kobo 原生支持更换自定义字体。自定义字体存放于根目录下的 `fonts` 目录。
    - 字体格式可以是 OpenType 或 TrueType。
    - 要让粗体和斜体正常显示，拷入的属于同一家族的字体文件，其 PostScript Name 中的 Font Family 必须具有相同的值。否则，Kobo 将认为其属于不同的字体家族。
        - 可以通过 [FontForge](https://fontforge.github.io/en-US/) 来修改字体文件的 PostScript Name。在 macOS 上运行 FontForge 需要安装 XQuartz 框架。
- Kobo 的字典位于 `/.kobo/dict`。
    - 英文字典的文件名为 `dicthtml.zip`，其他语言的字典名形如 `dicthtml-$sourceLang-$targetLang.zip`，如英日字典名为 `dicthtml-en-ja.zip`。
    - 要修改字典，只要用下载得到的[字典文件](https://www.mobileread.com/forums/showthread.php?t=232883)替换那些不常用的内建字典。
    - 应当将内建的英日字典替换为中文字典。如果将其他字典替换为中文字典，会出现汉字过小的显示问题。

## CJK 支持

- Kobo 由于被日本企业乐天（Rakuten）收购，对日文支持较好。其系统内建了三个日文字体，两个来自森泽（Morisawa）：Gothic MB101（ゴシック MB101，PostScript Name 为 `A-OTF Gothic MB101 Pr6N R`），和 UD Kakugo（UD 角ゴ，PostScript Name 为 `KBJ-UDKakugo Pr6N M`，这也是任天堂 Switch 的 UI 字体）；另一个来自 FONTWORKS，著名的筑紫明朝（TsukuMinPr6N）。
    - 很奇怪的是，Kobo 西文界面全部使用衬线体 Georgia 作为界面字体，而日文界面却选用了两个无衬线体，又因为其 list view 中大量使用的斜体，显示效果非常扎眼，可以认为是典型的失败 l10n 案例。
- Kobo 原生系统没有任何中文支持。随附的日文字体可以显示部分汉字，未包含的汉字在主界面中显示为方框，在阅读界面中显示为空白。
- 可以通过拷入中文字体解决阅读中文书籍的问题。
- 要在 UI 上正确显示中文，需要修改系统文件，并拷入伪装为系统内建日文字体的中文字体。
    - 首先，制作一个 KoboRoot.tgz 升级包，在其中的 `./usr/local/Trolltech/QtEmbedded-4.6.2-arm/lib/fonts` 路径下放入两个虚假的空字体文件 `Gothic MB101.otf` 和 `Ryumin.otf`，安装该升级包，从而使系统内建的日文界面字体失效。
    - 其次，用 FontForge 将欲作为界面字体的中文字体的 PostScript Name 改为 `KBJ-UDKakugo Pr6N M`，然后拷入 `fonts` 目录。
        - 应当使用 GBK 字符集的中文字体来修改。
    - 最后，任意打开一本电子书，唤出字体菜单，使 Kobo 系统发现 `font` 目录中的「内建字体」。这时 UI 中的中文已经可以显示。
        - 每次重启系统（更准确地说是启动 Nickel 图形界面），都需要重复该步骤以显示中文。

## 电子书格式

- Kobo 宣称支持的格式有 14 种，即：EPUB, EPUB3, PDF, MOBI, JPEG, GIF, PNG, BMP, TIFF, TXT, HTML, RTF, CBZ, CBR。
- Kobo 使用的主力电子书格式是 ePub，不支持 Amazon 的 .azw/.azw3 格式。
    - 但是，Kobo 对标准的 ePub（.epub） 文件支持较差，许多高级特性（例如阅读时间统计、快速翻页）等只在阅读其私有的 Kobo ePub（.kepub) 格式时可用。
    - 可以用 Calibre 将标准的 ePub 文件转换为 Kobo ePub 格式；为此，需要先在 Preferences > Plugins 搜索安装 KePub Input 和 kePub Output 插件。也可以使用命令行工具 [`kepubify`](https://geek1011.github.io/kepubify/)。
    - 转换好的 .kepub 文件可能不会被 Kobo 正确识别，需要手动将后缀名改为 .kepub.epub。
        - 一个简单的方法是用 Automator Service 或 Hazel 监控 Kobo 的根目录，规则为当有文件的后缀名是 .kepub 时，自动追加 .epub。
- Kobo 对 PDF 的支持非常差，几乎不可用。KOReader 下表现良好，表明并非性能问题。

\-- NORMAL --
