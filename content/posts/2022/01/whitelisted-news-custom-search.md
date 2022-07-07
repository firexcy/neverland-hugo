---
title: "[Preview] 为了「派早报」不翻车，我们做了个官方新闻搜索引擎"
date: 2022-01-18
tags:
  - "tutorial"
  - "workflow"
---

**Note:** This article was published as a member-exclusive post for [SSPAI Prime](https://sspai.com/prime), which you may find [here](https://sspai.com/prime/story/whitelisted-news-custom-search); the content below is a selected preview thereof. Please consider subscribing to SSPAI Prime if you find content like this helpful. Thanks for your support.

「派早报」是最受少数派读者熟悉和喜爱的常规栏目之一。虽然这个栏目的主题说起来并不复杂——汇总前一天我们认为比较重要的科技资讯；但实际运行中会涉及很多需要考量的细节。就以**选择资讯来源**这件事来说，除了要关注信源的权威和准确，遵纪守法当然也要常记心头。

[ Intermediate content is omitted from this preview ]

目前，提供自定义搜索引擎功能的主流搜索引擎主要是 Google 和 Microsoft Bing（很遗憾，我们短暂的调研中并未发现国产主流搜索引擎提供类似的功能），它们都可以免费使用，但在配置难易程度、免费档位限额等方面有所差异。

下面，我们就分别介绍如何使用这两家服务的自定义搜索功能，打造一个「白名单信源定向搜索引擎」。

![](https://cdn.sspai.com/2022/01/17/afcd4c45b23ddaf681dab55c0ec9789e.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

## **准备工作：搜集信源网址**

作为一个前置问题，为了定向搜索这些「白名单」媒体发布的内容，首先需要**收集其各渠道的网址**。如上所述，《稿源单位名单》名单列举的信源既包括网站，也包括微博、微信和 app。其中，网站的地址是最好收集的，一搜便知，但其他几个渠道就比较难处理了。

不过，对于微博而言，注意到其标准链接的格式是：

```
https://weibo.com/[用户ID]/[微博ID]
```

而其中的用户 ID 可以通过访问用户的微博首页（链接形如 `https://weibo.com/u/[用户ID]`），从地址栏看到。这样，只要定向搜索地址中包含

```
https://weibo.com/[用户ID]
```

的页面，也就相当于搜索该用户的公开微博。

![](https://cdn.sspai.com/2022/01/17/afd4c59534a73d9806f0abe2f33219f9.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

至于微信公众号和 app 内容……它们的开放程度不提也罢。好在官网和微博渠道相结合，一般而言已经能够满足派早报收集素材的需求了。后文将以[此列表](https://gist.github.com/firexcy/e146daf07db98f06c74d106edcd12a7a#file-white-txt)中的 30 个网站和微博账号为例演示。

## **Google 方案**

Google 的自定义搜索引擎功能正式名称为「[可编程搜索引擎](https://developers.google.com/custom-search/docs/overview)」（Programmable Search Engine），通过网页访问基本功能是完全免费的，只需注册 Google 账号即可。

[ Intermediate content is omitted from this preview ]

---

### **延伸：使用批注（Annotation）配置文件批量添加网站**

Google 自定义搜索引擎的定制功能很强大，除了添加搜索目标网站这一基本操作，还可以选择各个目标网站在搜索结果中的权重。就实现本文目的而言并不需要用到这种程度的能力，但还是做简单介绍，供有兴趣的读者自行探索。

这里，首先需要从一个更宏观的层面了解 Google 自定义搜索的排序逻辑。Google 自定义搜索**通过「标签」（label）和「注释」（annotation）两个步骤来标记搜索目标网站**。

其中，「标签」可以理解为对于目标网站的分类，每个标签都有一个名称和下列三种模式（mode）之一：

- 过滤（`FILTER`），即在全网范围内只搜索某些网站；
- 排除（`ELIMINATE`），即从全网搜索结果中排除某些网站；
- 增强（`BOOST`），即提高某些网站的权重。

**每个新创建的自定义搜索都有** `**_include_**` **和** `**_exclude_**` **两个默认标签**，分别被赋予了过滤和排除两种模式。

而「注释」则是给网站打标签的过程。注释配置可以通过 XML 或 TSV 格式来表达，但包含的信息基本是一致的，都含有网址（`URL`，可以包含通配符 `*`）、标签（`Label`）两个必选参数和权重分数（`Score`，取值范围是 `[-1.0, 1.0]`）、评论（`Comment`）两个可选参数。读者可以阅读官方文档了解[各个参数的含义](https://developers.google.com/custom-search/docs/annotations)和[权重分数对搜索结果的影响](https://developers.google.com/custom-search/docs/ranking)。

例如，上面步骤中，我们通过网页界面将澎湃新闻的网站（`thepaper.cn`）增加到白名单中时，等价于新增了一条网址为 `*.thepaper.cn/*`（通配符即对应「包含站点中的所有页面」的选项），标签为默认标签之一 `_include_` 的注释。由于没有赋权重分数，作为一个「过滤」模式的标签，权重默认为 +0.7。

了解这些背景知识后，读者就可以通过自行编写配置文件来细致调整不同白名单网站的权重高低了，上传方式是切换到「高级」（Advanced）选项卡，点击「搜索引擎注释」（Search engine annotations）下的「新增」（Add）按钮。（可以使用[这个示例文件](https://gist.github.com/firexcy/e146daf07db98f06c74d106edcd12a7a#file-white-tsv)尝试。）

![](https://cdn.sspai.com/2022/01/17/def8b4ef2035abbb8dfc96ba8e5fa747.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

---

[ Intermediate content is omitted from this preview ]

## **必应方案**

就国内使用而言，必应有一个不言而喻的优势：访问方便。

尽管如此，**必应并不是我们优先推荐的选择**，原因在于作为微软的云服务产品，它继承了该厂的传统特征——**名称变幻莫测、注册配置繁琐**。截至本文写作时，必应自定义搜索（Bing Custom Search）功能属于 Azure 服务中的「必应搜索服务」（Bing Search Services）大类；微软还给它抢注了一个非常高调的域名 [customsearch.ai](https://www.customsearch.ai/)。

成本方面，必应自定义搜索功能适用 [Bing Search API 的定价表](https://www.microsoft.com/en-us/bing/apis/pricing)，对于**每月 1000 次以内，每秒请求不超过 1 次的使用场景是免费的**——比较抠门，但对我们的用途不构成障碍。

必应自定义搜索引擎主要分为两大步骤：一是在 Azure 管理界面**创建一个必应自定义搜索资源**（Bing Custom Search resource）——可以理解为在微软那里开户方便它收钱；二是通过**必应自定义搜索门户**（Bing Custom Search portal）**创建和配置搜索引擎**。上述两个网站都可以使用普通的个人微软账号（包括最常见的 Outlook 邮箱账号）登录。

[ Intermediate content is omitted from this preview ]

此外，由于必应自定义搜索的网页版和 API 共用一套计费标准，API 在免费档位的次数和频率限制内也是免费的。有兴趣的读者也可以试试通过其 API 来访问自定义搜索功能，具体可参考[官方文档](https://docs.microsoft.com/en-us/bing/search-apis/bing-web-search/reference/endpoints)，在此不赘述。
