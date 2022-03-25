---
title: "Mac 的内置硬盘「作弊」了吗？"
date: 2022-03-11
tags:
  - "macOS"
  - "explainer"
---

**Note:** This article was published as a member-exclusive post for [SSPAI Prime](https://sspai.com/prime), in three installments (part [I](https://sspai.com/prime/story/mac-ssd-cheating-1), [II](https://sspai.com/prime/story/mac-ssd-cheating-2), and [III](https://sspai.com/prime/story/mac-ssd-cheating-3)), of which the first was made freely available as a preview and republished here. Please consider subscribing to SSPAI Prime if you find content like this helpful. Thanks for your support.

## 一

Mac 的固态硬盘性能一直是苹果宣传的重点。特别是近年 Apple T2、M1 等自研芯片整合了主控芯片后，Mac 内置固态硬盘相比竞品的性能优势似乎越发明显。在这样的背景下，如果有人站出来说「Mac 的固态硬盘速度有作弊之嫌」，想必会引起不少关注和争议。上个月，这样的讨论确实发生了。

Mac 的固态硬盘性能一直是苹果宣传的重点。特别是近年 Apple T2、M1 等自研芯片整合了主控芯片后，Mac 内置固态硬盘相比竞品的性能优势似乎越发明显。在这样的背景下，如果有人站出来说「Mac 的固态硬盘速度有作弊之嫌」，想必会引起不少关注和争议。

![](https://cdn.sspai.com/2022/03/11/6a1f576e25db42b637e0d89e5e84adf8.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

Mac 一直致力于宣传内置 SSD 的高性能（来源：苹果）

上个月，这样的讨论确实发生了。

打开话匣的是 [Hector Martin](https://twitter.com/marcan42)。先介绍一点背景：此君绝非哗众取宠的无名群众，而是一位资深的信息安全顾问和 Linux 研究者，曾因将 Linux 系统 [移植到 PS4 上](https://www.youtube.com/watch?v=QMiubC6LdTA) 而出名。去年以来，Martin 又将目光投向了 [Asahi Linux](https://asahilinux.org/about/)，这是一个旨在让 ARM 架构 Mac 运行 Linux 系统的开源项目，目前进展颇多，已接近发布公测版。能主导这样一个高难度项目，Martin 关于 Mac 的观点自然会引起社区的重视。

在 2 月中旬的一串 [推文](https://twitter.com/marcan42/status/1494213855387734019) 中，Martin 就提出了一项争议很大的主张：**苹果的定制硬盘确实快得出奇，但却是以牺牲数据一致性（data integrity）为代价的。**

这件事的背景是，Martin 在一台 M1 版 MacBook Air 上测试 Linux 系统时，发现很多写入操作慢的出奇，与类似操作在 macOS 下的速度完全不可同日而语。为了找出问题根源，他测试了苹果内置硬盘和其他两款常见固态硬盘的读写性能。

结果非常耐人寻味：

| 硬盘型号 | 仅写入 | 写入并冲刷缓冲 |
| --- | --- | --- |
| 内置硬盘 | 40,000 IOPS | 46 IOPS |
| 西部数据 SN550 NVMe | 20,000 IOPS | 2,000 IOPS |
| 三星 860 EVO SATA | 5,000 IOPS | 143 IOPS |

换言之，在「仅写入」的测试中，苹果内置固态硬盘可以达到 4 万次的 IOPS（每秒读写次数），这是主流第三方 NVMe 固态硬盘的 2 倍、SATA 固态硬盘的 8 倍。

但到了「写入并冲刷缓冲」的场景，内置硬盘仅仅取得了 46 IOPS 的「好成绩」，相当于第三方 NVMe 固态硬盘的 2.3%、SATA 固态硬盘的 32.2%，还不如很多机械硬盘。

怎样理解 Martin 前后两次测试的区别和意义呢？

我们知道，**现代计算机中最主要的性能瓶颈就是存储。**因此，软硬件设计中普遍采用**多级缓存**的设计来改善性能。就写入数据这一场景而言，待写入的数据至少要经过系统缓存（OS cache）、磁盘缓冲区（disk buffer）这两道中间环节，才能最终进入永久存储（permanent storage）——机械硬盘的盘片或固态硬盘的闪存颗粒。

![](https://cdn.sspai.com/2022/03/11/a254575f07cfbaca69d4303e30cdab90.PNG?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

macOS 中的多级缓存（来源：WWDC 2019 演示文稿）

借用送快递来打比方，这就好比一个快件要经过区域分站、小区驿站等中转节点，才能最终送到你手上。

通常情况下，发件方（写入数据的应用程序）并不关心这些底层的区别；它们只是把快件（写入的数据）交给快递公司（操作系统），至于送达方式、成功与否全凭后者的反馈。而为了提高处理效率，操作系统的常见做法是只要快递送到了驿站（数据写进了缓冲区），就反馈说送达成功（写入完成）。至于最后一步「送货上门」（写入永久存储，中文讨论中也常称为「落盘」），则是由操作系统在之后再根据自己的节奏完成——但这已经不受应用程序控制了。

诚然，从日常使用角度而言，前一项数据是用户直接感知的「写入性能」，Mac 内置硬盘也确实有亮眼表现。但一旦发生断电等故障，那些还滞留在驿站的快件（缓冲区未落盘的数据）就有丢失的风险。

此外，快件从驿站派送上门的顺序，往往不同于到达驿站的顺序；派件员（硬盘主控）可能为了省时省事等目的将其重新排列组合。这在平时也无妨，但对于数据库日志、文件系统日志等特殊场合，常常要求关于一项操作的记录必须**先于**这项操作本身落盘（好比从银行存取现金，一定是先记账、再动钱）。这些预写日志（write-ahead log，WAL）会被打上称为「[写入屏障](https://docs.fedoraproject.org//en-US/Fedora/14/html/Storage_Administration_Guide/writebarr.html)」（write barrier）的标签，享受「优先派送」的待遇，它的落盘效率直接影响到后续操作何时能进行。

因此，如果说 Martin 测试的前一项数据代表了数据**日常写入**的效率，那么后一项数据则代表了数据**落袋为安**的效率，同样不能忽视。而正是在这项性能上，Mac 发生了翻车。

不仅如此，Martin 还宣称**发现了 macOS 的一项「作弊」行为。**

在测试落盘性能时，他最初使用了 [POSIX](https://en.wikipedia.org/wiki/POSIX) 标准定义的 `fsync()` 系统调用。POSIX 是一套旨在促进操作系统相互兼容的接口标准，Linux 是在 POSIX 标准的指导下开发的（尽管并未完全遵循），而 macOS 更是通过了其 [认证](https://www.opengroup.org/openbrand/register/apple.htm)。因此按理说，两个系统执行 `fsync()` 的结果应该是一致的，也就是像标准所 [规定](https://pubs.opengroup.org/onlinepubs/9699919799/functions/fsync.html) 的那样，「强制对缓冲中的数据执行物理写入，并确保系统崩溃等错误后，截至调用前的所有数据均已录入磁盘」。

实际情况并非如此。Martin 发现，Linux 的确执行了 `fsync()` 所附加的冲刷缓冲动作，测出的写入效率也比不冲刷缓冲时相应降低。但如果在一台 MacBook Air 上用 `fsync()` 写入数据，五秒之后通过 PD 协议发去一条强制重启指令，这些理论上应该落盘的数据还是会丢失。他又换了一台 Mac mini，用 `fsync()` 写入数据五秒之后直接拔了插头，同样出现了丢数据的情况。

这种现象只有一种可能原因，那就是 **macOS「无视」了** `**fsync()**` **所附加的落盘要求。**

的确，如果你在 macOS 下查阅 `fsync()` 的手册页面（可以在终端执行 `man fsync` 查阅）中，就能看到这样一段说明：

> 注意，尽管 `fsync()` 将所有数据从宿主冲刷到驱动器（即「永久存储设备」），该驱动器自身可能**在相当长的时间内都并不会将数据在物理意义上写入盘片**，并且可能不依先后顺序写入。具体而言，如果驱动器断电、操作系统崩溃，应用程序的数据**可能只被部分写入，或完全没有写入**。磁盘还可能重新排序数据，导致**后来的写入还存在，而早先的写入则丢失。**  
> 这并不只是理论上的罕见场景，而是很容易在现实工作的负荷或驱动器断电故障中复现。  
> 对于要求保证更高数据完整性的应用程序，Mac OS X 提供了 `F_FULLFSYNC` 这一 `fcntl` 命令。`F_FULLFSYNC` 要求驱动器冲刷所有缓冲区数据，写入永久存储。  
> \[ 节选翻译；粗体均为笔者所加 \]

换言之，在 macOS 下， `fsync()` 并不会冲刷缓冲区。要实现与 Linux 下相同的效果，应该使用另一个函数 `fcntl()`，并附加 `F_FULLFSYNC` 作为命令参数。

事实上，促使 Martin 开展这项测试的疑问——内置硬盘在 macOS 和 Linux 下性能差距巨大，其原因正在于此。如果对于同一项操作，Linux 因为 `fsync()` 的要求「送货上门」，而 macOS 却耍滑头地送到驿站就点了送达，那么两者的效率当然不能同日而语。

Martin 由此得出的观点是：如果一直「岁月静好」，Mac 内置硬盘确实速度令人望其项背。但一旦发生断电的意外事故，它就比第三方硬盘有更大风险遭遇数据丢失，对于没有电池作为后备供电的桌面型 Mac 就更是如此。

显然，Martin 的观点不可能不在社区引起热议。截至本文写作时，他的推文已经获得了近 1800 次转发，5900 多次点赞；在 [Hacker News](https://news.ycombinator.com/item?id=30370551) 和 [Reddit](https://old.reddit.com/r/apple/comments/sun6pa/apples_custom_nvme_drives_are_amazingly_fast_if/) 上的讨论帖也堆到了数百层高。这些讨论中，社区用户从不同角度对 Martin 提出了补充和质疑观点。

---

那么，Martin 说得有道理吗？与 Linux 相比，macOS 真的是一个不那么负责任的「快递公司」吗？这将是本文 [下一部分](https://sspai.com/prime/story/mac-ssd-cheating-2) 的主题。
