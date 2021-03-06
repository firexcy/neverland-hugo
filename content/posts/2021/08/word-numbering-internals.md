---
title: "Word 编号的内部结构与工作原理"
date: "2021-08-10"
tags:
  - "microsoft-office"
  - "tutorial"
---

**注：**本文为发布在少数派上的 [付费教程](https://sspai.com/series/183) 节选。利益相关：员工。

* * *

在从宏观角度了解 Word 中的编号如何定义和应用后，我们再将镜头拉近，观察编号段落的内部结构。

再次回忆：**编号是段落格式的一部分，也必须依附于段落而存在。**本质上，编号只是段落首行开头处的一个文本范围（run），和普通段内文本一样有着字体、字号、颜色等文本格式属性，但其特殊之处在于：其一，编号的内容是根据一系列规则自动计算和生成的，而不是手动输入的；其二，编号有自己的对齐和缩进设置，因此会波及地影响其所在段落的实际缩进。

要有一个直观的认识，只要点击任一一个编号数字，灰色底色覆盖的部分就是编号部分的范围。不过，这个看起来自成一体的编号范围，其内部实际上是由很多部分组成的：

![](https://p178.p0.n0.cdn.getcloudapp.com/items/12uAzPwj/dd1931b4-5225-4549-a4b7-f61944367d39.png?source=viewer&v=6ba2cab9686e8f74fb5336072d020407)

上图中的概念很多，我们结合编号设置的主阵地——「定义新多级列表」对话框中的选项逐一介绍。

要打开「定义新多级列表」对话框，可以在任意编号上单击右键，选择「项目符号和编号」，然后单击「多级符号」选项卡下的「自定义」按钮；或者单击工具栏上的「多级列表」按钮，在下拉菜单中选择「定义新的多级列表」。

可以看出，该对话框被一道分隔线分为「编号格式」和「位置」两个部分；此外，「字体」按钮还可以打开一个类似于普通字体对话框的界面。这三个部分也就分别对应了编号格式的三大类——与编号数字、对齐方式和编号字体相关的设置。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/xQubOzQl/adb0e1d9-c30a-4590-9557-fcdf58894647.png?v=33338a86a15c4da59aecedcca1e7b0e4)

#### 1\. 与编号数字相关的格式

**编号格式：** 即以什么数字或文字显示编号。Word [实际支持的编号格式](http://webapp.docx4java.org/OnlineDemo/ecma376/WordML/ST_NumberFormat.html) 有数十种之多，会根据语言版本不同显示不同选项（例如中文版会提供「壹、贰、叁」等中文大写数字，日文版会提供「壱、弐、参」等日文大写数字），这里不一一列举。

注意这里的下拉菜单只负责设置编号中的变量，即数字部分；数字前后的固定文本（例如「第一章、」中的「第」「章」二字和后接的顿号）需要在旁边的文本框中手动输入。

**包含上级编号：** 很多场景下，除了需要显示当前级别的编号，还要包含上级编号。这时，可以在「包含的级别编号来自」下拉菜单中选择需要的级别，相应的上级编号会被追加到编号格式文本框中，你可以反复操作直至添加完所有所需的级别。同样地，你需要手动输入组合编号中的固定部分（例如「5.1(a)」中的句点和括号）。

如果需要在某级编号中包含所有上级编号、且全部使用阿拉伯数字（形如 `1.2`，`2.3.3` 等），则可以勾选**「正规形式编号」**（legal style numbering，直译为法律格式编号，因在英美法律文书中常用，故名）。

**起始编号和重新开始编号的间隔：** 这两个选项都与编号数字的「起点」相关。其中，「起始编号」很好理解，就是该级数字从序列中的第几个起算，例如如果设置为 2，则该级数字会（取决于数字格式）从 `2`、`B` 或 `乙` 开始。

「重新开始编号的间隔」则指该级数字应在遇到哪一上级后重新起算。注意这里可以选择在**任一上级编号**后才重置，未必是**紧邻**的上级编号。例如，在下面的编号序列中，二级编号`（一）, （二）, ...` 和三级编号 `1. , 2. ， ...` 都被设置为在一级编号后重置，因此 `第一节（二）` 下的编号 `2.` 并未重置，直到遇到下一个一级编号 `第二节` 才重新从 `1.` 起算。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/NQuw4E04/939ec11a-6fc0-4805-a2e0-17606c47806c.png?v=50e7ba67ccfedab5fd0e0c8084d141d6)

不难看出，上述与编号数字相关的设置都仅仅是计数规则，而从未包含数目本身。的确，Word 从不会直接记录任何编号数字，而是根据段落套用的编号规则，现场「掰手指」算出编号的值，显示在段落开头。

因此，如果你看到两个段落位置上紧邻、编号上连续，这并不表明它们是「一家人」，属于同一个编号序列（或用 OOXML 的术语来说，引用同一个编号实例）。例如，两个显示了编号 `10.` 和 `11.` 的段落完全可能分属甲乙两个不同序列，其中前一个段落是甲序列中的第十个，后一个段落是乙序列中的第一个，只是乙序列恰好设置为从 11 起算——就好像哪怕马拉多纳穿 10 号球衣，姚明穿 11 号球衣，他们也不是一个球队的。

![一组「貌合神离」的编号示例，第 11 项与之前编号不属于同一序列（注意观察底色），因此并不服从于其他编号的格式设置](https://p178.p0.n0.cdn.getcloudapp.com/items/8Lub1bep/3b9544d4-9c78-4283-9b45-c153b102dc5a.gif?source=viewer&v=682692acb09c8cca6d48972ebbed3816)

这种「关公战秦琼」的情况经常发生于在多个文档间来回复制编号的场合。与很多用户想象的不同，当编号被移植到另一个文档时，它未必会自动融入到新文档的编号序列中，而往往会保持原来的编号层级、序列和样式。只是迫于用户的强迫就范——例如手动拖拽标尺、设置字体和滥用编号项右键菜单中的「重新开始编号」（真名是「从这里分拆出一个新编号序列」）和「继续编号」（真名是「从这里缝合两个编号序列」），才显得跟上下文的编号打成一片。一旦事后再次调整编号样式，这些貌合神离的编号就会露出真实面目，显得不听使唤。

要避免这种情况，在移动编号段落时，应当尽量以 Word 粘贴选项中的「纯文本」或「匹配目标格式」方式粘贴，从而去除段落先前带有的编号信息。如果要鉴别编号序列是否存在间断，可以单击要检查的编号，使其处于选中状态，只有与其属于同一序列的其他编号才会一并显示底色。

#### 2\. 与对齐方式相关的格式

**编号对齐方式和对齐位置：** 编号有三种对齐方式，左对齐、居中对齐和右对齐，都是**相对于所在段落的左侧边缘**而言的，分别指编号文本的左侧边缘、中心线或右侧边缘与段落的左侧边缘对齐。而所谓的「对齐位置」就是指上述对齐基线的位置，这是一个绝对数值，从标尺的零点起算。下图中三个段落的编号对齐位置都是 0 英寸，可以看到，后两个设置了居中对齐和右对齐的编号向左突出了一部分。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/wbuwB9BX/566d065d-ecae-4693-bf4b-483e3233ec2c.png?v=74aaed3bc7468a7f783f9e86601fba57)

可见，仅在编号对齐方式设置为左对齐时，对齐位置等价于于编号段落的首行起点。对于居中或右对齐的编号，对齐位置控制的是编号的中间线或右边缘位置，因此段落的视觉起点会延伸到更靠左的位置（例如本节开头图中的第四行）。

（**注：** 顺带一提，如果你对于经常出现在缩进设置中的 0.63、1.27、1.9 和 2.54 这几个默认数值感到眼熟却莫名其妙，是因为……微软是一家满脑子英寸制美国公司，这几个默认数值是从 0.25 英寸、0.5 英寸、0.75 英寸、1 英寸换算成厘米产生的。为简明起见，本文举例时暂将 Word 的单位设置改为英寸值。）

**「编号之后」和制表位添加位置：** 这组设置决定了编号后的实际文本从何处开始。其中，「编号之后」可在「制表符」（默认）、「空格」和「无」之间选择。比较简单的情况是设置为「无」（或「空格」）。此时，实际文本会紧随编号文本（或附加一个额外空格）后立即开始。

但如果「编号之后」设置为「制表符」（tab），那么编号和实际文本之间会间隔一个制表符的长度。可那到底是多长呢？答案是……「看情况」。

Word 中的制表符是一个长度可变的字符，它很像中学物理课上那辆运动在光滑平面上的小车，会一直延伸到下一个**制表位**（tab stop，起源于打字机上用于控制对齐的 [同名装置](https://en.wikipedia.org/wiki/Tab_stop)）为止。对于没有手动设定制表位的段落，Word 默认将标尺上每 0.5 英寸（0.63 厘米）当作一个制表位（段落的悬挂缩进位置也视为一个制表位）。

因此，如果编号内容结束于 0.49 英寸处，那么随后的制表符会延伸到 0.5 英寸的位置。换言之，编号与实际文本只间隔了 0.01 英寸。但如果编号内容结束于 0.51 英寸，那么制表符会延伸到下一个默认制表位，即 1 英寸处，此时编号与实际文本间隔了 0.49 英寸。

这就解释了下图上半部分所示的常见问题：10 以上编号之后的实际文本从很远的位置才开始。这是因为随着编号进入两位数，所占空间变得更大，已经来不及在前一个制表位（下图中的 0.5 英寸位置）之内结束，于是实际文本被「挤」到了下一个制表位（1 英寸位置）。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/kpuKOkAD/11088456-fa9f-49c0-95c9-f0ba42956def.png?v=26b1737ea3caee155e5a96b91c38764a)

这时，「制表位添加位置」就能派上用场。它是指在编号段落的指定位置增加一个自定义的制表位，从而覆盖其左侧的全部默认制表位（悬挂缩进除外）。

还是以上图为例，观察到所有编号末端都不会超过 0.6 英寸，故通过在该处添加一个制表位，就可以实现所有让各段的文本起始位置本对齐到 0.6 英寸的效果（如下半部分所示）。

**文本缩进位置：** 这是一个让人一言难尽的设置。不妨做一个实验：先将该项数值填写为 0，然后不停单击右侧的上箭头，逐渐增大设置，同时观察预览框中的变化。可以发现，该设置最初只会影响第二行开始的缩进距离；可一旦增大到超过编号部分的宽度，继续上调数值就会同时影响首行实际文本的起始位置。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/v1ubQ0Dd/e8ddf89c-bd44-40e2-9a28-7ca3fd2955f6.gif?source=viewer&v=a812f8307ce853553618b5313665a147)

可见，「文本缩进位置」并不是一个独立的参数，它只是在间接调整着编号段落的特殊缩进：

- 当**文本缩进位置 < 编号对齐位置**时：相当于设置首行缩进，后续行文本将从编号对齐位置（也就是编号段落的左侧缩进）更左边开始；
- 当**文本缩进位置 = 编号对齐位置**时：相当于关闭特殊缩进，后续行文本将从编号对齐位置开始；
- 当**文本缩进位置 > 编号对齐位置**时：相当于设置悬挂缩进，后续行文本将从编号对齐位置的右边开始；并且因为悬挂缩进位置被视为制表位，首行文本也将被编号后的制表符（如果有）「推」到缩进位置，于是最终结果就是首行文本和后续行文本对齐。

细心的读者可能发现少了一种情况：但如果想让后续行文本比首行文本的缩进更大呢？答案是使用上文介绍的「制表位添加位置」选项，在文本缩进位置之前添加一个制表位，从而将首行文本「堵」在这个制表位上。

下图演示了这四种不同情况：

![](https://p178.p0.n0.cdn.getcloudapp.com/items/12uARqGo/d741ccf2-964b-40bc-9884-e80921d3fa1a.png?v=472edf283f4443f5769cf5e0d82c0c37)

显然，「文本缩进设置」设计是复杂且令人困惑的，也违反了尽量避免操作副作用的程序设计原则。但木已成舟，从用户角度，我们能做的也只是提醒自己在设置时多做几个心算，同时注意观察预览图和标尺。

#### 3\. 与编号字体相关的格式

这部分相对简单明了，即在编号定义对话框中点击「字体」按钮打开的设置，与普通段内文本的字体设置无异。

不过，在编号定义对话框中做的字体设置会应用到所有编号项中。如果你想单独修改（或重置）某处特定编号的字体设置（例如从别处复制而来的编号段落附带了奇怪的格式），可能会发现编号部分是无法直接用鼠标选中的。如何解决呢？

如之前的段落一章中所讨论，作为段落格式的一部分，编号的字体格式也是由所在段落结尾的换行标记所控制的。因此，只要打开换行标记的显示，然后对换行标记进行字体设置，就能间接地修改编号的字体，比如……

![](https://p178.p0.n0.cdn.getcloudapp.com/items/WnuYZKE1/bc6da8be-ff37-484b-b3e7-558cca1d8597.png?v=45ee169d6a5ea3b982d5fbde23fade27)

从另一个角度说，这也提示我们要特别保护好段落标记这个编号的「命门」，在复制粘贴、使用格式刷等避免选中不必要的段落标记，导致编号格式被覆盖或丢失。

## 编号的工作原理

在了解了编号设置方式和内部结构的基础上，我们最后再深挖一下编号的工作原理。

文章开头将编号功能比作「艺术」，并不纯粹是种揶揄。在批评文学艺术时，柏拉图曾说艺术是模仿的模仿、影子的影子，与真理隔了三层。柏拉图认为，现实世界是对理念世界的模仿，而艺术又是对现实世界的模仿。

类似地，Word 中的编号也是从一个抽象的范式出发，经过逐层「模仿」和「套用」，最终变成为文档中显示的实际编号数字。

在这个模仿链条的最上层，是 Word 文档通过内部编号部件（`numbering.xml`）存储的一系列编号定义（OOXML 标准称「抽象编号定义」，abstract numbering definitions）。定义的开头是名称、类型、链接的段落样式等基本信息，然后依次列举九级编号各自的格式。上文介绍的「定义新的多级列表」对话框中的各个选项，在编号定义中都有对应的属性。

编号定义并不会被直接使用。对于文档中每一套编号，Word 都会以一个现有编号定义为模板，建立一个「实例」（OOXML 标准称「编号定义实例」，numbering definition instances）——描绘出一个「仿制品」。这个「仿制」过程并不完全是照葫芦画瓢，而是可以根据需要覆盖模版中的部分设定。

使用上文介绍的各种方法创建编号时，都会导致新的编号定义和编号实例被创建出来。其中，通过自动编号和多级列表功能创建编号时，Word 文档的编号部件 `numbering.xml` 中会出现一对新的抽象编号定义以及一个引用该定义的编号实例。而用样式定义功能创建编号时，除了编号定义和编号实例，样式部件 `styles.xml` 中还会多出一个样式定义，它本身不记录任何编号格式，唯一的作用就是记录这个列表样式的名称。

最后，当将一个段落设为编号段落时，Word 在该段落的属性中写下要套用的编号实例 `numId` 和所属层级 `ilvl`。这样，就可以据此逐层查阅编号部件中的实例和定义，确定要显示的编号数字和格式。

以下图中的第二个段落 `b) [...]` 为例，其所在段落的属性表明该段落的编号层级为第二级、套用 id 为 42 的编号实例；Word 据此前往编号部件中检索相应的编号实例，发现它把皮球踢给了 id 为 24 的抽象编号定义；最终，在这个抽象编号定义中，Word 找到了第二级编号应当具有的格式设置，从而显示在文档中。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/eDuj7jPW/6c6b65a2-23b7-4516-a61c-1c1c658a7ace.png?source=viewer&v=b3dcce2cd4356374195ec4d6ece55397)
