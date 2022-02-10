---
title: "「第一步」>「第二步」，还是「第一步 - 第二步」？"
date: "2019-04-17"
categories: 
  - "post"
tags: 
  - "design"
  - "typography"
---

在写操作说明类文章时，经常需要描述包含多步的操作。这种场合，我个人倾向的用法是 `「第一步」>「第二步」`。这个用法最初是从苹果那里学来的，中文的苹果说明书统一使用 `“第一步” > “第二步”` 的体例，将其中的引号换成直角引号，就是我的用法。

不过，最近我发现少数派的编辑总是会把首页文章手工改成 `「第一步 - 第二步」` 的形式。经过沟通，得知那是他们的内部体例，理由是苹果早年的用法是 `“第一步” - “第二步”`，而他们一方面和我一样想换用直角引号，另一方面又嫌步步打引号太啰嗦，而且直角引号和连字符之间间距太大，所以简化成了现在的形式。

个人角度，我觉得这种用法在视觉上还算清晰，但语义上不太说得通。第一，如果给每个步骤单独打上引号，可以认为是在使用引号「表示特定称谓」的功能；但只在整个步骤的首尾打上引号，似乎在功能上找不出什么理由。如果只是为了和前后文作视觉区隔，用空格或者粗体会不会更简单有效呢？第二，如果选择用「横线」连接各个步骤，或许更规范的做法是选用 em dash（`—`）而不是连字符。

当然，体例问题很多时候无所谓对错，关键是统一，所以我只是建议他们把这些内部规范公布出来，以便用户参考。

借此机会，我还顺手查了一下几家主流系统厂商的内部规范：

[《苹果体例指南》](https://help.apple.com/applestyleguide/#/apsg72b28652)（_Apple Style Guide_）：

> _Pull-down menus:_ A pull-down menu is a menu in the menu bar. When you give instructions for choosing an item from a pull-down menu, use the style shown here.
> 
> Choose \[_menu_\] > \[_item_\] > \[_submenu item_\].
> 
> Choose Edit > Find > Find Next.
> 
> Choose File > Save As.
> 
> Don’t use an angle bracket when you’re simply identifying which menu contains the item.
> 
> _Correct:_ the Page Setup command in the File menu
> 
> _Incorrect:_ the File > Page Setup command

[《微软体例指南》](https://docs.microsoft.com/en-us/style-guide/procedures-instructions/writing-step-by-step-instructions)（_Microsoft Style Guide_）：

> **Simple instructions with right angle brackets**
> 
> Abbreviate simple sequences by using right angle brackets. Include a space before and after each bracket, and don't make the brackets bold.
> 
> **Example**
> 
> Select **Accounts** > **Other accounts** > **Add an account**.
> 
> **Accessibility tip** Screen readers may skip over brackets and read instructions such as **Menu** > **Go To** > **Folders** as _Menu Go To Folders_, which might confuse customers. Check with an accessibility expert before using this approach.

[《谷歌开发者文档体例指南》](https://developers.google.com/style/procedures)（_Google Developer Documentation Style Guide_）：

> Multi-action procedures
> 
> In general, use one step per action. However, you can combine small actions into one step, using arrows (>) for sequential menu selections.
> 
> **Recommended:**
> 
> 1\. Click **Next** > **Finish**.
> 
> Also recommended:
> 
> 1\. Click **File** > **New** > **Document**.
> 
> Don't make the steps too long. If they feel too long, consider splitting them into multiple steps.

几点观察：

1. 在步骤之间的符号选择上，三家公司都使用了大于号（`>`）。不过，苹果和微软嘴上说的都是用右尖括号，即使自己打出来的还是大于号，或许是意识到前者不太方便输入吧。至于谷歌管这符号个叫「箭头」（arrow），就实在有点莫名其妙了。
2. 微软和谷歌都选择了将各步的菜单名称加粗，但苹果没有这么做。在英文语境下，加不加粗倒基本只是醒目程度的区别，因为英文单词之间天然有空格。但如果写的是中文，又不加任何区别的话，菜单项名称就可能与前后文混淆。或许这也是为什么苹果中国在做本地化的时候会给菜单项额外打上引号。
3. 几份指南都提示应该考虑是不是一定要用这类简写式来描述操作步骤。例如，如果只是描述菜单的包含关系，最好直接写成「某菜单项下的某子菜单项」；更复杂的步骤，最好拆成几步描述，而不是堆砌一长串菜单名称。微软还特别指出这种简写法可能给使用读屏器的视力缺陷用户造成困扰。
