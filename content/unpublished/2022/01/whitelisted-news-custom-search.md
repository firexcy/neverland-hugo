---
title: "为了「派早报」不翻车，我们做个了官方新闻搜索引擎"
date: 2022-01-18
draft: true
tags:
  - "tutorial"
  - "workflow"
---

**Note:** This article was published as a member-exclusive post for [SSPAI Prime](https://sspai.com/prime), which you may find [here](https://sspai.com/prime/story/whitelisted-news-custom-search); the content below is a selected preview thereof. Please consider subscribing to SSPAI Prime if you find content like this helpful. Thanks for your support.

「派早报」是最受少数派读者熟悉和喜爱的常规栏目之一。虽然这个栏目的主题说起来并不复杂——汇总前一天我们认为比较重要的科技资讯；但实际运行中会涉及很多需要考量的细节。就以**选择资讯来源**这件事来说，除了要关注信源的权威和准确，遵纪守法当然也要常记心头。

对此，最为相关的法规是[《互联网新闻信息服务管理规定》](http://www.cac.gov.cn/2017-05/02/c_1120902760.htm)。根据该规定第 15 条，互联网新闻信息服务提供者转载新闻信息，应当转载**国家规定范围内的单位发布的新闻信息**。

实践中，这里的「国家规定范围内的单位」是指[《互联网新闻信息稿源单位名单》](http://www.cac.gov.cn/2021-10/18/c_1636153133379560.htm)中列举的稿源单位。该名单最近一次[修订](http://www.cac.gov.cn/2021-10/20/c_1636326280912456.htm)是在 2021 年 10 月，涵盖了各级各地的机关、新闻媒体的网站、微博和微信公众号等。

![](https://cdn.sspai.com/2022/01/17/45f0c6178cdf0a74178eb2f4bde47cb2.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

当然，上述法规中的「新闻信息」和「互联网新闻信息服务提供者」有专门的法规定义，派早报所汇集的科技行业资讯，并不完全属于这个范畴。但毫无疑问，多加参照总是一种稳妥的选择，官方认可的来源也确实在可信度、内容质量上更有说服力。因此，我们会在选编资讯时，**优先参考这些来源发布的报道。**

问题来了：**怎样快速从这些来源中搜索信息呢？**

现行的《名单》共包含 1358 个来源，即使只考虑「派早报」编写中较为常用、更新及时、内容「接地气」的来源，也能找出二三十家，一一搜索显然是不现实的。固然可以通过搜索引擎的 `insite:` 语法指定网站范围，但每次搜索都要带上一长串后缀也很不方便。

我们找到的方案是**自定义搜索引擎**，也就是通过专门的入口，在一批特定的网站范围内搜索的定制化搜索引擎。

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

首先，访问 [Google 可编程搜索引擎的网站](https://programmablesearchengine.google.com/)，用自己的 Google 账号登录。然后，点击「新增」（Add）按钮，依次设置随意一个目标网站（例如新京报的网站 `bjnews.com.cn`，后面会继续添加）、搜索语言（中文简体）、自定义搜索引擎的名称，最后点击「创建」（Create）完成该步骤。

![](https://cdn.sspai.com/2022/01/17/b8c3fd5f37c731c698392836d5f8a2ea.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

此时，在左侧边栏中选择刚才创建的搜索引擎，进入「配置」（Setup）界面。这里，已经可以从「公开 URL」（Pubic URL）获得自定义搜索引擎的公开链接，还可以通过右侧的预览框直接尝试搜索效果。

不过，我们目前还需要为这个自定义搜索引擎添加更多目标网址。方法是点击「搜索站点」（Sites to search）下的「新增」（Add）按钮。由于我们要批量添加数十个网站，这里选择「批量包含站点」（Include sites in bulk）选项，然后将上一节中收集好的链接地址粘贴到文本框中；下方保持默认选项「包含站点中的所有页面」（Include all pages on these sites），确保子域名和子页面都可以被搜索到。

![](https://cdn.sspai.com/2022/01/17/c7c09b0f5ee59801b954679a2e28a9e4.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

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

除此之外，如果想让搜索界面更加个性化，可以在侧边栏的「外观和体验」（Look and feel）中调整配色、页面布局等，但本文创建的搜索引擎只是方便内部使用，外观不是主要考虑对象，在此也不多花时间。

完成配置后，就可以通过公开 URL 访问这个自定义搜索引擎了。自定义搜索的地址是固定的，可以保存到收藏夹以便日后使用。当然，如果用的比较频繁，最方便的方式还是将其添加为浏览器（或 Alfred 等启动器）中的自定义搜索引擎，方法是将搜索网址：

```
https://cse.google.com/cse?cx=[自定义搜索引擎编号]#gsc.q=[关键词]
```

中的`[关键词]`替换为相关软件要求的占位符即可。下图演示的是 Chrome 浏览器中的填写方法（位于「更多」>「设置」>「搜索引擎」>「管理搜索引擎」>「其他搜索引擎」>「添加」）：

![](https://cdn.sspai.com/2022/01/17/5f9350acea40503ac828e3df68eb2994.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

## **必应方案**

就国内使用而言，必应有一个不言而喻的优势：访问方便。

尽管如此，**必应并不是我们优先推荐的选择**，原因在于作为微软的云服务产品，它继承了该厂的传统特征——**名称变幻莫测、注册配置繁琐**。截至本文写作时，必应自定义搜索（Bing Custom Search）功能属于 Azure 服务中的「必应搜索服务」（Bing Search Services）大类；微软还给它抢注了一个非常高调的域名 [customsearch.ai](https://www.customsearch.ai/)。

成本方面，必应自定义搜索功能适用 [Bing Search API 的定价表](https://www.microsoft.com/en-us/bing/apis/pricing)，对于**每月 1000 次以内，每秒请求不超过 1 次的使用场景是免费的**——比较抠门，但对我们的用途不构成障碍。

必应自定义搜索引擎主要分为两大步骤：一是在 Azure 管理界面**创建一个必应自定义搜索资源**（Bing Custom Search resource）——可以理解为在微软那里开户方便它收钱；二是通过**必应自定义搜索门户**（Bing Custom Search portal）**创建和配置搜索引擎**。上述两个网站都可以使用普通的个人微软账号（包括最常见的 Outlook 邮箱账号）登录。

首先，[登录 Azure 门户](https://portal.azure.com/)（首次使用需要提供付款方式等信息），[创建一个自定义搜索资源](https://aka.ms/bingcustomsearchtrialkeys)。具体步骤可以跟随[官方文档](https://docs.microsoft.com/en-us/bing/search-apis/bing-web-search/create-bing-search-service-resource)，主要就是填写资源的名称和所需费用档位（免费）。完成后，在这个新创建资源的管理界面左侧点击「密钥和终结点」（Keys and Endpoints），然后从右侧的两个密钥中任选一个复制备用。

![](https://cdn.sspai.com/2022/01/17/2c533f55bd02f8b043004519d8b642a0.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

然后，用同一个微软账号[登录必应自定义搜索门户](https://customsearch.ai/)。在主界面点击左上角的「新建实例」（New Instance）按钮；任起一个名字后确认，进入该搜索引擎的配置界面。

![](https://cdn.sspai.com/2022/01/17/84741e297d4529c0b297796926113322.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

此时，注意到**界面顶部有两个大标签：「配置」**（Configuration）和**「生产」**（Production）。熟悉云服务的读者可能一看便知含义，其他读者可以将这两者的关系简单理解为**「草稿」和「正式版」**：「配置」部分中的调整并不会立刻生效，而是要通过点击右上角的「发布」（Publish）按钮，应用到「生产」环境后才会反映出来。

要添加搜索目标，方法是「配置」>「搜索体验」>「活动」选项卡上，输入目标网站的网址。注意必应不支持 Google 那样的通配符，因此**这里需要输入纯粹的网址**；同样地，勾选下方的「包含子页面」（Include Subpages）。

![](https://cdn.sspai.com/2022/01/17/a770c9130ff2b3150aff39c4d77ff017.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

除了手动逐一添加，必应也支持**批量上传网址列表**，格式是包含纯链接的 txt 格式文本文件。

添加好网址后，可以在同一页面进行调整优先级、编辑和删除等操作。此时，已经可以通过右侧的预览框测试搜索效果。

![](https://cdn.sspai.com/2022/01/17/7b706b1d675862e92aa9bdb2409bb215.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

不过，这个搜索功能目前还是个「草稿」，还不能通过公开地址访问和使用。为此，切换到托管用户界面（Hosted UI）选项卡，根据自己的喜好调整搜索界面外观后，**在第四步的「订阅密钥」（subscription keys）填写在开头保存的密钥**（重要，略过则无法完成后续步骤）。

![](https://cdn.sspai.com/2022/01/17/2a37f645380983733308710cfcaa8a79.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

确认右侧预览效果无误后，**点击右上角的「发布」（Publish）按钮**，将当前配置发布到生产环境。

此时，切换到「生产」（Production）>「终结点」（Endpoints）>「托管用户界面」（Hosted UI）选项卡。在右侧，将「市场」（Market）选择为「zh-CN」（即中文简体）。这样，即可在下方的 HTML 终结点（HTML Endpoint）部分看到可供公开访问的自定义搜索网址了，形如：

```
https://ui.customsearch.ai/hosted-page?customconfig=[配置编号]&version=latest&market=zh-CN&q=[关键词]
```

与 Google 方案类似，你可以收藏这个页面，或者将其添加为浏览器、启动器等的自定义搜索引擎。

![](https://cdn.sspai.com/2022/01/17/817457c98d119e26ea1b8b76ca7b6fd3.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

此外，由于必应自定义搜索的网页版和 API 共用一套计费标准，API 在免费档位的次数和频率限制内也是免费的。有兴趣的读者也可以试试通过其 API 来访问自定义搜索功能，具体可参考[官方文档](https://docs.microsoft.com/en-us/bing/search-apis/bing-web-search/reference/endpoints)，在此不赘述。
