---
title: "如何不借助插件在全平台优化维基百科显示效果"
date: "2017-11-05"
categories: 
  - "post"
tags: 
  - "tutorial"
---

维基百科对我们的重要性不言而喻，无论是在生活中还是学习中，如果要获取对某一话题的初步认识，维基百科一般都是那个最便捷且相对可靠的信息来源。

但或许是因为太过关注内容本身，即使在这个网页设计技术百花齐放的年代，维基百科的外观却与十年前没什么太大区别。如果说其页面设计上的素面朝天还可以美其名为「简约」的话，字体排印上的简陋就只能评价为「放任自流」了。特别是在阅读篇幅较长的词条时，那小而拥挤的正文字体总是让我的眼睛酸痛到怀疑人生。

![维基百科简约（陋）的默认风格](https://i.loli.net/2017/11/05/59fe5dbf34ad9.png)

正因如此，改善维基百科的阅读体验是一个「硬」需求。目前，常见的方法通常有两种。一是利用各浏览器自带的阅读模式。但是，这种方法的自定义灵活性较小，且依赖于浏览器的支持。主流的 Chrome 浏览器干脆就没有内置阅读器功能。二是利用浏览器插件，如 Stylish、Wikiwand 等。这种方法可定制性强，但加载插件需要消耗额外的资源。另外，这两种方法的共同弊端在于不具有跨平台性：配置好的阅读环境无法在不同电脑上同步，对于移动端也缺乏良好的支持。

其实，作为一个自带 geek 属性的服务，维基百科本身已经提供了强大的外观定制功能。利用这一功能，我们不仅可以在预置的几种主题间切换，而且可以自定义页面的 CSS、JavaScript，打造出最适合自己的维基百科外观。下文就介绍如何操作，并给出一些参考配置方案。

**注意：维基百科的各项设置需要登录才能访问。**注册过程非常简单，在此不赘。

登录后，点击页面右上角的 **Preferences/参数设置** 链接打开设置，然后切换到 **Appearance/显示** 选项卡。可以看到，维基百科共提供了五种皮肤供用户选择。然而，它们中的绝大多数都只会让本就简陋的页面变得更加复古……

![听起来很芬芳的「科隆香水蓝」主题……祝你拥有愉快的一天](https://i.loli.net/2017/11/05/59fe5dbff08e0.png)

唯一比较符合当下设计审美的，大概只有 **MinervaNeue** 这款皮肤，它实际上就是维基百科移动版页面的桌面端移植。选中该选项，然后点击页面底部的 **Save/保存**即可应用该皮肤，其效果如下：

![MinervaNeue 皮肤的效果](https://i.loli.net/2017/11/05/59fe5dbf3a096.png)

可以看出，界面的整洁度和可读性已经比之前高了不少。不过，这样的效果仍然不能让人完全满意。例如，**字号**还是过小，在电脑屏幕上看起来较为吃力；没有**两端对齐**，文本块的右侧边缘看起来不够整齐等。对有的用户而言，可能还希望换上自己喜欢的**字体**。要进一步完善效果，就要用到自定义 CSS 的功能了。

再次进入设置页面，点击 MinervaNeue 主题右侧的 **Custom CSS/自定义 CSS** 链接。由于我们是第一次修改该主题的样式，将会直接跳转到创建页面。

![CSS 编辑界面](https://i.loli.net/2017/11/05/59fe5dbf151f3.png)

在代码框中输入下列内容：

```
.mw-body {
    font-size: 1.25em !important;
    text-align: justify;
    -moz-hyphens: auto;
    -webkit-hyphens: auto;
    hyphens: auto;
}
```

这段代码的作用是将正文部分的字号修改为 1.25 [em](https://www.zhihu.com/question/46279241)（可以反复尝试出最适合自己的值；维基百科默认值是 0.85 em，小得丧心病狂），并开启两端对齐和英文连字符。

输入完成后，点击页面底部的 **Save page/发布页面**按钮。这时，再刷新维基百科的页面，就可以看到修改后的效果了。

![修改了字号和对齐属性后的效果](https://i.loli.net/2017/11/05/59fe5dbfdc6c7.png)

另一个需要解决的问题是字体。维基百科默认只指定 `Serif` （无衬线）字体。实践中，这种将决定权完全交给浏览器和系统的做法往往不尽如人意，而且在不同配置环境下的表现很不统一。为了让其[在各平台上都显示为较高质量的黑体](https://www.zhihu.com/question/19911793)，可以在上述代码中加上一行：

```
font-family: -apple-system, "Helvetica Neue", Helvetica, "Nimbus Sans L", Arial, "Liberation Sans", "PingFang SC", "Hiragino Sans GB", "Source Han Sans CN", "Source Han Sans SC", "Microsoft YaHei", "Wenquanyi Micro Hei", "WenQuanYi Zen Hei", "ST Heiti", SimHei, "WenQuanYi Zen Hei Sharp", sans-serif;
```

类似地，如果想在正文中使用宋体（西文部分使用衬线体），则可以将这行代码改为：

```
font-family: Georgia, "Nimbus Roman No9 L", "Songti SC", STSong, "AR PL New Sung", "AR PL SungtiL GB", NSimSun, SimSun, "TW\-Sung", "WenQuanYi Bitmap Song", "AR PL UMing CN", "AR PL UMing HK", "AR PL UMing TW", "AR PL UMing TW MBE", PMingLiU, MingLiU, serif;
```

效果如下：

![将正文修改为衬线字体的效果](https://i.loli.net/2017/11/05/59fe5dbfd9c30.png)

（上面的字体回退顺序参考了[此 GitHub 项目](http://zenozeng.github.io/fonts.css/)，在此感谢。）

当然，你也可以改为自己喜欢的字体，如[思源宋体](https://github.com/adobe-fonts/source-han-serif)：

```
font-family: Source Serif Pro, Source Han Serif, serif;
```

需要注意的是，维基百科不同语言版本虽然账号是互通的，**但偏好设置和自定义 CSS 却相互独立**。因此，你需要为自己常用的每种语言版本（如中文和英文）重复一次上述设置。另外，iPad 上的 Safari 浏览器默认访问的是移动版页面；如果想在 iPad 上看到同样的效果，需要在词条底部切换为桌面版。（如果想在 iPad 上使用自定义字体，可以参考少数派之前发表的[这篇文章](https://sspai.com/post/36259)。）

* * *

当然，上面步骤所实现的效果是比较基础的，CSS 的潜力远不止这些。前面提到的页面美化插件 Stylish，其原理就是额外加载一段自定义的 CSS 代码，以达到修改页面外观的效果。因此，既然维基百科本身支持自定义 CSS，我们完全可以「移花接木」，借用他人已经写好的样式文件，达到不借助插件实现复杂效果的目的。

为此，我们先安装 [Stylish 插件](https://sspai.com/post/34508)，然后在 [UserStyles](https://userstyles.org/) 网站（Stylish 插件的样式库）上搜索 Wikipedia，从中挑选一个符合自己口味的，例如[这个](https://userstyles.org/styles/140009/wikipedia-material-updated-12-8-2017)采用仿 Material 设计的主题，点击 **Install Style** 安装。

![在 UserStyles 上找到合适的主题并安装](https://i.loli.net/2017/11/05/59fe5f33e43ba.png)

然后，在 Stylish 插件的设置页面，切换到 **Manage** 选项卡，找到我们刚才安装的主题，点击 **Edit** 进入编辑模式。

这时，我们就能看到该主题所采用的 CSS 代码了。需要注意的是，大多数主题的 CSS 代码都不止一段，每段根据不同规则适用于不同的页面，这可以从其下方的 **Applies to** 选项中看出。就维基百科的主题而言，只有那些适用于 `wikipedia.org` 全站的 CSS 片段才是用来调整词条页面的外观的；我们只需要这些片段。

![找到所需的 CSS 代码](https://i.loli.net/2017/11/05/59fe5f7722c29.png)

将上述片段复制出来后，对维基百科关闭 Stylish 插件，并切换回默认的 **Vector** 主题，点击其右侧的 **Custom CSS/自定义 CSS** 链接。将找到的 CSS 代码按照前述方法依次复制进代码框并保存。刷新页面，就能看到换上新装的词条页面了。

![最终效果](https://i.loli.net/2017/11/05/59fe5fb4b60f5.png)
