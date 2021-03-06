---
title: "WWDC 2020——关于 Mac 未来的半成品答卷"
date: "2020-07-06"
categories: 
---

## 引言

一届形态空前的 WWDC 在不久前落下了帷幕。尽管被迫迁移到了线上，但今年 WWDC 的水准和信息量都被广泛认为更胜以往，现有的各个系统都获得了不同程度的优化改进。

不过，要论本届 WWDC 上最受关注的主角，恐怕还是 Mac 平台——架构迁移、框架更新、设计换代，苹果可谓从里到外为它换上了新装。对于刚刚走出「键盘门」阴影不久、仍在因软件质量下滑备受诟病的 Mac 平台，这不可不谓一针强心剂和一场及时雨。

![Mac 平台是本届 WWDC 当之无愧的主角](https://p178.p0.n0.cdn.getcloudapp.com/items/04uY67R6/hello_mac.jpg?v=05b8ed1ec349454a41223982833c746b)

Mac 平台是本届 WWDC 当之无愧的主角

然而，「新」的并不总是「好」的。过去两周，在浏览相关讲座、文档和社群反馈后，我的体会是：本届 WWDC 上针对 Mac 的大量更新固然令人兴奋，但仍然留下了很多不确定因素，并不足以解决 Mac 平台近年面临的问题。尽管表达出了充分的诚意，但在 Mac 平台的发展问题上，苹果在 WWDC 2020 上只交出了一张「半成品」式的答卷。

## 架构

首先不得不提的，自然是今年 Keynote 主题演讲上的压轴大戏——经过漫长猜测和期待的铺垫，苹果终于在 15 年之后再次更换 Mac 的硬件架构，从基于 Intel 处理器的 x86 架构迁移到基于自研芯片（Apple silicon）的 ARM64 架构。

面对这样一场浩大的工程，用户最关心的或许还是两点：第一，新处理器的性能与 Intel 处理器相比如何？第二，现有软件是否还能正常运行？

先看第一个问题。从技术角度，ARM 架构与 x86 架构最本质的区别在于指令集不同：前者属于精简指令集（reduced instruction set computing，RISC），而后者属于复杂指令集（complex instruction set computing，CISC）。

「指令」可以通俗理解为处理器掌握的「技能」，例如读取、存储、计算操作等。RISC 处理器掌握的指令数量少，实现同样的任务要比 CISC 处理器花费更多的代码和内存，但也因此具有更加灵活，方便通过并行执行来加快执行速度等优势。不少观点认为，虽然 CISC 目前在桌面电脑市场还是主流，但这主要是历史原因（Intel 的强势、广泛的软件支持等）造成的；RISC 和 CISC 在性能上并没有绝对的优劣，例如很多超级计算机使用的就是 RISC 处理器，实际性能表现更多取决于计算场景和软件优化。

实际情况也确实如此。与创新迟缓的 Intel 处理器相比，苹果自研的 A 系列处理器始终保持着快速进步的势头。从性能测试看，iPad Pro 上的 A12Z 处理器的 Geekbench 跑分成绩已经超过了使用 Intel 第十代 Core i5 处理器的 MacBook Air (2020)。如果再考虑进功耗和散热上的明显优势，换用 ARM 处理器对 Mac、特别是 MacBook 的使用体验将有很大促进作用。

![Apple silicon 有望以更低能耗实现更高性能](https://p178.p0.n0.cdn.getcloudapp.com/items/rRulg84n/apple_silicon.jpeg?v=fc3fd3a85682f651aabc7d159585ca0b)

Apple silicon 有望以更低能耗实现更高性能

至于第二个软件兼容性问题，苹果也是有备而来，从箱底搬出了当年从 PowerPC 迁移到 Intel 处理器时的解决方案。

首先，苹果重新启用了 Universal 技术，让软件可以同时包含适用于 Intel 和 ARM 两种处理器的可执行文件，称为「通用二进制」（universal binary）格式。其次，对于没有专门针对 ARM 架构编译的旧版软件，Rosetta 2 技术会将其「翻译」为新处理器可以运行的代码。与当年的初版相比，新版 Rosetta 可以在软件安装时就完成「翻译」工作，而不是等到每次运行时再翻译，因此理论上效率和性能都更高。

不过，尽管迁移到 ARM 架构的整体前景是是乐观的，**实际执行效果仍然存在不确定因素，并将很大程度上取决于第三方软件能否及时适配新架构。**

首先，通过 Rosetta 2 翻译的未适配软件，**性能会受到较大影响**。

根据部分开发者在收到 Developer Transition Kit 测试机（搭载与 iPad Pro 相同的 A12Z 处理器）后进行的 Geekbench 跑分测试，Rosetta 2 翻译造成的性能损耗 [大约为 25–40%](https://9to5mac.com/2020/06/29/first-benchmarks-surface-for-apples-arm-based-developer-transition-kit/)。这对于浏览网页等日常操作或许不会有很大影响，但对于处理复杂文档、多媒体编辑、软件开发等较为繁重的任务，就是比较明显的性能损失了。

其次，尽管苹果宣称「大多数开发者将能在 [几天内](https://www.apple.com/newsroom/2020/06/apple-announces-mac-transition-to-apple-silicon/)（in a matter of days）使其应用在新架构上运行」，但**实际的适配工作仍然有着不少门槛**。

例如，苹果自己在 [开发文档](https://developer.apple.com/documentation/xcode/porting_your_macos_apps_to_apple_silicon) 中就采用了更谨慎的口径，提示了架构迁移将会带来的适配成本。苹果指出，ARM 和 Intel 处理器在虚拟内存页面大小、缓存容量、指令集等参数上存在差异，依赖于这些特性的软件必须更新代码才能继续运行（首当其冲的就是虚拟机软件）；ARM 处理器独有的 [「大小核」](https://en.wikipedia.org/wiki/ARM_big.LITTLE) 结构也要求开发者更积极地将能耗效率纳入考量。

![Apple silicon 的「大小核」设计需要专门优化才能发挥优势](https://p178.p0.n0.cdn.getcloudapp.com/items/ApuAgKmo/async_cores.png?v=90fa376487547a82aa73139b9b65bdd4)

Apple silicon 的「大小核」设计需要专门优化才能发挥优势

为此，苹果提倡尽可能使用 Metal、DriverKit 等官方提供的、较新的技术或接口，而不是 OpenGL、Kernel extension 等第三方或较旧的选项。但对于那些有较长开发历史的软件来说，改换这些较为底层的技术并不是一朝一夕可以完成的。

何况，架构迁移的进度并不完全取决于开发者的积极性。所谓「一个好汉三个帮」，软件开发中，并不是所有功能都需要由开发者自己实现，而是往往可以借用很多别人造好的「轮子」——第三方库。但根据苹果的要求，架构迁移必须是以一个软件为整体进行的——只有主程序本身及其使用的所有第三方库都适配 ARM 架构，整个软件才能以原生模式运行。问题是，开发者并不能左右第三方库的适配进度，从而可能面临等待和重写/放弃部分功能的两难。

不仅如此，对于用户购买决策和日常操作体验影响最大的，往往不是适配迅速的独立应用，而是那些由巨头们开发的「大型软件」——微软的 Office、Adobe 的 Creative Cloud 等。这些尾大不掉的软件能多快完成适配，恐怕只能靠求神拜佛才能知道。事实上，在 Mac 上一次从 PowerPC 到 Intel 架构的迁移中，Adobe 花了 10 个月才发布了能在 Intel 架构 Mac 上原生运行的 Create Suite 3，而微软则花了一年半才发布了适配新架构的 Office for Mac 2008。

或许正是考虑到用户可能有此顾虑，苹果在 WWDC 上专门 [演示](https://youtu.be/GEZhD3J89ZE?t=5742) 了这两家软件在 ARM Mac 上的运行效果，并且不惜用上了「super smooth」「responsive」这类平时只会用来修饰自家产品的溢美之词。然而，经过「精心」编排的操作演示也跟真实体验完全不是一回事（别忘了乔布斯演示的初代 iPhone [必须遵守特定步骤才能不死机](https://www.nytimes.com/2013/10/06/magazine/and-then-steve-said-let-there-be-an-iphone.html?pagewanted=all)）。考虑到 Word 目前在 Intel Mac 上都还运行得磕磕绊绊，我个人对于它适配 ARM Mac 的进度和效果只能持保留态度。

![苹果演示 Office 已经可以在新架构上运行，但实际效果仍然有待观察](https://p178.p0.n0.cdn.getcloudapp.com/items/X6uo7qbq/office_on_mac.jpg?v=583b41ccf7844c344a59b201bb63b9fe)

苹果演示 Office 已经可以在新架构上运行，但实际效果仍然有待观察

最后，迁移到 ARM 架构对于 Mac 应用生态还有一项重要影响——**iOS 应用将可以不经修改地直接在 ARM Mac 上运行**。苹果已经表示会把这做成一个默认选项——如果开发者不主动取消，其开发的 iOS 应用将可以直接在 ARM Mac 上的 App Store 被用户直接搜索到并下载安装。

从积极的角度说，这么做显然有助于大幅充实 Mac 平台的应用数量。特别是对于那些惰于开发桌面端应用的「大厂」服务，哪怕只是用上放大版的 iPhone 应用，也算一种体验升级（我一直觉得对着手机屏幕点外卖是非常折磨人的）。

但反过来说，允许直接运行 iOS 应用，又可能进一步为部分厂商忽视 Mac 平台提供借口；如果今后的 Mac App Store 被 iOS 应用充斥，很难说是优化还是劣化了 Mac 平台的生态。

更令人担忧的是，对于那些真正有志于开发优质跨平台应用的开发者，iOS 应用的通行还可能为用户提供一种「投机省钱」的动机——宁愿牺牲部分体验，将就使用廉价的 iOS 版，也不愿为 Mac 版另外付费。由于 iOS 应用上架 Mac App Store 是默认的，如果为了堵住上述空子而选择不上架，又可能面临被用户指责为「贪婪」的舆论风险。

因此，在充实 ARM Mac 的应用数量和维护开发者的积极性之间，苹果或许还需要更为审慎的考量。

## 框架

除了架构更新，今年的 WWDC 也针对 Mac 应用的开发框架宣布了很多新变化。

如果你对「框架」（framework）的概念比较陌生，可以这样通俗地理解：如果将操作系统比作一家餐厅，为系统开发应用比作做菜，那么开发框架就类似于「食材库」，为烹饪提供现成的原料。

在过去，macOS 和 iOS 虽然是同一品牌旗下的两家「分店」，但「食材库」是各自专属的，分别称为 AppKit 和 UIKit。两者虽然在内容上有很大的重合与相似，但并不互通。因此，两家分店的菜谱就因为备料不同而无法通用。

### Mac Catalyst

去年的 WWDC 上，苹果在一年的酝酿后正式向开发者开放了 Mac Catalyst 技术，其作用是将 UIKit 从 iOS 移植到了 macOS 上。由于有了完全相同的食材库，iOS 分店的菜也可以端上 macOS 分店的桌了。

但 Mac Catalyst 并不是一个完美的解决方案。最大的问题在于食谱可以照搬，但食客的口味难以统一。

想象一下，一家开在南方的分店，即使能 100% 复刻出北方分店里的咸豆腐脑，也难免显得格格不入。类似地，让 iOS 应用在 Mac 上能够运行只是最低限度的要求。两个平台的应用从控件外观（按钮、菜单等）、输入方式（触控/鼠标加键盘）到操作逻辑（全屏/多窗口）都有诸多区别，照搬照套只会得到「橘越淮而为枳」的古怪效果。

去年 WWDC 前夕，知名 Mac 和 iOS 应用开发商 Iconfactory 曾 [发文](https://sspai.com/post/54715) 表达过这种担忧，事实证明一语成谶：一年过去，Mac App Store 上使用 Mac Catalyst 开发的应用屈指可数；一些原本十分优秀的 iOS 应用经过移植，获得的反响也令人失望。

![在 macOS Mojave 中作为首批 Catalyst 应用出现的 Home 应用，因为与 macOS 格格不入的设计受到批评](https://p178.p0.n0.cdn.getcloudapp.com/items/eDu1EWNJ/home_app.png?v=7b796a7f81d808d2b7242d3e1e8d5126)

在 macOS Mojave 中作为首批 Catalyst 应用出现的 Home 应用，因为与 macOS 格格不入的设计受到批评

这个问题在今年的 WWDC 上得到了回应。简单来说，苹果赋予了 Mac Catalyst 应用「入乡随俗」的能力，可以针对 iPad 和 Mac 两种运行环境，显示出不同的布局和外观。

用苹果的术语，今后通过 Mac Catalyst 开发的 Mac 应用将能运行在两种「idiom」（一种用于判断设备类型的机制，可以形象地翻译/理解为「方言」）之下。

其中，iPad idiom 与以往相同，相当于将 iPad 应用调整尺寸后直接运行。而在新增的 Mac idiom 中，iPad 上的界面元素将被自动「翻译」为对应的 Mac 形态，例如按钮、滑块等；iOS 风格的开关也会变成在 Mac 上看起来更自然的复选框。此外，系统会自动设定界面元素和文本的最佳尺寸，而不像以前那样机械地缩小为 iPad 版的 77%。

![学会适应 Mac 口味的 Catalyst 应用，看起来更加自然](https://p178.p0.n0.cdn.getcloudapp.com/items/2Nu5pYbk/mac_idiom.png?v=a40b9bb16a24086622cfb5f248f560d8)

学会适应 Mac 口味的 Catalyst 应用，看起来更加自然

当然，天下没有免费的午餐。要想获得新版 Mac Catalyst 获得的更好效果，开发者也要相应付出更多的劳动，例如在代码中增加专门用于 Mac 的布局安排。为 iPad 的尺寸和分辨率设计的图片资源，也需要搭配对应的 Mac 版本。苹果建议，如果开发者追求适配效率、希望优先保持与 iPad 的兼容性和原有界面布局，则可以考虑继续使用 iPad idiom。否则，就可以考虑选择 Mac idiom 获得更原生的适配效果。

### SwiftUI

不过，Mac Catalyst 制作的 Mac 应用再「惟妙惟肖」，毕竟也只是模仿和妥协；在苹果的规划中，各个平台「大一统」的目标，最终还是要通过新一代框架——[SwiftUI](https://developer.apple.com/xcode/swiftui/) 来实现。

什么是 SwiftUI？用官方的话说，这是一种使用「声明式」（declarative）语法，在所有苹果平台上构建用户界面的简便方式。

沿用之前做菜的比方，如果说直接用 UIKit 和 AppKit 开发应用是亲自下厨，那么用 SwiftUI 就类似于找了一个帮手，你只要向他描述想要实现的效果，他会负责为你找齐所需的食材并调出当地适销的口味。

当然，有人使唤固然省事，但也不是没有隐患：请来的帮手未必能准确领会你的意图，也未必掌握做出你想要的菜所需的全部技能。

这正是 SwiftUI 在去年推出后受批评最多的两个问题：首先，SwiftUI 实现的效果往往与开发者想象的有较大区别，声明式语法执行的准确度没有保障；其次，SwiftUI 并不支持 AppKit 和 UIKit 具备的全部功能，因此开发者很多时候还是得挽起袖子直接写相应的 AppKit 或 UIKit 代码。

今年，苹果宣布开发者以后可以只使用 SwiftUI 开发整个应用，而不是像以前一样需要将 SwiftUI 代码嵌入在其他框架的代码中。同时，新版系统的小部件（widget）等功能将只能使用 SwiftUI 开发。

![使用 SwiftUI 让开发者可以通过相同的代码在不同平台上获取最佳显示效果](https://p178.p0.n0.cdn.getcloudapp.com/items/BluOz7eP/swift_ui.png?v=93a152ffe6134a002a73bc7c3a822fa8)

使用 SwiftUI 让开发者可以通过相同的代码在不同平台上获取最佳显示效果

尽管这些变化并不意味着 SwiftUI 能在短时间内完全取代 AppKit 和 UIKit，但 SwiftUI 将成为统领苹果平台界面开发的主要框架，已经成为不少开发者的共识。

显然，如果苹果今年的 UI 开发框架更新能够一一兑现，那么用户能感受到的进步将是明显的。然而，**仍然有一些理由让我们保持谨慎乐观**。

首先，**界面并不是开发的全部**。无论 AppKit、UIKit 还是 SwiftUI 都只是用于搭建用户界面的开发框架，而界面设计只是应用开发中的诸多环节之一。在界面之下诸多更为底层的部分，iOS 和 macOS 仍然存在很大差异，而这是 Mac Catalyst 力所不及的。

最典型的例子可能就是自动化。macOS 中，系统和应用之间可以通过 [Apple Event](https://en.wikipedia.org/wiki/Apple_event) 传递指令和信息；帮助用户实现自动化功能的 Apple Script 脚本和 Automator 应用也建立在 Apple Event 的基础上。而 iOS 在早期一直缺乏类似的框架，只是到了晚近才通过 SiriKit 为应用提供了一定的自动化能力，但在功能性、通用性上都暂时还远达不到 Apple Events 的高度。因此，对于那些看重自动化功能的应用而言，苹果的框架在现阶段还没有提供足够的跨平台能力。

![Mac 原生应用的自动化能力显著高于 iOS 应用](https://p178.p0.n0.cdn.getcloudapp.com/items/Z4uYGl6N/script-editor_dictionary_2x.png?v=0de0a3058594762066f01d06126f9d2c)

Mac 原生应用的自动化能力显著高于 iOS 应用

此外，macOS 和 iOS 在音视频处理、文件系统等层面也存在不同程度的差异；由于使用场景不同，macOS 应用还要额外考虑多用户切换、第三方硬件等因素的潜在影响。如果只满足于界面适配、而忽视了这些细节，所得的移植应用与 macOS 仍然只会是貌合神离的。

其次，**通过赋予 Mac Catalyst 更多的重要性，苹果似乎正在鼓励一种「iOS 本位」的应用开发思路**。尽管 iOS 应用的功能已经今非昔比，但在深度上仍然整体弱于 Mac 应用，很多专业工具的 iOS 版都是 Mac 版的简化。这很多时候并非是开发者在偷懒，而是不同平台在性能、使用场景等方面的天生区别导致的。担忧在于，如果跨平台成为压倒一切的优先目标，是否可能促使开发者在设计软件功能时追求「最小公分母」、而不是充分挖掘 Mac 平台的特征和潜力？与之前提到的允许 Mac App Store 下载 iOS 应用类似，这或许是苹果追求充实 Mac 平台软件数量的同时，需要长远考虑和仔细衡量的。

## 设计

在架构和开发框架的变动之外，macOS 今年在设计语言上也迎来了很大的 [更新](https://developer.apple.com/design/human-interface-guidelines/macos/overview/whats-new-in-macos/)。

最明显的变化在于图标。过去，macOS 的图标并没有固定的形状，只是根据应用的类型有一些较为模糊的设计惯例，如工具类应用使用圆形图标、文档类应用使用矩形透视图标等。macOS 11 则统一改用了和 iOS 一致的圆角矩形图标，但仍然保留了以往设计中的丰富细节和透视、阴影等元素。去年亮相的 SF Symbols 也登陆 Mac 平台，数量大增、且支持了彩色。

![更加丰富多彩的 SF Symbols 登陆 Mac 平台](https://p178.p0.n0.cdn.getcloudapp.com/items/JruLejA8/sf_symbols.png?v=009d2ca5e09e9b4d0ba89e547ef7037a)

更加丰富多彩的 SF Symbols 登陆 Mac 平台

此外，新版系统的窗口设计变得更加扁平，去掉了边框的渐变色和按钮的底色，边沿从尖角变为圆角；菜单、工具栏、列表的留白尺寸大幅增加；侧边栏、控制按钮和弹窗提示的风格也得到翻新。

尽管「皮肤」层面的变化并不直接关系到软件功能，但仍然会对用户的使用体验产生潜移默化的影响。在我看来，macOS 11 的视觉变化同样是喜忧参半。

从好处来说，这些变化确如苹果所言，让苹果系统家族的整体性、规范性更强；在和 iOS 呼应的同时，又保留了以往 Aqua 风格引以为豪的细节——用官方的话说是「审慎而富有表现力」（judicious expressiveness）；更大的留白也被广泛解读为触控版 Mac 的铺垫。对于那些从 iOS 入门苹果生态的用户，这些跨平台的一致性或许有助于让 Mac 更易于上手。

但另一方面，从很多老用户的视角看，新的设计又似乎在追求亮眼的道路上走得太远，而牺牲了易认性和操作效率。

例如，有的元素对比度过低，如菜单栏过度透明，以至到了影响阅读菜单文字的程度；而有的对比度又过高，如窗口边框在削减渐变色后成了一片「惨白」，显得非常刺眼。

![新版设计存在较为明显的对比度问题](https://p178.p0.n0.cdn.getcloudapp.com/items/nOueLz9d/20200701-Big%20Sur%20menu%20bar.jpg?v=2d4571307f9f5b90e99932ea0aa739c0)

新版设计存在较为明显的对比度问题

又如，新的留白尺寸颇有些大而无当，在空间寸土寸金的 MacBook 上更是接近一种挥霍。（颇为矛盾的是，苹果从几年前开始，就为了增加 MacBook 的可显示内容，默认启用了高于物理像素数的分辨率设置。）哪怕这真的是在为触控 Mac 作准备，也至少可以提供一个选项，允许用户切换回更「紧凑」的界面布局。

## 总结

尽管 Mac 在本届 WWDC 上得到的关注不可谓不多，但似乎都缺少一根主轴——Mac 平台未来发展的清晰轨迹。

近两周来，国外开发者社群的热门讨论点之一，就是「在 AppKit、UIKit 和 SwiftUI 间如何选择」（Craig Federighi 在接受访谈时含糊地 [回答](https://daringfireball.net/thetalkshow/2020/06/24/ep-286)「没有绝对的正确道路」）。这从侧面说明，比起获得更多的选项，开发者更需要的可能是一份时间表和路线图：AppKit 会不会像当年的 Carbon 一样最终谢幕？如果 SwiftUI 最终会成为各平台通用的唯一开发框架，它何时才能真正在功能上独当一面，目前的并行状态会维持多久？这些问题都是今年的 WWDC 付之阙如的，但如果一直悬而未决，显然会影响人们为 Mac 开发应用的信心。

今年 WWDC 没有解决、反而在某种程度上放大的另一个问题，是 Mac 的「身份危机」：在 iOS 系统和硬件不断增强的背景下，Mac 如何维持自己在苹果生态中的独特价值，而不是在 iOS 的身后亦步亦趋，逐渐退化为一个「交差」式的产品线。

如上文所述，Mac 平台在今年获得的更新几乎都是靠 iOS 反向输送的：Apple silicon 芯片是在 iOS 上多年打磨后成熟的，新的 UI 开发框架都是起源或率先应用于 iOS，界面设计的变化也是大幅取材于 iOS。这不禁让人担心，Mac 是不是会变成一位「差不多先生」，和 iOS 穿着差不多的衣服、提供着差不多的功能、运行着差不多的应用；却标着更高的售价、有着更不确定的未来？

对此，苹果的官方口径始终是否认计划将 Mac 和 iPad 合二为一。但仅仅维持 Mac 的独立身份，并不足以维持它的独特性。

![“No.”](https://p178.p0.n0.cdn.getcloudapp.com/items/2Nu5pJo6/mergingmacipadslide.jpg?v=b182adb6b33d29edea953628dae0b2e0)

“No.”

2015 年，苹果高级副总裁 Phil Schiller 在接受采访时，曾经 [论述](https://medium.com/backchannel/exclusive-why-apple-is-still-sweating-the-details-on-imac-531a95e50c91#.wrz9at3q9) 过苹果各个产品线之间的关系：Apple Watch 的使命在于尽可能替代 iPhone 的使用场景，iPhone 要尽可能替代 iPad，iPad 要尽可能替代 Mac 笔记本，而 Mac 笔记本又越发能替代 Mac 桌面机。在这个传导关系的最前端，Mac 桌面机的作用「在于挑战我们对计算机能力的认识、完成其他计算机以往从未实现的任务」。

据此，苹果的产品线似乎是一列火车，后面的车厢随着位移、不断占据前面车厢曾经的位置，而前面的车厢此时则进入了新的领域。作为火车头牵引着整列火车的，正是 Mac 产品线——「如果 Mac 桌面机的任务是和笔记本竞争、追求轻薄，那么它就没有存在的必要了。」但从今天的现状看，即使 Mac 仍然在苹果的产品线中占据一席之地，它的「火车头」角色已经不保，从牵引者变成了被牵引者。

![Mac 在苹果产品线中的「火车头」地位不保](https://p178.p0.n0.cdn.getcloudapp.com/items/wbuWLZD6/apple-prod-line.png?v=982100908acb5ab9a9c4353a69cdfafa)

Mac 在苹果产品线中的「火车头」地位不保

在我看来，Mac 要走出这一「身份危机」，只靠照着 iOS 补缺补差是不够的，而是应当**重新认清并聚焦于塑造其身份的内核**。

对于 iPad 来说，这个身份内核是它的形态——一块尺寸介于手机和电脑之间、轻薄便携的触控屏幕。iPad 之所以能在早年软件功能和应用数量都未成气候的情况下，仍然开拓出一个专属于它的产品门类，主要功劳就在于这块开辟了独特使用场景的屏幕。iPad 的历次更新和产品线划分，也主要是围绕着屏幕参数做文章。可以说，哪怕 iPadOS 变得再强大，没有这块屏幕，iPad 也不成其为 iPad。

与此不同，虽然 Mac 的工业设计也是吸引人们购买的重要因素，但无论苹果在设计上如何精进，Mac 归根到底仍然是一台电脑——一个创新停滞、销量下滑成为既成事实的传统品类。另一方面，尽管 Mac 在近年设计决策备受争议，但很多用户仍然感到难以割舍，主要还是出于对 macOS 和 Mac 第三方软件的依赖；「黑苹果」的流行也从侧面印证了 macOS 的吸引力。可见，**软件才是塑造 Mac 的身份内核**。

因此，Mac 和 iPad 的发展本不应是相互冲突的：如果说 iPad 的目标是探索「广度」，通过便携的形态和丰富的外设，适应不同场景的需求；Mac 的目标则是探索「深度」，通过自定配置和安装软件，最大程度地提高特定工作的效率。

此外，由于普通用户的需求向移动端转移是不可避免的趋势，Mac 未来的销售很可能会愈发依赖于市场的长尾部分，即那些需求高度个性化的专业用户；这与 iPad 聚焦的大众消费市场也能形成区分。但是，要抓住这类用户，在扩展 iPad 的份额的同时维护 Mac 的市场地位，就更应当强调软件的扩展性、稳定性，而非追求「新鲜感」。

从这个角度看，macOS 近来的很多变化都显得「广度」有余而「深度」不足。以本届 WWDC 上的更新为例，移植而来的 iPad 应用多是针对日常场景、内容消费等的「轻量」应用，对于处理专业的工作需求可能并无太多帮助；新版设计造成信息密度下降，也无益于提高工作效率。

与此同时，苹果为追求「安全」「隐私」的目标而持续削减着 macOS 的自由度和扩展性，在文件系统、软件运行方面施加了很多偏向激进的限制，给专业用户造成了很大不便；这个趋势在 macOS 11 中似乎还在进一步加强。如果说外观和设计上的「iOS 化」只是习惯问题，这种软件设计理念和功能导向上的「iOS 化」则会直接威胁到 Mac 的独立身份。

![比起亮眼的外观和功能上的微创新，核心用户更需要的或许是找回 macOS 的扩展性和自由度](https://p178.p0.n0.cdn.getcloudapp.com/items/yAuY9P9x/bigsurfeatures.png?v=5540be1b43372b67fbcfd61a6713f435)

比起亮眼的外观和功能上的微创新，核心用户更需要的或许是找回 macOS 的扩展性和自由度

抛出一个个新功能，却忽视了同步给出指引；为 macOS 补缺补差，却忽视了维护区分于 iOS 的独特价值——正是在这个意义上，今年的 WWDC 成为了一张关于 Mac 未来的半成品答卷。

诚然，对于传统电脑在移动时代如何演进，行业目前也没有完全成功的先例；通过尝试让 Mac 和 iPad 互相靠近，苹果或许也还在反复试探一个微妙的平衡点。只是，用户和开发者会有足够的耐心和信心陪它一起实验下去吗？
