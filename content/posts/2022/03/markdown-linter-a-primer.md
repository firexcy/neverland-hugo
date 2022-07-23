---
title: "给你的 Markdown 挑挑刺——语法检查器入门与进阶"
date: 2022-03-25
summary: "会写 Markdown 的人很多，但写得好 Markdown 的人却很少。有没有什么工具能充当「秘书」，检查文件中的 Markdown 语法和风格，并且提出解决方案、自动修复问题，甚至自动补齐中英文之间的「盘古之白」呢？本文介绍的 Markdown 语法检查器（linter）就能做到。"
tags:
  - "markdown"
  - "explainer"
---

**Note:** This article was published as a member-exclusive post for [SSPAI Prime](https://sspai.com/prime), which is made [freely available](https://sspai.com/prime/story/markdown-linter-a-primer) as a preview and republished here. Please consider subscribing to SSPAI Prime if you find content like this helpful. Thanks for your support.

This article is also another installment in my (informal and implied) series of “nitpicking workflows for writing.” The previous posts in this bucket were concerning misuses and abuses of [punctuation marks](https://type.cyhsu.xyz/2018/07/a-guide-to-compositions/) (2018), [hyperlinks](https://type.cyhsu.xyz/2020/08/hyperlink-best-practices/) (2020), and [formatting](https://type.cyhsu.xyz/2021/03/do-not-shout/) (2021). I humbly offer these as my way of conducting public service.

## 引言

[Markdown 标记语言](https://daringfireball.net/projects/markdown/) 是如今互联网上写作的主流格式，被各类发布平台和创作工具广泛支持。哪怕不熟悉这一语言的用户，也很可能在潜移默化中对 `#`（标题）、`**`（加粗）、`-`（列表）这些 Markdown 风格的标注方式建立起认知。

然而，**会写** Markdown 的人很多，但**写得好** Markdown 的人却很少。这一方面是 Markdown 生态系统自身的问题：[语法变种和实现方式](https://www.w3.org/community/markdown/wiki/MarkdownImplementations) 五花八门，互不兼容甚至相互矛盾。

但另一方面，也鲜有人愿意花时间去仔细阅读 Markdown 的技术规范；大多数人都只是读了一两篇「速成」，就自我批准出师了，对于一些细节问题并未关注；如果在写作中遇到，也是凭想象和直觉随意判断。

由此，就产生了大量语法天马行空、版面张牙舞爪，让读者和排版软件都困惑不已的 Markdown 文件。

当然，每个人精力有限，强求所有 Markdown 用户都去研读标准是不切实际的。那么，有没有什么工具能充当「秘书」，检查文件中的 Markdown 语法和风格，并且提出解决方案、自动修复问题呢？

有编程经验的读者看到这里，或许已经联想到写代码时常用的一种辅助工具——**语法检查器（linter）**。没听说过也没关系：这个词来自于「lint」，本意是指「绒毛」——是的，就是毛衣上、口袋缝里那些讨厌的毛球。这些毛球既影响美观，又容易堵塞洗衣机；引申用来形容代码里的错误语法、混乱版式等问题，可谓形象。

（**注：**
Linter 一词没有完全对应的中文翻译，实践中译为「校验器」或「检查器」的都有，但都无法充分表达 linter 既检查语法问题、又检查版式（风格）等「审美」问题的综合性，也常与另一种只检查是否合乎技术标准的工具 validator 混淆；本文姑且用「检查器」来称呼。）

这跟 Markdown 有什么关系呢？实际上，Markdown 属于一种「[标记语言](https://en.wikipedia.org/wiki/Markup_language)」（markup language），虽然与 Python、JavaScript 这类「编程语言」服务于截然不同的目的，但同样都是通过各种记号（token）来标记文件、表明各部分的不同作用（例如 Python 中的定义、循环控制；Markdown 中的被强调文本、引用段落）。文本编辑器在处理时，也是通过识别这些记号进行语法分析（lexical analysis），进而提供关键词高亮、提取大纲、渲染预览等语法功能。

换言之，在编辑器眼中，Markdown 只不过是另一种「语言」罢了。既然如此，如果能用 [ESLint](https://eslint.org/) 检查 JavaScript，用 [PyLint](https://pylint.org/) 检查 Python，当然也可以造出一个 Markdown 语法检查器，专门给 Markdown 文件「挑刺」。

下面，本文就将依次介绍两种 Markdown 格式检查器：一种**通用于各种 Markdown 文档**，主要用来检查和修复文件中 Markdown 格式标记本身的规范性；另一种则**专用于中文 Markdown 文档**，用来满足一种历史悠久的「强迫症」——中英文之间要加空格。

结构上，本文会考虑不同层次的需求：如果你是 Markdown 初学者，不妨先学习这些检查器的规则文档，了解 Markdown 使用中的常见错误，然后尝试使用所介绍的工具和插件，优化自己的文档。如果你是高级用户，则不妨尝试后续段落介绍的配置选项和命令行工具，定制出反映自己偏好和思考的自动化流程。

## 让 Markdown「干净又卫生」——markdownlint

正如主流编程语言都有不止一种检查器，Markdown 的检查器也有很多竞品，但其中使用者最多、维护最为活跃的要数 markdownlint；这也是 [WordPress](https://wordpress.com/)、[MDN](https://developer.mozilla.org/) 等很多知名开源项目的选择。

markdownlint 有两个版本，分别是 Mark Harrison 基于 Ruby 的 [原版](https://github.com/markdownlint/markdownlint) 和 David Anson 基于 Node.js 的 [移植版](https://github.com/DavidAnson/markdownlint)。由于比较方便部署（例如下文介绍的网页版和 VSCode 插件），Node.js 版在人气和活跃程度上后来居上，本文也优先介绍该版本。

截至本文写作时，markdownlint（Node.js 版）总共有 [50 条规则](https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md)，编号从 MD001 到 MD050，其中有两条已被废弃；Ruby 版则有 [39 条规则](https://github.com/markdownlint/markdownlint/blob/master/docs/RULES.md)。两个版本的规则编号是兼容的，相同编号的规则内容也相同。

这些规则各有分工，有的规范 Markdown 中的空格与留白，有的规范链接的使用，有的则规范标题、列表等具体样式（可阅读文档了解完整的 [分类标签](https://github.com/DavidAnson/markdownlint#tags)）。

具体到内容上，有的规则显得很像「废话」，但确实容易在匆忙中忽略，例如：

- MD001：标题层级一次只应增加一个级别（例如，一级标题后面不能直接来一个三级标题）；
- MD025：一个文档中只应有一个一级标题（对于一些内容管理系统，也包括 [YAML frontmatter](https://jekyllrb.com/docs/front-matter/) 中的 `title` 属性）；
- MD029：数字列表的前缀应为递增的数字（或全部写成 1）。

有的并不影响含义和最终渲染结果，只是为了文件整洁，满足「强迫症」，例如：

- MD005：同一级别的列表，开头缩进的空格数量应保持一致；
- MD012：不应连续出现一个以上的空行；
- MD037：强调标记（`*` 或 `_`）内侧不应紧邻空格。

还有的则见仁见智，更多是审美和「哲学」上的取舍，例如：

- MD026：标题段落不应以标点符号结尾（理由是「标题不是完整的句子」）；
- MD036：不应为整行文字加粗或斜体（理由是「这种情况请设为标题」）；
- MD045：图片应有题注（理由是「方便视觉不便者和读屏器」）。

篇幅所限，这里不一一列举。markdownlint 的 [规则文档](https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md) 非常完整，对于每条规则都给出了描述、实例和说理，本文**强烈建议花些时间逐条阅读**。这既有助于自己写出更规范的 Markdown 文件，也可以在理解和思考的基础上做出取舍，为后文介绍的自定义配置做准备。

### 网页版

对于初识 markdownlint 的用户来说，最直观、最方便的体验方式，就是使用原作者提供的 [网页版演示工具](https://dlaa.me/markdownlint/)。

打开该工具后，点击右上角的「Browse…」打开任意一个 Markdown 格式文件（你可以下载本文 [演示用的文件](https://p178.p0.n0.cdn.getcloudapp.com/items/YEurygOp/15ab6b4b-946d-4ff8-9d11-661dee974970.md?v=0de8ecaee7091f6ed465e5babf2087d5)），或者手动将 Markdown 内容粘贴到左上角的文本框中。

![](https://cdn.sspai.com/2022/03/25/0b54a1fb26bea1625445d0624d4c9632.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

（**注：**
这个工具在加载后就只在本地运行，文本内容不会被上传，因此可以放心使用。）

这时，右下角的文本框就会以

```text
<行数> - <规则名称> <规则内容> [ 出错原因 ]
```

的格式逐条列举输入文件存在的问题。

例如，在上图的例子中，第一条问题点：

```text
9 - MD004 / ul-style Unordered list style [Expected: asterisk; Actual: dash]
```

是指文件第 9 行违反了 MD004（无序列表样式）。

根据这一规则，同一个 Markdown 文件中的无序列表标记应当保持一致，不能混用。这里，文件中第一个无序列表项（第 8 行）是用星号开头的；按照 MD004，后续的列表项也应当都用星号开头（Expected: asterisk），而第 9 行却使用了横线开头（Actual: dash），因此检查器报错。

对此，只需要点击这条错误信息末尾的「Fix」字样，markdownlint 就会将开头的横线改为星号，从而满足 MD004 的要求。

用同样的方法审阅其他错误信息，视情况决定是否接受即可。

### 在 VSCode 中使用

#### 安装和基本使用

网页版工具虽然方便，但也只适合演示和临时使用。如果要将 markdownlint 融入写作流程，还需要更为方便的调用方式。一种理想的选择，就是将其安装为编辑器扩展，边写文章、边检查错误。

本文以目前流行的 [Visual Studio Code](https://code.visualstudio.com/)（VSCode）为例演示。

如开头所铺垫，作为一款代码编辑器，VSCode 是将 Markdown 作为一种「语言」提供支持的。此外，VSCode 也具有任何成熟代码编辑器必备的**「快速修复」（Quick Fix）**功能：检测和提示代码中的问题，并提供修改建议和「一键修复」的快捷方式。

而 markdownlint 插件的作用，正是将 Quick Fix 的支持范围延伸到 Markdown，让 VSCode「学会」这门语言边边拐拐的细节。

markdownlint 插件用起来非常简单。首先前往 [VSCode 市场页面](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)，点击「Install」按钮，跳转到 VSCode 完成安装。

还是以上文提供的测试文件为例，安装插件后再打开这个文件，就会看到界面上多出了很多波浪线，每处波浪线都对应一处发现的错误：

![](https://cdn.sspai.com/2022/03/25/dd1fb3e140dc06aec20aa851cf3c6581.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

markdownlint 的错误检查是实时的；标记和建议会随着输入和编辑而不断刷新。

对于这些错误，可以进行的操作包括：

- 将鼠标移动到画线位置，将会弹出一个浮窗，其中说明了该处存在错误的原因——与上文在网页版中看到的提示完全一致。
- 点击「快速修复」（或按 `Command`\-`.` 快捷键），就可以调用 markdownlint 引擎自动改正这条错误。
- 按 `Shift`\-`Command`\-`M` 快捷键弹出「问题」面板，查看所有问题的列表，点击其中的条目可以跳转定位。
- 按 `Shift`\-`Command`\-`P` 快捷键弹出命令面板，输入「format」，选择「格式化文档」，修复文件中的所有错误（初次运行可能需要先选择 markdownlint 作为默认引擎）。

![](https://cdn.sspai.com/2022/03/25/3dd957d334f1d0c653bacfcf1d7c740d.gif)

#### 自定义配置

如上文所说，markdownlint 的规则并不是什么「神谕」或「铁律」，至多只是该项目作者基于较多经验和观察的「一家之言」，不可能适合每个人的口味、与每个使用场景兼容。因此，根据自己的偏好和需求予以调整是非常必要的。

对此，好消息是，markdownlint 提供了充分的调整空间，每一条规则都可以随意开关，其中很多还提供了细粒度的专用选项。坏消息是，作者似乎默认用户都是谙熟纯文本配置的高手，没有像大多数插件那样提供 UI 选项，所有设置都只能通过手写配置文件调整；下文将尽量用简单易理解的方式介绍其方法。

首先，按 `Shift`\-`Command`\-`P` 打开命令面板，输入「settings」，选择「首选项：打开设置（JSON）」，打开 VSCode 的配置文件。

然后，在这个文件中加入一个名为 `markdownlint` 的对象（位置任意，但可以与其他插件的配置写在一起方便管理）。形如：

```json
{
  // 其他插件设置
  "markdownlint" : {
    "config" : {
      "<规则编号>" : { <配置内容> },
      // 更多配置
    },
    "focusMode" : true
  },
  // 其他插件设置
}
```

其中，`config` 子对象即用来添加针对各个规则的配置。不同规则有不同的设置方法，具体需要查阅规则文档来确定：

- **有的规则只有简单的「开」或「关」两种状态。**

  例如，MD001 要求标题一次增加一级，[文档](https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md#md001---heading-levels-should-only-increment-by-one-level-at-a-time) 也没有为其列举更多参数（parameter）。如果你不喜欢这个规则，那么可以通过添加 `{ "MD001" : false }` 将其直接关闭。

- **有的规则提供更细致的选项。**

  例如，MD007 要求无序列表开头缩进的空格数量保持一致，并且默认为每 2 个空格为一级。但实践中很多人习惯以 4 个空格为单位来缩进。根据 [文档](https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md#md007---unordered-list-indentation)，该规则提供一个名为 `indent` 的整数型参数，默认值为 2（`number; default 2`）。据此，在配置中添加 `{ "MD007" : { "indent" : 4 } }` 即可将缩紧步进改为 4。

  又如，MD024 禁止文中出现两个内容相同的标题。根据 [文档](https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md#md024---multiple-headings-with-the-same-content)，该规则有一个名为 `siblings_only` 的布尔型参数。据此，如果添加（`{ "MD024" : { "siblings_only" : true } }`），那么这条规则只会检查**紧邻的标题**是否重复。或者，也可以彻底禁用这条规则（`{ "MD024" : false }`）。

再注意到，上面的例子中，与 `config` 对象平行，还有一个 [`focusMode` 键](https://github.com/DavidAnson/vscode-markdownlint#markdownlintfocusmode)。这是我认为非常必要的一条配置：**写作过程中，一行内容在完成输入之前，不符合 Markdown 语法是很正常的。** 按照默认设置，这些还没写完的内容都会被当作「有问题」，打上波浪线。这显然是多此一举，也会造成视觉干扰。

将 `focusMode` 设为 `true` 后，插件就**不会检查光标所在的当前行**，回避了上述问题。此外，也可以将该键的值填为具体的数字，从而将忽略范围扩展到当前行上下的相应行数，进一步减少干扰。

最后，该插件还可以设置 [仅在存盘时检查](https://github.com/DavidAnson/vscode-markdownlint#markdownlintrun)、[根据路径忽略特定文件](https://github.com/DavidAnson/vscode-markdownlint#markdownlintignore) 等，限于篇幅在此不赘，有兴趣的读者可以进一步阅读 [文档](https://github.com/DavidAnson/vscode-markdownlint#configure)。

### 在命令行中使用

#### 安装与基本使用

尽管 VSCode 插件已经可以满足大部分人的需求，但专业用户可能还希望有一个命令行界面，以实现批量化、自动化的处理。

markdownlint 确实提供了命令行版本。但比较幽默的是，它不仅有命令行工具，而且有**两个**命令行工具，第一个叫做 [`markdownlint-cli`](https://github.com/igorshubovych/markdownlint-cli)，第二个……当然就叫做 [`markdownlint-cli2`](https://github.com/DavidAnson/markdownlint-cli2)。这两者的 [开发背景和区别](https://dlaa.me/blog/post/markdownlintcli2) 过于琐碎，就本文目的，读者只需知道 `markdownlint-cli2` 相对较快，并且和 VSCode 插件版共用一套配置语法，结合使用比较方便；本文也将以其为例演示。

下面的操作假定读者熟悉终端的基本知识和使用方法，并且已经 [安装好 Node.js](https://nodejs.org/zh-cn/download/)。

首先，通过 `npm` 安装 `markdownlint-cli2`：

```bash
npm i -g markdownlint-cli2
```

`markdownlint-cli2` 的使用方式主要有两种：

```bash
markdownlint-cli2 [文件路径]     // 检查文件并报告问题
markdownlint-cli2-fix [文件路径] // 检查并直接修复文件
```

![](https://cdn.sspai.com/2022/03/25/bcc698ced77c769610a5fde452137911.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

其中，文件路径可以是一个或多个实际的文件名，也可以是通配符。例如：

```bash
markdownlint-cli2 "**/*.md"
```

是指检查当前目录以及任意层级子目录中，所有以 `md` 为后缀名的文件。

#### 自定义配置

`markdownlint-cli2` 与 VSCode 插件使用完全相同的配置语法。因此，在根据自己习惯配置好 VSCode 插件后，只要将其中 config 对象的内容复制出来，保存为一个名为 `.markdownlint.json` 的文件（也可以用一些其他的文件名和格式，详见 [文档](https://github.com/DavidAnson/markdownlint-cli2#configuration)），与待检查的 Markdown 文件放在同一文件夹（如果要检查多个文件，则放在其共同的最上级文件夹），`markdownlint-cli2` 就会自动读取并执行。

在下图例子中，由于通过配置文件改变了部分规则，下方的终端的输出也少了相应条目：

![](https://cdn.sspai.com/2022/03/25/817088686409d30b5829833bc3b2303b.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

值得一提的是，如果某个文件夹中存放了上述配置文件，而其配置内容与 VSCode 插件的设置不同，那么在编辑这个文件夹内的 Markdown 文件时，VSCode 也会优先使用这个外部配置文件的设置。这特别适合为不同项目微调配置。

最后，如果你有固定的设置想要搭配 `markdownlint-cli2` 使用，又不想每次都创建一个配置文件，也可以用：

```bash
markdownlint-cli2-config [配置文件路径] [Markdown 文件路径]
```

的语法来手动指定配置文件路径。

## 保持中英文之间的「盘古之白」

在很多中文社区，中英文之间要手动加空格——俗称「盘古之白」——都是不成文的风格要求。这项要求是否合理、又该如何满足，是很有价值的话题，但超出了本文的讨论范围。

这里，只简单概括通说：中英文之间加入空隙，是为了实现视觉上的区隔，更加美观和易读。理想情况下，这种「空隙」应当由排版引擎自动加入，宽度宜为 1/4 个全角空格（em）。但由于数字排版环境复杂多变，在大多数时候（包括最常见的网页环境）不能指望排版引擎有这种能力，因此只能退而求其次，手动插入一个半角空格（因其宽度**通常**接近于 1/4 em），达到类似效果。

（**注：**
如果有进一步兴趣，请阅读知乎讨论「[中英文混排时中文与英文之间是否要有空格？](https://www.zhihu.com/question/19587406)」，W3C 标准草案《中文排版需求》[§3.2.2](https://www.w3.org/TR/clreq/#mixed_text_composition_in_horizontal_writing_mode)，以及收听《字谈字畅》播客 [第 14 期](https://www.thetype.com/typechat/ep-014/)。）

相比之下，本文关心的问题是：如果想要在中英文之间手动加空格，有什么自动检查和补全的方法吗？

答案是当然有，而且选择也不止一个。其中，最著名的可能是 [pangu.js](https://github.com/vinta/pangu.js/) 项目。如果你用过一个叫做「[为什么你们就是不能加个空格呢？](https://chrome.google.com/webstore/detail/%E7%82%BA%E4%BB%80%E9%BA%BC%E4%BD%A0%E5%80%91%E5%B0%B1%E6%98%AF%E4%B8%8D%E8%83%BD%E5%8A%A0%E5%80%8B%E7%A9%BA%E6%A0%BC%E5%91%A2%EF%BC%9F/paphcfdffjnbcgkokihcdjliihicmbpd?hl=zh-CN)」的浏览器插件，那你也就用过 pangu.js——它正是出自同一位作者之手、以 pangu.js 为底层支撑的。

另一个选择是 [AutoCorrect](https://github.com/huacnlee/autocorrect)。与主要关注文本内容的 pangu.js 相比，AutoCorrect 出生于 Ruby 语言的中文社区，因此从一开始就考虑到了编程代码中的中英混排场景（可以参见该项目的 [测试文件](https://github.com/huacnlee/autocorrect/tree/main/tests/fixtures)），通用性更强。

不过，两者在实际使用的区别很小，唯一比较明显的差别是 pangu.js 会**在链接文本的前后加上空格**，而 AutoCorrect 不会；这也只是见仁见智的选择。此外，pangu.js 没有官方的 VSCode 插件，只有几个第三方插件，但已久不更新，命令行工具也依赖于 Node.js，一般用户初次运行起来可能有点繁琐；而 AutoCorrect 则提供了官方 VSCode 插件，命令行版本没有外部依赖，选项也更多。

因此，下文将同时介绍这两个工具，读者按偏好选择其一即可。

### 网页版

与 markdownlint 类似，AutoCorrect 也提供了一个 [在线预览版](https://huacnlee.com/autocorrect/)，既可用来测试该工具的效果，也可用来处理实际文件。

![](https://cdn.sspai.com/2022/03/25/a20cf3bfac09f39620180ebb4e0fa82a.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

打开该工具后，在左上角的下拉菜单中选择「Markdown」，粘入自己的内容，然后点击下方的「Format」按钮即可看到输出。

pangu.js 没有官方网页版。

### 在 VSCode 中使用

AutoCorrent 提供了第一方的 [VSCode 插件](https://marketplace.visualstudio.com/items?itemName=huacnlee.auto-correct)。安装后，建议在「设置」>「扩展」>「AutoCorrect」中按需调整该插件的两个选项：

- Enable：是否允许实时检查。如果启用，文件里中英文未留空的位置将会被当作「问题」予以提示，并且可以通过 Quick Fix 功能一键添加空格。
- Format On Save：是否在保存时自动修复中英文之间的空格。

这两个选项都是默认启用的，但我**建议考虑关闭**。理由也与上面配置 markdownlint 时类似：文档是否「整洁」并没有必要在写作阶段就特意关注，而是修订校对阶段的任务。特别是对于中英文空格这种「小节」，启用实时修复只会让界面充斥着提示问题的波浪线，非常干扰写作。

无论是否启用这些选项，都可以通过命令面板中的「AutoCorrect: Format document」命令来手动为文件添加中英文空格。如果想要更方便，还可以点击该命令右侧的齿轮图标，为其指定一个快捷键，随时满足自己的强迫症。

![](https://cdn.sspai.com/2022/03/25/1f9025bab440e9dcd8d61c9100a66f23.gif)

pangu.js 没有官方 VSCode 插件，但有几个第三方移植版，其中用户较多、效果也不错的是 xlthu 开发的 [Pangu-Markdown](https://marketplace.visualstudio.com/items?itemName=xlthu.Pangu-Markdown)。安装后，在命令面板选择「Pangu Format」即可检查全文并追加空格。

### 在命令行中使用

AutoCorrect 提供了为各个平台编译的命令行工具，官方文档提供的安装脚本如下：

```bash
curl -sSL https://git.io/JcGER | bash
```

（**注：**
有义务提醒，`curl | sh` 风格的安装方式是有 [内在风险](https://0x46.net/thoughts/2019/04/27/piping-curl-to-shell/) 的，请务必逐行审阅 `curl` 下载的 [安装脚本内容](https://github.com/huacnlee/autocorrect/blob/main/install) 再决定要不要运行。）

与 markdownlint 类似，AutoCorrect 也可以选择是只报告问题，还是直接修复文件：

```bash
autocorrect [文件路径]       // 检查文件并报告问题
autocorrect --fix [文件路径] // 检查并直接修复文件
```

![](https://cdn.sspai.com/2022/03/25/2bca344136fee54763f60f1ca0a1e854.png?imageView2/2/w/1120/q/40/interlace/1/ignore-error/1)

更完整的使用方法可以使用 `autocorrect --help` 查看，或者 [阅读在线文档](https://github.com/huacnlee/autocorrect#using-cli)。

至于 pangu.js，其命令行工具则需通过 `npm` 安装：

```bash
npm i -g pangu
```

相比 AutoCorrect，其功能也比较简单，只能将补齐空格后的内容直接显示出来，必须配合 `>` 重定向才能写入到文件：

```bash
pangu -t [文本内容]             // 检查指定文本内容
panfu -f [文件路径]             // 检查指定文件
pangu -f [文件路径] > [写入路径] // 检查指定文件并将结果写入到文件
```
