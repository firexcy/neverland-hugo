---
title: "用小书签改善 Safari 网页阅读效果"
date: "2019-01-04"
categories: 
  - "post"
tags: 
  - "ios"
  - "tips"
---

我们每天都要浏览大量的网页，但不是每个网页的设计都能做到为读者着想。实际上，相当比例的网页设计十分糟糕，读起来非常费劲。对此，Safari 的阅读模式是一个不错的解决方案，但并不是在所有网页上都能成功启用、或是取得理想的效果。使用 Stylish、Tampermonkey 等浏览器插件也是一种途径，但不适用于 iOS，而桌面版 Safari 也对第三方插件[越发不友好](https://web.archive.org/web/20181021114306/https://developer.apple.com/safari/whats-new/)了。

上述问题可以通过使用[小书签](https://zh.wikipedia.org/wiki/小书签)（bookmarklet）来解决。小书签的本质是一段 JavaScript 脚本，典型用途之一就是修改当前浏览器页面的外观，包括但不限于字体、字号、颜色等。相比于完整的浏览器插件，小书签尽管功能比较简陋，但优势在于通用性极强，可以用在包括 iOS 版 Safari 在内的任何浏览器上。

要将小书签添加到 Safari 中，最简单的方法是在桌面端操作，将下文给出的链接拖拽到书签栏即可；它们会随着 iCloud 同步到 iOS 端。如果要[在 iOS 上操作](https://support.apple.com/zh-cn/guide/iphone/bookmark-favorite-webpages-iph42ab2f3a7/ios)，则可以先长按复制这些小书签的链接，然后任意将一个网页（例如本页）保存到收藏夹，再通过编辑功能将其链接改为前面复制的内容。

**注：**小书签是一个历史相当久远的功能，网上的资料也很丰富（少数派几年前有过一篇很详尽的[文章](https://sspai.com/post/26196)），故本文不多赘述其原理和制作方法。

### 修改网页字体

字体是网页设计中的重要环节。选用一个美观的字体组合，不仅能让用户阅读信息更加顺畅，也有利于增强网站的视觉辨识度。遗憾的是，很多网页设计者都忽略或者滥用了字体设计。有的不加考虑，放任系统调用 Arial、Times New Roman 等让人直翻白眼的回退字体；有的则矫枉过正，选择了一些乍看很有风格、实则根本不适合阅读的「个性」字体。遇到这类网页时，运行下面这个小书签，可以将页面字体统一为系统默认字体（San Francisco），获得更好的可读性。

[👓 Normalize Fonts](javascript:(function()%7Bif(document.styleSheets.length)%7Bvar%20x=document.styleSheets%5Bdocument.styleSheets.length-1%5D;x.insertRule('*%20%7B%20font-family:%20-apple-system,BlinkMacSystemFont,PingFang,sanserif%20!important;%20%7D',x.cssRules.length);%7D%7D)();)

![将网页字体修改为系统默认字体](https://cl.ly/d8f89e/font.png)

将网页字体修改为系统默认字体

**注意：**

1. 这个小书签理论上对于绝大多数网页都能奏效，但也存在一些例外情况。例如，如果目标网页使用了 HTML 的 `font` 标签（已经被废弃）来指定字体，就超出了上面代码的控制范围。修改网页外观的第三方插件也可能与该小书签的功能冲突。
2. 如果你嫌 San Francisco 太过沉闷，不妨选择把字体换成 Seravek（成品：[👓 Normalize Fonts - Seravek](javascript:(function()%7Bif(document.styleSheets.length)%7Bvar%20x=document.styleSheets%5Bdocument.styleSheets.length-1%5D;x.insertRule('*%20%7B%20font-family:%20seravek%20!important;%20%7D',x.cssRules.length);%7D%7D)();)）。这也是我在 Safari 阅读模式中最常使用的字体，它在保证版面清爽易读的前提下，为笔画加入了很多俏皮的细节，非常适合用来攻克那些令人眼神涣散的长篇大论。
3. 比较遗憾的是，从 Safari 12 开始，苹果似乎[禁止](https://www.reddit.com/r/MacOS/comments/9jp5m3/psa_safari_12_disablednerfed_setting_custom_fonts/)了用 `font-family` 属性调用系统内置字体以外的字体。换句话说，即使本机已经安装了 `font-family` 列表中指定的外部字体，也会被 Safari 忽略。因此，修改字体选择范围仅限于 iOS/macOS 的[自带字体](http://www.jklstudios.com/misc/index.html#requiredfonts)。

![用 Seravek 字体显示的维基百科](https://cl.ly/372a85/seravek.png)

用 Seravek 字体显示的维基百科

### 放大网页字号

另外一种常见的网页设计问题是字号过小，读起来十分吃力。虽然 Safari 中可以很方便地通过两指缩放手势放大页面，但那会让文字过宽或者超过屏幕边框，需要反复左右卷动页面才能阅读，比较影响效率；理想的解决方案应该是只放大字体，而保持其他元素大小不变。下面这个小书签就可以实现上述需求。运行后，网页字号会被放大到 17px——苹果在 [iOS 设计准则](https://developer.apple.com/design/human-interface-guidelines/ios/visual-design/typography/)中指定的默认正文字号。如果仍然觉得字体不够大，可以反复运行，字号会以 2px 为单位步进。

[➕ Zoom Text](javascript:(function(){var%20p=document.getElementsByTagName('*');for(i=0;i<p.length;i++){if(p[i].style.fontSize){var%20s=parseInt(p[i].style.fontSize.replace('px',''));}else{var%20s=17;}s+=2;p[i].style.fontSize=s+'px'}})();)

![将网页字号缩放到标准正文尺寸](https://cl.ly/f7cb9e/size.png)

将网页字号缩放到标准正文尺寸

### 调用 Instapaper 显示网页文章

如上文所提及，Safari 的阅读模式并不是在所有网页上都能启用，也并不是总能取得理想的页面重排效果。这时，可以考虑使用更为专业的第三方服务来替代。例如，Instapaper 作为知名的「稍后读」服务，其设计的考究是广为承认的，它的重排版引擎能「驯服」绝大多数张牙舞爪的页面。只是，对于那些一扫而过的页面，如果仅仅为了改善阅读效果就将它们统统保存到 Instapaper 再阅读，不仅有些繁琐，也会让自己的稍后读列表很不整洁。

实际上，Instapaper 提供了一个简易接口（`https://www.instapaper.com/text?u=[页面链接]`），可以直接调用其排版功能显示特定网页上的文章，而不用先行保存。下面这个小书签的功能就是调用该接口显示当前网页的文章：

[📖 Instapaper](javascript:location.href%20%3D%20%22https%3A%2F%2Fwww.instapaper.com%2Ftext%3Fu%3D%22%20%2B%20encodeURIComponent(location.href)%3B)

![用 Instapaper 临时显示当前网页文章](https://cl.ly/c0631e/instapaper.png)

用 Instapaper 临时显示当前网页文章

注意：第一次运行该小书签时，会被要求登录 Instapaper。

### 高亮特定关键词

阅读网页时，我们经常会希望让一些内容醒目显示，例如高亮文档中的特定术语、新闻报道中反复出现的人名等，以起到辅助阅读的效果。为此，用 ⌘F 开启自带的查找功能当然是最简单的做法，但 Safari 的查找功能并不好用，加入了很多不必要的遮罩和动画元素，反而会干扰阅读；另外，⌘F 只能做到每次高亮一个关键词。如果你被类似的问题困扰过，可以试一试下面这个小书签：

[🖍 Highlight…](javascript:(function()%7Bvar%20count=0,%20text,%20dv;text=prompt(%22Search%20phrase:%22,%20%22%22);if(text==null%20%7C%7C%20text.length==0)return;hlColor=prompt(%22Color:%22,%20%22yellow%22);dv=document.defaultView;function%20searchWithinNode(node,%20te,%20len)%7Bvar%20pos,%20skip,%20spannode,%20middlebit,%20endbit,%20middleclone;skip=0;if(%20node.nodeType==3%20)%7Bpos=node.data.toUpperCase().indexOf(te);if(pos%3E=0)%7Bspannode=document.createElement(%22SPAN%22);spannode.style.backgroundColor=%20hlColor;middlebit=node.splitText(pos);endbit=middlebit.splitText(len);middleclone=middlebit.cloneNode(true);spannode.appendChild(middleclone);middlebit.parentNode.replaceChild(spannode,middlebit);++count;skip=1;%7D%7Delse%20if(%20node.nodeType==1&&%20node.childNodes%20&&%20node.tagName.toUpperCase()!=%22SCRIPT%22%20&&%20node.tagName.toUpperCase!=%22STYLE%22)%7Bfor%20(var%20child=0;%20child%20%3C%20node.childNodes.length;%20++child)%7Bchild=child+searchWithinNode(node.childNodes%5Bchild%5D,%20te,%20len);%7D%7Dreturn%20skip;%7Dwindow.status=%22Searching%20for%20'%22+text+%22'...%22;searchWithinNode(document.body,%20text.toUpperCase(),%20text.length);window.status=%22Found%20%22+count+%22%20occurrence%22+(count==1?%22%22:%22s%22)+%22%20of%20'%22+text+%22'.%22;%7D)();)

运行该小书签后，Safari 会先后弹出两个输入框，分别用于指定要高亮的关键词和要使用的高亮颜色（默认为 `yellow` 黄色，可以输入任意合法的[颜色名称](https://www.w3schools.com/colors/colors_names.asp)或 Hex 颜色代码）。

![用不同颜色标记网页中的关键词](https://cl.ly/02c30c/highlight.png)

用不同颜色标记网页中的关键词

* * *

以上就是我平时常用的改善网页阅读效果的小书签。要获得最便捷的使用效果，建议将这些小书签保存在「个人收藏」（Favorites）文件夹中，并且保持书签名称以一个相关的 emoji 开头。这样，无论在 macOS 还是 iOS 上，只要点按地址栏就可以直观地看到这些功能的图标，并且便于直接点击运行。

另外，不要忘记收藏栏的隐藏快捷键——⌥⌘-\[书签编号\]。例如，上文提到的修改字体和字号这两个小书签分别保存在我收藏夹中的第二和第三个位置，因此，在遇到难看的网页时，只要先后按下 ⌥⌘2 和 ⌥⌘3 两组快捷键，就可以迅速获得一个可接受的阅读效果。

最后，你可以在[这里](https://github.com/firexcy/bookmarklets)找到本文提及的小书签的代码，并根据自己的需求修改使用。
