---
title: "用 Apple Configurator 给 iOS 设备安装中文字体"
date: "2017-11-08"
tags:
  - "ios"
  - "tutorial"
---

随着 iOS 设备的性能和功能日渐强大，越来越多的人选择将其作为主力工作设备使用。然而，相比于桌面操作系统，iOS 在办公应用上的一大缺失就是无法自由安装字体。如果说系统内建的西文字体数量尚可满足需求，中文字体仅靠一个苹方撑场面的现状，显然是远远不够的。

俗话说得好，苹果关上一扇门，就会打开一扇窗；在自定义字体上，这句话同样适用。利用苹果提供的 [**Configuration Profile（配置描述文件）**](https://developer.apple.com/library/content/featuredarticles/iPhoneConfigurationProfileRef/Introduction/Introduction.html)功能，我们就可以方便地控制 iOS 设备的一些隐藏功能，包括自定义字体。

此前，少数派上已经有借助 Workflow 安装字体的[教程](https://sspai.com/post/36259)，App Store 上还有一款名为 [AnyFont](https://itunes.apple.com/us/app/anyfont/id821560738?mt=8) 的 app 专门用于满足这一需求。可惜的是，它们只能安装体积较小的西文字体，而无法正常安装 CJK 字体。[1](#fn1)

但这个问题其实并不难解决。其实，针对描述文件的制作和安装，苹果提供了一个官方工具——**Apple Configurator**，并通过 Mac App Store 免费提供。借助该工具，我们就能方便地生成包含自定义字体的描述文件并安装到设备上。

更重要的是，由于 Apple Configurator 的本意是为企业和学校等机构提供一个批量部署 iOS 设备的工具，它对于批量、重复操作是非常友好的，这也就意味着能用较少的时间一次性安装好常用字体。

下面，我们以安装开源的 [Source Serif Pro](https://github.com/adobe-fonts/source-serif-pro) 和[思源宋体](https://github.com/adobe-fonts/source-han-serif)这两款字体为例，演示具体的操作步骤。

![高质量的开源衬线体 Source Serif Pro 和思源宋体](https://ws1.sinaimg.cn/large/006tNc79ly1flalieubw5j31kw0q6qki.jpg)

### 准备字体和制作描述文件

在正式创建描述文件之前，应当先准备好字体文件。对于本例中用到的两款字体而言，都可以从其 GitHub 库中下载最新版本。需要注意的是，**iOS 系统只支持安装格式为 `.otf` 和 `.ttf` 格式的字体文件**；换言之，同一个字体家族（family）中的各个字重（如西文的 Light/Roman/Bold，中文的幼/中/粗等）是要各自安装的，那种将其打包在一起的 `.ttc` 文件并不受支持。

（上述两款字体的下载链接：[Source Serif Pro](https://github.com/adobe-fonts/source-serif-pro/archive/2.000R.zip) | [思源宋体](https://github.com/adobe-fonts/source-han-serif/raw/release/SubsetOTF/SourceHanSerifCN.zip) ）

做好上述准备后，从 [Mac App Store](https://itunes.apple.com/us/app/apple-configurator-2/id1037126344?l=en&mt=12) 安装 Apple Configurator。打开后，点击 **File** > **New Profile…** 创建一个新的描述文件。在弹出的编辑页面中，左侧是该描述文件的功能分类，右侧则是该类下的具体设置。

首先，在默认的 **General** 页面中，为该描述文件在 **Name** 文本框中填入一个易于辨认的名称，如 `Source Serif Pro`。

![为描述文件设置名称](https://ws2.sinaimg.cn/large/006tNc79ly1flal77t313j31kw1hewtn.jpg)

然后，切换到 **Fonts** 页面，点击右侧的 Configure，就会弹出对话框要求选择字体。该字体的名称及其预览会显示在右侧窗格中。

由于单个描述文件的容量上限约为 20 MB，故对于单个字体文件一般只有 KB 量级的西文字体而言，完全可以将多个字体文件整合进一个描述文件中。方法是：添加第一个字体后，点击右侧窗格中的加号按钮，然后选择下一个字体；如此反复，直到所有欲安装的字体都添加完成。

![将字体添加到描述文件中](https://ws2.sinaimg.cn/large/006tNc79ly1flal78nawkj31kw1heh3q.jpg)

而对于思源宋体这样的中文字体，由于体积过大，两个字体文件往往就会超过上述 20 MB 的上限，故最好还是单独制作描述文件。

添加完毕字体后，点击 **File** > **Save…** 保存该描述文件，并关闭编辑窗口。重复上述流程，直到为欲安装的各个字体都制作好描述文件。

（你可以在[这里](https://github.com/firexcy/ios-cuscom-fonts)下载到我预先做好的 Source Serif Pro 和思源宋体配置文件。）

### 将描述文件安装到 iOS 设备

制作好字体描述文件后，就可以将其安装到设备上了。用线缆将 iOS 设备连接到电脑，并保持设备在下面的流程中持续亮屏和解锁。连接的设备会以缩略图形式显示在 Apple Configurator 窗口中。

鼠标单击选中设备，然后点击工具栏上的 **Add** > **Profiles**，在弹出的窗口中选择刚才制作好的描述文件。注意该对话框支持多选，因此可以一次性选中全部想要安装的字体。

![选择要安装到 iOS 设备的描述文件](https://ws1.sinaimg.cn/large/006tNc79ly1flal78cd3qj31kw18qx6p.jpg)

之后，iOS 设备会自动跳转到设置 app，要求用户确认安装并输入解锁密码来确认，按照提示操作即可完成安装。

此时，打开 Pages 等 app，会发现已经可以在字体选择器中使用刚才安装的字体。

![在 iOS 版 Pages 中选用自定义字体](https://ws2.sinaimg.cn/large/006tNc79ly1flalplw360j31kw16ohdt.jpg)

在 Safari 中，如果安装了网页所指定的字体，系统同样能成功调用，而不会再回退（fall back）到默认的苹方，大大提升了显示效果。

![在 iOS 版 Safari 中显示思源宋体](https://ws1.sinaimg.cn/large/006tNc79ly1flalcad5ehj31kw16ob2a.jpg)

如果日后不再需要这些自行安装的字体，只需打开设置 app，进入 **通用** > **描述文件**，点击对应的描述文件并选择移除即可。

1. 这是因为它们的机制都是将字体文件籍由 [base64 编码](https://en.wikipedia.org/wiki/Base64)后，通过 URL Scheme 传给系统；而动辄十几 MB 的 CJK 字体经过这一流程生成的 URL 显然过长，往往被判断为非法，进而被直接忽略。 [↩](#ffn1)
