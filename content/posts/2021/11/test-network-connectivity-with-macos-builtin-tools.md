---
title: "用自带工具快速判断 macOS 和 iOS 的网络质量"
date: "2021-11-17"
tags:
  - "macos"
---

很多人都会在浏览器收藏夹里常备一个网速测试工具。每当连上一个新网络需要测试效果，或是感觉网络卡顿需要排查故障，这类工具就能派上用场。

但是，这个「裁判员」的选择并不应该是随意的。如果用运营商提供的测速页面，则只能反应到城域网关这一小段的连通性，以此代表实际网速无异于自欺欺人；另一方面，如果测速平台的规模太小，经常匹配到一个远在天边的节点，也会出现「误诊」的问题。

目前，比较常见的选择是 Ookla 旗下的 [Speedtest.net](https://www.speedtest.net/)；Netflix 开设的 [fast.com](https://fast.com/) 也被广泛使用。但是，就国内使用而言，前者并非在所有城市都能找到合适的测速节点，而后者的可访问性则较差。

好消息是，从今年的 macOS Monterey 开始， macOS 已经内置了一个网络情况测试工具 `networkQuality`。这个工具**利用 Apple 遍布全球的 CDN（内容分发网络）服务器来测速**，比较客观准确，在很多场景下可以免去寻找第三方工具的麻烦。同时，它还会**对当前网络的拥堵情况作出直观的高低评价**，帮你快速估测此地是否适合打电话、玩游戏。

### 基本使用

`networkQuality` 是一个命令行工具，需要使用「终端」App（或者你首选的其他终端模拟器）运行。方法是：

首先，点按「程序坞」（Dock）中的「启动台」（LaunchPad）图标，在搜索栏中键入「终端」，然后点按「终端」图标。

（或者，在「访达」中，打开 `/应用程序/实用工具` 文件夹，然后双击「终端」。）

在打开的终端窗口中，输入 `networkQuality`（注意大小写），然后回车。

![](https://cdn.sspai.com/2021/11/17/article/b6ac52917165bba1d690c7fa3ed43861?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

此时，系统会开始同时测试下载和上传速度，并将当前速率实时显示在终端窗口中，形如：

```
current download capacity: 247.850 Mbps - current upload capacity: 9.545 Mbps
```

大约半分钟后，测速完成，终端会显示一段测速结果，形如：

```
Upload capacity: 16.938 Mbps
Download capacity: 232.850 Mbps
Upload flows: 20
Download flows: 16
Responsiveness: Low (188 RPM)
```

其中，「Upload/download capacity」是指上传/下载的带宽；「Upload/download flows」是指刚才测试中完成传输的测速文件数量。

至于「Upload/download responsiveness」，是指上传和下载的综合「响应能力」，根据 Apple 的 [支持文档](https://support.apple.com/zh-cn/HT212313)，它的衡量指标是每分钟往返次数 (RPM)，即在正常工作条件下，网络能够在一分钟内完成的连续往返次数或事务数量。

根据 RPM 的高低数值不同，networkQuality 对响应能力的评价也分为「低」「中」「高」三个等级。这可以大致反映当前网络的拥堵程度，从而帮助间接估测视频通话、游戏等应用的效果：

- 评价为「Low」（低），说明同一网络的设备会互相影响，导致其他设备的网络连接不可靠；
- 评价为「Medium」（中），则表明多设备共享网络时会造成短暂卡顿；
- 评价为「High」（高）则最为理想，表明网络通畅，多设备并行联网也能和平共处，保持良好连通。

### 技术细节和进阶操作

如上所述，`networkQuality` 工具会使用 Apple 的 CDN 作为测试服务器。

具体而言，该工具默认会从一个外部 json 格式文件（目前位于 [https://mensura.cdn-apple.com/api/v1/gm/config](https://mensura.cdn-apple.com/api/v1/gm/config) ）获取测试配置。该文件包含三个测试文件地址：

- 一个小文件下载地址（目前位于 [https://mensura.cdn-apple.com/api/v1/gm/small，](https://mensura.cdn-apple.com/api/v1/gm/small%EF%BC%8C%E5%A4%A7%E5%B0%8F%E4%B8%BA) 大小为 1 字节、内容为字母 x）；
- 一个大文件下载地址（目前位于 [https://mensura.cdn-apple.com/api/v1/gm/large](https://mensura.cdn-apple.com/api/v1/gm/large%EF%BC%8C%E5%A4%A7%E7%BA%A6)，大约 4GB，内容为字母 x 的填充）；
- 一个上传文件测试地址（目前位于 [https://mensura.cdn-apple.com/api/v1/gm/slurp](https://mensura.cdn-apple.com/api/v1/gm/slurp%EF%BC%89%E3%80%82)）。

**此外，**`networkQuality` **命令可以接受一些参数。**比较有实际意义的包括：

- `-c` 会输出 json 格式的测速详情；
- `-s` 会分开测试下载和上传，而非像默认那样对两者同时测试（同时测试更能反映通话等真实应用的场景）；
- `-I` 可以测试特定网络接口的速度，例如，命令 `networkQuality -I en0` 是指测试内建 Wi-Fi 网络的速度。

更多参数和说明，可以用如下命令查阅手册页面 `networkQuality(8)`：`man networkQuality`

### iOS 上的使用

`networkQuality` 除了可以在 macOS 上使用，iOS 中也藏着一个该工具的简化版本。

首次使用前，需要安装 Apple 提供的 [描述文件](https://developer.apple.com/bug-reporting/profiles-and-logs/?platform=ios&name=Wifi)（访问需要登录 Apple ID），并在「设置」中出现的「已下载描述文件」选择「安装」。

此后，在「无线局域网」设置页面中网络名称右侧点击「信息」图标，就可以看到一个额外的「诊断」菜单项。进入后，可以看到「响应能力」字样，点击「测试」按钮即可获得类似于 macOS 上的测速结论。

![](https://cdn.sspai.com/2021/11/17/article/a9fe3b973c93e2d33ddfb64c35d82cd7?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

稍有遗憾的是，这个测试并不显示具体网速，但用来临时判断一下网络条件还是堪用的。
