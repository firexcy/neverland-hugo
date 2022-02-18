---
title: "用 Drafts 优化 OmniFocus 的批量任务收集"
date: "2017-04-15"
tags:
  - "gtd"
  - "ios"
  - "omnifocus"
---

## 一、文本化的任务收集

「收集」是 GTD 流程中的第一步，也是至关重要的一步。面对头脑中随时一闪而过的各种想法，能否**准确而快速**地将其收集到 Inbox 中，决定了任务管理是否有效。此外，在收集想法到 Inbox 中时，我们往往需要同时添加若干条新事项，而不希望被繁琐的「添加—保存」步骤拖慢效率、打断思路。

针对这种需求，主流任务管理 app 大多都提供一种「快速添加」的功能，即在界面上提供一个按钮（如 OmniFocus 中的「Save+」），当用户输入完一条任务信息并点击该按钮时，应用不会回到主界面，而是保存该条任务并清空输入框，让用户可以直接继续输入。

![OmniFocus 中的快捷输入功能](https://ww1.sinaimg.cn/large/73403117ly1fehxdrdk4vj20h40cqt9n.jpg)

但这种功能的局限也是明显的，所谓的「快速添加」并没有那么快捷。用户不仅需要手动打开 app、点击添加按钮，而且如果想修改截止日期、备注等具体参数，仍然需要多次点击。

这不禁促使我们思考：是否存在这样一种方式，能够一步到位地**批量**收集任务并**定义其具体参数**呢？

事实上，这样的方法是存在的，那就是用**文本**来描述任务。

来看下面这段语句：

```
- Item 1 @due(+1d 10p)
- Item 2 @defer(tue)
```

即便不加说明，读者应该也能很容易猜出它的含义。这段语句描述了两个任务 `Item 1` 和 `Item 2`，其中 `Item 1` 将截止于明天（`+1d`）的晚上 10 点（`10p`），而 `Item 2` 推迟至周二（`tue`）开始。

这种用类似于 Markdown 的格式描述任务及其属性的语法称为 **[Taskpaper](https://www.taskpaper.com/)**，它来源于 macOS 上一款基于纯文本的任务管理工具。在 Taskpaper 中，每条任务以一个短横线（hyphen，「-」）和一个空格为引导——非常类似 Markdown 中的无序列表，其后跟随任务名称，然后用 `@due`、`@flagged` 等标签描述其截止日期、旗标等属性。

显然，这种基于纯文本的任务描述方法**天然地适合批量输入任务**，也免去了在各个输入框中来回设置日期、上下文等参数的麻烦——用户手不离键盘就能完成全部输入过程。在 iOS 这种缺乏有效自动化工具的平台上，Taskpaper 语法的优势显得尤为明显。

**那么，对于 OmniFocus 用户，能否利用 Taskpaper 语法在任务输入上的便利来优化收集流程呢？**答案是肯定的。OmniFocus 在 2.14 版后，增加了大量[自动化功能](https://discourse.omnigroup.com/t/implementation-details-for-omnifocus-2-14-automation/24179)，其中就包括对 Taskpaper 语法的支持。在该版本之后，只要通过如下 URL Scheme：

```
omnifocus:///paste?content=内容
```

将符合 Taskpaper 格式的文本传送到 OmniFocus，后者即可自动识别其中包含的任务和属性。OmniFocus 目前支持的 Taskpaper 语法如下表所示：

![Taskpaper 标签](https://ww1.sinaimg.cn/large/73403117ly1fel5qwreeqj21gc136grz.jpg)

**不过，用什么工具承担撰写 Taskpaper 语句并发送给 OmniFocus 的职能呢？**理论上，只要是能接受输入并运行 URL Scheme 的 app，如常用的 Workflow、Launch Center Pro 等，都可以做到。不过，本文还是**首推 Drafts**，这不仅是因为其简洁的界面和宽裕的输入空间十分适合任务收集的情境，更是因为其内建的快捷键和脚本支持能进一步提高输入的效率。基于此，下面就以 Drafts 为例演示如何建立和优化这一工作流。

首先建立最基础的动作，将 Drafts 和 OmniFocus 连接起来。我们在 Drafts 中新建一个动作，其中包含一个 URL 步骤，内容为：

```
omnifocus:///paste?content=[[draft]]&x-success=drafts4://
```

并将该动作的「after success」属性改为「Trash」。（你可以点击[这里](https://drafts4-actions.agiletortoise.com/a/2A5)直接导入该动作。）

![在 Drafts 中新建动作](https://ww1.sinaimg.cn/large/73403117ly1fehxdrpjwyj22bo112nc9.jpg)

接着，我们在 Drafts 的工具栏中增加一个**指向上述动作的快捷按钮**。（你可以点击[这里](https://drafts4-actions.agiletortoise.com/k/2A6)直接导入该按钮。）另外，我还为该按钮设置了一个快捷键（Ctrl-Option-O，与 Mac 版 OmniFocus 的 Quick Entry 保持一致），便于使用 iPad 时直接在键盘上完成全过程。

![在 Drafts 中新建脚本按钮](https://ww1.sinaimg.cn/large/73403117ly1fehxdri1b1j21qq112qbs.jpg)

这样，只要按照 Taskpaper 语法输入需要批量添加的任务，然后点击键盘上方的按钮/按下 Ctrl-Option-O，就能将这些任务批量添加到 OmniFocus 的 Inbox 中、并自动返回到 Drafts，该条 draft 会在动作执行完毕后被自动删除。

此外，为了加快标签的输入，你还可以**将下面这些常用标签的快捷键导入 Drafts 中。**（[@context](https://drafts4-actions.agiletortoise.com/k/2A7)、[@due](https://drafts4-actions.agiletortoise.com/k/2A8)、[@defer](https://drafts4-actions.agiletortoise.com/k/2A9)、[@flagged](https://drafts4-actions.agiletortoise.com/k/2A0)）它们的效果是点击后在当前位置插入对应标签，并将光标移动到括号之间；如果选中一段文本再点击该按钮，则可以直接将选中文本包括在标签之内。

这样一来，我们就实现了用 Taskpaper 语法批量收集任务到 OmniFocus 的流程。下面的动画演示了在 iPad 上使用快捷键操作的过程：

![发送 Taskpaper 语句到 OmniFocus](https://ww1.sinaimg.cn/large/73403117ly1fel4xi5motg20qo0k0wto.gif)

需要注意的是，目前 OmniFocus 尚未支持**指定任务所在的文件夹或项目**。当然，这或许不应在本文讨论之列——按照 GTD 的逻辑，收集任务到 Inbox 时无须考虑其具体归属，因为那是后一个步骤（整理）中要做的事情。但需求不主流并不代表需求不存在。例如，我在 OmniFocus 中有一个叫做「Curiosity」的 Single Action List，用来保存我在日常阅读、浏览中偶然遇到、希望进一步了解的各种东西。在录入这种目的性明确的任务时，我就希望能直接将其发送到指定位置，而不用事后再进入 Inbox 手动归类。

好在，得益于 Drafts 强大的脚本功能，我们可以「自力更生」，间接实现指定文件夹/项目的功能；事实上，**上文中提供的动作已经增加了对 `@project` 和 `@folder` 两种标签的支持。**只要在输入时添加 `@project(项目名)` 或 `@folder(文件夹名)` 之一，再运行该动作，即可实现发送到指定项目或文件夹的效果。

例如，下面的输入：

```
- Task 1 @project(general)
- Task 2
```

会在名为「General」的项目中新建两个任务「Task 1」和「Task 2」。

而输入：

```
- Project 1 @folder(personal)
    - Task 1
    - Task 2
```

会在名为「Personal」的文件夹中新建一个名为「Project 1」的项目，其中包含两个任务「Task 1」和「Task 2」。

需要注意的是：第一，**输入的项目名或文件夹名无须完全正确**，因为 OmniFocus 对输入有一定的模糊识别能力；第二，由于实现机制本身的限制，每次输入中**只能指定一个项目或文件夹**，而不能单独指定。如果输入中出现多个 `@project` 或 `@folder` 标签，所有输入都会被发送到第一个标签指定的项目或文件夹。但反过来说，要给输入的任务/项目指定目的地，只要写一次 `@project` 或 `@folder` 即可，无须每条任务指定一次。（你还可以导入这两个标签的快捷输入按钮：[@project](https://drafts4-actions.agiletortoise.com/k/2Aa)、[@folder](https://drafts4-actions.agiletortoise.com/k/2Ab)。）

来看一下最终的实现效果：

![发送任务到指定项目](https://ww1.sinaimg.cn/large/73403117ly1fel4xi6k8sg20qo0k0k4w.gif)

* * *

## 二、细节探究

经过上文的配置，我们已经实现了借助 Taskpaper 语法，用纯文本的形式批量快速收集任务到 OmniFocus。那么，这些功能是怎样实现的？如何修改这些功能使其更加符合自己的偏好？为此，下文就来具体说明上面导入的动作和按钮是**如何通过 Drafts 内建的 JavaScript 和正则表达式支持实现其功能的**。

需要说明的是，Drafts 支持全部的基础 JavaScript 语法及正则表达式，且有较为详尽的[官方文档](https://agiletortoise.zendesk.com/hc/en-us/categories/200192004-Drafts)。因此，下文目的并不在于详细介绍语法或翻译文档，而重在对于代码中的一些关键思路和所用到的 Drafts 独有的函数/属性进行介绍。

### 2.1 快捷输入标签的实现机制

Drafts 中的快捷按钮功能相当多样，不仅可以输入特定字符、执行某个动作，还可以运行一段 JavaScript 脚本。以上文中提供的用于输入 `@context` 标签的按钮为例，点击该按钮执行的代码是：

```
var sel = getSelectedText();
var selRange = getSelectedRange();
if (!sel || sel.length == 0) {
  setSelectedText("@context()");
  setSelectedRange(selRange[0]+9,0);
}
else {
  setSelectedText("@context("+sel+")");
  setSelectedRange(selRange[0]+selRange[1]+10,0);
}
```

这段脚本主要使用了与文本选择有关的几个函数。其中，`getSelectedText()` 获得的是当前选中的文本，而 `getSelectedRange()` 将返回两个值，分别是**当前光标所在位置**和**选中文本的长度**。在上述代码中，这两个值被一起传递给了 `selRange`，因此后面用 `selRange[0]` 和 `selRange[1]` **分别指代**。

代码的第三行对选中的文本长度进行了判断，如果长度为 0，就**直接插入**「@context()」这段文本。之后的 `setSelectedRange()` 函数用于选中文本，它需要输入两个值：光标的起始位置和选中文本的长度，当后一个值为 0 时，就相当于将光标置于前一个值指定的位置。我们希望将光标放在「@context」后的括号中间，换句话说，放在**从「@」算起第 9 个字符的位置**，这就是 `(selRange[0]+9,0)` 的来源。以此类推，如果我们需要输入「@due()」并移动光标，则应相应改为 `(selRange[0]+5,0)`。

如果选中文本的长度不为 0，代表我们希望将一段已经输入的文本转化为标签，因此，我们用加号（+）将「@context」、一个左括号、选中的内容和一个右括号依次连接起来，交给 `setSelectedText()` 函数。另外，在这种情况下，我们希望**光标被放在括号之外**，因此交给 `setSelectedRange()` 的光标起始位置应该是**原来的后推「@context()」的长度（10 个字符）、再加上选中文本的长度（`selRange[1]`）**，故完整的表达就是 `(selRange[0]+selRange[1]+10,0)`。类似地，如果这里是要将选中文本转化为 `@due()` 标签，则应改为 `(selRange[0]+selRange[1]+6,0)`。

### 2.2 指定文件夹或项目的实现机制

如上所述，OmniFocus **没有提供对 `@project` 或 `@folder` 标签的原生支持**。但是，在其 URL Scheme 中，`paste` 动作可以附加一个 `target` 参数，用于指定发送到的具体位置。例如：

```
omnifocus:///paste?target=/task/general
```

会将当前的剪贴板内容创建为「General」项目下的任务。[1](#fn1)

而下列 URL：

```
omnifocus:///paste?target=/folder/personal
```

会将当前的剪贴板内容创建为「Personal」文件夹下的项目。

这就为我们自行创建对 `@project` 或 `@folder` 标签的支持提供了可能：只要用正则表达式提取 draft 中出现的相应标签内容，将其填入上述 URL Scheme 并执行即可。事实上，上文提供的动作就用下列 JavaScript 脚本对输入进行了处理：

```
var text = draft.content;
var folderTag = text.match(/@folder\(.+?\)/g);
if (folderTag != null) {
var target = '/folder/' + folderTag[0].slice(8,-1);
} else {
    var projectTag = text.match(/@project\(.+?\)/g);
    if (projectTag != null) {
        var target = '/task/' + projectTag[0].slice(9,-1);
    } else {
        var target = 'inbox';
        }
}
draft.defineTag('target',target);
```

该段代码用到了 [Drafts 中特有的 `draft` 对象及其属性和函数](https://agiletortoise.zendesk.com/hc/en-us/articles/202771590-Action-Step-Script)。在 Drafts 中，`draft` 是一个预先定义的对象，指当前这条 draft。该对象有多种属性，如 `content`（文本内容）、`createdDate`（创建日期）、`archived`（是否被归档，布尔值）、`uuid`（该条 draft 的唯一代码）等。上述代码的第一行即将 `text` 变量定义为当前 draft 的内容（`draft.content`）。

接着，代码用正则表达式 `/@folder\(.+?\)/g` 查找文本中的 `@folder` 标签，其中 `.+` 匹配的是**不限数量的、换行符以外的任意字符**。而将表达式夹在 `//g` 之间则代表搜索所有的结果。匹配结果被传给了 `folderTag`。然后，将第一个匹配到的结果（`folderTag[0]`）进行切割，去掉开头的「@folder(」（8 个字符）和结尾的「)」（1 个字符），只留标签括号中的部分（`slice(8,-1)`），拼成 `/folder/文件夹名`的形式，赋给 `target` 变量。

如果没有搜索到 `@folder` 标签，代码将继续搜索 `@project` 标签，方法类似。如果仍然没有搜索到，说明没有指定项目或文件夹，则将 `inbox` 赋给 `target` 变量，即发送到 Inbox。最后，将 `target` 变量的值定义为一个 Drafts 标签[2](#fn2) `[[target]]`，以便在之后的步骤中引用。事实上，它将在下一步中，通过 URL Scheme：

```
omnifocus:///paste?content=[[draft]]&target=[[target]]&x-success=drafts4://
```

发送给 OmniFocus。

### 2.3 语法细则

OmniFocus 支持大部分的 Taskpaper 语法，但也**存在一些变通**，下文列举的是两者的主要差异。

#### 2.3.1 关于短横线

在 Taskpaper 中，任务必须以一个短横线（`-`）开头，但 OmniFocus 无此要求。因此，下面两段语句：

```
- Task 1
- Task 2
```

和

```
Task 1
Task 2
```

是等价的。

#### 2.3.2 关于备注

在 Taskpaper 语法中，紧跟一条任务之后、不以短横线开头的一行，被认为是该条任务的**备注（Notes）**，例如：

```
- Task 1
Some Notes
```

OmniFocus 同样能识别该语法。在这种场合，**任务前的横线不能被省略**。例如，不能写成：

```
Task 1
Some Notes
```

否则，备注将被识别为另一条任务。

#### 2.3.3 关于子任务

在 Taskpaper 语法中，任务间的隶属关系通过缩进来体现，你可以通过输入一个制表符（Tab 键）将一个任务标记为其上一行的子任务，例如：

```
- Task 1
    - Task 2
    - Task 3
```

表示一个名为「Task 1」的任务，其下有两个子任务「Task 2」和「Task 3」。如 §2.3.1 所述，任务前的横线可以省略。你还可以通过 @parallel 标签指定「Task 1」下的子任务是平行的（`@parallel(1)`）还是顺序的（`@parallel(0)`），如不指定，默认为平行。

需要注意的是，根据 Taskpaper 原本的规则，可以用`项目名:`的格式来新建一个项目。但 OmniFocus 并未接受这一设定。因此，即使输入：

```
Task 1:
- Task 2
- Task 3
```

也不能创建一个名为 `Task 1` 的项目。对于 OmniFocus，该输入与上个例子是等价的。如果想将任务发送到一个既有的项目，你应该如前文所述，使用我们自行定义的 `@project` 标签。

1. 注意，`target` 参数的值须经 URL 编码。但为易读性起见，本段中的 URL 没有做此处理。实际执行中，该 URL 会被 Drafts 自动编码为 `omnifocus:///paste?target=%2Ftask%2Fgeneral`。 [↩](#ffn1)
2. [标签（Tags）](https://agiletortoise.zendesk.com/hc/en-us/articles/202843484-Templates-and-Tags)是 Drafts 另一项重要功能，类似于 Workflow 中的变量。Drafts 提供了一些默认标签，但用户也可以自行定义新的标签。与步骤内部执行的 JavaScript 脚本中的变量相比，标签的优势在于可以在步骤之间传递数据。 [↩](#ffn2)

 

\-- NORMAL --
