---
title: "macOS Mojave 动态桌面功能探析"
date: "2018-10-09"
categories: 
  - "post"
tags: 
  - "macos"
---

前不久推出正式版的 macOS 10.14 (Mojave)，应该可以称为四年前的 Yosemite 以来，macOS 在用户界面上变化最大的一次更新。千呼万唤始出来的原生「黑暗模式」让人耳目一新，也引发了第三方应用的适配热潮。

相比之下，另一项用户界面的新功能——动态桌面（dynamic desktop）受到的关注则少得多。这是一项默认关闭的功能，启用方法是打开「系统偏好设置」>「桌面与屏幕保护程序」，从「动态桌面」中选择系统自带的两套壁纸之一。

![新增的两套动态壁纸](https://cl.ly/b56fa950dfc8/syspref.png)

显然，如此低调的功能很难引起用户的注意，大多数评测文章都选择将其一笔带过。苹果自己的态度似乎也是一样：在六月的 WWDC Keynote 演示中，Craig Federighi 留给动态桌面的台词只有[一句话](https://developer.apple.com/videos/play/wwdc2018-101/?time=5998)：

> Your desktop actually subtly changes throughout the day from morning, to afternoon, to evening. 你的桌面［背景］将随着一天从早上、到下午、再到晚上的推移而微妙地改变。

乍听起来，这确实并不稀奇，也没有任何技术门槛。随时间变化切换壁纸是很多桌面美化软件的基础功能，更别提十多年前的 Windows Vista 就已经原生支持[视频壁纸](https://en.wikipedia.org/wiki/Windows_DreamScene)了。

但问题实际上并不只是**「按时间切换图片」**这么简单。因为，晨昏变化的节奏并非一成不变，而是随着四季变换各有不同。除非生活在赤道或者极地，从夏到冬一定是昼渐短、夜渐长的。如果全年都按照一个节拍切换壁纸，其效果在绝大多数日子里都将跟真实景象不同步。

随着季节推移变化的不只是昼夜长度，还有**太阳高度**。显然，夏天的太阳比冬天的同一时间要「高」。太阳高度还与纬度有关。假如你生活在北京，而系统在中午时分给你换上了一张「阳光从头顶直射」的壁纸，你其实应该有一种违和感才对，因为北京根本不会有 90 度的日照。地处北纬 40 度的北京，太阳最高也只能达到 73.5 度，并且一年只有一次，时间是在夏至那天的（地方时）正午。

![北京在春分日和夏至日的太阳高度变化](https://cl.ly/826a080207b4/bj-sun-angle.png)

可见，要真正让桌面和窗外的光照**同步**变化，机械地踩着时间点换图片是远远不够的。理想情况下，同一组图片的切换节奏应当呼应太阳运动、在四季各不相同，并且根据用户的地理位置和日期，有选择地「跳过」一些不符合实际情况的照片。

## 动态桌面的实现机制

macOS Mojave 的动态桌面充分考虑了上述问题。在苹果的实现方案中，壁纸的切换不是以时间为标准，而是以**太阳方位**为标准。具体而言：

1. 每套壁纸包含 16 张静态图片（实验表明似乎可以更少，但不能更多）。
2. 每张静态图片都被标记了对应的太阳方位。定位的方式是所谓的[「地平坐标系」](https://en.wikipedia.org/wiki/Horizontal_coordinate_system)，即用高度角（Altitude，定义为太阳和地平线的夹角）和方位角（Azimuth，定义为太阳按顺时针方向偏离正北的角度）两个值确定太阳在天球中的位置。
3. 启用后，系统将会根据用户的位置和时间计算太阳的实时方位，并与每张壁纸所记载的信息进行比对，将其中与此时此地太阳位置最近似的那一张作为桌面背景。

![地平坐标系图示（来源：timeanddate）](https://cl.ly/fe1de461ed55/horizontal-coordinate-system.png)

实际例子可能更有助于理解动态桌面的机制。我目前的所在地处于北纬 40 度，与北京基本相同。10 月 5 日的早上 6:30 尚未日出，此时的太阳高度为 -6.75 度，方位为 90.6 度。启用「沙丘」动态壁纸后，桌面显示为该系列中的第三张。根据壁纸的元信息（后文将说明方法），这张照片是在太阳高度 -4.25 度，方位 86.34 度的场景下拍摄的，与现实环境非常接近。如果将系统日期拨回三个月前的 7 月 5 日，会发现壁纸变成了系列中的第五张（太阳高度为 7 度）。的确，夏天的这一时刻，太阳应该已经升起了。

再将日期调回 10 月 5 日。这一天，太阳在下午 12:48 时达到最高位置。但如果试着慢慢将时钟调过这一时刻，会发现壁纸并没有切换为系列中最明亮的第八张，而是直接从第七张跳到了第九张。原因在于，秋天的太阳即使在正午也只能达到 45 度左右，而第八张壁纸是在太阳处于 53 度时拍摄的，因此不会被显示。相反，在 Mojave 刚刚开始公测的七月时，这张壁纸会从上午 10:40 左右开始持续显示约五个小时。

![动态桌面在不同日期的差异](https://cl.ly/1ec0a403f859/switch-pattern.png)

更有趣的是，在另一套动态壁纸 Solar Gradients 中，一张图片对应的太阳高度为 88.4 度。如上所述，由于北纬 40 度的太阳全年最高也只能达到 73.5 度，我将始终不会看到这张最亮的壁纸被用作桌面——它实际上成了热带地区用户的「会员特权」。

Craig Federighi 的那句**「subtly（微妙）」**毕竟并不是随口说说而已。

## 壁纸资源、技术细节与自制方法

遗憾的是，即使 Mojave 的动态桌面在设计上如此讲究，苹果却并没有给予这个功能太多关注。系统自带的动态壁纸只有两张，并且没有提供让用户自行制作的选项。

但这并不意味着自己动手的大门就被关闭了。自从 Mojave 测试版发布以来，动态桌面引起了不少开发者的兴趣和关注。在他们的努力下，这一功能的实现细节已经十分清晰了，自己制作起来也并不麻烦。

下面列出的是一些现有的动态壁纸资源，可以直接下载并[设置](https://support.apple.com/zh-cn/guide/mac-help/change-your-desktop-picture-mchlp3013/mac)为桌面。有兴趣的读者可以继续阅读后文的技术细节与自制方法。

- 开发者 [Marcin Czachurski](https://twitter.com/mczachurski) 制作的地球卫星主题壁纸（[Dropbox](https://www.dropbox.com/s/kd2g59qswchsd0v/Earth%20View.heic?dl=0)） ![](https://cl.ly/f5a8369428fd/earth.gif)
- Jetson Creative 制作的四组实拍动态壁纸（[网站](https://www.jetsoncreative.com/mojave)） ![](https://cl.ly/e470d57ba610/24hrs.png)
- 笔者制作的渐变主题壁纸（[链接](https://cl.ly/e192bbc44f86/gradient.heic)） ![](https://cl.ly/59f533dec5fc/grad.gif)

与以往的普通壁纸相同，新的动态壁纸也都存储在 `/Library/Desktop Pictures` 路径下，文件名分别是 `Mojave.heic` 和 `Solar Gradients.heic`。

`.heic` 是什么格式？喜欢用 iPhone 拍照的用户实际上不会对它感到陌生。自 iOS 11 以降，大多数 iPhone 都已经默认改用 [HEIF](https://en.wikipedia.org/wiki/High_Efficiency_Image_File_Format)（High Efficiency Image File Format，高效率图像文件格式）存储照片。这里的 `.heic`，就是 HEIF 格式的可选扩展名之一。与传统的 JPEG 相比，这种新格式在缩减空间占用和减少画质损耗上有着更好的表现。

不仅如此，HEIF 还是一种「容器」（container）格式——它不仅能存储单张静态照片，而且能存储**一组**连续照片、以至视频；这就为将动态壁纸打包在一个文件里提供了可能。实际上，这两个文件可以直接用系统内建的预览 app 打开，并从侧边栏中看出两套壁纸的构成——都包括 16 张构图相同而光线各异的静态图片。

但这并没有回答我们最关心的问题：壁纸的自动切换是靠什么控制的？试着用 16 进制编辑器打开一张动态壁纸，从头略微往下翻阅，就能在第一张图片的 EXIF 信息中看到玄机：一个自定义的 `apple_desktop` 命名空间和其项下的 `solar` 属性。

![隐藏在 EXIF 信息中的参数](https://cl.ly/3b611993f0ed/exif.png)

下面的「破译」过程需要一点浅显的 macOS 经验。`solar` 属性值末尾的等号是 base64 编码的明显[特征](https://en.wikipedia.org/wiki/Base64#Output_padding)。用 `base64 -D` 命令解码，发现输出以 `bplist` 开头，这是二进制[属性表](https://en.wikipedia.org/wiki/Property_list#macOS)文件的魔数。为此，再用 `plutil` 命令将其转换为可读的 XML 格式。

![将动态壁纸的配置信息转为可读形式](https://cl.ly/eb752a836b6f/convert.png)

这样，苹果在 Mojave 的动态壁纸中设置的机关就展现出全貌了。可以看到，在 `si` 根键下，每张静态图片被都标记了 `i`、`a`、`z` 三个键值，分别对应照片的序号、拍摄时的太阳高度角和方位角。

此外，沙丘壁纸还有一个 `ap` 根键，其下的 `l` 和 `d` 两个值分别指定了在设置中启用亮暗两种「静态」选项时，要显示的图片序号。（太阳渐变壁纸没有 `ap` 根键，因此在设置中没有「静态」选项。）

至此，原理上的铺垫就全部完成了，最后要解决的就是如何据此自行制作动态壁纸。显然，这涉及到格式转换、信息编码等操作，全部手工完成会非常繁琐。好在，已经有开发者制作出了[命令行工具](https://github.com/mczachurski/wallpapper)，可以使用 Homebrew 安装：

```bash
$ brew tap mczachurski/wallpapper && brew install wallpapper
```

这里简单介绍一下该工具的使用方法。首先，将想要制作成动态壁纸的图片文件按序号依次命名。然后在**同一目录**下创建一个 JSON 文件（如 `config.json`），在其中逐行指定照片的参数：

```json
[
{"fileName":"1.png","isPrimary":false,"isForLight":false,"isForDark":false,"altitude":-0.34275283875350282,"azimuth":270.9334057827345},
…
{"fileName":"16.png","isPrimary":false,"isForLight":false,"isForDark":false,"altitude":-38.04743388682423,"azimuth":53.509085812513092}
]
```

其中，`fileName` 为文件名，`isPrimary` 表示是否将图片用作记录整套壁纸元信息的「首要图片」，`isForLight` 和 `isForDark` 分别指是否用作开启亮/暗两种「静态」选项时使用的图片，`altitude` 和 `azimuth` 则是照片对应的高度角和方位角。

准备完毕后，在终端执行 `wallpapper -i config.json` 即可获得打包好的 HEIC 格式动态壁纸。

如果你想要查询照片拍摄时的太阳位置，或者了解所在地的太阳轨迹，可以使用 [SunCalc](https://www.suncalc.org/) 等在线工具，iOS 上的 [Sky Guide](https://itunes.apple.com/us/app/sky-guide/id576588894?mt=8) 等天文类 app 也可以提供帮助。想要省事的读者也可以使用我制作的[模板配置文件](https://cl.ly/1b0449fdfb89/dynwp-config-sample.json)，其内容原样复制了系统自带的沙丘壁纸中图片的参数，只需找 16 张光线情况与该套壁纸类似的图片，依次命名为 `1.png` 到 `16.png`，并用上述工具制作即可。

![用 Sky Guide 应用查询太阳方位](https://cl.ly/6c096fa8cfa1/skyguide.jpeg)

## 结语

动态桌面是一个很有苹果做派的设计。就像 OS X 窗口最小化时的[「果冻」特效](https://arstechnica.com/gadgets/2000/01/macos-x-gui/6/)、iOS 6 中随屏幕倾斜变换光泽的[音量滑块](https://gizmodo.com/5917967/you-wont-believe-how-insane-this-tiny-new-detail-in-ios-6-is)一样，你可以完全不意识到它的存在，也可以刨根问底，然后惊异于其考虑之深。

当然，对于这类设计，历来不乏「不务正业」的批评。特别是在 macOS 软件质量整体不如以往的大背景下，将本就有限的开发资源，分散给这样一些对性能和稳定没有实质帮助的功能，似乎显得有些奢侈。

尽管如此，我仍然欢迎这样的设计。毕竟，软件设计并不只是关乎功能。设计中的人文色彩及其对用户感受的间接影响，也是细微却重要的方面，说它是一种特殊的「功能」也不为过。每天傍晚，当我看到壁纸随着窗外的日落准时切换成另一种色泽时，很难不产生一点「虚拟与现实无缝衔接」的愉悦。

几个月前，英文苹果社区中曾经有过一次小规模讨论：一些核心用户遗憾地[表示](http://www.peter-cohen.com/2018/05/imac-past-present-future/)，已经很久没有看到像早期 iMac 那样颇有些异想天开（whimsical）的设计了。[糖果配色](https://en.wikipedia.org/wiki/IMac_G3)、[屏幕转轴](https://en.wikipedia.org/wiki/IMac_G4)这些「无用」但有趣的设计，在近年来让位于实用主义的、参数导向的考量。这结论或许对硬件产品线是成立的；但苹果用动态桌面、Animoji，和 Siri 的[玩笑](https://www.macrumors.com/2018/04/11/apples-siri-learns-new-jokes/)告诉我们，它的 whimsy 毕竟还在软件的很多角落里闪现。
