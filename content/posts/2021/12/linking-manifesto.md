---
title: "让链接无处不在——《泛在链接宣言》的理论与理想"
date: "2021-12-29"
categories: 
---

## **引言**

11 月底，一则 [「微信更新外链规则」](https://www.thepaper.cn/newsDetail_forward_15603756) 的新闻在国内引发了不小的涟漪。在《关于〈微信外部链接内容管理规范〉的更新说明》中，微信宣布，将在点对点聊天中允许直接访问外部链接，而在群聊中试行允许直接访问电商类链接。

尽管这条新闻细读之下有些讽刺——本意促进互联互通的链接，竟然要受制于一个平台的生杀予夺，而微信的调整也有点不情不愿、半遮半掩，但这总算是往健康、开放的方向迈了一步。

**而同一时间，国外也有一群人在为「链接」的未来发出呼吁。**不过，他们想得要更远一些。

12 月初，一份名为 [《泛在链接宣言》](https://linkingmanifesto.org/)（_Manifesto for Ubiquitous Linking_）的文档出现在互联网上。简而言之，这份《宣言》向开发者呼吁：通过调整界面设计、提供 API 等方式，**让用户能方便地通过链接访问应用内资源，从而提高工作效率、维持专注。**

![](https://cdn.sspai.com/2021/12/29/article/d43af54570963e0bb3af471d7371ad61?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

打个比方，如果你在笔记里写了一句「参见周一的**会议记录**」，那么应该能给「会议记录」四个字加上链接，点击后就能直接打开当时做记录的 Word 文档；在任务清单里写了一条「阅读某篇**论文**」，应该可以把「论文」链接到想要看的那份 PDF 文件。更理想地，你应该还能在上述 Word 或 PDF 文件中加一个**反方向的链接**，点击即可直接打开提到了它们的笔记或清单，方便继续写作、标记任务完成等。

![](https://cdn.sspai.com/2021/12/29/article/4aba7e383c3caecff41eed0c2fedaf2e?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

如果你对近年红得发紫的「双向链接」笔记有所耳闻，应该会觉得上面的描述看着挺眼熟——这差不多就是将笔记场景中的双向链接**推广和化用到了系统的各个角落**。

确实，这些效果本来也不是什么「黑科技」，目前都能在某种程度上实现，只是远不够完美：要么依赖于应用和平台的特殊支持，但老死不相往来；要么薄如蝉翼，容易随着文件移动、设备更换而失效；要么晦涩难用，让普通用户一看就打消了学习的念头。

《泛在链接宣言》所呼吁的，正是让这种灵活的链接用法变得更**通用、开放、稳固和易用**。

## **从认知理论到软件设计**

那么，这份宣言的背后都是何许人也，他们又为何要为这种「泛在链接」的未来而奔走呢？

《宣言》的 [发起人](https://linkingmanifesto.org/about-the-originators/) 和最初联署者是二十几名软件的开发者、学者和有影响力的专业用户。对于国内读者而言，其中大多数名字或许都显得有点陌生；但如果提到他们的作品——DEVONthink、OmniFocus、BBEdit、PDFpen 这些持续开发十几年甚至几十年的知名软件，这个阵容就显得「群星荟萃」了。

这其中，起到组织者和联系人作用的是 [Luc P. Beaudoin](https://cogzest.com/about/founder/) 博士，他是一位身兼学术和行业背景的开发者。

学术方面，Beaudoin 持有认知科学 Ph.D. 学位，在加拿大西蒙菲莎大学（Simon Fraser University）担任认知科学和教育学的兼职教授。他的主要研究兴趣是「认知效率」（cognitive productivity），即利用知识解决问题、创造产出和提高自我的效率和效果。他认为，对于效率的讨论不应局限于技术，还应当引入动机、情绪和自我调节等心理学的方法和概念。

实务方面，Beaudoin 有多年的软件开发从业经历，曾与《宣言》的另外两名发起人一起设计认知辅助软件近十年。在此过程中，他们借鉴了教育心理学的理论，并很早就意识到，**应当允许学习者为任意信息创建双向链接**。后来，他将这一理念从学习场景泛化到一般用途，开发了 macOS 应用 [Hook](https://hookproductivity.com/)，其主要功能就是帮助用户在各类应用内资源之间创建和管理双向链接。（Hook 的用法可以参阅少数派上的 [介绍](https://sspai.com/post/68344)。）

![](https://cdn.sspai.com/2021/12/29/article/3257fe20a929da4f365975a8f62d6b5e?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

Hook 应用

有这样的背景做铺垫，也就不难理解为什么《宣言》读来颇有些学院风，而且在 [「动机」](https://linkingmanifesto.org/motivation/) 一节大量引用认知科学的理论了。

认知科学如何为提倡链接提供依据呢？你一定听说或经历过这样的「悲剧」：外出游玩，满心期待地踏上旅途，但却被漫长而坎坷的交通消磨了兴致；等终于到达目的地，已经精疲力竭、无心游玩了。

在使用电脑工作时，我们也常常会遇到类似的问题。为了打开需要查阅的信息，一般做法是在文件夹、收藏夹里手动翻找；或者稍微「高级」一点，用搜索功能定位。但无论浏览还是搜索，都是为了访问信息要做的额外工作，也因此都是横亘在我们与目标之间的阻碍。且不提时间的消耗，每多打开一个应用、多点开一层文件夹，受到干扰、以至遗忘最初目标的可能性就高了一分；如果大费周章后仍然求而不得，那种焦灼和愤懑更会直接影响工作状态。

从心理学的角度看，这是因为**人的心智容量（mental capacity）——包括记忆力和注意力——是有限的**。例如有 [研究](https://en.wikipedia.org/wiki/The_Magical_Number_Seven,*Plus_or_Minus_Two#The*%22magical_number_7%22_and_working_memory_capacity) 认为，年轻人的工作记忆只能容纳 7 个数字、6 个字母或 5 个单词。在电子设备上查找信息看似简单轻松，但实际上需要身体和思维的多步参与，都会消耗有限的心智容量并导致疲劳。

另一种流行的理论认为，存在一种理想的「心流」（flow）状态——文艺点说就是「忘我」或「神驰」：人完全沉浸于当前的活动中，高效而不假思索，暂时隔绝了对时间、外物和生理的感知，且感到愉悦和满足。而要达到和维持这种心流状态，除了技术娴熟等主观条件，也需要尽量减少外部干扰和「打乱节奏」的行为——例如从写作切换到检索，以避免占用大脑有限的处理能力。

如何解决这个问题呢？正如哆啦 A 梦的「任意门」能免去舟车劳顿、直达目的地；如果可以**直接定位到脑中所想的内容**，就能回避时间和注意力的无谓消耗。

我们习以为常的超链接就可以起到这种「任意门」的功能。

## **承互联网未竟之志**

尽管在大多数人印象中，「超链接」（hyperlink）就是「网址」的同义词，链接的另一头就是一个网页；但实际上，**超链接的触角所及远超出万维网的范围，可以指向任何可识别的资源**——无论其位于远程还是本机、存放在网页上还是应用内、性质是开放还是私有、形态是数字还是实体。

从技术角度看，链接的现代定义见于标准组织 IETF（互联网工程任务组）的《统一资源识别符（URI）：标准语法》（[RFC 3986](https://datatracker.ietf.org/doc/html/rfc3986#section-1.1)）。根据该标准，URI 是「识别抽象或实体资源的简洁文本序列」；URL（网址）则是 URI 的形式之一。一个通用的 URI 格式是：

```
[协议名]://[用户名]:[密码]@[主机名]:[端口]/[路径]?[查询参数]#[片段 ID]
```

用这种格式，我们可以给电脑上任何应用内的任何资源编排一个地址。例如：

- 硬盘「下载」文件夹里的一个 PDF 文件：`file:///Users/JohnAppleseed/Downloads/helloworld.pdf`
- 「备忘录」应用里的一条记事：`notes://shownote?identifier=56049685-cb9c-54f0-a717-63afea0f3cc9`
- 「邮件」应用里的一封电子邮件：`message://<24873dbedad041118a3cf0b5f47cd6f0.20211231124933@no-reply.example.com>`

当一个链接不只是简单地打开一个网站、启动一个应用，而是直指网页、应用内部的特定内容时，这样的链接就成为了**「深度链接」**（deep link）。将深度链接恰当放置在需要来回参考跳转的位置上，它就可以充当理想中的那扇「任意门」。

值得一提的是，尽管深度链接随着移动应用的普及才大规模应用，并因笔记软件的兴起为更多人所关注，但本身并非一个晚近才有的技术，而是**早已存在于互联网先驱的设想中**。

1939 年，曼哈顿计划的主要推动者、美国工程师 Vannevar Bush 构想过一种用缩微胶卷储存资料的 [「记忆扩展机」](https://en.wikipedia.org/wiki/Memex)（Memex）。在这台形如办公桌的资料阅读和检索装置中，用户可以通过为不同材料输入编码来建立链接——称为「联想踪迹」（associative trail）。通过串联起材料和注释的踪迹，Memex 相当于帮助用户把材料「装订成一本新书」。

![](https://cdn.sspai.com/2021/12/29/article/a7f557c298bb5445584dc98327326db5?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

Memex 设想图

60 年代，人机交互先驱 Douglas Engelbart 设计的 [NLS](https://en.wikipedia.org/wiki/NLS_(computer_system)) 中，超链接的雏形就已经出现，并且可以指向包括文本、资源、注释在内的各类信息。90 年代，到了「超文本」概念提出者 Ted Nelson 设想的 [「上都计划」](https://en.wikipedia.org/wiki/Project_Xanadu)（Project Xanadu）中，任何文本的任何部分都可以并排显示、对比、建立双向链接。

![](https://cdn.sspai.com/2021/12/29/article/591f76dbeca2674beb8a1aca9b64e36d?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

因此，深度链接与其说是一种技术创新，不如说是互联网早期技术理想的落地实施。

**然而，问题到这里只解决了一半。**上述设想和标准的共同问题在于，它们只提出了一种「可能性」；但落到实际使用中，**深度链接能否被创建和触发，都依赖于具体软件的支持**。

如果一个软件从设计上就没有清晰的数据结构，那就像一座缺乏道路和区域规划的城市，很难为其中的建筑物——软件中的信息资源——编制出有逻辑、有规律的地址。如果厂商没有开放的态度和意识，软件就会成为围墙高筑的私家花园，要么根本不对外公开内部构造和联系方式，要么只对自己人开放，而让「慕名而来」的访客吃闭门羹。

这并不是一个容易解决的问题。历史上，Memex、NLS 和 Project Xanadu 先后折戟，共同原因都是曲高和寡、未成气候。近年来，开发者和用户社区也做过类似尝试。例如在 2011 年，iOS 笔记应用 Drafts 的开发者就主持编写过 [x-callback-url](http://x-callback-url.com/) 规范；支持这种规范的应用可以用一套标准的链接语法相互调用和传递信息。同样地，这些规范获得了一定规模的支持，但总体看还是偏向小众，远称不上普及。

![](https://cdn.sspai.com/2021/12/29/article/1c569acde8ce527da8bc380d2976e384?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

因此，即使现阶段其实已经可以通过手动方式获得不少应用的深度链接，但其麻烦程度足以打消大多数用户付诸实践的念头。**如果把大量时间花费在探索获得链接的方法上，用链接提高效率也就无从谈起了。**

实际上，对于《宣言》首倡者 Beaudoin 在开发的 Hook 应用而言，其主要价值主张正是能帮助用户相对轻松地抓取深度链接。为此，开发过程中，他们花了很大精力与 [链接支持情况五花八门的应用](https://hookproductivity.com/what-mac-apps-are-compatible-with-hook-app)「搏斗」。对于不支持生成资源链接的应用，Hook 试图用自动化脚本、甚至模拟用户操作的方式，硬把链接从它们的缄默尊口里抠出来。

例如，PDF Expert 没有提供任何自动化的能力，Hook 就自动帮用户点击其菜单中的的「在 Finder 中显示」，然后从 Finder 中复制路径，这才能获得当前阅读的 PDF 文件链接。类似地，为了生成 Notion 的链接，Hook 只能通过模拟按下其「复制链接」的快捷键（Command + L）来实现。

因此，**《宣言》想要实现的，正是让创建资源链接这项功能被更多软件厂商自发支持。**为此，它在 [「技术要求」](https://linkingmanifesto.org/technical-requirements/) 一节提出了一系列具体的倡议：

- 第 1—2 条对**创建链接的能力**提出总体要求：软件能链接到不应该只是一个笼统的对象（例如写作软件中的整篇文档或任务管理软件中的整个项目），而且**应该能链接到其内部的节点或区域**（例如文档某一页或者选中的某段话、项目中的任务和子任务）。
- 第 3—5 条规定了**什么是「好」的链接**，分别要求链接是**稳固、可读和易用的**：链接应该在移动、重命名之后仍然保持有效；链接中的各部分应该清晰可辨，便于理解和选择；生成和访问链接应该「像复制粘贴那样简单易用」。
- 第 6—8 条对于**生成链接的机制**提出了要求：软件应该提供获取和打开资源链接的接口（API）；对于那些既有网页版也有原生应用的服务，则应该允许在网页版链接和应用深度链接之间相互转换，或者使用 [通用链接](https://developer.apple.com/ios/universal-links/) 这类技术将两者合二为一。

值得一提的是，《宣言》的技术要求尽管细致，但也不失「分寸」。与常见的技术规范、技术文档相比，它「不要求使用特定的 API，使用特定的的编程语言或技术」，也「不要求使用符合 RFC-3986 标准的链接」。

这种做法似乎很「佛系」，但在我看来是一种必要的妥协：这样一来，开发者就不用对现有的技术架构伤筋动骨，也可以灵活决定链接格式、API 的开放程度。这保证了开放和自利之间的平衡，更有利于吸引开发者加入。

## **链接的未来有多远？**

理想很丰满，但不容忽视的事实是，**原本作为互联网象征的链接，如今境遇可谓备受冷落、四面楚歌。**科技大厂为了「肥水不流外人田」，对链接极尽混淆（请尝试解读任意一篇微信文章的网址）和阻断（请再读一遍本文第一段）之能事；随着用户对链接的认识越发淡化，很多浏览器也顺水推舟，干脆不再在地址栏显示完整链接。

我为此专门请教了 Beaudoin：链接对于用户的益处固然是没什么争议的，但在这样的大环境下，拥抱链接功能对开发者的好处是什么呢？他们有什么动机去花功夫实现《宣言》的技术要求呢？

对此，Beaudoin 持乐观态度。他表示，「优秀的软件开发者必然想要开发优秀的软件」，而链接能力是优秀软件的必备特质。那种「围墙花园」式的开发思路是「自大」的，不存在绝对的光荣孤立、自给自足。Beaudoin 还希望，随着《宣言》的推广，能有更多用户意识到链接的意义和价值，从而反向促使开发者更好地支持链接。

**多元化也是需要解决的问题。**查阅《宣言》发起人的背景，不难发现清一色都是 Apple 生态中的开发者。这是有意为之的选择吗？有没有考虑过在其他平台上实现《宣言》的前景？

Beaudoin 将这种「扎堆」的原因归结为社区和技术两方面。他说，macOS 是一个对独立开发者颇具吸引力的平台。开发者通过博客、播客、邮件通讯等渠道，和用户形成了紧密的互动，双方对于 Mac 软硬件都有较高忠实度。技术上，经典的 AppleScript 内置在系统中，多年来一脉相承，加上 x-callback-url、快捷指令等自动化框架，让 macOS 平台上的跨应用协作相对便捷。

相比之下，Windows 平台规模更大，但社区也相对松散，缺少一个连贯的、系统内置的自动化框架。尽管实现链接功能在技术上是可行的，但开发者从文化和收益角度都没有足够的动力。Beaudoin 认为，要化解这一问题，还需要微软作为第一方有更多担当。

Beaudoin 的解释与我的理解基本一致。实际上，**Windows（以及回答中未提到的 Android）都支持深度链接机制**，本就可以直接执行一些跨平台应用的深度链接。

例如，Windows 平台支持 [URI scheme](https://docs.microsoft.com/en-us/windows/uwp/app-resources/uri-schemes)。通过访问形如 `ms-appx:` 前缀的链接，可以控制应用打开特定资源或者执行特定操作。类似地，Android 平台上，[深度链接](https://developer.android.com/training/app-links/deep-linking) 可以直接跳转到应用内部的 Activity（可以粗略理解为特定界面）。不过，之所以对于深度链接的应用和讨论明显少于 Apple 平台，除了 Beaudoin 提到的文化和收益因素，可能也是由于这两个平台上的应用跳转和唤醒机制选择很多。

![](https://cdn.sspai.com/2021/12/29/article/79b19a78c35b0c4d6e92754056a4f1ee?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

Windows 和 Android 上访问深度链接的效果

最后，**安全和隐私问题也值得关注。**当《宣言》的报道在 TidBITS 和 Hacker News 等社区上帖出后，一些用户在表达兴趣的同时，也对潜在的隐私泄露、越权访问等隐患提出了担忧。这种担心是否多余呢？

对此，Beaudoin 指出**「创建链接」和「访问数据」是两个不同层次的操作**；《宣言》关注的只是创建链接，而从链接访问到数据这一步，则可以通过被链接应用和用户的权限设置加以控制。

例如，即使掌握了一封他人邮件的链接，如果这封邮件从来没有进入过自己控制的账户，那再怎么点击也定位不到原文；即使拿到一个云端资源的链接，如果不知道正确的账号密码，那连登录这关都无法通过。此外，操作系统内置的隐私保护和权限控制也能起到额外的保护作用。例如，macOS 已经在点击指向其他应用的 URL Scheme 时要求用户确认；沙盒机制将不同应用的数据严格区分，等等。

## **结语**

《泛在链接宣言》是一个值得尊敬的项目。一方面，它以互联网早期设想和学术理论为基础，反映出一种理想主义的思索；另一方面，它的具体主张也体现了务实、谦抑的态度，具有可操作性和灵活度。

从技术上看，《宣言》所选择的载体——链接并不高深，与其他能实现类似效果的途径相比，甚至可谓简陋。但在我看来，这反而是一种优势：普通用户即使对深度链接一无所知，也能根据对网址的朴素认知，大致推断其含义和作用；链接在各种系统中都能获得支持，开发者实现起来也只需考虑好链接格式，而无需担心平台专属功能的限制；纯文本的形态，也让链接的存储和传输方便而低廉。

因此，**我赞同《宣言》的主张，并衷心希望它能得到更多的关注和参与。**正如 Hacker News 上一位用户的 [评论](https://news.ycombinator.com/item?id=29610247) 所说：

> 我希望这不只是「良心」技术专家自我觉醒和相互推动的孤勇，而是由社会参与的抗争。应该认识到，在封闭系统中秘密完成的工作并没有贡献价值；也应该相信，对于浏览线上信息系统时所见，社会有权评论、检查、讨论、分享、链接、引用、交流。互联互通的信息理应是广义上的互联网工作的一部分。如果从这种状态脱离而成为零落孤岛，是减损自身价值的，也是有损于社会、阻抑社会联系的。

《链接宣言》是一份开放签署的文件。任何人都可以在其网站上留言 [签署](https://linkingmanifesto.org/sign-the-manifesto/)，表达自己的支持。

**当然，比起简单的振臂一呼，更重要的是付诸实践。**如果你是软件开发者，那么最好的支持和参与方式莫过于在自己的作品中践行《宣言》的倡议，或者根据自己的经验为它的修订完善建言献策。

如果你是一般用户，那么不妨多做相关尝试，例如在日常工作中用链接代替临时的翻找，有意识地标记和整理主题相关的信息；在同类软件中做选择时，多关注它们对链接功能的支持程度，优先选择那些支持创建和解析通用链接的产品。抛开对《宣言》主张的支持不谈，仅仅对于提升个人效率而言，这也是很多资深用户普遍推荐、真实有效的心得技巧。

愿链接的未来长青。

* * *

## 附录：《泛在链接宣言》部分翻译

**注：**如下翻译由本文作者经宣言组织者 Luc P. Beaudoin 许可后完成并发布，仅供参考。宣言 [发起人](https://linkingmanifesto.org/about-the-originators) 保留对原文文本的权利。时间所限，宣言网站的附属材料（如 [动机](https://linkingmanifesto.org/motivation/)、[历史](https://linkingmanifesto.org/about/)、[发起人介绍](https://linkingmanifesto.org/about-the-originators/) 等）未及全部翻译，有兴趣的读者可前往参阅原文。

### 宣言正文

[原文链接](https://linkingmanifesto.org/)

我们承认，大量有用信息可以通过数字方式获得，且将其连接起来可以获得巨大价值。互联的知识能使人创造出色的产品、解决重要问题，并提升自我。

我们亦承认，人在心流状态下工作效果最佳。任何情境切换，即使只是搜索信息，都会干扰心流，同时消耗宝贵的心智容量（mental capacity）、脑力和时间。与其搜索信息，不如触发妥当放置的信息链接，这更为简单快捷，亦更利于维持心流。

我们肯认，为促进认知效率，复制资源链接是与复制其他类型信息——包括所有非暂时性的数字信息——同等重要的功能。

我们邀请软件开发者通过下列方式尽一己之力：

1. 确保用户可以通过用户界面，便捷获得当前打开或选定的资源链接；及
2. 提供应用编程接口（API），以获取或构建指向该等资源的链接（即获取其地址和名称）。

为帮助人们受益于经软件处理的信息，我们倡导对信息资源的链接提供广泛支持。这将有助于实现 Ted Nelson 和 Douglas Englebart 等信息技术先驱所设想的「超媒体」（hypermedia）的潜力。

### 技术要求

[原文链接](https://linkingmanifesto.org/technical-requirements/)

本文档规定了为满足「泛在链接」所需，软件应达到的技术要求。

链接是对信息资源（数据）的引用，用户可以通过操作链接来访问该等信息资源。链接由资源的地址和名称组成。地址通常采用 [RFC-3986 所述统一资源标识符（URI）的形式](https://datatracker.ietf.org/doc/html/rfc3986)，即 `scheme:[//authority]path[?query]`。Web URI 很常见，但也有定制化、应用专用的 URI。

开发处理信息资源的软件时，开发者应努力：

1. 确保由其软件创建和处理、可被用户访问的资源（无论一个对象或整个文档）均可通过链接识别和访问。
2. 支持识别和访问深层嵌套的选区，例如一段文本范围或多层对象中的节点（如思维导图中的节点、或项目中的任务）。
3. 确保指向信息资源的链接是稳固（robust）的。例如，如果一个资源在分配地址后被重命名或移动，原链接地址应仍可使用。
4. 如果可能，确保顶级（主要）资源（例如文档整体）和该资源内层（次要）的标识符是可区分的，并且有明确文档说明，以便用户选择访问整体资源还是其中嵌套的内容项（如特定锚点、页面和/或字符所在位置）。
5. 复制链接和访问链接资源的用户界面应达到复制和粘贴那样的简单易用程度，并考虑可访问性（accessibility）因素（如提供键盘快捷键并确保菜单项易于访问）。
6. 提供具有下列功能的应用编程接口（API）：
    - 获取链接、地址或其他唯一标识符和名称，指向当前选定或打开的资源以及深层嵌套的选区（如果有）；
    - 通过链接地址打开或显示资源；如提供深层链接，则打开或显示资源中的位置或项目。
7. 如果用户可以通过软件的用户界面创建资源，则同时提供一个 API 用于创建具有用户指定参数（如名称）的资源，该 API 返回的是新创建资源的链接地址。
8. 如果软件创建的资源既可以从浏览器访问，也可以从专用应用访问，则同时公开一种将本地地址转换为 web 地址的方案；这种方案应同时允许将本地 URL 或 ID 转换为 web URL 和反向转换。可以使用 [通用链接（universal links）](https://developer.apple.com/ios/universal-links/) 避免为从 web 和本地访问信息资源分别创建地址。

本宣言不要求使用特定的 API，也不要求使用特定的的编程语言或技术（如 [x-callback-url](http://x-callback-url.com/)）。本宣言不要求 API 使用符合 RFC-3986 的链接（尽管使用这种标准格式可能是有益的）。但本宣言要求开发者公开具有明确文档的 API，以满足广泛链接的上列需求。因此，软件开发者可以用自己选择的技术实现链接机制。
