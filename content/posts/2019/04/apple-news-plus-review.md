---
title: "Apple News+ 一周体验"
date: "2019-04-02"
tags:
  - "apple"
  - "review"
---

虽然今年苹果春季发布会的阵容与人们预期的一样强大，但最终发布的「现货」只有 Apple News+ 这一项。关于该服务的优势和亮点，现有的报道已经很充分了。简单概括，就是每月 9.99 美元无限阅读数百种杂志（目前总数为 251 种）、专门为屏幕阅读设计的排版、推荐内容来自真人编辑、比其他平台更好的隐私保护、支持离线阅读及家人共享等。

尽管在之前很少使用系统自带的 News 应用，但作为一个喜欢翻阅各种外刊的读者，我很难不对 Apple News+ 产生浓厚的兴趣。由于今年恰好有地理位置上的便利，我在发布会结束后的第一时间便升级了系统、开启了该服务的免费试用，并在这近一周的时间内花了很多时间在 News 应用中阅读。本文将介绍我这段时间的使用体验，并尝试探讨 Apple News+ 对用户的价值。

## 惊艳的第一印象

点进新增的 News+ 页面后，居于最上方的是杂志的分类目录和近期阅读的杂志封面。如果关注了特定杂志的频道，该杂志的新刊会自动出现在「我的杂志」书架上。点按杂志标题右侧的下载图标，可以将整本杂志缓存到本机，以供没有网络连接时阅读（但有 30 天的有效期限制）。不过，杂志一旦下载就[不能手动删除](https://support.apple.com/en-us/HT209514)，只能等待 News 应用在 30 天后或设备容量不足时自行清理。

![Apple News+ 在 iPhone 和 iPad 上的界面](https://cl.ly/490410/news-on-iphone-ipad.png)

Apple News+ 在 iPhone 和 iPad 上的界面

向下滑动，就能看到 News+ 的另一项主打功能——人工编辑做出的内容推荐。根据观察，推荐的标准比较灵活，有的是推介杂志新刊并列出专题文章，有的则直接推荐单篇特稿，还有的按照话题筛选来自不同刊物的文章。不过，目前的推荐话题都是时尚、科技、家居等比较宽泛的类目，显得有些松散，与 App Store 首页中编辑内容的质量仍有差距。好在，试用的这几天中，推荐内容的更新较为及时和频繁：上架的新刊都能第一时间看到，话题推荐板块则基本每隔半天打开就有更新。可见，苹果在该服务上投入的编辑资源是有保障的，后续应该有不少进步的空间。

![几种不同推荐板块](https://cl.ly/abe3c9/recommends.png)

几种不同推荐板块

Apple News+ 的内容呈现技术是以 [Apple News Format](https://developer.apple.com/documentation/apple_news/apple_news_format) 为基础的。这是苹果为 Apple News 定制的一种私有格式，它通过 JSON 语法定义页面中元素的布局、外观和功能，可以实现比普通网页格式更丰富的视觉效果和交互。虽然 Apple News Format 在 2015 年就已随着初版 News 应用一起上线，但它此次也迎来了[功能更新](https://developer.apple.com/documentation/apple_news/what_s_new_in_apple_news_format)，包括根据屏幕宽度动态调整布局、文章链接支持显示标题和预览图等；显然，这是为了让 Apple News+ 更好地支持不同尺寸的设备和版式复杂的杂志文章而做的铺垫。

![Apple News Format 的内部结构（来源：苹果）](https://cl.ly/a4c0bd/ANfmt.png)

Apple News Format 的内部结构（来源：苹果）

在 Apple News Format 的加持下，Apple News+ 的排版效果堪称惊艳。发布会上，苹果就重点演示了《国家地理》杂志的动态封面。其实，连很多静态封面也支持视差（parallax）效果，左右移动设备时，可以观察到封面的前景和背景以不同的速率移动。

![Apple News+ 中的主打杂志，其中很多的封面具有动态效果](https://cl.ly/cbb7a5/featured-cover.png)

Apple News+ 中的主打杂志，其中很多的封面具有动态效果

点进一篇文章后，封面会以缩略图形式漂浮在左下角，点按即可浏览杂志目录。

![Apple News+ 的内文阅读界面](https://cl.ly/1242ed/bodytext.png)

Apple News+ 的内文阅读界面

文章排版最大程度地保留了纸刊的样式，包括字体、主题色等；但同时又不止步于照搬原版，而是考虑到了移动设备的优势，例如通过横向卷轴展示多幅图片，为版面元素加入动画。特别「机智」的《连线》杂志还为产品推荐板块额外加上了直通「剁手」页面的链接。

![《连线》杂志同一篇文章在 Apple News+ 上和纸刊上的对比；注意前者多出的「立即购买」链接](https://cl.ly/21e2b0/wired.png)

《连线》杂志同一篇文章在 Apple News+ 上和纸刊上的对比；注意前者多出的「立即购买」链接

Apple News+ 并不是苹果引入期刊资源的第一次尝试。早在 2011 年，苹果就在 iOS 5 的主屏幕上加入了 Newsstand 图标，用于汇集设备上安装的新闻和杂志应用。可惜，Newsstand 成为了 iOS 用户最「痛恨」的功能之一。这不仅是因为那个赘余的图标，更因为它并没有给出版方提供任何实质的帮助，而后者往往并没有足够的技术基础做出良好的移动应用，其用户体验可想而知。

![Apple News+ 的失败榜样——Newsstand](https://cl.ly/5959ce/newsstand.png)

Apple News+ 的失败榜样——Newsstand

Apple News+ 显然从 Newsstand 的折踵中吸取了教训。这一回，从排版到分发的全套工具都是由苹果提供的，杂志社只要拿自己的内容套用即可。这种恰当的分工使得 Apple News+ 在阅读体验上前进了一大步——我第一次感觉到传统杂志也可以成为数字设备上的原住民，而不是在纸刊基础上缩减和妥协的产物。

## 差强人意的细节

然而，至少在现阶段，Apple News+ 并不是处处都如宣传中的那样「光鲜」。

首先，并不是所有刊物都能充分发挥 Apple News Format 的潜力。除了少数几份被归入「Featured」类别的主打杂志外，很多杂志的文章基本还止步于静态页面、文本配图的简单样式，和直接访问网站观看的效果区别不大。这还是比较好的情况；根据 MacStories 的[统计](https://www.macstories.net/news/a-complete-list-of-all-the-magazines-available-for-apple-news-in-the-u-s-so-far/)，超过半数的杂志目前甚至没有文字版，而只提供了扫描版的 PDF 图像。实际上，连那些主打杂志的过刊，也是以 PDF 格式提供的。考虑到 Apple News+ 推出的时间很短，要求所有文章都在一夜之间采用新格式当然不太现实；但靠 PDF 格式凑数则未免有偷懒之嫌，毕竟多数杂志在其他平台上都提供过文字版。

![屈尊以 PDF 格式显示在 iPhone 上的 Ive 爵士](https://cl.ly/09870f/pdfIve.png)

屈尊以 PDF 格式显示在 iPhone 上的 Ive 爵士

其次，Apple News+ 的操作体验也有很大的改善空间。例如，杂志文章一般篇幅较长，时间有限的读者需要多次才能看完，因此其他很多软件都会提供同步阅读进度和书签的功能。但 Apple News 至今不支持记忆阅读进度，更遑论在设备间同步；虽然支持保存文章，但功能的入口却设在了分享菜单的深处，关注特定杂志更是要进入搜索界面才能操作。令人困惑的是，文字大小的设置反倒是会在各个设备间同步的，但不同设备的尺寸迥异，在 iPad 上看来舒适的尺寸，放在 iPhone 上可能就显得很不成比例。

再如，杂志目录的信息密度很低，在没有标注栏目名称和题注（byline）的情况下，仅靠标题很难了解文章主题。

![《纽约客》杂志在 Apple News+ 和网页上的目录；前者省略了很多有用信息](https://cl.ly/5fbb78/nyer-toc.png)

《纽约客》杂志在 Apple News+ 和网页上的目录；前者省略了很多有用信息

另外，Apple News+ 的阅读权限是严格限制在该服务范围内的，用户不能在 News 应用以外的任何地方（例如杂志自己的网站上）阅读这些文章。从该服务中分享的文章链接是指向 News 应用的 deep link、而不是公网上的 URL，接收者如果不是订户就无法阅读。即使是在 News 应用内，新旧板块之间的衔接也不够完善。我在这周中就多次遇到过在普通版中点击付费版收录的文章，却仍不能完整阅读的情况。

Apple News+ 所宣传的「洁净」也是要加一些注脚的。在发布会上，苹果惯例地强调了 Apple News+ 和其他苹果服务一样以保护用户隐私为要务，具体举措包括在用户本机而非云端运行推荐算法、禁止广告商和内容方追踪用户阅读历史等。但这并不代表没有广告。相反，即使在付费之后，Apple News+ 中的广告数量也远比想象的多。

![各处出现的广告](https://cl.ly/91ffc6/ads.png)

各处出现的广告

实际上，苹果在向出版方发布的[《广告指南》](https://developer.apple.com/news-publisher/News-Publisher-Advertising-Guide.pdf)（PDF）中，允许在九处不同位置投放广告，包括段落间、文章间、通知中心插件等。考虑到大多数用户会在浏览器中安装广告拦截插件，他们在从网页迁移到 Apple News+ 时，很可能反而明显感到广告增多。不仅如此，「禁止追踪」的对象只是用户的**阅读历史**，而追踪广告的**展示和点击量**则不在此限——《指南》明示允许通过跳转链接、1x1 像素透明图片等技术追踪这些信息，并允许针对特定年龄、性别、地域的用户定向投放广告。

还有一个绕不开的话题——《华尔街日报》与苹果的合作。早在发布会前，这家大牌报纸的加盟就引来了广泛关注。在《纽约时报》《华盛顿邮报》等同段位媒体拒绝与苹果合作的背景下，《华尔街日报》的决策不仅令人意外，也留下了一个悬念——它会愿意在苹果的平台上开放多少文章。毕竟，《华尔街日报》本身订阅价格不菲，即使「折扣」后也在每月 20 美元以上，数倍于其他主流大报（作为对比，《纽约时报》的数字版常规价格为每月 8 美元，并常有五折优惠），也远超 Apple News+ 的一揽子定价。如果能通过 Apple News+ 读到《华尔街日报》的全部内容，只此一项便足够值回票价了。

事实证明，《华尔街日报》的确不会那么慷慨。该报纸在 26 日的[刊文](https://www.wsj.com/articles/wall-street-journals-partnership-with-apple-marks-shift-in-strategy-11553556819)（该链接有付费墙）中指出，通过 Apple News+ 提供的内容和它们自己提供的订阅服务是「完全不同」的。前者只会展示那些「普通读者感兴趣」的文章，包括国内新闻、政治、体育和休闲内容，以及部分商业新闻；而该报纸最精华的商业和财经文章则需要通过手动搜索才能看到。另外，Apple News+ 的用户只能看到近三天的文章，并且阅读权限与报纸网站并不通用。

![《华尔街日报》的文章只在编辑推荐中能看到少量入口](https://cl.ly/3e0d21/wsj.jpeg)

《华尔街日报》的文章只在编辑推荐中能看到少量入口

我此前订阅了《华尔街日报》的数字版，因此在 News 应用中看到的是付费状态下的内容，无法验证在只订阅 Apple News+ 的情况下是否存在只能看近三天文章的限制。但可以确定的是，《华尔街日报》并没有和其他刊物一样出现在 News+ 板块的书架中，用户也看不到当期报纸的完整目录，而只能从编辑推荐板块中找到有限数量的文章链接。可见，Apple News+ 附带的《华尔街日报》只能说是锦上添花，而不足以成为做出付费决策的主要考量因素；如果真的对完整阅读权限有需求，直接订阅该报纸的数字版仍然是唯一的选择。

## Apple News+ 的竞争力

当然，评价 Apple News+ 的优劣还要将它和竞争者对比之后才能做出结论。提供「打包」式杂志订阅并不是一种很新颖的模式。除了被苹果收购以为 Apple News+ 做准备的 [Texture](https://www.texture.com)（已经[宣布](https://www.texture.com/support/Knowledgebase/Article/View/306/)即将结束独立运营），如今还有 [Magzter](https://www.magzter.com)、[Scribd](https://www.scribd.com) 等公司提供功能和价格均相近的订阅服务。此外，亚马逊的 Kindle Unlimited 订阅虽然以图书为主，但也[涵盖](https://www.amazon.com/kindle-dbs/fd/ku-aycr-magazines)了不少杂志内容；[PressReader](https://www.pressreader.com) 的模式则是与图书馆和酒店合作，用户可以在连接到它们特设的 WiFi 热点时无限阅读期刊。

在杂志内容的呈现形式上，这些竞争服务有的只提供 PDF 图像（如 Magzter），有的只提供文本（如 Scribd），也有的两者均提供、并允许用户在两种模式间切换（如 Kindle）。但无论采用哪种做法，呈现效果都不尽如人意。PDF 格式的局限性无需多言，即使像 Kindle 那样提供文本，其样式也非常单调，并且常有错漏（何况 Kindle 软件本身的排版效果一直很差）。

![Kindle 的杂志阅读允许用户在扫描版和文字版间切换，但效果都难以让人满意](https://cl.ly/233190/kindle.png)

Kindle 的杂志阅读允许用户在扫描版和文字版间切换，但效果都难以让人满意

表现最好的可能是 PressReader，它会在图像版本上高亮框出文章标题，点按后即可跳转到对应的文字版，并且界面上会给出相关内容推荐。但即使如此，它也没有能完全克服传统刊物在移动设备上水土不服的问题，读者在使用时能明显感到这是一种妥协后的效果。与它们相比，Apple News+ 的确有比较明显的优势。

![设计相对较好的 PressReader](https://cl.ly/1e54be/pressreader.png)

设计相对较好的 PressReader

不过，这种优势是有前提的，那就是内容提供方充分利用了 Apple News Format 的功能；但从前文可以看出，有条件做到这一点的只是少数。对于大多数只是简单转换格式、甚至直接丢给用户一个扫描版的文章，其在 Apple News+ 上的阅读体验和在其他平台上并无本质区别。

要获得成功，Apple News+ 还需要说服读者从传统的订阅渠道转移。为此，苹果少见地打起了价格牌，在发布会上指出：如果一一订阅该服务中所有刊物，每年需要花费 8000 美元以上，因此 Apple News+ 不到两位数的月费就显得十分超值了。

显然，这种算法是有所夸大的。首先，没有人会真的去订阅几百种杂志。对于一般人而言，同时阅读三四份刊物可能已经是精力上限。另外，8000 美元的价格显然是用名义上的标价计算的，但实际情况是几乎没有人会按原价订阅杂志。除了《纽约客》《时代》等名声相对显赫的杂志，大多数 Apple News+ 中的刊物都可以在亚马逊等网站上用一季度甚至一年 5 美元的价格订阅纸刊，并且附送 Kindle 版和官网阅读权限。极端如《连线》等媒体甚至隔周就会出现 4 美元/两年这种「跳楼价」。

![亚马逊上几乎每天都会出现的廉价杂志订阅，其中很多是 Apple News+ 所收录的](https://cl.ly/f8ca6d/amzndeals.png)

亚马逊上几乎每天都会出现的廉价杂志订阅，其中很多是 Apple News+ 所收录的

不仅如此，如今期刊内容的免费获取渠道也极为广泛。这里的「免费」并不是指盗版；很多杂志都会在其网站上将纸刊内容都会同步甚至提前全文刊出，且其中很大比例是没有付费墙的。即使有的限制了阅读篇数，其执行也通常极为宽松。因此，即使没有 Apple News+，通过现有渠道阅读杂志内容也是相对方便和廉价的，平均成本未必会达到每月 10 美元。

实际上，期刊目前的低廉定价和 Apple News+ 杂志库的庞大是同一枚硬币的两面，其成因都在于期刊行业的营利模式和业务现状。与报纸、电视等其他大众传媒类似，杂志行业的主要收入并不在于销售，而是来自广告。在美国，期刊行业广告收入占总收入的比例是 51.1%，显著高于来自订阅和零售的收入（34.9%）。因此，即使赔本销售杂志，如果能由此扩大发行量和读者群，随之增加的广告投放也足以让杂志社维持经营。

![美国期刊发行行业收入来源统计（来源：IBISWorld）](https://cl.ly/249fa0/us-mag-seg.png)

美国期刊发行行业收入来源统计（来源：IBISWorld）

但在近年，随着广告投入越发向数字平台转移，期刊行业的传统商业模式已经难以维持。以美国为例，该行业的收入总额连续多年下滑，从 2009 年的 3970 万美元跌至 2018 年的 2112 万美元，雇员人数从 14 万余人缩减到 8 万余人。仅去年一年，就有包括《Interview》《The Village Voice》在内的多家著名刊物宣布停刊。因此，通过低价促销和加入 Apple News+ 这样的平台来维持覆盖面，某种程度上也是不得已而为之的选择。发布会前几周，有消息称苹果对 Apple News+ 的内容方[收取高达 50% 的收入提成](https://www.latimes.com/business/technology/la-fi-tn-apple-subscription-news-20190325-story.html)，引发了不少关于苹果是否过于「贪婪」的讨论。这或许能体现双方谈判地位的差异，但换一个角度看，既然很多杂志之前已经通过各种渠道提供了电子版，将这一现成资源挪用到苹果平台上销售并不需要多少额外成本，因此即使在「克扣」后也是一种净得。

当然，对于处于金字塔顶端的一些刊物，例如《华尔街日报》《纽约时报》来说，情况可能有所不同。这些媒体本身具有较强的订户基础，拥有自己的广告发行渠道，并已在向数字发行转移的方向上取得了一定成功，因此并不依赖于苹果提供的平台；Apple News 的封闭式特征反倒会影响它们自己网站的流量。不仅如此，这些大牌媒体往往并不满足于沦落为科技公司的内容提供商，而是希望强化自己的品牌识别度，和订户建立直接的业务和情感联系——《纽约时报》在其面向 2020 年的运营策略[报告](https://www.nytimes.com/projects/2020-report/index.html)中就反复强调读者的「忠诚」「参与」和对报道的反哺作用。于是，它们要么干脆不和苹果合作，要么用缩水的内容谨慎试水。这进一步限制了 Apple News+ 能为用户带来的优惠程度。

总之，Apple News+ 并不是苹果替消费者行道、与期刊业博弈的让利之举，而是苹果与内容方基于各自对内容和平台的渴求展开的合作。10 美元的打包价当然具有一定吸引力，但并不是一笔稳赚不赔的投资。

## 国内用户的替代选择

在国内语境下讨论 Apple News+，还必须面对一个现实问题——这一服务在可预见的未来都不会在中国上线。同时，由于苹果对 News 应用执行了异常严格的锁区策略，我们至今没有稳定、简便地从国内访问 Apple News+ 服务的方式。

这固然是一种遗憾，但比起纠结于讨论 Apple News+ 算不算「何不食肉糜」，更实际的做法是考虑是否有读到该服务所提供资源的替代方法。这超出了本文讨论范围，但其答案毫无疑问是肯定的。如上所述，如果你只是固定关注特定几种刊物，有很大概率可以直接在官网免费读到多数纸刊文章，或者通过比较低廉的价格在亚马逊等平台上订阅；对于价格敏感的读者，也可以通过[隐私模式](https://support.apple.com/zh-cn/HT203036)、[Calibre 的新闻下载功能](https://manual.calibre-ebook.com/news.html)、和浏览器插件等技巧节约开支。

![Calibre 的新闻下载功能足以获取多数刊物的文章](https://cl.ly/3210c4/calibre-download-news.png)

Calibre 的新闻下载功能足以获取多数刊物的文章

如果你的确对杂志资源的数量有很高要求，那么也可以选择 Scribd、Kindle Unlimited 这些定价相近或更低的替代服务。另外，虽然图书馆在今天非常容易被人遗忘，但它们往往会提供非常丰富的数字资源（参见[国家图书馆的列表](http://www.nlc.cn/dsb_zyyfw/qk/qkzyk/)）。因此，不妨试着调研一番就近图书馆的网站（或咨询图书馆员），一般都会有意外收获。

![不少国内院校和图书馆都会订阅的 ProQuest 数据库，其中就收录了《华尔街日报》的全文](https://cl.ly/cd1f85/proquest-wsj.png)

不少国内院校和图书馆都会订阅的 ProQuest 数据库，其中就收录了《华尔街日报》的全文

此外，国外不少图书馆的注册[不需要居民身份](https://blog.the-ebook-reader.com/2011/09/22/library-ebooks-for-non-residents-where-to-get-ebooks-if-your-library-is-lacking/)，通过获取它们的读者证（一般为免费或收费低廉），就可以访问汇集了大量期刊资源的数据库。总之，只要留心并愿意阅读，没有什么真正能成为读者的障碍。

## 结语

Apple News+ 能不能说服用户从其他阅读平台转移？答案对我来说是否定的。

这当然是建立在我特定的使用习惯和需求上的回答。我平时阅读的杂志以文字为主要内容，Apple News+ 的专门排版对这类杂志的优化作用有限（反正横竖都是字），反倒是在电纸书上用自己习惯的排版设置阅读更让我感到舒适。另外，我比较倾向于依靠自己而不是他人的推荐来寻找阅读材料，并且从去年开始一直在试图控制自己在摄入信息上花费的精力，因此也并不十分看重 Apple News+ 主打的无限杂志和人工推荐文章功能。

![Apple News+ 的高级排版对《纽约客》这类基本都是文字的刊物效果有限](https://cl.ly/71a052/nyer.jpeg)

Apple News+ 的高级排版对《纽约客》这类基本都是文字的刊物效果有限

相反，如果一位读者经常阅读《体育画报》《国家地理》这类图片多、排版复杂的杂志，那么 Apple News+ 的确能提供目前无出其右的电子阅读体验。此外，如果你习惯了社交网络或新闻聚合应用的信息流模式，但又对算法推荐的副作用有所顾虑，苹果的人工推荐或许可以让你既不改变相对熟悉的操作逻辑，又能接触到更为全面的视角。再考虑到软硬件整合、隐私保护等苹果的传统优势，Apple News+ 至少是一个颇具说服力的选择。

不过，一项服务的「价值」并不完全取决于功能的强弱和成本的计算，还在于用户究竟能从中获益多少。然而，这或许不是苹果重点关心的问题。Apple News+ 是苹果内容战略中的一片拼图，新版商业故事中的一段脚本。但宏图是拼给华尔街看的，故事是讲给投资者听的；Apple News+ 一名中的加号，连接的也是内容生产者。

![Apple News+ 并不能为读者的阅读质量负责](https://cl.ly/d7aa71/keynote-bg.png)

Apple News+ 并不能为读者的阅读质量负责

在发布会上，库克提到「站在书报亭前的满足感」，并以此为喻引出对 Apple News+ 的介绍。这是一个恰如其分的比喻——Apple News+ 的功用确实是，但同时也只是把书报亭搬到了用户面前。但究竟是能从中获取更广博的视野、更高质量的阅读材料，抑或是止步于视觉上的饱足和坐拥无限资源的富余感，就是我们身为读者只能自负其责的问题了。
