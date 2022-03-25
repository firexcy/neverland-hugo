---
title: "[Preview] 2022 年，搭配 Zotero 的 WebDAV 存储方案还有什么选择？"
date: 2022-03-21
tags:
  - "academic"
  - "review"
---

**Note:** This article was published as a member-exclusive post for [SSPAI Prime](https://sspai.com/prime), which you may find [here](https://sspai.com/prime/story/webdav-services-compared); the content below is a selected preview thereof. Please consider subscribing to SSPAI Prime if you find content like this helpful. Thanks for your support.

## 引言

近日，Zotero 6 的发布让很多用户重新对这款工具产生了兴趣（参见少数派的 [介绍文章](https://sspai.com/post/72163)）。在相关讨论中，一个常被提起的话题就是怎样解决资料库同步的问题。

的确，Zotero 虽然本身是一个开源项目，但存储服务是额外收费的，并且 [价格](https://www.zotero.org/settings/storage) 很难说是便宜：

| 容量 | 年费 |
| --- | --- |
| 300 MB | 免费 |
| 2GB | $20 |
| 6GB | $60 |
| 无限 | $120 |

其中，300MB 的免费档位放在今天实在是不够看；而各个付费档位即使与国外一线服务相比，也是偏高的；再考虑到付费了也仅限于 Zotero 使用，从性价比角度可以说是毫无竞争力，社区中也只有少数用户本着支持开源项目发展的心态而付费，当作一种捐助。

好在，Zotero 并不是只能通过官方服务来同步，而还一直支持通过 WebDAV 协议同步数据（需桌面和移动端做相应设置，位置见下图，具体步骤参阅 [官方文档](https://www.zotero.org/support/sync#webdav)）。

![](https://cdn.sspai.com/2022/03/22/489c77bed7ce5317e9c565cd32955b99.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

在 Zotero 桌面端和移动端配置 WebDAV 协议同步数据，注意两部分的对应

借助这项功能，用户可以将 Zotero 数据库存储在自己拥有的其他网络位置，从而节约成本。不仅如此，OmniFocus、DEVONthink、2Do 等知名效率工具也支持 WebDAV 同步数据，搭配起来能起到一鱼多吃的效果。

但一个相伴随的问题就是，**从哪里找支持 WebDAV 的服务呢**？答案并不乐观。随着时间推移，支持 WebDAV 协议的网盘服务已经越来越少，而通过家庭 NAS 或 VPS 服务器搭建，对于不少用户又门槛过高。

## 可选方案与挑选原则

值得一提的是，Zotero 的官方文档库中提供了一份由社区维护的 [列表](https://www.zotero.org/support/kb/webdav_services)，列举了经验证可以配合 Zotero 使用的、支持 WebDAV 的存储服务。可惜的是，这份列表上次更新还是一年半之前，其中列举的也都是国外服务，难以保证在国内能顺利访问。

我们认为，从 Zotero 同步文件的使用场景出发，一个合格选择主要应当考虑的因素包括：

- **价格：** 免费午餐当然最好，或者提供价格公允、不超出市场主流定价太多的升级选择。
- **容量：** 考虑到文献主要为占据空间不大的 PDF 格式，平均尺寸以 MB 量级居多，并且多数人会另外选用高容量和廉价的方案存储占空间的文件，因此用来做 Zotero 服务的网盘无需太大，能达到 10GB 对不少人便可谓宽裕。
- **稳定：** 这包含数据安全性和提供服务的稳定性。考虑到 Zotero 中存储的文件大多不是私人文件，而是公开发表的文献，数据安全性的标准可以相对个人资料备份用服务略微放宽（当然，用户自己也应该有冗余备份的意识）。服务的稳定性则主要取决于服务商的口碑和历史。服务时间越久、业务越稳定的服务商越值得信赖；那些名不见经传、动辄低价倾销的服务商，则很可能跑路就在眼前。
- **速度：** 仍然是考虑到文献相对较小的尺寸，这个标准同样可以相对主力数据同步盘放宽。（为了反映这一真实场景，后文的速度测试中，我们用 `curl` 调用 WebDAV 协议，上传三个容量合计约 10MB 的 PDF 文件，统计各个服务完成上传的平均时间；测试环境为非晚高峰时段的广东电信 200M 宽带直连。）

![](https://cdn.sspai.com/2022/03/21/42e8073f4e56a4114ccfd024e4738287.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

基于此，我们逐一考察了上述列表中的服务，排除了那些国内访问不畅、免费空间过小的选择；再补充了一些我们所知的其他选项，得出了一份能反映当前（2022 年初）情况的列表：

| 服务 | 免费空间 | 升级方案 | 速度 | 限制 |
| --- | --- | --- | --- | --- |
| Box | 10GB | 100GB: $120/年 | 较快 | WebDAV 不在技术支持范围内 |
| Koofr | 最多 10GB | 10GB: €5/年  
25GB: €10/年，或 $20/终身  
100GB: €20/年，或 $30/终身 | 一般 | \- |
| Koofr（连接其他网盘） | 取决于连接的服务 | 取决于连接的服务 | 取决于连接的服务 | 免费账号每日限流 1GB |
| TeraCLOUD | 最多 15GB | 300GB: $80/年  
3TB: $120/年 | 快 | \- |
| 坚果云 | 1GB | 42GB: ¥200/年  
96GB: ¥400/年 | 快 | \- |

**简单结论如下：**

- **如果不想付费：**
    - 最稳定可靠、速度也可接受的是 Box 的免费方案；
    - 国内访问速度最快的是 TeraCLOUD 的免费方案；
    - 如果有大容量的 OneDrive 或 Dropbox 账号，则可以首选 Koofr 提供的 WebDAV 中转功能，性价比极高。
- **如果愿意付费：** 坚果云仍然是一个优秀的选择，Koofr 常年销售的廉价终身方案也可以作为备选。

具体介绍和使用方法见下文。

[ Intermediate content is omitted from this preview ]

## 题外话：关于 WebDAV

在涉及网盘的讨论中，支不支持 [WebDAV](http://www.webdav.org/) 协议，经常被用来作为衡量服务商够不够「大方」、心态够不够开放的标准。诚然，在公开标准越发受到挤压，私有协议和臃肿客户端成为主流的市场环境下，能提供 WebDAV 协议是值得鼓励的；但也有必要指出，**不应该因此过于拔高 WebDAV 协议的评价**。

事实上，WebDAV 是主流文件传输协议中较为落后的一种。作为一个诞生于 1996 年的协议，WebDAV 使用语法冗长的 XML 格式传递请求和响应，效率不高、开发起来也不方便。尽管实现了名义上的标准化（IEEE [RFC 4918](https://datatracker.ietf.org/doc/html/rfc4918)），却一直缺乏统一的实现方式，以至于 [实践中的做法](https://www.ics.uci.edu/~ejw/authoring/implementation.html) 四分五裂、不同软件商自说自话，相对主流的方案——例如微软在 Windows 和 Office 中的实现，以及苹果在 macOS Finder 中的实现——都存在或多或少的「怪癖」或 bug，进一步影响了用户的顺畅使用和存储提供商的有效支持。因此，[有观点](https://news.ycombinator.com/item?id=19250319) 认为 WebDAV 只有在用户能同时控制客户端和服务端的场合才能稳定工作；但如果能做到这一点，其实有很多更好的协议可用，根本就没有 WebDAV 什么事了。

某种意义上，WebDAV 之所以在今天还被保留使用，很大程度上是历史原因造成的：早期软件中的支持一直被保留下来，贸然移除必然面临阻力；苹果基于 WebDAV 开发的 CalDAV（用于访问远程日历）和 CardDAV（用于访问远程通讯录）成为了业界事实标准，也起到了「续命」作用。近年来，[remoteStorage](https://remotestorage.io/)、[JMAP](https://jmap.io/) 等较新的协议也一直在试图挑战 WebDAV 的地位，尽管尚未成功。
