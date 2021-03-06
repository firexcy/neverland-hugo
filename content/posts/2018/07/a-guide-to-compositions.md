---
title: "疑难符号使用与输入指南"
date: "2018-07-05"
tags:
  - "typography"
---

## 一、引言

在电脑和手机上，文本输入是我们再熟悉不过的操作。但提到输入，很多人首先想到的只是输入文字，而符号——包括标点符号和特殊字符——的输入则往往不太受到重视。观念上，这似乎是一件非常琐碎而简单的事情，不值得单独讨论和专门学习。

真的是这样吗？请试试看能不能答得出下面几个问题：

英文中的右单引号、缩写词中的撇号和表示英尺的「撇」是一个符号吗？它们是垂直的还是弯曲的？

![](https://cl.ly/sflt/quiz1.png)

表示一个范围时，连接前后数字的横线符号是键盘上加号左边的那个吗？这个键是「减号」吗？

![](https://cl.ly/sgj4/quiz2.png)

外国人名字里的圆点是怎么打出来的？这个圆点到底有多大？

![](https://cl.ly/sgDF/quiz3.png)

从网上甚至很多印刷品文章中的使用情况看，人们对符号用法和输入方法的掌握程度并没有自己想象的那么乐观。但是，只要掌握少量的基础知识和技巧，正确输入和使用符号是非常轻松的。下文中，我将总结一些容易误用的符号，并说明各平台上输入符号的一般方法。结合我的学习和使用体会，本文将不会按符号的用法来归类，而是按符号的「外形」归类，将几组形态类似而经常被互相混淆的符号放在一起比较说明。

![本文涉及的主要符号及其输入方式](https://cl.ly/sgSJ/compositions-list.png)

## 二、引号和各种「撇」

### 引号的弯与直

把引号放在最前面说，不是因为它的使用率最高，而是因为它最容易被用错。众所周知，引号不是**一个**符号，而是**一对**符号，有前后之分；它们是双引号 `“”`（U+201C 和 U+201D Left/Right Double Quotation Mark）或单引号 `‘’`（U+2018 和 U+2019 Left/Right Single Quotation Mark），即所谓的「弯引号」。但是，键盘上却只有一个「引号」键，而且输入的也不是「正牌」的、弯曲的引号，而是垂直的 `'`（U+0027 Apostrophe）和 `"`（U+0022 Quotation Mark），即所谓的「直引号」。这种违反直觉的安排实际上是打字机时代的遗产：为了节省空间、减少机械结构，打字机的键位安排思路是「能少一个是一个」，而现代键盘则为了迁就习惯而将其原封不动地继承了下来。

![两种引号](https://cl.ly/sgu6/quotes.png)

中文用户可能对这个问题感受不太明显，因为任何中文输入法下的引号键都会输出弯引号。「按一次是前引号，再按一次是后引号」是小学信息课就会教的口诀（尽管显然不严谨）。但对于几乎不需要输入法辅助的英文用户来说，图省事直接用直引号就是再常见不过的做法。因此，引号的「弯」「直」之辨是西文排版的入门课之一。翻开任何一本英文排版书籍，几乎都能找到对于直引号痛心疾首的批判，理由也很明显——太丑。在排版中使用直引号（常常也被嘲讽地称为「打字机引号」或「呆（dumb）引号」）被认为是一种偷懒或业余的行为。

macOS 和 iOS 作为一家设计导向的公司的产品，显然不会「放任」这种审美上的瑕疵，默认情况下所有的直引号都会被自动纠正为成对的弯引号。以 Word 为代表的多数排版软件也会这么做。但对于工作内容涉及代码编辑的用户来说，这种替换显然会造成困扰（代码中的引号几乎都是直引号）。因此，建议关闭引号的自动纠正功能（多数软件的「编辑」>「替换」菜单下），而使用组合键来输入引号：左侧的双引号和单引号分别是 Option + `[` 和 Option + `]`，而对应的右侧引号则只要分别加按 Shift 键。iOS 的键盘默认输入的已经是弯引号，直引号可以通过长按获得。

### 要不要用中文引号？

但引号输入还有一个非常中国特色的问题，即是否应该使用「直角引号」（`「」`，U+300C 和 U+300D Corner Brackets）。

不可否认，尽管国家标准规定中文引号的形态与西文相同，但直角引号在中文互联网上的人气似乎已经盖过了前者，成为了很多在线社区的成文或事实标准。至少在两三年前，提供切换引号形态的设置选项就成了输入法的通行做法；新款国行 MacBook 甚至直接把直角引号印到了键盘的大括号键上，中文状态下可以直接用 Shift + `[` / `]` 打出，iOS 的中文键盘上则可以通过长按引号键输入。

![Mac 产品的新中文键盘布局（来源：Apple）](https://cl.ly/sgjE/MLA22CH.jpeg)

问题是，很多人换用直角引号只是一种随大流的选择，并不了解为什么要这么换、和原来的用法比起来有什么优劣，以至于经常打出 `「‘’」` 这样不伦不类的用法（单层引号的内部应当嵌套双层引号 `「『』」`，macOS 在输入时会自动处理）。实际上，对直角引号的提倡是从知乎开始的，可以追溯到 2012 年前后。在知乎上以「直角引号」为关键词搜索，仍然可以看到当时大量的讨论和争议。

![两种引号在不同网页设定下的显示效果](https://cl.ly/sgFD/square-quotes.png)

概括地说，直角引号的提倡者主要有如下理由：其一，与冒号、分号等标点都有用于东亚文字的全角版本不同，弯引号缺少一个中文专用的版本。无论中文西文，弯引号都是同样码位上的同一对字符，其外形完全取决于字体。在中西文混排的场合，弯引号常常因为套用西文字体而显示为半角宽度，与汉字和其他中文标点差异很大，从而对排版效果产生不利影响。其二，提倡者认为直角引号的形态与方块字更加契合。其三，直角引号在香港、台湾和日本都是官方规范，这也为将其「进口」到简体中文世界提供了依据。

本文无意对两种引号的选择作出结论，也缺乏这么做的资格和必要。但无论你站在哪一边，都应当是基于技术上或审美上理由的自主选择，而不是出于对标准原教旨式的遵从（请注意两岸涉及标点符号的标准文件都不是强制性的）或无谓的「格调」「潮流」之争。

### 撇号和角分符号

最后，有必要提一下撇号和角分符号，它们都是常见的、因为形态与引号相近而经常被误用和混用的符号。

撇号（apos tro phe）是英文中用来标示所有格（John’s apple）和省略（isn’t）的符号，其正确形态是一个右单引号，即 `’`（U+2019 Right Single Quotation Mark），因此同样需要注意避免用成直引号。另外，对于 rock ’n’ roll 这样连用撇号的情形，要特别注意撇号的方向：字母 n 两侧的撇号很容易被系统自动「修正」为一对引号；这也是为什么提倡尽可能直接用组合键输入引号，而不是依赖软件纠正。

角分符号（primes）是常见于度量单位的符号，包括表示英尺、分钟等的角分 `′`（U+2032 Prime）和表示英寸、秒数等的角秒 `″`（U+2033 Double Prime）。这组符号在 macOS 和 iOS 上都没有快捷的输入方法；不少西文字体也没有包含它们，正确输入很多时候反而会带来不佳的排版效果。因此有观点认为，除了在用到时调用符号面板输入，用直引号来代替也是可接受的妥协方案，并且可以开启斜体来更好地模仿原符号的倾斜。（但注意不要用弯引号，因为角分符号的形态无论如何不可能是弯曲的。）

![角分符号的几种常见用例对比](https://cl.ly/sgRW/prime.png)

## 三、各种「横线」

另一组误用频率不亚于引号的符号，大概就是包括连字符、连接号和破折号在内的各种「横线」形符号了。它们一方面数量繁多且形态相近，另一方面在中英文中的形态和用途并不完全对应，从而更容易产生误认。

![各种「横线」在中英文中的用途对比](https://cl.ly/sgnt/en-cn-dashes.png)

为了方便讲述和记忆，我们按照从短到长的顺序来梳理这些符号。最短的横线是**连字符** `-`（U+2010 Hyphen-Minus），也是最容易输入的，就在键盘上数字 0 的右侧。但与多数人的直觉不同，连字符在大多数时候并不需要手动输入：它的主要用途是将较长的西文单词断成两行，而这是由软件自动加在行尾的。需要手打连字符的场景基本只有在多个部分组成的名称或词汇内部，例如 Rolls-Royce、whack-a-mole，等等。

那为什么我们会觉得连字符是一个高频符号呢？这是因为它经常被当作更长一些的**连接号**（dash）用了。在西文中，连接号有一短一长两个，分别是 `–`（U+2013 En Dash）和 `—`（U+2014 Em Dash），它们的名字来源于活字印刷术语——「em」是金属活字的垂直长度，「en」则是前者的一半。

![金属字模图示，图中 c 的长度就是 1 em。（来源：维基百科）](https://cl.ly/sffe/em-length.png)

连接号在英文中的用途非常广泛。先看较短的 en dash。各种数字（pages 1–10）、日期（Tuesday–Thursday）、年份（1949–2018）、地名（a Beijing–Shanghai train）之间都是用它来连接。它也用在一些由两个人共同提出的理论、概念中（Herfindahl–Hirschman index）。至于较长的 em dash，它在英文中的作用很像中文的破折号，用于句中的插入语前后（类似逗号）、引出补充说明或列举（类似冒号）、标示中断或间隔等。

两种连接号在 macOS 上可以分别通过按 Option + `-`（即连字符键）或 Option + Shift + `-` 得到。iOS 的英文键盘上，长按连字符键就能在弹出的浮动条中看到它们。

以上说的是英文中的情况，中文里的这些「横线」又是如何使用的呢？首先，连字符在中文里基本是没有用武之地的。其次，对于起连接作用的符号，国内标准将其细化为短横线、一字线和浪纹线三种，分别对应前面所说的 en dash、em dash，和 `～`（U+FF5E Fullwidth Tilde）。至于三种形态的各自用途，国标的列举过于繁琐，简记方法是：一字线（em dash）和浪纹线可以互换，用于表示时间、地域、数字的起止；其他表示「连接」的场合都用短横线（en dash）。

至于我们最熟悉的破折号，实践中的用法并不统一。最通用的做法是连续使用两个 em dash `——`。这种用例的问题在于它本质上还是两个独立的字符，因此如果字体设置不正确，会产生中间断开的视觉效果，不符合规范；在一些极端情况下，还会出现后半截被挤到下一行开头这一令人困惑的情况。因此，排版中有时也会使用占两个汉字空间的 `⸺`（U+2E3A Two-Em Dash）充当破折号，相应的问题当然就是输入不便。

至于这些符号在中文环境下的输入，在 macOS 上与英文基本没有区别，多出的破折号通过 Shift + `-` 输入也是人尽皆知。iOS 上的情况比较混乱，可以参看下图。

![iOS 键盘上的各种「横线」](https://cl.ly/sfT7/dashes-on-ios-keyboards.png)

## 四、各种「圆点」

### 句号

在中文中，除了最常见的圆圈形句号 `。`（U+3002 Ideographic Full Stop），理工学科的用户一定也经常见到用与英文句号形态接近的全角「句点」`．`（U+FF0E Fullwidth Full Stop）充当句号的做法。这是为了避免和数字 0、字母 o 等「圆圈」形字符混淆（想象一下它们被用于下标且位于句尾时的情形）。另外，国内参考文献标准中，作者、题名等各属性间也是使用 `．`，而不是英文句号。

![阿列夫–零还是阿列夫–圈圈？](https://cl.ly/sgOL/fullwidthdot.png)

macOS 的中文输入法没有直接输入全角句点的组合键，需要先按 Shift + 6 打开标点输入面板，按一下 tab 键切换到「符号」选项卡，然后向下翻找。iOS 上，全角句点可以通过长按中文键盘上的英文句号按键找到。

### 省略号

中文状态下输入省略号几乎人人都会，Shift + `6` 组合键会输出连续的两个`…`（U+2026 Horizontal Ellipsis），这也是中文省略号的标准形态。问题在于，按照国内规范，省略号在高度上应当居中，因此也有拿两个数学专用的 `⋯`（U+22EF Midline Horizontal Ellipsis）充当省略号的做法（iOS 中文键盘上长按省略号就能看到这个字符）。这实际上是一种「以（造）形害（语）义」——标点符号的形态应该是通过调整字体来控制的——并不值得提倡。

掌握程度普遍较差的是英文状态下省略号的输入方法。实际上这也是很多英文用户搞不清楚的，原因还是拜打字机所赐。当时，由于键盘上没有省略号的一席之地，人们的权宜之计是连用三个句点 `.`（U+002E Full Stop）代表省略号，有时还在两两之间加上空格，即 `. . .`。这种不规范的习惯被保留至今。虽然大多数自动纠正机制都会把三个点自动替换成正确的省略号 `…`，但正宗的输入方式还是值得一记：Option + `;`（分号键）。iOS 的英文键盘上可以通过长按句号来输入省略号。

![省略号的打字机式用法和规范用法](https://cl.ly/sfsQ/ellipses.png)

### 间隔号

间隔号这个名字听起来或许令人有些陌生，实际上却是一个被频繁使用的标点，外文人名（史蒂夫·乔布斯）、词曲名（《天净沙·秋思》）、节日和纪念日（「3·15」消费者权益保护日）中的「圆点」，用的都是间隔号。

根据标准，间隔号对应的字符是 `·`（U+00B7 Middle Dot）。但由于在形态上与其相似的符号太多，很多人在用到时会打开输入法的符号列表随手找一个，经常中枪的包括 `•`（U+2022 Bullet）乃至 `●`（U+25CF Black Circle），看起来颇为古怪。还有一些用户因为不了解间隔号的输入方法，用连字符、空格，甚至英文句号代替，这显然也是不规范的。

![哪个才是乔布斯？](https://cl.ly/sh6z/middots.png)

实际上，间隔号的输入非常容易：大多数中文输入法将这个字符映射在 `~` 键（即紧邻主键盘区数字 1 左边的按键）上，直接按下即可输入。iOS 的中文输入法直接提供了间隔号。

需要指出，按照国标，间隔号在形态上应该占据一个汉字的宽度。这就产生了一个和中文弯引号一样的问题：中文的间隔号没有单独的码位，在与西文混排时往往因为调用西文字体而显示为半角宽度。这个问题目前没有很好的解决方案。一些观点指出可以使用日文的 `・`（U+30FB Katakana Middle Dot）来代替，但这显然存在输入难度和兼容性上的问题。

## 五、「看不见」的符号

### 回车的「软」与「硬」

将回车键说成是「符号」似乎有些奇怪，但如果打开 Word 敲一下回车，你将能看到一个浅蓝色的段落标记，并且可以选中、移动和删除，这就是它符号身份的证明。回车不仅被程序当作符号看待，而且有一个专门的码位（U+000D Carriage Return）。当然，它确实具有区别于普通符号的特殊身份——控制字符；换句话说，其主要作用是传递某种控制功能。

与回车相关的一些疑惑也正来源于这种双重身份。例如，Word 文档打开项目编号时，按下回车就会让段落序号递增，但有时我们只是想让原来的段落新增一行；在微信中，按下键盘右下角的蓝色按键（相当于回车）就会把信息发出去，但有时我们只是想给消息分个段。在这两种情形下，软件都把回车操作理解为控制功能（新建段落或发送消息），尽管我们预期的结果更多是语义上。那么，有没有一个不带控制性含义、纯粹表示换行的「符号」呢？答案是肯定的，这就是所谓的「软回车」，它在 Unicode 中的身份是 U+2028 Line Separator。

![软回车与硬回车](https://cl.ly/sfm6/hard-and-soft-returns.png)

桌面系统上，软回车的输入方式取决于软件。大多数字处理软件可以用 Shift + 回车来获得软回车；但在一些该组合键被其他功能占用的软件中（如 Numbers），则也可能是 Option + 回车。iOS 上，不借助外接键盘输入软回车是相对困难的，比较可行的方式是为其设定一个自动替换短语。部分设计周全的 iOS 应用也可能在软键盘上方的工具栏中提供这一符号（如 OmniOutliner）。

「软」「硬」回车的区别主要适用于带格式文本。纯文本不存在「段落」的概念（只有「行」），也就无所谓「软」和「硬」。至于比较特殊的 Markdown，连续的两个换行符对应渲染结果中的新段落，而如果想得到一个「软回车」，则要输入两个空格，然后一次回车。

最后要提醒的是，回车不是用来调节排版的工具。任何的行间距、段落间距都应该使用排版软件的样式设置来处理；开启新页的方式不是一路回车到底，而是插入分页符。

### 空格和制表符

将输入空格的方法拿出来单说似乎也是非常可笑的。但如果在 Unicode 字符集中搜索「space」，你将会看到十几种不同的「空格」。它们并不只是「回字的四种写法」那样无聊的学究，而是切实地在排版和字符显示中发挥不同作用。

对于日常使用，除了最普通的空格（U+0020 Space），最好还能了解不换行空格（U+00A0 No-Break Space）的用法。如其名称所示，不换行空格最主要的作用就是禁止在其位置换行。譬如，在 `10 Kg`、`© 2018` 这样的用例中，如果数字和单位、符号与文字之间的空格处发生断行，显然会使读者产生困惑。这时，用不换行空格就能起到将空白前后标记为一个整体的作用，强制使其位于同一行。此外，在 HTML 和 TeX 等标记语言中，连续的多个普通空格会被当作一个空格看待，用不换行空格就可以绕开这种限制，获得连续的空白——这也是为什么它又被叫做「硬空格」（hard space）。

![普通空格（上）与不换行空格（下）在两端对齐时的区别（注意红字部分）](https://cl.ly/sfTR/nbsp.png)

不换行空格的输入方式因软件而异，如在 Pages 里是 Option + 空格，而在 Word 里是 Option + Shift + 空格，HTML 语言中则可以用 `&nbsp;` 来标示。

与回车一样，空格也不应被滥用为控制排版的工具。标题居中、段落缩进（即「开头空两格」）应当靠排版软件的样式设置来实现。靠空格实现的上述效果是灾难性的。

最后，tab 键对应的制表符（U+0009 Horizontal Tabulation）也是一个与空格相似的字符，通常占据四个空格的位置。从名字可以看出，制表符本来是用来在打字机上制造表格效果的，但这在富文本流行的今天已经越发显得过时和简陋了。如今 tab 键更多是被单纯用来控制段落缩进。在编程界，代码缩进该用 tab 还是空格是一场不亚于 Vim 与 Emacs 之争的圣战，但这超越了本文的讨论范围。

## 六、疑难字符拾遗

### 带声调字母

带声调字母在英文中是很少用到的，在中文世界反而因为汉语拼音的普及而变成了常见需求。原理上，输入带声调的拼音字母是通过「借用」附加了变音符（diacritic）的拉丁字母来实现的，其与拼音四声的对应关系分别是：阴平——`¯`（长音符 macron）、阳平——`´`（锐音符 acute）、上声——`ˇ` （抑扬符 caron），和去声——\`\`\`\`\`（沉音符 grave）。

带声调字母的输入在 iOS 上非常简单：只要按住对应的字母键，就可以在弹出的浮动条中看到它们。这一技巧同时适用于中英文输入法，但带上声 `ˇ` 的字母只在中文键盘上才能找到。macOS 上，最简单的方法是切换到中文输入法，直接输入需要注音的字的拼音，然后按 Tab 键，就会发现韵母上出现了声调。反复按 Tab 直到看到所需的声调，然后直接回车即可上屏。另外，较新版本的 macOS 借鉴了 iOS 上的交互方式，长按键盘上的普通字母即可看到与其相关的带声调版本。

![带声调字母的输入](https://cl.ly/sgKR/accented-characters.png)

### 数学符号

最常用的加减乘除四则运算符号中，只有加号 `+`(U+002B Plus Sign）是可以在键盘上直接打出来的。键盘上的减号实际上是连字符，而不是数学上的 `−`（U+2212 Minus Sign）；乘和除则干脆没有（分别应该是 U+00D7 `×` Multiplication Sign 和 U+00F7 `÷` Division Sign）。又因为与减号和乘号形态相近的符号过多，即使用符号面板输入也非常容易选错。如果有经常使用这些符号的需求，建议为它们各自指定一个自定义短语。

此外，macOS 和 iOS 的输入法都支持输入符号名称的拼音时在候选词中显示符号，但通过这种功能打出来的四则运算符号并不是上述标准形式，而是 emoji 化的「加粗版」（在 Unicode 中属于 Dingbats，即装饰字符的范畴），在规范用途中要注意避免。

我们还知道，一些字母在科学上具有特殊含义。有时候，是否大写、是否加粗、是否使用衬线体等样式上的区别，都会对语义产生影响（例如函数符号就是小写、斜体、衬线体的 \`\`）。这些符号规范的输入方法不是输入普通字母，然后用字体设置改变样式，而是使用 Unicode 中 [Mathematical Alphanumeric Symbols 区块](https://www.unicode.org/charts/PDF/U1D400.pdf) 的专用字符。macOS 上可以在字符输入面板的 Maths Symbol 分类中找到这些符号，iOS 上则只能依靠自定义短语或第三方 app。

![手动输入的「数学符号」和 Unicode 专门指定的数学符号，注意两者在宽度和形态上的区别](https://cl.ly/sfiK/math-symbol.png)

顺带一提，在 Twitter 上有时能看到一些非常奇特的用户名，明显与系统默认字体不同。这实际上就是利用了上述数学字符的样式是特定的，因此在显示时具有无视系统字体的「特效」的原理。

### 版权、商标符号和其他

常用的版权和商标符号（`©`、`®`、`™`）在 macOS 上可以分别通过 Option + `g`/`r`/`2` 输入。Word 的自动纠正则会将 `(c)`、`(r)` 和 `(tm)` 替换为对应的符号形态。与它们有关的常见误用有两种：一是用成了中文输入法所提示的 emoji 版本；二是手动输入 TM 字样，然后改成上标。

事实上，macOS 几乎为每个 Option + 字母/数字键的组合都 [安排](https://forlang.wsu.edu/help-pages/help-pages-keyboards-os-x/) 了一个特殊符号，如果再加按 Shift 键，则可以直接输入的字符还有更多。读者如果有兴趣不妨依次试一遍，并挑一些自己用得到的专门记忆。

![macOS 键盘在按下 Option 和 Option + Shift 时的符号映射](https://cl.ly/sh51/option-keyboard.png)

## 七、符号输入方法概述

当然，很多时候我们用错符号，未必是因为不知道该用什么，而是因为不知道如何输入、或者因为觉得过于麻烦而不愿输入。虽然上文在说明符号用法的同时，都给出了各自的输入方式；但篇幅所限，提到的符号也只是 Unicode 的冰山一角。为此，在文章的最后，让我们归纳一下常见的符号输入方法，以便今后在遇到任何符号输入需求时都能应对。

概括而言，主要存在下列四种方法，它们在学习成本、效率、灵活性三方面有不同的表现：

- **通过组合键：**即通过按下特定的按键组合来输入字符，如通过 Option + `[` 来输入左双引号 `“`。这种方法的效率最高，但缺点是存在学习和记忆成本，并且可能和第三方软件的快捷键冲突。
- **通过输入面板：**即通过在专用的符号输入窗口或软键盘中点击来输入字符。这种方法的学习成本最低，但使用起来也最麻烦。
- **通过自动纠正：**即由软件自动将形态相近且输入方便的符号替换为正确的字符，例如将两个连字符 `--` 修正为长连接号 `—`。这种方法学习和使用成本都很低，但缺点是不够灵活，在不需要修正时（例如写代码时）需要额外步骤来关闭。
- **通过用户词典：**即预先定义一串易记的输入码和所需字符的对应关系，从而在输入时可以直接从候选词中选取。这种方法的效率、灵活性都较高，但需要花一定成本来设置。

另外，如今的用户每天面对的不只是一台设备，而是不同形态、不同操作系统的多台设备，不同平台对符号输入的支持情况也存在各自的特点：

- **macOS** 是一个对符号输入特别友好的系统。如上所述，默认键盘布局为各类常用特殊字符提供了组合键。任何文本框中，都可以用 Control + Command + 空格呼出功能完善的 [符号输入面板](https://support.apple.com/zh-cn/ht201586)，可以分类检索或者按名称搜索；中文输入法下按 Shift + `6` 可以呼出标点选单。macOS 还具有系统级的 [自动替换和自定义短语](https://support.apple.com/kb/PH25699?locale=zh_CN) 功能，并且可以通过 iCloud 与 iOS 设备同步。
- **Windows** 的情况则稍微麻烦一些。Windows 的默认键盘布局没有提供太多符号输入组合键；由于软件开发环境相对割裂，也很难提供系统层面的文本替换功能，基本需要依靠各个应用自行支持（例如 Word 的 [自动更正](https://support.office.com/zh-cn/article/%e9%92%88%e5%af%b9%e5%a4%a7%e5%86%99%e3%80%81%e6%8b%bc%e5%86%99%e5%92%8c%e7%ac%a6%e5%8f%b7%e9%80%89%e6%8b%a9-%e8%87%aa%e5%8a%a8%e6%9b%b4%e6%ad%a3-%e9%80%89%e9%a1%b9-e7433b94-f3de-4532-9dc8-b29063a96e1f?omkt=zh-CN&ui=zh-CN&rs=zh-CN&ad=CN)）。不过，Windows 内建了一个称作「字符映射表」（Character Map）的输入面板，可以在开始菜单的附件中找到；同时，系统的很多位置可以通过输入字符的 Unicode 编码，然后按 Alt + X 组合键来获得该字符（例如，输入 `221A` 后按 Alt + X 即可得到根号 `√`）。
- **iOS** 在早期版本中的符号输入功能比较羸弱。但经过多年的进化，如今的内建输入法已经比较完善。无论中文键盘还是英文键盘，都提供了很多现成的常用字符，在一些键位上长按还可以看到与其相关的更多字符。此外，可以安装 [Symbolay](https://itunes.apple.com/us/app/symbolay/id854373775?mt=8%0A%0A)、[UniChar](https://itunes.apple.com/us/app/unichar-unicode-keyboard/id880811847?mt=8) 这类第三方 app 来获得字符分类列表、键盘扩展等功能。
- **Android** 平台的碎片化较为严重，甚至不存在一个共同的默认键盘，因此无法作出概括性的评论。如果只考察第一方 app，Gboard 和 Google 拼音输入法都能直接输入大量特殊符号。另外，得益于平台的开放性，安装第三方的文本替换和符号输入工具是非常容易的，在 Play Store 上以 Unicode 为关键词搜索就能找到大量这类 app。

![Windows 和 macOS 的字符输入面板](https://cl.ly/sfUk/composition-panels.png)

综合上述情况，我的建议是采用**「分级处理」**的策略应对符号输入的需求：

- 对于常见、高频的标点符号（将在下文列举），应当记住直接输入的按键组合。
- 对于常用但在移动设备上输入不便的符号，或者相对不常见、但自己使用较多的符号（例如理科可能会较多地用到专用数学符号），最好用文本替换功能为其指定输入码，以便用到时快速、准确地输入。
- 对于其他低频使用的符号，偶尔用到时使用符号输入面板（电脑上）或第三方 app（移动设备上）即可，没有必要花费过多时间提前学习组合键或设置文本替换。

此外，还有很多效率类工具可以为符号输入提供便利，例如跨平台的 TextExpander，macOS 上的 LaunchBar、Keyboard Maestro，Windows 上的 AutoHotKey 等。但这些工具的主要功能并非符号输入，在此不过多赘述。

最后，考虑到符号数量繁多，在遇到陌生符号或者拿不准用法时，下面这些文档和工具可以作为参考：

- Unicode 的官方 [字符列表](https://www.unicode.org/charts/) 是符号名称、形态和用例的权威参考，只是检索起来相对不便。
- [Unicode Table](https://unicode-table.com) 是一个非常全面和美观的网页工具，可以按照编码、名称等检索 Unicode 字符，还可以将陌生符号粘贴到搜索框来反向查找。
- [GB/T 15834—2011](http://www.moe.gov.cn/ewebeditor/uploadfile/2015/01/13/20150113091548267.pdf) 是中国关于标点符号用法的国家标准，强烈推荐通读。
- [《中文排版需求》（CLReq）](https://www.w3.org/TR/clreq/) 是 W3C 描述中文排版需求与问题的文件，目前尚处于草案阶段，但已经比较完善。文档的 §3.1（标点符号与其排版）及附件 A（中文标点符号表）对中文标点的相关技术问题做了细致的说明。

![网页工具 Unicode Table 和 iOS 应用 UniChart](https://cl.ly/shC7/char-tools.png)

## 八、结语

必须承认，上文归纳的很多符号的区别是细微的，有的离「吹毛求疵」只有一步之遥，因此难免受到质疑：有必要吗？毕竟，圆点的大小和横线的长短似乎是很无聊的区别，用直引号代替弯引号、用连字符代替连接号也是大众做法，「几十年就是这样下来」。人生苦短，为什么要把时间花在学习和输入符号上？

首先，符号的正确搭配能让文本更加美观。长文本中穿插的符号就像湖面上泛起的波澜、绸缎上镶嵌的装饰，为版面带来节奏和纹理。对我来说，这一个理由便足够了——美本身就是值得追求的。从更实用主义的角度说，符号不只是文字的附庸，而是本身就具有语义上的重要作用。否则，句读也就无以成为专门的学问，一个逗号也就无以 [引发涉及数百万美元的诉讼](https://www.nytimes.com/2018/02/09/us/oxford-comma-maine.html)。

符号的规范程度也能反映使用者对文本的用心程度。当专业人员将使用直引号斥为「dumb」时，他们指责的或许并不是这个符号本身，而是使用者的态度：如果一个人都不愿意多花一点精力输入成对的引号，怎么能让人相信他会认真对待自己写出的文章呢？我的阅读经验也印证了这一点：虽然标点使用考究的媒体未必是（尽管更可能是）可信赖的，但胡乱使用标点的媒体几乎一定不可能输出什么有价值的内容。

至于输入正确符号的成本问题，如果说在打字机时代因为硬件条件的限制而采用妥协性的方案是可以接受的，那么在软件功能强大、输入方式多元的当今，还以「麻烦」为借口坚持使用不规范的符号，就显得没有什么说服力了。而且，本文在一开始就给出了解决方案：结合自己的使用频率，综合使用组合键、输入码和输入面板。在写这篇文章的过程中，我思考怎么故意输错符号的时间，反而远多于输入正确符号的时间，因为后者经过反复操作已经是肌肉记忆的一部分了。

当然，本文并不主张在任何时候都要一板一眼地使用最规范的符号。正如没有必要在口语对话中用书面表达一样，私人、日常的交流需要一些非常规的用法来表达更微妙的意涵，这也被颜文字、emoji 的大行其道所印证。何况，无论是在正式场合追求规范的符号，还是在非正式场合选择更加活泼的变通形式，最终的目的都是一致的——用符号更好地表情达意，拓展文字传递信息的带宽。
