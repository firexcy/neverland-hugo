---
title: "译文 | Marzipan 带来的期待"
date: "2019-05-16"
categories: 
  - "translations"
tags: 
  - "apple"
  - "design"
  - "ios"
  - "macos"
---

**译者按：**本文原题为[《What to Expect From Marzipan》](https://blog.iconfactory.com/2019/05/what-to-expect-from-marzipan/)，是国外知名设计团队 [Iconfactory](https://iconfactory.com/) 的博客文章。文章讨论了苹果预计将在今年 WWDC 上正式发布、用于将 iOS 应用迁移到 macOS 上的 Marzipan 框架，及其对开发者和设计师两个群体的潜在影响。文章指出，尽管 Marzipan 让从 iOS 到 macOS 的过渡看起来只是点开一个开关的功夫，但实际工作远没有那么简单。相反，优秀的应用必须针对 Mac 平台的键鼠操作、屏幕尺寸和多窗口等特性作出功能和设计上的适配，并考虑到更专业用户群体的需求。文章反复提及了苹果系统历史上的数次类似变迁，并对 Marzipan 在短期问题后的最终成功表达了乐观态度。文章最后以一段巧妙而应景的植入式广告结尾。

[钟颖](https://weibo.com/1765732340)对译文的初稿提出了宝贵的专业意见，在此表示感谢。

* * *

今年的 WWDC 很显然会是不同寻常的一届。我们此前在本站写过关于[黑暗模式](https://blog.iconfactory.com/2018/10/dark-mode-and-css/)的思考，现在该来谈谈即将走进 Mac 的 iOS 应用了。

我指的当然就是 Marzipan，一项苹果在去年的主题演讲（Keynote）上公布、但几乎没给出什么细节的技术。我们知道 Mojave 系统中的一些应用使用了这项技术，但也就仅限于此了。

![借助 Marzipan 在 macOS 上运行的 iOS 版 Twitterrific](https://blog.iconfactory.com/wp-content/uploads/2019/05/Olliepan.jpg)

借助 Marzipan 在 macOS 上运行的 iOS 版 Twitterrific

得益于 [Steve Troughton-Smith](https://twitter.com/stroughtonsmith) 的[辛勤工作](https://www.highcaffeinecontent.com/blog/20190301-Bringing-iOS-Apps-to-macOS-Using-Marzipanify)，我们已经更清楚地了解 Marzipan 会给应用程序架构和可用 API 带来怎样的幕后变化。

我今天将要关注的话题，是这项新技术将如何影响产品的开发、设计，和推广。我发现很多人认为这次过渡会很简单，但经验表明它不会像看起来那么容易。

过去这一年，我一直在开发一款新产品，它能原生运行在三个操作系统上：iOS、tvOS，和 macOS。因此，我自觉有些底气来谈论一下三个平台的差异。我从这个项目获得的最大收获，就是认识到交互设计模式的差异会在整个产品中引起连锁反应。

（我们还没有公开谈论这个项目，但 [Patreon 赞助者](https://www.patreon.com/iconfactory)会提前得到消息。）

## 历史小回顾

在谈论交互细节之前，让我们先来看看 Macintosh 平台上工具和开发框架的变迁。Marzipan 或许有一定新颖之处，但肯定不是没有先例。

![](https://blog.iconfactory.com/wp-content/uploads/2019/05/MPW.png)

我的年纪大到足够见证 Mac 的最初发布：1984 年时，你还能买到软盘，在上面用 Pascal 语言或者 68K 汇编代码编程。几年后，构建革命性电脑界面的途径就进化成了 MPW，即[麦金塔编程工坊](https://en.wikipedia.org/wiki/Macintosh_Programmer%27s_Workshop)（Macintosh Programmer’s Workshop）。

![](https://blog.iconfactory.com/wp-content/uploads/2019/05/CodeWarrior.png)

再往后快进几年，又出现了新的语言和工具。很多人开始用 [CodeWarrior](https://en.wikipedia.org/wiki/CodeWarrior) 和 C++ 来编写自己的 Mac 应用。我就是在这样的编程环境下开发了 Iconfactory 的[第一款软件产品](https://files.iconfactory.net/archive/if3/icondropper/icon.htm)。

接着，NeXTSTEP 在 2000 年将纪元推进到了现代。它带来了我们不曾了解的 Objective-C 语言，称为 Project Builder 的 IDE（集成开发环境），还有 Foundation 和 AppKit 两个新的优秀框架。这些工具在多年间充分满足了 Mac 开发的需求，甚至还在 2007 年为 iOS 的 UIKit 框架提供了基础。

如今，新一代的 macOS 工具集将包括 Swift 语言、UIKit 框架，和 Marzipan 技术；或者按我们喜欢的叫法，[Chameleon 2.0](http://chameleonproject.org/) :-)

如你所见，用来构建 Mac 应用程序的工具，在过去 35 年间已经经历了巨大变化，但重要的是看到在同一时间段内什么没有变化。你还在用像素点阵屏幕作为输出设备，用键盘和鼠标作为输入设备。人机交互模式有所变化，但只是轻微的。改进和微调的确存在——例如触控板和手势操作——但你仍然可以只借助 Mac [初创团队订立的基本概念](http://www.folklore.org/)来使用它。

## 一切的关键在于交互

看起来，让你的 iOS 应用在 Mac 上运行不过是在 Xcode 里拨开一个开关的功夫。Steve Troughton-Smith 在[转换应用](https://twitter.com/stroughtonsmith/status/1123703388955467776)时，只用到了 Simulator（模拟器）、他做的 [marzipanify](https://github.com/steventroughtonsmith/marzipanify) 工具，和对开发框架的一系列巧妙修改。

对于包括笔者在内的很多开发者而言，按下转换按钮会是件激动人心的事。然而，让现实压制住兴奋之情也很重要：那个编译选项只不过是漫长曲折的前路上的第一步。好的交互设计不是白捡来的。

如上所述，Mac 已经经历了多次开发工具和框架的变迁。但这一次变动将牵涉到很大一群对于目标平台毫无经验的开发者。对于一个 Mac 开发者，从 CodeWarrior 和 C++ 迁移到 Project Builder 和 Obejctive-C 并不要求学习任何新的惯例：他们仍然在 Mac 上开发。但对于将要开始使用 Marzipan 的 iOS 开发者，事情就没这么简单了。

![](https://blog.iconfactory.com/wp-content/uploads/2019/05/Desktop.png)

在 iPhone 刚出现时，很多应用是由一些将他们在 Windows 或 Mac 上的直觉带到新平台的人开发的。这些应用用起来让人感觉不对劲；它们的消亡，在很大程度上是因为人们都认识到小型手持设备需要一套不同的交互方式。当你将在 iOS 上的开发经验带到 Mac 上时，不要重蹈覆辙。

如果你已经在 iOS 平台上做过一定时间的开发，或许在着手开发 iPad 应用时已经有过这种「拨开开关」的体验。让应用在 iPad 上启动和运行起来是很容易的，但随后你就会意识到大屏幕要求对设计和代码做出大量改动。你将需要重新设计应用，引入主视图/详情视图和自动布局约束。你甚至需要适配应用，使其支持 Smart Keyboard 的输入。

看看你的代码里有多少针对 iPhone 和 iPad 所做的区分，就能理解开发 macOS 应用意味着什么。（原文使用了「user interface idiom」这一术语，这是 UIKit 中一种用于判断设备类型的机制，开发者可以借此指定应用在不同设备上的布局——译者注。）如果你是那种嫌开发 iPad 版应用要花太多额外功夫的人，或许你面对 Mac 所需的差异化处理也会有同样的想法。

本文中的很多思考是我在开发 tvOS 应用时形成的：我发现一套通用的用户界面设计工具并没有帮上多大忙。用上熟悉的 UIKit 部件，例如 `UIImage`、`UIColor` 和 `UIButton` 是好事，但我最终发现两个平台上的版本几乎没有共用的代码。有的视图可以直接在平台间相互移植，但只要涉及控制器（controller）就想都别想。这是为什么呢？

简单来说，一个电视应用上的交互包含六种事件：上、下、左、右、选择、返回。在屏幕上随意定位是行不通的：控制器必须在用户进行这些基本交互时提供引导。用来在按钮和集合视图（collection view）中的项目间移动所需的代码则完全不同。类似地，如果用户准备用 Tab 或箭头键来操作你基于 iOS 代码的应用，macOS 上的 UIKit 并不能魔术般地让问题迎刃而解。

类似的问题还会在这些情景下出现：用户需要通过拖动鼠标选中多个项目；用鼠标右键打开快捷菜单；用快捷键加快操作；或者为常用操作设定功能键。

如果你的代码假定点触屏幕是为了滚动页面，那要怎么实现拖拽框选呢？右键点击是不是类似于检测到另一根手指？需不需要引入新的机制来支持定义快捷键和创建菜单栏选项？还会有办法在 [Carbon 事件回调](https://github.com/shpakovski/MASShortcut)（Carbon event callbacks）间建立连接吗？（Mac OS X 引入的 Cocoa 框架并不便于后台运行的程序设定全局快捷键，因此不少开发者选择使用旧的 Carbon 框架提供的接口实现这一功能——译者注。）

我并不知道上述任何一个问题的答案，但我可以保证，这些新的交互方式会要求你花费额外的功夫来改进你的应用。

你也很可能会发现 `UIResponder` 这样的类突然变得更为重要。在应用内部传送事件（event）变得更难了，因为事件在多个视图和窗口实例、菜单栏和应用程序代理（application delegate）之间传递。

为了理解你将要展开的工作的规模，我建议首先阅读一下[《macOS 人机交互指南》](https://developer.apple.com/design/human-interface-guidelines/macos/overview/themes/)（_macOS Human Interface Guidelines_, HIG）。这些规则自初代 Mac 之时就已经存在，易于理解，对于每一位 Mac 开发者都是很有价值的参考。

![这种标准的 macOS 控件要如何在 iOS 上工作呢？](https://blog.iconfactory.com/wp-content/uploads/2019/05/PopupButton.png)

这种标准的 macOS 控件要如何在 iOS 上工作呢？

除了学习你不了解的知识，你还将有机会思考一些在 Mac 上简单而熟悉的功能——例如[弹出菜单按钮](https://developer.apple.com/design/human-interface-guidelines/macos/buttons/pop-up-buttons/)（pop-up button）——应当如何同时在 iOS 和 macOS 上实现。这个简单的控件在 iOS 上并没有任何对应物，但总有一天会出现，而你也就要用它来在两个平台上写程序。

## 设计的考量因素

并不只有程序员会受到 Marzipan 的影响。作为设计师，你也将会面临挑战。

上面提到的《指南》应该是[你的第一站](https://developer.apple.com/design/human-interface-guidelines/macos/overview/themes/)：里面没有任何代码，描述也往往附有优秀的图示。

在从 iOS 转移到 macOS 的过程中，变化最明显的设计元素就是屏幕。如果你为 iPad 做过应用设计，那你已经了解了来自大屏幕和为尺寸变化适配视图的挑战。这不是一项简单的工作，但如果跳过这一步，得到的设计就只是「大号 iPhone」，会令用户十分不满。

Mac 下的场景略有不同，因为你的应用呈现在一个可以调节尺寸的窗口中：可能前一秒还在 iPhone SE 的局促尺寸下运行，后一秒就拥有了 iPad Pro 那样的宽阔空间。

尺寸可变的窗口还允许在同一时间显示一个以上的视图。在 iOS 上，你已经习惯了独占整块屏幕，只需考虑用户集中于一处的注意力。相反，在 Mac 上，会有很多程序争抢输入和输出机制。

macOS 上，「窗口焦点」（window focus）的概念标示着哪个部件正在接受用户输入。有些标示是自动的，例如窗口边框颜色的变化，但你也需要通过指引用户的操作，改进自己应用视图的操作体验。如果控件因为属于后台窗口而不在活跃状态，就不应该醒目显示。

「焦点」的概念还会引发一个不太明显的设计变动：无处不在的键盘。

Mac 始终连接着键盘，人们也围绕着这一输入设备形成了很多习惯。而对于 iOS 而言，用键盘工作只是锦上添花，很多应用也没花功夫去利用键盘。使用 Marzipan 意味着采纳一种新的交互机制，而不仅仅是点触屏幕。

![](https://blog.iconfactory.com/wp-content/uploads/2019/05/Menu.png)

既然定义用户体验是你的工作，你也就要负责创建菜单栏中的选项。苹果对于菜单设计有很多[建议](https://developer.apple.com/design/human-interface-guidelines/macos/menus/menu-anatomy/)，但一个良好的开端就是在菜单项中用动词指示操作、用形容词指示状态。

把菜单栏选项想象成一种让他人探索应用功能的途径：Mac 用户常常会摸索新应用的菜单，以此了解可以实现的功能。同样重要的是明确应用中最常用的操作，并为其设定快捷键，从而加快用户的操作。

菜单或许在一开始会让人觉得古怪：它们实际上是一种用不到时就被隐藏的界面元素。因此，这部分体验虽然重要，却很容易被忽略。但如果你做得不好，用户就会跟你抱怨 :-)

最后一项需要考虑的交互变化是鼠标与手指的区别。iOS 上只有正在点触屏幕与否两种状态。鼠标指针有第三种状态：应用可以知道指针正在一个视图上悬停。通过在用户的鼠标靠近时突出显示界面中的重要元素，这项新功能可以极大提高应用的可用性。

至于资源文件，你得要制作一些新的图像文件。最明显的就是 [Mac 桌面图标](https://developer.apple.com/design/human-interface-guidelines/macos/icons-and-images/app-icon/)，它应当与 iOS 版图标相似，但不能相同。工具类应用通常具有圆形图标，而文档类应用则具有透视构造。与 iOS 应用不同，显示在 Mac 桌面上的文档有一个不同于应用本身的图标。

![Iconfactory 设计的 macOS 和 iOS 图标示例](https://blog.iconfactory.com/wp-content/uploads/2019/05/Icons.png)

Iconfactory 设计的 macOS 和 iOS 图标示例

另外一点需要了解的是，Marzipan 目前会按照比 iOS 版小 30% 的尺寸显示应用——一张 100pt 大小的图片会在屏幕上被绘制为 77pt。这一缩放是在运行时自动完成的，目的是适应 Mac 更大的感官尺寸和更小的点击区域。鼠标指针比手指更精确，需要的操作空间更小。

我希望正式版会改进这种做法，允许针对不同平台指定不同图片。否则，你就得确保那些具有精细细节的设计能被正常渲染。极细线条和其他像素尺寸的形状可能出现问题。

说到像素，或许有必要重新开始支持 @1x 分辨率的屏幕了。如今 iOS 上的一切都是 @2x 尺寸的了，但在 Mac 上，你会遇到很多仍在使用非视网膜屏幕的用户（特别是外接显示器用户）。真棒。

我们把设计上最大挑战留到最后来说。那就是你设计的**对象**——那个将要使用你 iOS 应用的 Mac 版的人。

## 另一类顾客

你之前一直在为开汽车的人做应用。现在你得到了一类新客户：一群开卡车的人。（乔布斯曾经将电脑和平板的差别比作卡车和汽车的差别，此处借用了这个比喻——译者注。）这些人对于你的产品有一些完全不同的期待。

有不同期待是正常的：如果你的应用能做的只是复制在移动设备上的功能，何必要在 Mac 上使用呢？诚然，便利性是一个因素，但给那群用户提供更强大的环境，才更能满足他们的希望和需求。

要理解这是怎样一类用户，花点时间去听[最近的一期《Accidental Tech Podcast》](https://overcast.fm/+CdQwKWV0/30:12)。这一段的话题是关于 iTunes 的，但结论在你的应用上也很适用。

极简主义在 iPhone 上一直是一项适当的追求。你的目标受众不需要也不希望他们的主要任务受到干扰。

iPad 的出现让情况发生了变化；应用的沉浸程度加深了，因为更大的屏幕尺寸可以让人完成更多工作。如今随着 Mac 的加入，人们将会期待更加强大的功能。去[听听 John Siracusa](https://overcast.fm/+CdQwKWV0/51:30)——一个[对 macOS 略知一二](https://arstechnica.com/author/john-siracusa/)的人——是怎么讨论列表视图的，然后你就能开始理解自己的新目标了。我们不妨管这叫做「反极简主义」。

这些用户还形成了一个社群，与你以往遇到的群体都不相同。这群人热情、友善，如果你对他们首选的平台表现出热情，他们就会成为忠实的支持者；但如果你的成果达不到标准，他们也会成为批判者。

用同一个应用取悦两组截然不同的用户并非易事，但如果使用 Marzipan，这就是你将要承担的任务。

这就引出了我们最后一个、也是最重要的一个话题。你要靠什么为这么多工作提供资金呢？

## 钱在何处

产品必须盈利，否则就会消亡。但如果做一个 Mac 应用只是拨开开关的功夫，客户为什么要为它付费呢？

在我看来，通用版应用是 iPad 生态系统中发生过最坏的事情。开发者无从弥补新交互功能和复杂应用所需的额外工作造成的成本。苹果通过提供统一的下载渠道简化了用户的事前操作，但同时也恶化了开发者的境况，因为让用户最喜欢的应用变成通用版，是开发者没有财力支撑的。苹果的客户很少直接为苹果的软件付费，因此第三方产品的资金问题可能是他们的盲点。

我对 Marzipan 最大的担忧，就是 Mac 应用成为通用版下载的一部分。没有什么会比这更快地磨灭我对这个项目的热情了。

## 重复出现的未来

至此，我想我们已经很清楚适配 Marzipan 对于设计师和程序员都会是个漫长的过程了。对于消费者也同样如此。

不妨回顾一下早期版本的 Mac OS X：曾经的 NeXT 软件迭代了多少回才变得像是 Mac 软件？不同人会有不同观点，但在我看来，新系统花了几年才让我觉得舒服。

![](https://blog.iconfactory.com/wp-content/uploads/2019/05/MaXT.jpg)

那曾是[一团乱麻](https://twitter.com/stroughtonsmith/status/1125024327919910912/photo/1)，直到终于被解决。

在过渡中，macOS 的长期用户会[永远失去一些功能](https://arstechnica.com/gadgets/2003/04/finder/3/)。另一些变化在最初会让人不适，但[我们会适应过来](https://daringfireball.net/2002/11/that_finder_thing)，即使 ⌘N 这类肌肉记忆会十年不变。（从 Mac OS X 开始， ⌘N 在 Finder 中的功能从新建文件夹被改为打开新窗口，让很多 Mac OS Classic 用户感到不适——译者注。）

但别理解错了，人人都能学会适应，即使是初来乍到。正如你[最近在学习新编程语言时所体会到的](https://swift.org/)，路上会有颠簸，你会发现要处理意料之外的变化。

但最终，我们会得到一个全新的、美好的结果，让所有人都满意。

我希望这篇文章能帮你了解 Marzipan 的前方会有些什么。请记住如果需要，我们始终能提供帮助，无论是设计一个[应用图标](https://design.iconfactory.com/category/icons/)、为[用户界面设计](https://design.iconfactory.com/category/interface-design/)提供帮助，还是为开发高质量 Mac 应用提供[咨询](https://iconfactory.com/contact)。我们[从 1997 年起](https://iconfactory.com/20years)就在做这些工作，所以让我们的经验为你提供指导吧！
