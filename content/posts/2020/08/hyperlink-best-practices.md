---
title: "小议超链接的规范使用"
date: "2020-08-31"
tags:
  - "design"
  - "opinion"
---

超链接是互联网最突出的功能之一，添加超链接也是所有网络用户需要掌握的基本功。

然而，「会用」超链接并不等于能「用好」超链接。或许是因为操作太过容易，我们在添加超链接的时候往往颇为随意，而不会仔细考虑做成超链接的内容和地址是否合理。

回想一下，你是否遇到过下面这样的超链接用法，或者自己这样用过：

1. 将操作指示作为链接文本：「[点击这里](http://example.com/)」「[查看相关信息](http://example.com/)」「[🔗](http://example.com/)」
2. 将网址作为链接文本：[http://example.com/](http://example.com/)
3. 为连续的词语添加超链接作为列举手段：「苹果在过去几个月和开发者可谓 [冲](https://www.theverge.com/2020/6/16/21293419/hey-apple-rejection-ios-app-store-dhh-gangsters-antitrust) [突](https://www.macrumors.com/2020/08/13/apple-removes-fortnite-from-app-store/) [不](https://arstechnica.com/tech-policy/2020/08/apple-apologizes-to-wordpress-no-longer-requires-free-app-to-add-purchases/) [断](https://www.engadget.com/apple-epic-app-store-account-212948667.html)。」
4. 将一长串话作为链接文本。

这些用法都是值得商榷的。

超链接的正确用法并不是个新话题。早在 2004 年，谷歌工程师 Jed Hartman 就撰文讨论过 [链接文本的合理用法](https://www.kith.org/jed/2004/12/09/link-text/)；上面列举的几种不当用例正是来源于该文。

一些开发文档也涉及了这个问题。谷歌的 [《开发文档风格指南》](https://developers.google.com/style/link-text)（Developer Documentation Style Guide）就为此专设一节，并指出链接文本应该「描述读者点击链接后将会看到的内容」，如被引文档的标题或对其内容的描述。Mozilla 维护的 MDN 文档库也讨论了「[链接最佳实践](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks#Link_best_practices)」（link best practices），同样建议回避上述几种做法。

但正如我们所见，时至今日，超链接的使用在实践中仍然是很随意的；不少网站超链接的外观设计也往往不尽人意。

为此，我想从链接文本和链接地址的选择、链接外观的设计等方面，讨论自己认为较优的用法，希望能为超链接的规范使用提供一些参考。

## 一、链接文本的选择——追求「名副其实」

### （一）从 HTML 标准看链接文本的要求

要回答链接文本如何设置，首先要从**什么是超链接**说起。

根据 HTML 标准，[超链接](https://html.spec.whatwg.org/multipage/links.html#hyperlink) 是「指向其他资源的链接，通常由用户代理（一般即为浏览器——笔者注）展示给用户，使用户可以令用户代理导航到这些资源」。

此外，超链接通常是通过 [「锚」（anchor）元素](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-a-element)（`a`）构造的；当一个锚元素含有 `href` 属性时，该元素就代表一个由其内容标记（label）的超链接。

这些定义固然晦涩，但我们仍然可以从中得出一些有用结论：

1. [HTML 元素是有「语义」（semantics）](https://html.spec.whatwg.org/multipage/dom.html#elements-in-the-dom)、也即内在含义的。例如，锚元素的存在就说明「此处有链接，点击可跳转到相关信息」。
2. 锚元素的内容（即链接文本）和其 `href` 属性（即链接地址）之间是**标记**和被标记的关系。换言之，**链接文本要「名副其实」，能够说明链接地址的内容**。

在此基础上，我们就可以说明为什么前面提到的几种「流行」用法是有待商榷的：

第一种用法（将操作指示作为链接文本）的主要问题在于**赘余**。既然锚元素的存在本身就说明有链接、可点击，再加入「点击」「更多」之类的描述，就好像是在说「这是一个有链接的链接」一样，成了同义反复。

早年，并非人人都「认识」超链接，这么写或许还有些教育用户的意义，但这在今天已经不是个问题了。此外，这样的链接文本也无法说明被链接的内容。因此，不妨删去「点击」「更多」，代之对被引内容的说明：

> 要进一步了解某话题，可以参阅 [某文章](http://example.com/)。

第二种用法（将网址作为链接文本）同样会让读者无从知晓其内容。此外，从排版角度，冗长的网址也会给断行、对齐的处理造成不便，影响版面的整洁度。因此，更好的做法仍然是描述链接地址的内容，而不是直接把地址写进正文（当然，因行文需要展示链接地址的场合除外）。

第三种用法（将超链接的连用作为列举手段）可谓有利有弊。一方面，这么做确实具有一定「修辞」功能，可以传达俏皮、讽刺等意味。但正如那些被滥用的「梗」一样，其新意和趣味会随着反复使用而磨损，最终引起读者的厌倦；这么做也违反了「名副其实」的原则，给阅读造成不便。因此，最好还是把「文采」留给别处，用更清晰的方式来列举超链接。

例如，与其使用上述那种抖机灵写法：「苹果在过去几个月和开发者可谓 [冲](https://www.theverge.com/2020/6/16/21293419/hey-apple-rejection-ios-app-store-dhh-gangsters-antitrust) [突](https://www.macrumors.com/2020/08/13/apple-removes-fortnite-from-app-store/) [不](https://arstechnica.com/tech-policy/2020/08/apple-apologizes-to-wordpress-no-longer-requires-free-app-to-add-purchases/) [断](https://www.engadget.com/apple-epic-app-store-account-212948667.html)」，不如原原本本地把具体内容呈现给读者：

> 苹果在过去几个月和开发者可谓冲突不断，先后 [拒收了电邮服务 Hey 的官方 app](https://www.theverge.com/2020/6/16/21293419/hey-apple-rejection-ios-app-store-dhh-gangsters-antitrust)、[下架了人气游戏 Fortnite](https://www.macrumors.com/2020/08/13/apple-removes-fortnite-from-app-store/)、[强迫 WordPress 通过内购销售域名](https://arstechnica.com/tech-policy/2020/08/apple-apologizes-to-wordpress-no-longer-requires-free-app-to-add-purchases/)，并 [「言而有信」地关停了 Epic 的开发者账号](https://www.engadget.com/apple-epic-app-store-account-212948667.html)。

第四种用法（链接文本过长）是否不值得鼓励，现有讨论并未达成共识，但我的观点仍然是应该尽量避免。理由是，如果链接文本很长，它很可能是在摘录或描述被引内容的局部，而非全文；如果给这样的局部引用加上指向原文整体的超链接，不仅不具有对应关系，也不便于读者跳转之后找到相关段落。

因此，更好的做法是把链接加在文章标题上（同时说明被引段落的位置），然后用普通文本做摘录和总结：

> 根据 [某文章](http://example.com/) \[某节、] 的观点，「……」。

另外，不合规范的链接用法还会产生一些较为间接、但同样不容忽视的负面影响。例如，这会**降低网页的可访问性**（accessibility），给依赖于读屏器的用户造成不便，使他们很难通过听到的链接文本判断目标页面的内容（参见 [不同读屏器对于链接文本的处理方式](https://www.deque.com/blog/text-links-practices-screen-readers/)）。又如，搜索引擎在索引网站时，常常 [通过链接来判断网站的关键词](https://support.google.com/webmasters/answer/7451184#uselinkswisely)。如果一个网站的链接文本都是「跑题」的，它给搜索引擎的「印象分」就会大打折扣，**导致搜索排名降低**。

### （二）先问「加不加」，再问「加在哪」

从上文的讨论可以看出，要修正超链接的「问题用法」，只靠给链接换个位置可能是不够的，往往还需要调整甚至重写相关表述。

这是因为，**超链接的质量间接反映了写作的质量**：如果你发现难以从文本中找出合适的部分做成链接，那么很可能是因为行文表述不够具体、充分，信息标注不够明确、规范。

这里，超链接的便捷再次埋下了隐患。过去，我们用括号、脚注提示相关信息，用引注、参考文献表明内容来源。到了面向网页的写作中，这些**传统注记方式的职能在很大程度上被超链接包揽了**。但与此同时，那些原本需要研究、检索支撑的工作，被简化成了复制粘贴网址；原本写成白纸黑字、受读者审视的引文，被藏到了链接背后。在方便的同时，这也为我们提供了「纵容」自己降低写作标准、滥用超链接的借口。

因此，**比起「在哪里添加超链接」，一个更优先的问题或许还是「要不要添加超链接」。**

如果文章讨论的话题线索复杂、众说纷纭，那么我们就有责任先梳理、溯源，筛选出尽可能一手、高质量的来源做成链接，而不是将大把链接一股脑塞给读者，同时产生「内容充实」的良好自我感觉。如果被引文章篇幅较长、内容艰深，或与当前段落的关系并不一目了然，那么我们也有责任作出必要的标注和解释，而不是抛出一个超链接，让读者自己点开「细品」「领悟」。

例如，前段时间，美国国会召集四大科技公司 CEO 的反垄断听证会受到了媒体的广泛关注（可参阅 [我介绍此事的文章](https://type.cyhsu.xyz/2020/08/big-tech-congressional-hearing/)）。不少报道在行文中提及了微软 20 年前受到的司法部指控，以此介绍美国法院的反垄断判案标准。

这个案例引用当然是切题的，但到了为其添加超链接时，很多文章就颇为随意，一般都选择链接到自己网站的其他文章，或是当年的媒体报道。然而，这并不符合前面介绍的「名副其实」原则（最相关的文件应当是判决书，或至少是对判决结果的报道），也不足以使读者了解判决逻辑是什么、从何而来。

实际上，如果遵循法律引注的要求，提及判例应当附上相关案件的完整索引信息和必要的解释说明：

_United States v. Microsoft Corp._, 253 F.3d 34, 59 (D.C. Cir. 2001) (holding that a balancing approach under the rubric of the “rule of reason” is applied for the analysis under §2 of the Sherman Act).

这样，读者不仅能了解案件的当事方（联邦政府诉微软公司）、审理的时间地点（2001 年由联邦法院哥伦比亚特区巡回法庭审理），主要的判决理由（法院可以通过衡量利弊判断垄断行为是否合法），而且如有兴趣进一步探究，还可以自己找到判决原文阅读（《联邦案例汇编》第三辑第 253 卷，第 34 页以下，相关段落位于第 59 页）。

诚然，出于效率和简洁的考虑，网上写作没有必要像学术写作那样一板一眼地遵循引注规范（[Bluebook](https://en.wikipedia.org/wiki/Bluebook) 等引注标准确实也因为繁琐、封闭而颇受诟病）。但功夫有时需要下在那些看不见的地方；如果下笔前对写作对象做了充分的研究，写作时做了充分的说明和标注，「超链接加在哪」几乎不会是个问题。

## 二、链接地址的选择——精简而不失具体

要做出好的超链接，除了关注链接文本的选择，**链接地址的规范性也不应忽视**。

一方面，做成超链接的地址应当尽量**精简**，即在不影响链接功能的前提下，包含尽量少的无关信息。直接从浏览器地址栏复制的 URL 未必适合直接拿来做成链接，因为其中可能包含了很多无关的参数（parameter）。

例如，搜索结果页和邮件通讯中很多 URL 都含有 `utm_source` 等用于流量分析的参数：

```
https://example.com?utm_source=news4&utm_medium=email&utm_campaign=spring-summer
```

将其留在超链接中不仅没有实际功能，而且不利于保护读者的隐私。

又如，在插入商品销售页的链接时，应当从中删除无关的引荐代码（affiliate token）；如果要加入自己的引荐代码，则应当作出明确披露。

另一方面，链接地址又应当足够**具体**，即尽可能精准定位到相关资源。如果引述的内容集中于文章的某一节，那么插入的 URL 最好具体到片段（fragment）。

例如，如果撰文讨论常见的网页标准，那么在插入相关维基词条的链接时，就可以具体到：

```
https://en.wikipedia.org/wiki/Web_standards#Common_usage
```

这样，读者在点击后就可以直接跳转到其中最相关的「Common Usage」一节。

类似地，如果文章涉及 GitHub 代码或 YouTube 视频，也不妨利用它们为特定行号或时间戳创建链接的功能。

前不久，谷歌还为 Chrome 浏览器开发了一个名为 [「链接到文本片段」](https://chrome.google.com/webstore/detail/link-to-text-fragment/pbcodcjpfjdpcineamnnmbkkmkdpajjg)（Link to Text Fragment）的插件，可以帮助用户制作出指向页面上任意文本的链接。遗憾的是，这个插件 [背后的标准](https://wicg.github.io/ScrollToTextFragment/) 仍处于早期草案阶段。在它被广泛采纳之前，更务实的做法或许还是像上文建议的那样，不怕啰嗦地向读者尽量具体描述引文的位置。

## 三、链接外观的设计——平衡谨慎与活泼

最后，超链接的质量并不只取决于文章作者；网站的设计者对此也有一份责任，那就是**合理地设计超链接的外观**。

传统网页中的超链接是其貌不扬的，始终以蓝色文字加下划线的形态示人。但在近年，给链接文本加粗、添加夸张的下划线、换用高饱和度的颜色似乎蔚然成风；超链接俨然成了很多网站彰显个性的秀场。

![Vox 的超链接；彩色粗体的设计在链接密集时让版面不整洁且缺乏层次](https://p178.p0.n0.cdn.getcloudapp.com/items/kpubOn00/vox-link-design.png?v=2089da52ea45f216c9513fbb7031ebe1)

Vox 的超链接；彩色粗体的设计在链接密集时让版面不整洁且缺乏层次

然而，**网页元素的外观应该与其功能相匹配**。正如前文反复强调的，超链接只能说明链接文本存在一个关联页面，而不能说明它相对于上下文更加重要。因此，也就没有理由使其在视觉上过分突出。此外，过度设计超链接还会进一步放大前述滥用行为的危害，让版面效果变得凌乱而没有层次。

当然，这并不是说超链接的设计就只能是死气沉沉的。我就曾见过不少既恰如其分、又不失新意的超链接设计。试举两例：

一是排版设计师 Matthew Butterick 的 [Butterick’s Practical Typography](https://practicaltypography.com/) 网站。这个网站实际是一本电子书，深入浅出地讲解了很多实用的排版技巧和关注点。它的设计抛弃了「下划线 = 超链接」的传统做法，转而通过 CSS 的 `:after` 在每个超链接之后加上一个小红圈，同时链接文本会在鼠标悬停时被淡红底色高亮。这样的设计既降低了侵略感，又保留了视觉提示功能，与中国传统的「圈点」批注有着微妙的相似。

![Practical Typography 的链接设计](https://p178.p0.n0.cdn.getcloudapp.com/items/Jru6yx04/practical-typography.png?v=87528f1d75ff344ed1c90917bed29675)

Practical Typography 的链接设计

二是软件工程师 Jestem Króliczkiem 的个人博客 [beepb00p](https://beepb00p.xyz/)。作为一个技术向、长篇说明文为主的博客，它的设计亮点在于为常用的外部网站（例如 GitHub、维基百科等）的链接添加了 SVG 图标，并为跳转到文内其他段落的链接添加了上下箭头。这些图标的加入不仅使链接对象一目了然，也给原本「素面朝天」的文本页面平添了几分趣味。

![beepb00p 的链接设计](https://p178.p0.n0.cdn.getcloudapp.com/items/12uJRvWW/beepb00p.png?v=10833b8869d7e2ee93d48edd22aee134)

beepb00p 的链接设计

## 结语

你可能已经注意到，本文在讨论各种链接用法时，一直回避使用「正确」「错误」等定性的标签，而代之以「合适」「更好」等评价。的确，超链接的用法和设计并没有成文的标准，而更多是一种「风格」（style）。既然是风格，就没有绝对的对错之分，而是会随着时代、技术、观念等外部因素而变，并且体现着不同写作者、设计者的个性。

然而，随性不等于随意。从小处说，链接的质量体现了作者的态度，反映了文章的质量。往大处说，互联网是由超链接织成的，它的价值也很大程度上取决于超链接的广度、深度和精度。在筑篱修渠成为科技巨头的发展要务、互联网的开放价值备受威胁的今天，用高质量的超链接拓展信息的边界，或许就是我们作为普通用户守护互联网为数不多的方式之一。
