---
title: "2022 年，搭配 Zotero 的 WebDAV 存储方案还有什么选择？"
date: 2022-03-21
draft: true
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
- **如果愿意付费：**坚果云仍然是一个优秀的选择，Koofr 常年销售的廉价终身方案也可以作为备选。

具体介绍和使用方法见下文。

## 具体介绍

### Box

#### 用法速查

- WebDAV 地址：`https://dav.box.com/dav/`
- WebDAV 验证方式：同登录用户名和密码
- 官方文档：[WebDAV with Box](https://support.box.com/hc/en-us/articles/360043696414-WebDAV-with-Box)

#### 具体说明

[Box](https://www.box.com/) 可能是这几个服务里最「大牌」的一家，创立于 2005 年，并且已经在 2015 年上市。与同辈 Dropbox 相比，Box 的 B 端业务相对突出，因而在宣传上比较低调，但也少了很多「花里胡哨」的噱头。

根据 Box 的支持文档，其对 WebDAV 的支持已经于 2019 年末结束。但这其实是个文字游戏，真正停止的只是「技术支持」，即官方不会回答相关技术问题，而非彻底关停 WebDAV 服务。

定价方面，Box 的免费空间比较慷慨，达到 10GB，对于存储学术文献来说比较充裕。但如果有进一步的空间需求，早年的引荐增加空间活动已经停止，个人版只有年费 120 美元的 100GB 选项，性价比很低。

速度方面，由于 Box 在 [全球多地](https://www.box.com/zones) 设有数据中心，国内访问一般会被安排到位于日本或德国的服务器，速度也相对理想，完成前述上传测试的平均时间为 10.7 秒。

### Koofr

#### 用法速查

- WebDAV 地址：`https://app.koofr.net/dav/Koofr/` 或 `https://app.koofr.net/dav/<连接的外部网盘名称>/`
- WebDAV 验证方式：登录用户名和专用密码
- 官方文档：[Koofr with Zotero via WebDAV](https://koofr.eu/blog/posts/koofr-with-zotero-via-webdav)

#### 具体说明

[Koofr](https://koofr.eu/) 是一家斯洛文尼亚存储服务提供商，从 2012 年开始提供服务，近年来经常在一些「美国服务的欧洲替代品」讨论中被提及（[一个例子](https://european-alternatives.eu/product/koofr)）。

Koofr 有详尽的 [官方文档](https://european-alternatives.eu/product/koofr) 和相对活跃的 [博客](https://koofr.eu/blog/)，界面设计也比较简约流畅，从这些角度给人印象不错。

WebDAV 是 Koofr 官方支持且作为亮点宣传的功能之一，官方博客还有一篇 [文章](https://koofr.eu/blog/posts/koofr-with-zotero-via-webdav) 专门介绍如何搭配 Zotero 使用，只需注意其登录使用的是单独密码，需在后台的 **Password** > **App passwords** 界面手动生成。

Koofr 提供 2GB 的免费空间，引荐四人后可提高至 10GB，竞争力一般。不过，该服务的升级方案相对非常廉价，各个容量档位的年费甚至跟一线产品的月费差不多；不仅如此，在 StackSocial 等网站还能找到常年销售的几种永久套餐，价格也属可接受范围。（当然，前十年没有跑路不代表接下来十年不会跑路，这里不做担保，请读者自行衡量取舍；因为没有给我们打钱，这里也就不加链接了。）

当然，鱼与熊掌毕竟不能兼得，由于服务器位于欧洲且并未针对国内连接优化，Koofr 的速度算不上理想：完成前述上传测试的平均时间为 24.1 秒，只能说对于 Zotero 的使用场景来说差强人意。

但本文之所以把 Koofr 拿出来推荐，主要是考虑到它的一项特殊功能——**可以连接 Dropbox、Google Drive 和 OneDrive（个人版或企业版）作为「外挂」，直接调用被连接服务的存储空间。** 不仅如此，被连接的服务也可以通过 Koofr 的 WebDAV 功能来访问。不严肃地说，这三家网盘的「羊毛」多到仿佛凌空一抓就是一把；通过 Koofr 的这个功能，你完全可以抛开它本身的空间，将其视作其他网盘的「WebDAV 插件」来用。

![](https://cdn.sspai.com/2022/03/21/0045dcc2a6c7275a783f0d35d9016c03.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

至于配置方法，Koofr 也提供了 [完整的文档](https://koofr.eu/help/connect-other-cloud-services/)，简而言之在后台的 [Places 页面](https://app.koofr.net/app/admin/places) 授权即可，打开一看便知。这里只提示几个要点：

- 连接的第三方服务可以通过形如 `https://app.koofr.net/dav/<连接的外部网盘名称>/` 的地址来实现 WebDAV 访问，例如 `https://app.koofr.net/dav/Dropbox/`，其中大小写敏感、空格需用 `%20` 转义。因此，建议给所连接服务**设置一个全小写且没有空格的名称**。
- 该方法下，数据传输需要花费从你的电脑到 Koofr 服务端，加上 Koofr 服务端到第三方服务的双重时间，因此**速度很难谓之理想**。在连接 OneDrive 测试时，完成前述上传测试的平均时间为 40 秒，即使考虑到传输文献的轻量场景，也只能评价为勉强可接受。
- 经过测试，Google Drive 可以链接并通过网页端中转传输文件，但通过 WebDAV 访问则无效。时间所限，我们暂时无法确定是否为个例、或问题存在于哪一方，建议优先使用 OneDrive 和 Dropbox 尝试。
- 免费账户连接第三方服务时，**通过 Koofr 中转的文件** [**不占用**](https://koofr.eu/help/connect-other-cloud-services/will-connecting-to-other-cloud-services-impact-my-space-on-koofr/) **Koofr 自身的空间，但** [**每天的流量**](https://koofr.eu/help/connect-other-cloud-services/external-clouds-transfer-limits/) **有 1GB 限制**，可以通过升级任意付费方案解除。考虑到 Zotero 的使用场景和 Koofr 的低廉定价，我们认为这一限制并不过分，如果重度使用，也不妨升级一个便宜的档位。
- 由于使用该功能需要授予 Koofr 对第三方网盘的读写权限，谨慎起见，我们建议**尽量使用不包含个人重要资料的账号**来授权。

### TeraCLOUD

#### 用法速查

- WebDAV 地址：`https://seto.teracloud.jp/dav/`
- WebDAV 验证方式：登录用户名和专用密码
- 官方文档：[Can I use WebDAV compatible apps？](https://teracloud.jp/en/support_guide_general_webdavcli.html)

#### 具体说明

[TeraCLOUD](https://teracloud.jp/en/) 的数据中心位于日本，似乎隶属于一家美国的云服务提供商，大约从 2018 年左右起向个人提供服务。与其他主打自主客户端的存储服务相比，TeraCLOUD 不仅是支持 WebDAV，甚至可以说是**只**支持 WebDAV，根本不提供官方客户端，而简陋的网页端本质上也就是一个 WebDAV 前端界面。

![](https://cdn.sspai.com/2022/03/21/2f5f757c336d991b430172690f1148ab.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

没有设计就是……

定价方面，TeraCLOUD 提供 10GB 的免费空间，填写他人的引荐代码后可以额外增加 5GB（文中不便直接包含，会员读者可在群内相互交流），对于 Zotero 的使用场景应该说是比较充裕了。升级方案不算便宜，但在国外服务语境下倒也算正常，同时从官方 [宣传历史](https://teracloud.jp/en/news.html) 看不时会有优惠活动。

如上所述，TeraCLOUD 的心思根本不在界面上，但好在布局简明。要设置 WebDAV 链接，前往 **My Page** > **Apps Connection** 打开开关、并生成专用密码即可（然后就忘记这个辣眼睛的网页端吧）。

得益于一衣带水的位置优势，TeraCLOUD 的访问速度非常理想，延迟在几十毫秒的水平，只花了不到 6 秒就完成了前述方法的上传测试——数值上比国产服务坚果云还要快。

### 坚果云

#### 用法速查

- WebDAV 地址：`https://dav.jianguoyun.com/dav/<自定应用名称>/`
- WebDAV 验证方式：登录用户名和专用密码
- 官方文档：[如何在 Zotero 中设置 WebDAV 连接到坚果云？](https://help.jianguoyun.com/?p=3168)

#### 具体说明

[坚果云](https://www.jianguoyun.com/) 严格来说不符合本文的筛选标准：免费账户受限于 1GB 的流量限制，使用起来比较捉襟见肘。但作为少数的国产且官方支持 WebDAV 的服务，出于完整考虑还是在此略作提及。

作为国产服务，坚果云的速度自然不用担心，完成上述测试的时间在 7—8 秒，定价上也比较亲民，42GB（[有文化的数字](https://en.wikipedia.org/wiki/42_(number)#The_Hitchhiker's_Guide_to_the_Galaxy)）档位对于 Zotero 主力用户——学生群体也不算过分。

### 题外话：关于 WebDAV

在涉及网盘的讨论中，支不支持 [WebDAV](http://www.webdav.org/) 协议，经常被用来作为衡量服务商够不够「大方」、心态够不够开放的标准。诚然，在公开标准越发受到挤压，私有协议和臃肿客户端成为主流的市场环境下，能提供 WebDAV 协议是值得鼓励的；但也有必要指出，**不应该因此过于拔高 WebDAV 协议的评价**。

事实上，WebDAV 是主流文件传输协议中较为落后的一种。作为一个诞生于 1996 年的协议，WebDAV 使用语法冗长的 XML 格式传递请求和响应，效率不高、开发起来也不方便。尽管实现了名义上的标准化（IEEE [RFC 4918](https://datatracker.ietf.org/doc/html/rfc4918)），却一直缺乏统一的实现方式，以至于 [实践中的做法](https://www.ics.uci.edu/~ejw/authoring/implementation.html) 四分五裂、不同软件商自说自话，相对主流的方案——例如微软在 Windows 和 Office 中的实现，以及苹果在 macOS Finder 中的实现——都存在或多或少的「怪癖」或 bug，进一步影响了用户的顺畅使用和存储提供商的有效支持。因此，[有观点](https://news.ycombinator.com/item?id=19250319) 认为 WebDAV 只有在用户能同时控制客户端和服务端的场合才能稳定工作；但如果能做到这一点，其实有很多更好的协议可用，根本就没有 WebDAV 什么事了。

某种意义上，WebDAV 之所以在今天还被保留使用，很大程度上是历史原因造成的：早期软件中的支持一直被保留下来，贸然移除必然面临阻力；苹果基于 WebDAV 开发的 CalDAV（用于访问远程日历）和 CardDAV（用于访问远程通讯录）成为了业界事实标准，也起到了「续命」作用。近年来，[remoteStorage](https://remotestorage.io/)、[JMAP](https://jmap.io/) 等较新的协议也一直在试图挑战 WebDAV 的地位，尽管尚未成功。
