---
title: "使用 Calibre 的命令行工具下载新闻"
date: "2019-08-17"
categories: 
  - "post"
tags: 
  - "book"
  - "ereader"
  - "tutorial"
---

Calibre 具有完善的[新闻下载功能](https://manual.calibre-ebook.com/news.html)，可以从各种媒体的网站抓取最新的文章并生成电子书文件。得益于开源社区的贡献，它还内置了针对一千多个不同网站编写的[配置方案](https://github.com/kovidgoyal/calibre/tree/master/recipes)（称作 recipe），并且更新非常及时。

但是，Calibre 的图形界面非常简陋且经常卡顿，使用起来体验较差。如果要使用定时下载新闻的功能，还必须保证软件一直在后台运行。另外，如果想在 Linux 服务器上运行 Calibre，一般也没有图形界面可用。

![Calibre 一言难尽的图形界面](https://cl.ly/89866a/calibre-fetch-news.png)

Calibre 一言难尽的图形界面

因此，使用命令行来下载新闻是更快捷、通用、且适合自动化的做法。本文将介绍用 Calibre 的命令行工具下载新闻的一般方法，然后在此基础上说明如何配置自动运行，并将下载好的文件通过不同方式传输到其他设备上阅读。

### 基本用法

Calibre 在命令行中的新闻下载功能是整合在其格式转换命令 [`ebook-convert`](https://manual.calibre-ebook.com/generated/en/ebook-convert.html) 中的。其基本用法是：

```
ebook-convert "Title of news source.recipe" outputfile.epub
```

其中，第一个参数是 recipe 的名称。不过，Calibre 在文档中没有指出的是，在使用内置方案时，`Title of news source.recipe` 不是指内置方案的文件名，而是指新闻网站的全称，`.recipe` 不是扩展名，只是一个后缀。只有在找不到对应的内置方案时，Calibre 才认为该参数是自定义方案的绝对路径。

要知道自己想阅读的网站有没有专用的内置方案，除了可以在 Calibre 的图形界面的新闻下载界面中查询，还可以使用 `ebook-convert --list-recipes` 命令。例如：

```
$ ebook-convert --list-recipes | grep 'New York Times'
	New York Times Book Review
	New York Times Sports Beat
	New York Times Technology Beat
	The New York Times
	The New York Times (Web)
```

所以，如果要下载当天的《纽约时报》，完整的命令应该是

```
ebook-convert "The New York Times.recipe" nytimes.epub
```

下载所得的 EPUB 文件如下图所示，除个别特殊样式不能正常显示之外，整体效果比较令人满意。

![用 Calibre 下载的报纸](https://cl.ly/8428e1/calibre-nyt.png)

用 Calibre 下载的报纸

### 定时下载报纸期刊

对于更新时间固定的报纸或期刊，在每次出新时手动下载显然是没有必要的。另外，最好能够在所下载文件的名称中标明日期，以便区分。

还是以下载每天的《纽约时报》为例。创建一个名为 `getnyt.sh` 的脚本文件（同时使用 `chmod +x` 为其增加运行权限），其内容为：

```
#!/bin/bash

TODAY=$(date +%m%d)
ebook-convert "The New York Times.recipe" nytimes-$TODAY.epub
```

这里，`TODAY` 变量使用了 `date` 命令的自定义日期格式功能，为下载的文件标注了日期。其他更复杂的日期格式可以用 `man date` 查阅。

下一个要解决的问题是如何让脚本定期运行。在 macOS 或 Linux 上，显而易见的答案是使用 `cron`。运行 `crontab -e` 打开 crontab 文件的编辑界面，在其中加入：

```
CRON_TZ=America/New_York
30 0 * * * /root/getnyt.sh >/dev/null 2>&1
```

这里用到了 `CRON_TZ` 变量来指定时区。《纽约时报》的更新时间是美国东部时间每天凌晨，虽然可以手工换算成国内时区，但直接使用纽约时区可以避免考虑夏时制的问题。`30 0 * * *` 指全年每月、每周七天的 0:30 分。类似地，对于一般每周四中午更新周刊内容的《经济学人》，相应的 cron 日程应该是 `0 12 * * 4`。（更详细的 cron 日程写法可以使用[这个工具](https://crontab.guru)阅读并测试。）

最后，由于 Calibre 在下载新闻时会输出很多日志，这里用`>/dev/null 2>&1` 让脚本静默运行。

### 将下载的期刊发送给其他设备

当然，新闻下载成电子书格式以后，终归还是要搬运到其他设备里阅读的。具体做法因需求而异，包括：

**直接连接到服务器下载：**如果你使用 iPad 等设备作为阅读器，那么可以直接使用 Documents 这类支持 SFTP 的文件管理工具登录服务器下载。

**添加到 Calibre 资料库：**如果你习惯用 Calibre 来管理所有的电子书，并且就是在平时存放 Calibre 资料库的电脑上运行脚本，那么可以考虑将下载好的电子书直接添加到资料库。Calibre 在命令行下使用 [`calibredb`](https://manual.calibre-ebook.com/generated/en/calibredb.html) 工具来维护资料库，对应的完整命令形如：

```
calibredb add --with-library /path/to/library nytimes.epub
```

你还可以进一步使用 Calibre 的[内容服务器](https://manual.calibre-ebook.com/server.html)功能在其他设备上访问下载好的新闻。

**存入网盘：**如果你是在远程服务器上运行 Calibre 下载新闻，那么更实际的方法或许是直接把下载好的电子书存进网盘。这可以通过 [rclone](https://rclone.org/) 来实现。该工具支持包括 Dropbox、OneDrive 和 Google Drive 等各大主流在线存储服务，具体的[配置方式](https://rclone.org/overview/)可以参考官方文档。以 OneDrive 为例，配置好以后，在上文脚本后加入一行

```
rclone copy nytimes.epub onedrive:/Documents/News; rm nytimes.epub
```

即可将 Calibre 下载的期刊文件转移到网盘。

如果想使用百度网盘，那么也可以配置 [BaiduPCS-Go](https://github.com/iikira/BaiduPCS-Go)，然后使用 `BaiduPCS-Go upload` 命令来上传。

**通过邮件发送：**最后，你也可以考虑将下载好的新闻通过邮件形式发送。这对于 Kindle 用户可能尤其实用，因为可以配合 Kindle 的文档服务功能实现新闻推送的效果。

Calibre 内置了一个用于发送邮件的命令行工具 `calibre-smtp`。由于该命令涉及的参数太多，建议使用脚本和变量来控制。例如，下面片段的作用是以 Gmail 发送下载好的当日《纽约时报》（注意很多开启了两步验证的邮件服务需要[配置专用密码](https://support.google.com/accounts/answer/185833?p=InvalidSecondFactor&visit_id=637016307474904521-2410294637&rd=1&hl=zh-Hans)）。

```
TODAY=$(date +%m%d)
DATELONG=$(date +%Y/%m/%d)
SMTP="smtp.gmail.com"
PORT="587"
USER="username"
PASSWD="password"
FROM="from@gmail.com"
TO="to@kindle.com"
MSG="Please find attached today’s New York Times. Have a good day!"

calibre-smtp --attachment nytimes-$TODAY.epub --relay "$SMTP" --port "$PORT" --username "$USER" --password "$PASSWD" --encryption-method TLS --subject "Today’s New York Times ($DATELONG)" "$FROM" "$TO" "$MSG"
```

### 额外考虑：Calibre 的网络环境配置

最后需要考虑的是，如果你的服务器本身访问新闻网站有困难，Calibre 也无法直接下载新闻。Calibre 遵从系统的代理设置，支持的代理类型为 HTTP 和 HTTPS，但不包括 Socks（但可以先通过 [Privoxy](https://www.privoxy.org)、[Proxifier](https://proxifier.com/) 这类工具转换）。对于 macOS，该设置位于「系统偏好设置」>「网络」>「高级」>「代理」；对于 Windows 10，则位于「设置」>「网络和 Internet」>「代理」。Linux 系统或者使用脚本的场景，则需执行：

```
export https_proxy=https://username:password@servername; export http_proxy=http://username:password@servername
```
