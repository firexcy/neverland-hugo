---
title: "订阅、云服务、套壳——关于 1Password 8 的是非争议"
date: "2021-09-22"
categories: 
  - "post"
---

_**Note:** The post was originally written as [a premium article](https://sspai.com/prime/story/1pw8-disputes) for members of SSPAI and subsequently released to the public as a trailer._ _You may want to [sign up for the membership](https://sspai.com/prime) if you’re interested in such content. Thanks for your support._ _Disclaimer of affiliation: employee._

* * *

**_Edit 1 \[2021-10-01\]:_** In a previous version, I translated the term “separation of concerns” to “分而治之”; this was incorrect. The former is a _design principle_ that a system should be separated into distinct sections, with each section addressing a separate concern, _i.e._, a set of information. The latter is more commonly used as the translation of the term “divide and conquer,” an _algorithm_ that recursively breaks down a problem into sub-problems that are simple enough to solve separately. A more proper translation, “分离关注点” has been adopted. Thanks @oscargong for the feedback.

* * *

## 事件梳理

[1Password](https://1password.com/) 是一款知名的密码管理工具，运营主体为加拿大公司 AgileBits, Inc.。

1Password 最初发布于 2006 年，当时只有 Mac 版，密码库以一个独立数据库的形式存储在本机硬盘、或用户指定的 Dropbox 等第三方网盘中。

![](https://cdn.sspai.com/2021/09/19/article/cbaf6a2eb6308f8aa9df9d738285125a)

后来，1Password 逐渐扩展到 iOS、Android、Windows 等平台，并于 2015 年末推出了自己的同步服务（[1Password.com](http://1password.com/)），许可收费模式也改为以订阅制为主，但独立密码库功能和买断制许可仍然保留。

2021 年 5 月，1Password 团队宣布推出 Linux 版客户端。根据在同期发表的 [Medium 文章](https://dteare.medium.com/behind-the-scenes-of-1password-for-linux-d59b19143a23)，该版本使用了一种「混合」架构，其中前端（软件界面）部分使用 Electron 框架编写：

> 1Password for Linux 是我们第一款混合 \[架构\] 应用。\[…\] **后端**用 Rust 写成，这个语言以其安全性和高性能而闻名。

> \[…\] **前端**使用 web 技术，这让我们得以能打造 1Password 的全新设计语言；不仅美观，而且让我们 \[的开发工作\] 高度敏捷、快速迭代。在为 [1Password.com](http://1password.com/) \[上的网页版\] 和浏览器插件开发界面时，我们就用了 TypeScript 和 React，并大获成功。因此，这次 \[继续使用这些框架\] 也就是自然而然的选择了。

> 我们此次发布 Linux 版的主要目标之一，就是打造一个**共用的内核**，其作用在于与 [1Password.com](http://1password.com/) \[上的服务端\] 通讯，并集中完成尽可能多的计算任务。我们希望在所有客户端共用一个代码库，实现集中开发功能、一次性修正漏洞。我们还希望通过组件架构的设计，避免这个共用的内核不会被恶意利用。

![](https://cdn.sspai.com/2021/09/19/article/18657924e6cb05f910db1af9e6f7bd01)

随后，在 8 月，1Password 团队[宣布](https://blog.1password.com/1password-8-for-mac-is-now-in-early-access/) Mac 平台的下一版本——1Password 8 进入初期测试（early access）阶段，并开放下载。

根据同期发布的[官方博客文章](https://appleinsider.com/articles/21/08/16/users-lobby-1password-to-abandon-new-electron-version)，不同于该软件过去在 Mac 平台一直坚持的原生框架开发路径，1Password 8 也已转向与 Linux 版相同的混合架构，即使用 Electron 框架编写用户界面，而原因则是「不得已而为之」：

> 如何为 macOS 开发 1Password 8，可能是我们做过的最复杂的决策。\[…\] 我们决定采取「双分支」的做法，开发两个 Mac 应用。其中一个用 SwiftUI 编写，面向最新版操作系统；另一个使用网页 UI，从而支持旧版系统。

> 尽管 SwiftUI 让我们在 iOS 和 macOS 版本之间可以共享代码的比例达到有史最高，我们还是发现需要为某些组件单独开发 \[两种\] 实现，才能在相应的系统上显得自然，有时整个功能都得单独开发。\[…\]

> 最终，我们痛苦地决定停止用 SwiftUI 开发 Mac 应用，把 SwiftUI 的开发集中在 iOS 上，靠 Electron 版应用支持所有版本的 Mac 操作系统。

![](https://cdn.sspai.com/2021/09/19/article/b56edae2441dbc861bf7b7fcbb62433b)

与开发框架的变动同步，1Password 8 的付费模式也发生了变化，取消了一直存在的「买断制」许可，只保留近年新增的订阅制。

不过，官方最初并没有明确指出这一点，只是到了用户在官方论坛发帖质询后，创始人 Dave Teare 才[出面回应](https://1password.community/discussion/comment/601917/#Comment_601917)：

> 鉴于 1Password 会员服务备受欢迎，而 [1Password.com](http://1password.com/) \[的网页版服务\] 在功能上远胜其他 \[既有客户端\]，我们下一代 1Password 应用将专注于会员 \[订阅制服务\]。\[…\] 现在是时候告别独立买断许可证了。

对现有买断制用户，则提供专属优惠鼓励迁移：

> \[为表感谢，\] 只要将你的现有许可证邮件发给我们，即可获得三年期的五折优惠。\[…\] 我们理解有人希望只在明确同意时付款；如果是这样，我们也提供了一项特惠：你可以花 99 美元购买一张价值 150 美元的礼品卡，足够使用 1Password 三年多。

在[另一则回复](https://1password.community/discussion/comment/602340/#Comment_602340)中，Teare 则明确表示将停止提供独立密码库的功能，但不排除未来推出自建（self-host）服务端的选项：

> 下一代 1Password 应用将仅能与 [1Password.com](http://1password.com/) \[上的订阅制服务\] 同步。\[…\] \[Mac 上的\] 1Password 7 不受影响，现有的同步方式均能继续使用。

> \[…\] 我们已经在琢磨允许用户自主搭建云服务的思路。那将成为你个人专属的 1Password 服务，完全运行在你的主机，或者你掌控的云端。但一个大问题是：有多少用户朋友需要这个功能？\[…\] 请参与[这项调查](https://1password.community/home/leaving?allowTrusted=1&target=https%3A%2F%2Fsurvey.1password.com%2Fself-host%2F)，帮助我们进一步理解你的使用场景。

## 反对观点

1Password 宣布上述开发方向和商业模式调整后，受到了大量质疑。

**最多的批评意见集中于改用 Electron 开发 Mac 版的决策。** 常见的角度包括：

- 新版界面显得不够「原生」。即使 1Password 8 在设计上试图模仿 Mac 原生应用的外观，但受限于 Electron 框架基于网页技术的本质，仍然留下了很多露出「套壳」本性的破绽。最典型的例子就是「偏好设置」界面——不再是独立的窗口，而是位置固定的一个模态对话框。
- Electron 在安全性方面的历史称不上光彩。过去几年中被发现的安全漏洞曾影响到 Slack、Skype 等知名应用，可能导致任意执行代码等后果。尽管这不能代表 Electron 当下的安全状况，但考虑到 1Password 作为敏感信息管理工具的定位，的确不免让人产生「自废武功」的担心。
- 一些反馈称 Electron 版本的 CPU、内存资源占用和耗电都高于原生版本（值得注意的是，这方面目前并无严谨测试结果，不少评论更是只看到 Electron 就直接得出了吃性能和耗电的结论）。
- 受限于 Electron 目前对 ARM 架构的适配进度，针对 Intel 和 Apple Silicon 机型的安装包不能通用（即提供 Universal Binary 版本），只能分别提供。

![](https://cdn.sspai.com/2021/09/19/article/ecfb6d1aa93da2fd5930a05e12f1d2df)

相比之下，**对于全面采用订阅制的批评则相对没有那么密集**。这或许是因为 1Password 已经在过去几年中逐步淡化买断制许可的地位（只留下一个很不明显的购买入口，需要花一番工夫才能买到），而不能接受订阅制的用户已有相当比例先行离开了。此外，仅从成本上计算，官方为老用户提供的前述优惠方式也确实并不会比定期购买大版本升级花费更多。

不过，仍然有一些观点**对仅保留订阅制、以及相关的取消独立密码库的变更提出了合理质疑**。

例如，名为「MikeV99」的用户对于订阅制的价值[提出](https://1password.community/discussion/comment/603660/#Comment_603660)了一种尽管罕见、但也引人思考的疑问：

> 我夫人今年 80 岁了，我明年一月也要满 80 岁。我做了你们这么多年顾客，升级过很多版本。如果我不按年订阅，终身订阅要收多少钱？

名为「thundersparrow」的用户则[提出](https://1password.community/discussion/comment/606748/#Comment_606748)了一种可以接受订阅制、但不能接受在线密码库的合理场景：

> 我是个技术支持顾问，为多个客户工作。对于每个客户，我都会创建一个本地密码库存放这位客户的密码。

> 我使用 Tresorit（类似于更安全的 Dropbox）作为主要的数据同步服务，通过它的文件夹同步功能来同步 macOS 上的所有 1Password 密码库。这在多台 macOS 设备上运行良好，甚至还能用来和为同一客户工作的同事协作。

> 我还会选择一些密码库，通过无线局域网同步功能同步到 iOS 设备上。我没有任何一个密码库通过 [1Password.com](http://1password.com/) 同步。\[…\]

> 我不会接受把密码库迁移到 [1Password.com](http://1password.com/) 上，因为这违反了「分离关注点」（the separation of concerns）的原则。

还有一些意见**对 1Password 快速融资、投入企业市场提出质疑**，认为这反映了一种「忘记初心」的倾向。这里的背景是 1Password 团队于 2019 年和 2021 年两次接受风险投资机构 Accel 的投资，投资额分别为 2 亿和 1 亿美元，投后估值已达到 20 亿美元。

![](https://cdn.sspai.com/2021/09/19/article/a72b0389085169eb46edf72b32ab952c)

例如，开发者 Drew McCormack [认为](https://twitter.com/drewmccormack/status/1426586869408665606)：

> 我得承认当初没理解 1Password 拿风投的原因。回头看来，我没意识到它已经不再是个密码管理应用，而蜕变成一个账户托管服务了。这就很说得通了。弯转得妙啊。

此外，不少用户表示比起功能和价格变化，更令他们感到不满的是**官方避重就轻、顾左右而言他的回应态度**。

例如，Hacker News 用户「bgentry」[表示](https://news.ycombinator.com/item?id=28143821)：

> 最可气的地方在于他们的客服团队一上午都在 Twitter 上误导别人，而不是老实回答新版是不是 Electron \[写的\]，\[说什么 「[还是原生的](https://twitter.com/1Password/status/1425429965747720200)」「[后端是用 Rust 写的](https://twitter.com/1Password/status/1425429965747720200)」「[更快更灵敏](https://twitter.com/1Password/status/1425470169133031435)」。\]

用户「kup0」则[表示](https://news.ycombinator.com/item?id=28148070)：

> 号称「顾客用钱包投票」选择了订阅制是很虚伪的。\[…\] 作为软硬件用户，我情绪上真的很烦老是遇到这样的反衬：喜欢一个产品、却对做产品的公司极度失望。

## 支持观点

尽管质疑声音颇多，也有不少一些观点则对 1Password 表达了支持，或至少表示理解。

一些人指出，**对 Electron「膝跳反应」式的批评是非理性的**。较有代表性的是开发者 Thaddeus Ternes 的[推文串](https://twitter.com/thaddeus/status/1427005912842133512)：

> UI \[用户界面\] 工具的决策和开发时间是一大商业风险。在 Apple 平台上，新工具的功能几乎从不会向后移植到旧版。选择支持旧版操作系统，就要放弃 \[新的\] 平台功能。相反，如果选择新工具，目标受众就很有限，每年增增减减的意外 \[功能\] 变动也只能由你承担。

> 但如果选择 Electron，就能 \[兼顾\] 支持旧版的系统和现代的功能，功能支持和排期也有清晰的路线图。Electron 实际上是一种降低开发风险的方式（有的服务商过去几十年就是靠帮人降低开发风险赚了大钱）。甚至可以说 Apple 的保密就是在强迫别的公司去用 Electron。

> 我本身并不很喜欢 Electron，但考虑到做软件生意的各种内在挑战，如果能不花钱就将风险转移出去，那是很有吸引力的。

另一些观点指出，1Password 弃用原生框架而转采 Electron 的决策中，**Apple 作为第一方、怠于提供良好的开发框架，也有一部分责任**。Jason Snell [撰文指出](https://sixcolors.com/post/2021/08/not-important-enough-1password-abandons-its-native-mac-app/)：

> 问题的根源在于：1Password 是以「亲 Mac 阵营开发者」的身份起家的，现在却认定 Mac 不够重要了。\[官方博客文章\] 很清楚地表明了 AgileBits 的优先级。\[…\] AgileBits 愿意在 iOS 上多花功夫 \[使用 SwiftUI 开发\]，因为这是个重要的平台，而 SwiftUI 显然是它的未来。但在 Mac 上实现 SwiftUI 就要做很多重复工作了。\[…\] \[他们博客文章等于在说，\] Mac 很重要，但没有重要到让我们做一个专属应用。这道出了 Mac 软件未来之痛。

> Apple 也难避其咎。如果 SwiftUI 真的是一统 Apple 各平台的钦定工具，那 1Password 就会用上了。\[…\] 一个历史悠久、受人喜爱的 Mac 应用被扔进废纸篓，被一个网页应用取而代之。这事不是没有先例；不幸的是，也不会后无来者。

还有人认为，**并不存在一种一以贯之的「原生 Mac 应用设计」**（有时被称为「不妥协的 Mac 应用」，[“Mac-assed” Mac app](https://daringfireball.net/linked/2020/03/20/mac-assed-mac-apps)），以此来要求和批评 1Password 是不合适的。

例如，设计师 Matt Birchler [撰文指出](https://birchtree.me/blog/desktop-apps-aint-what-they-used-to-be/)：

> \[Things、Reeder、iStat Menus 和 Craft\] 都是优秀的原生 Mac 应用，但它们用的定制 UI 元素可谓五花八门。

> 1Password 7 的 UI 哪部分是遵循 Mac 惯例或与系统内置 UI 元素相同的？\[…\] 与新版相比怎么就更像一个原生 Mac 应用了呢？

> 当今世界上，大多数人都在浏览器中完成大量工作，没有明确理由就不会另装一个应用；因此，Mac 上的原生与非原生应用之争，更多是一种学究而非务实。诚然，Electron 应用可能很差，但你在弃坑之前总得实际用用，知道它差在哪。同理，一个原生应用也未必就快速、轻量、可靠……macOS 版的「音乐」应用就是一例。

![](https://cdn.sspai.com/2021/09/19/article/ba59cd4d0eb67fa8504774972a196b2e)

其他一些辩护角度还包括：

- Casey Liss 在播客 [Accidental Tech Podcast](https://atp.fm/444) 中认为，**选用 Electron 的影响要结合应用的使用场景判断**。以 1Password 为例，除了初始设置时需要多花些时间整理和导入密码，此后需要与界面打交道的机会并不多（某种程度上说，1Password 的价值和目标，正是让用户花在「查密码」这件事上的时间尽可能短暂）。因此，界面是不是原生对于用户体验的影响就很有限了。
- Stephen Hackett 在播客 [Connected](https://www.relay.fm/connected/359) 中提出，1Password **提高对企业用户的重视程度是商业上合理的选择**。随着各大操作系统、浏览器纷纷推出和完善密码管理功能，可以预见将有越来越多的普通用户选择这些现成方案，导致 1Password 的市场机会受到蚕食。因此，转向企业市场是必要的。

## 相关事件/延伸阅读

**用 Electron 框架制作出原生质感的应用并非天方夜谭。** GitHub 通知管理工具 Lotus 的开发者[讨论](https://getlotus.app/21-making-electron-apps-feel-native-on-mac)了如何从窗口加载、标题栏可拖拽区域、字体选用、鼠标指针、菜单设置等细节入手，让 Electron 尽可能贴近原生效果。

![](https://cdn.sspai.com/2021/09/19/article/f89a2a5b991a7040da1d508caa840b37)

**1Password 并不是第一个因转向 Electron 和订阅制而被受到质疑的 Mac 应用。** 2020 年 4 月，另一款颇具口碑的老牌备份工具 Arq [宣布推出第 6 版](https://www.arqbackup.com/blog/arq-6-more-power-more-security-more-storage-savings/)，同样采用 Electron 编写界面部分（后台进程则继续使用 Objective-C），并取消了部分用户惯用的旧版功能。

![](https://cdn.sspai.com/2021/09/19/article/df21d2b051c67cc2b276d3e924d91587)

在收到大量负面评价后，开发者在几天后即[出面道歉](https://www.arqbackup.com/blog/arq-6-next-steps/)，宣布将逐渐加回缺失的功能。不到一年后的 2021 年 2 月，下一个大版本 [Arq 7](https://www.arqbackup.com/blog/arq-7-released/) 完全放弃了 Electron，重新用回了原生框架编写界面。
