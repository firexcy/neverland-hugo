---
title: "Apple Watch 指针表盘 —— The Missing Manual"
date: "2020-10-31"
categories: 
  - "post"
tags: 
  - "apple"
---

尽管 Apple Watch 的各个表盘总体延续了苹果软件上手即用的家族特征，但其中仍然存在简洁与复杂的风格之分。特别是有几个包含多种子表盘、刻度的指针表盘，其功能和用途并不是一目了然的。

遗憾的是，或许是为了把更多笔墨留给健康检测、运动记录这些「智能」味更浓的功能，Apple Watch 官方使用手册的「[表盘与功能](https://support.apple.com/zh-cn/guide/watch/apde9218b440/watchos)」章节非常粗略，只是以流水账形式列举了表盘的造型和功能，具体操作方法则都留给用户自己脑补。而网上的 Apple Watch 和 watchOS 评测虽然数量繁多，但也基本都对表盘一笔带过，或者照抄苹果在发布会和文案中的描述。

作为一个缺少机械表背景知识的用户，我对 Apple Watch 中的复杂表盘一直是一知半解的，watchOS 近来新增的正计时、GMT 等表盘更是让我一头雾水。在向使用手册和评测文章求助无门后，我只好走上了自学之路。以下就是我的自学笔记，希望对同样困惑于 Apple Watch 复杂表盘具体用法的读者有所帮助。

### 计时码表（Chronograph）

计时码表是 Apple Watch 最早的内建表盘之一，其布局在机械表中也属常见设计，但 Apple Watch 的版本仍然借助数字化的优势提供了更多灵活性。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/Blu1q6j9/chrono.png?v=ba34f3d223a8e9c198561d04a0627b74)

默认状态下：

- 外圈刻度、时针和分针与常规表盘相同；
- 秒针静止，始终指向 12 点方向；
- 两个小表盘中，12 点钟方向的表盘静止，6 点钟方向的表盘指示当前分钟的秒数。

轻按表盘右上角的按钮，表盘将进入**计时模式**。该模式下：

- 外圈刻度变为用户设定的标度，可在每圈 3/6/30/60 秒中选择，秒针每转一圈即表示经过相应的秒数；
- 两个小表盘中：
    - 12 点钟方向的表盘指示经过的分钟数，其刻度疏密随用户设定的外圈标度而变；
    - 6 点钟方向的表盘变暗，仍然指示当前分钟的秒数；
- 右上角为开始/停止计时按钮；
- 右下角为分段/重置按钮，在计时中按下可新增一个分段（用于记录跑步中的每圈用时等），同时表盘上会新增一根蓝色的秒针指示该圈经过的秒数；停止计时后再次按下，可返回普通模式。

### 专业计时码表（Chronograph Pro）

这是 watchOS 7 的新增表盘之一，在 Series 4 及以后的型号（即具有「圆角屏幕」的型号）上才能启用。该表盘的「专业」属性体现于更多的子表盘和支持[视距仪](https://en.wikipedia.org/wiki/Tachymeter_(watch))（tachymeter）功能。

![Zenith Chronomaster El Primero Revival](https://p178.p0.n0.cdn.getcloudapp.com/items/GGurdwxm/zenith.jpg?v=0658aaff025affbd8c1dc2464e12eef3 "Zenith Chronomaster El Primero Revival")

Zenith Chronomaster El Primero Revival

默认状态下：

- 外圈刻度、时针和分针与常规表盘相同；
- 三个小表盘中，3 点钟和 9 点钟方向的表盘静止，6 点钟方向的表盘指示当前分钟的秒数。

轻按表盘外圈，表盘将进入**计时模式**。该模式与上述「非专业版」计时码表的计时模式基本相同，主要区别在于：

- 开始/停止计时按钮和分段/重置按钮从右侧移至下侧；
- 原本位于 12 点钟方向的小表盘移至 3 点钟位置，仍然指示经过的分钟数；
- 9 点钟方向增加了另一个小表盘，用于以更大颗粒度显示经过的分钟数（如将外圈标度设置为 3 或 6 秒）或小时数（如将外圈标度设置为 30 或 60 秒）

![](https://p178.p0.n0.cdn.getcloudapp.com/items/WnurXPzR/chronopro.png?v=b263f10d1f974c74e8a5e6fc79d5b20a)

特殊地，如果将表盘编辑为「视距仪」，则轻按表盘外圈后表盘将变为**视距仪模式**。该模式下：

- 外圈刻度是一组数值渐小而间距渐大的数字，每个数字与该刻度原本对应的秒数的乘积总是 3,600（一小时中的秒数）。
- 因此，刻度指示的数字就是**速率**（rate），即以对应秒数为单位时间重复做某事时，一小时内能完成的次数。
- 例如：
    - 在汽车匀速行驶中开始计时，驶过一公里后停止计时，则秒针指向的数字就是当前速度对应的公里时速；
    - 在折千纸鹤时开始计时，折完一个后停止计时，则秒针指向的数字按当前效率每小时能折出的个数。
- 小表盘的功能与普通计时模式相同。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/geuqBX8r/tachymeter.jpeg?v=c9ed0d4344b424c4ce9030d1155190aa)

一个值得注意的细节是，**计时状态是在所有计时码表/专业计时码表表盘间同步的，且不受编辑表盘操作的影响。** 因此，在一个表盘上开始计时后切换到其他码表类表盘，或者编辑表盘切换外圈标度，计时仍将继续、且会适应当前表盘的标度来显示。

### 正计时（Count-Up）

正计时表盘是 watchOS 7 的新增表盘，其现实中的原型是[潜水表](https://en.wikipedia.org/wiki/Diving_watch)（Dive Watch）。由于潜水活动往往需要控制水下时间，潜水员会在入水时将潜水表外圈上的标记手动旋转到和分针对齐，这样，在水下就能直接根据分针指向的数字读出经过的时间。

![Three Seiko 55th Anniversary Dive Watches](https://p178.p0.n0.cdn.getcloudapp.com/items/Blu1q60E/seiko.png?v=134cf07e8463180c928cbcbd6dad184a "Three Seiko 55th Anniversary Dive Watches")

Three Seiko 55th Anniversary Dive Watches

默认状态下，刻度和指针的行为与常规表盘相同。

轻按表盘外圈，表盘将进入正计时模式。该模式下：

- 位于 12 点钟方向的倒三角形标记（marker）将会自动旋转到与分针对齐——
    - 此时直接按下绿色的「开始」（Start）按钮，表盘将从零开始向上计时；
    - 也可以先转动表冠令倒三角形标记偏离分针，再按下「开始」按钮；表盘将以偏离的分钟数为起点向上计时；
- 随着计时推移，分针扫过的路径上将会出现更多小刻度，每一个小刻度即代表经过一分钟。此外，分针指向的外圈数字即为经过的分钟数；
- 正计时过程中轻按表盘，当前计时读数将以数字形式放大显示，按下该界面的「停止」按钮即可结束计时。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/5zuwvlWd/countup.png?v=9b56c9cffedd86c6bb85da51ad38dacb)

### GMT 表盘

GMT 表盘也是 watchOS 7 的新增表盘，其现实中的原型是 [24 小时手表](https://en.wikipedia.org/wiki/24-hour_analog_dial#Watches)（24-hour watch）。这种手表具有可以旋转的外框，从而实现同步显示 GMT 时间和当地区时的功能，非常适合飞行、航海等场景。

![The Zodiac Aerospace GMT Limited Edition](https://p178.p0.n0.cdn.getcloudapp.com/items/OAuJNeEA/zodiac14.png?v=9617b3fac4286fc84edda742f37b505c "The Zodiac Aerospace GMT Limited Edition")

The Zodiac Aerospace GMT Limited Edition

默认状态下：

- 刻度和指针的行为与常规表盘相同；
- 外圈有 24 个刻度，对应一天中的 24 个小时，当前时刻由红色时针指示，且外圈上对应的刻度将变为数字显示；
- 外圈底色由用户设定的两种颜色平分，分别对应 6 PM 至 6 AM 和 6 AM 至 6PM 的刻度。

旋转数字表冠，表盘将显示世界各主要城市（及自动定位的当前所在地）的时间列表。选定一个城市后按右下角的确认按钮，即可将该城市所在时区设定为第二时区，此时：

- 内圈 12 点方向显示该城市的简写名称；
- 红色时针和外圈数字刻度指示第二时区的时间；
- 倒三角形的标记指向第二时区午夜 12 点对应的本地时间；
- 外圈的底色不再平分，两种底色的交界点为第二时区的日出/日落时间。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/eDuPeJky/gmt.png?v=159ed25b5d9d36ffb581425ebc811055)

这里，一个个性化技巧是，由于可以通过 iPhone 上的 Apple Watch App 自定义城市的英文简称（「时钟」>「城市简称」），只要将某个城市的简称改为想要显示的字样，再通过上述步骤将该城市设定为第二时区，就可以间接实现**在 GMT 表盘上显示任意文字**的效果。

### 太阳刻度盘（Solar Dial）

太阳刻度盘是随 watchOS 6 推出的，也是我心目中最兼具美观和实用的内建表盘之一。这个表盘在现实中并无形态固定的对应设计，具有类似功能的手表一般都是比较「天马行空」的特别款。（当然，中国传统的日晷在某种意义上也算是一个「太阳刻度」的仪表。）

![The Ochs Und Junior Day/Night](https://p178.p0.n0.cdn.getcloudapp.com/items/7Ku8n9dP/solar.png?v=f84c0a763eec0a2ca2e95bb1410c4c73 "The Ochs Und Junior Day/Night")

The Ochs Und Junior Day/Night

太阳刻度盘的设计细节很难列举完全，建议阅读钟表媒体 Hodinkee 为其专门写的一篇[《Apple Watch 太阳刻度表盘的另类之美与黄昏的剖析》](https://www.hodinkee.com/articles/the-eerie-beauty-of-the-apple-watch-solar-face-and-the-anatomy-of-nightfall)（_The Eerie Beauty of the Apple Watch Solar Face, and the Anatomy of Nightfall_）。概括而言：

- 外圈共有 24 个刻度，对应一天中的 24 个小时，其中，12 点钟方向为正午 12 时，6 点钟方向为午夜 12 时；时针末端根据当前的日出或日落状态显示为实心或空心；
- 时针的另一端是一个「迷你」表盘，可设置为数字或模拟表盘，以常规形式显示时间；
- 在内圈上，日出和日落的时刻附近各有四个圆点，从下往上分别对应太阳高度为地平线下 18°、12°、6° 和 0° 50'（即日出/日落，非 0° 的原因是存在[大气折射](https://en.wikipedia.org/wiki/Atmospheric_refraction)）的四个时刻，这就将白天与黑夜间的[暮曙光](https://zh.wikipedia.org/wiki/%E6%9B%99%E6%9A%AE%E5%85%89)（twilight）分为三个阶段：
    - 当 -6° ≤ 太阳高度 < -0° 50' 时，为**民用曙暮光**（civil twilight）。该时段主要关系到人的生活，被认为是尚可不借助补光继续从事户外活动的时间，一个与其相关的近似时间段——日落后 30 分钟至次日日出前 30 分钟——还关系到是否[需要开车前灯](https://en.wikipedia.org/wiki/Lighting-up_time)（lighting-up time）、是否构成[普通法上抢劫](https://en.wikipedia.org/wiki/Burglary)（burglary）等法律规定。
    - 当 -12° ≤ 太阳高度 < -6° 时，为**航海曙暮光**（nautical twilight）。之所以与「航海」挂钩，是因为在该时段，天空处于一个暗到可以看见星星，但亮到可以看见地平线的状态，对于海上导航意义重大。
    - 当 -18° ≤ 太阳高度 < -12° 时，为**天文曙暮光**（astronomical twilight）。该时段的「天文」意义在于，此时天空不被太阳照亮，所有肉眼可以看见的天体（最暗约六等星）逐一呈现或消失。
- 点按表盘，界面上将会显示当前的白天/黑夜状态以及日照时间；
- 转动表冠，可以操作时针查看当天其他时刻的太阳高度状态，小表盘还会对应显示该时刻与当前时刻的差值。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/X6udXyWQ/solardial.png?v=c039b795a5db1057fa56c4d00b2832c0)

### 尾巴

自问世以来，Apple Watch 的表盘就一直备受诟病。的确，与基于 Android、Tizen 等系统的智能手表相比，Apple Watch 的表盘既数量有限、又不向第三方开放，个性化和功能扩展的空间都显得落后。

之前，我也常常持这种批判观点，但这番仔细观察 Apple Watch 内建表盘的经历让我的态度大为改观。这些表盘给我的印象是，相比于显示更多功能，它们将更多功夫花在了「计时」这项手表的本职工作上，哪怕很多功能注定是小众或晦涩的（例如视距仪、暮曙光刻度）。这固然不能弥补个性化和功能缺失的遗憾，但个中体现出的设计功力和苹果式的细节控仍然是值得赞赏、未见超越的。

此外，Apple Watch 中的指针表盘虽然都有现实中的原型，但其设计并未拘泥于对机械表的模拟（analog），而是充分利用了数字介质的优势，在形态、功能等方面加以扩充，例如随时间、地点动态变化的配色、刻度等。这不禁让人想起乔布斯在发布初代 iPhone、展示触屏键盘功能时，也正是重点强调了其「呼之即来招之即去」、随输入框切换形态的灵活性。对于那种相较机械表的精工细作，数字表是否流于肤浅的质疑，这种源于而又高于的灵活性，或许就是一种有效的回应。

但也正因如此，Apple Watch 使用说明和媒体评测对于表盘的忽视就越发令人不解。对于苹果，向用户说明基础功能的操作方法和设计思路，既是宣传上的加分，也是应尽的义务。对于媒体，要避免评测陷入「交作业」的窠臼，仅靠摆拍和抖机灵是不够的，还需要多下一点追根究底的「无用」之功。比如，先从重新认识暮色的三个阶段开始？
