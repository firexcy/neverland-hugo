---
title: "播客客户端音频特效探微"
date: "2017-03-20"
categories: 
  - "post"
tags: 
  - "app"
  - "podcast"
  - "review"
---

**修订**

2017/05/27：加入了对 Castro 2.4 版中 Enhanced Audio 功能的测试。

* * *

## 问题的提出

播客可能已经迎来了自己最好的时代。随着聆听播客时间日渐延长，用户自然也会对播客传播流程中的最后一站——播客客户端提出更高的要求。因此，播客客户端市场的繁荣也是情理之中的了。

目前，市场上知名度和评价最高的播客客户端当数 [Castro](https://itunes.apple.com/us/app/castro-podcast-player/id1080840241?mt=8)、[Overcast](https://itunes.apple.com/us/app/overcast-podcast-player/id888422857?mt=8) 和 [Pocket Casts](https://itunes.apple.com/us/app/pocket-casts/id414834813?mt=8) 三款。其中，Castro 凭借流畅的动效和独特的 RSS 式管理方法独树一帜；Overcast 背靠 Marco Arment 的个人影响力和技术实力、以及不断演进的收费策略，牢牢把控话题点；而 Pocket Casts 则有着精致的设计和少见的跨平台支持，同样吸引了大批拥趸。

然而，播客客户端其实并非一个功能复杂的应用形态。**无论怎样创新，它的核心功能永远只有一个：播放。**相对于其他热门应用类别，用户花在与其进行视觉交互上的时间是相当有限的。因此，要在激烈的竞争中脱颖而出，开发者就必须将眼光放在那些用户「看不见」的地方，靠提升播放体验的软实力聚集人气。事实上，Overcast 之所以能在早期吸引大批用户，一个重要原因就是它具有两个「杀手级」功能：Smart Speed 和 Voice Boost，前者能减少播客节目中的停顿，后者则能提高人声的音量。后来，Pocket Casts 在一次大版本更新中也增加了这两个功能，只不过名称对应地改为 Trim Silence 和 Volume Boost。Castro 则至今未见有类似动作，但根据开发者的语气，这些功能似乎也在他们的开发计划之中。

**2017/05/27 更新：**Castro 2.4 版已加入与 Voice Boost/Volume Boost 类似的 Enhanced Audio 功能，请参见新增的测试内容。

![Overcast 和 Pocket Casts 的播放设置](http://ww1.sinaimg.cn/large/73403117ly1fdrxck4jy3j21060yvamu.jpg)

我们不妨来看看这些客户端自己是怎么宣传的。例如，Overcast 在其[官方首页](https://overcast.fm/)上宣传道：

> **Smart Speed:** Pick up extra speed without distortion with Smart Speed, which dynamically shortens silences in talk shows. Conversations still sound so natural that you’ll forget it’s on — until you see how much extra time you’ve saved. / 动态地缩短谈话节目中的无声部分，以此额外加快速度而不造成失真。对话听起来仍将十分自然，因而你甚至会忘记打开了这个功能——直到你看见省下了多少额外的时间。

> **Voice Boost:** Boost and normalize volume so every show is loud, clear, and at the same volume. Listen in more places, such as noisy cars, and still hear what everyone says without cranking the volume so high for quiet people that the loud ones blow your ears out. / 增强音量并使其均匀，让每档节目听起来都响亮、清晰，且音量均衡。这一功能使你可在更多场合（如嘈杂的车厢中）不用为声音小的主播过多调高音量，就能听清每个人的声音，同时避免被大嗓门刺痛你的耳朵。

而 Pocket Casts 则在其[帮助文档](http://support.pocketcasts.com/article/variable-playback-speed/)中定义道：

> **Trim silence** \[r\]emoves silences from audio without altering the cadence of the host. / 去除音频中的无声部分，而不改变主播的顿挫。

> **Volume boost** \[i\]ncreases the volume of voices, while reducing background noise. / 提高人声音量，同时降低背景噪音。

对此，一个自然的问题是：**这些功能到底能在多大程度上提升播客的聆听体验？**另外，**不同 app 中同类功能的具体表现又有何区别？**弄清这些问题，不仅能帮助我们在市场上众多播客 app 之间作出取舍，也有利于加深对其具体实现机制的理解。下文就试图通过实验逐一回答这些问题。

## 测试方法

软件方面，我们使用 Overcast 3.0.3 和 Pocket Casts for iOS 6.6 进行测试；用于测试的播客节目为 2017 年 3 月 9 日上线的[《Accidental Tech Podcast #212: Meatspace Windows》](http://atp.fm/episodes/212)和 2017 年 3 月 13 日上线的[《一天世界 #50: 华夷变态与文化挪用》](https://ipn.li/yitianshijie/50/)。之所以选择这两档节目，一方面考虑到它们都影响力较大、受众较广，代表性较强；另一方面，两档节目分别具备英文与中文、多人对谈与单人独白、语速偏快和语速平缓的特征，以其为素材，应该能够综合测试播客 app 的表现。

测试时，**将 iPhone 用 Lightning 线连接至 MacBook，用系统自带的 Quicktime Player 录制其音频输出。**为测试 Smart Speed/Trim Silence 功能，在两款 app 中分别打开此选项，但关闭 Voice Boost/Volume Boost，然后播放 ATP #212 的 0:00–1:00、一天世界 #50 的 2:00–3:00 两个片段，录制其输出；测试 Voice Boost/Volume Boost 时则仅打开该选项，关闭 Smart Speed/Trim Silence，录制片段同上。作为对比，另从这两档节目的官方网站下载节目的原始音频文件，截取同样片段备用。最后，将上述素材导入 Adobe Audition CC 中进行分析。

## Smart Speed/Trim Silence

首先看两款 app 在跳过空白功能上的表现。从长度上看，在播放这两段长度均为一分钟的音频时，Overcast 将《ATP》的片段缩短为 54.9 秒、将《一天世界》的片段缩短为 57.4 秒；Pocket Casts 则相应缩短为 51.8 秒和 57.7 秒。考虑到手工测试可能产生的误差，两者并无明显差异。

![](http://ww1.sinaimg.cn/large/73403117ly1fdrxcjz6bnj21z41400vt.jpg)

事实上，**两款 app 最大的差别在于其对空白片段的处理手法。**先从宏观上看：我们将纵轴的比例尺放大，以更好观察响度的细微变化。可以看出，Overcast 输出的频谱图中的黑色部分（即无声部分）要多于 Pocket Casts 的输出，给我们一种后者的剪裁策略总体上更为激进的印象。

![](http://ww1.sinaimg.cn/large/73403117ly1fdrxck4jlzj21z4140gyo.jpg)

这种印象是否正确呢？这就要将镜头拉近，分析具体例子中的表现。下图展示的是《ATP》片段第 3 秒左右的频谱；当时，主播 Marco Arment 在开场白中说，「Not only that my kids not know how to use computers…」，其中「use」和「computers」两词之间有一明显的停顿。从频谱图可以看出，原音频中 0.3 秒左右的空白被 Overcast 压缩至 0.15 秒左右，而在 Pocket Casts 的输出中则只有不到 0.05 秒了。对比来看，**Overcast 的输出还或多或少地保留了原来的一些音频特征，而 Pocket Casts 则毫不留情地将其全部裁去。**这与我们在上面得到的宏观印象是吻合的。

![](http://ww1.sinaimg.cn/large/73403117ly1fdrxckjneuj21z41407jj.jpg)

类似地，在《一天世界》片段中第 4 秒前后，主播不鸟万如一说，「2015 年初的 MacBook」，并在「年」「初」两字之间明显停顿。从两款 app 的输出中，我们可以得出与上文类似的结论。

![](http://ww1.sinaimg.cn/large/73403117ly1fdrxckj1mej21z4140qhf.jpg)

上面展示的是语句中的停顿，那么对于谈话中另一种常见的停顿——句与句之间的空白，两款 app 又是如何处理的呢？例如，《ATP》片段的 55 秒附近是两位主播的语气衔接。两款 app 在此的表现延续了上述特征。

![](http://ww1.sinaimg.cn/large/73403117ly1fdrxck2iekj21z4140ajw.jpg)

同样地，在《一天世界》测试片段的 57 秒前后，主播不鸟万如一的原话是「……都会支持 Metal，\[hum\]，如果你不知道……」，上述结论仍然适用。

![](http://ww1.sinaimg.cn/large/73403117ly1fdrxck3eckj21z4140gwf.jpg)

顺带一提，**不必担心 Smart Speed/Trim Silence 会波及到播客中偶尔穿插的音乐片段。**下面是《ATP》的结尾曲（ending theme）在两款 app 中输出的结果。如图所示，其波形与原始音频基本一致，表明该部分没有被 Smart Speed/Trim Silence 功能所裁剪。

![](http://ww1.sinaimg.cn/large/73403117ly1fdrxckfqzoj229w1ee7nm.jpg)

总结起来，**Overcast 和 Pocket Casts 的 Smart Speed/Trim Silence 都能有效缩减播客音频中的停顿和无声部分，但具体实现方法（或者说对这一功能作用的理解）不同**，这也可以从其命名上看出些许端倪：在 Overcast 看来，该功能是为了更「聪明」（smart）地加快播放速度，因此它的处理比较温和，保留了停顿部分的信息，只不过将其「快进」了，其策略可以概括为**「压缩式」**；而在 Pocket Casts 看来，该功能是为了「修剪」（trim），因此它的处理更为激进，会直接去除停顿部分，其策略可以概括为**「裁剪式」**。

具体听感与此也是一致的：在 Overcast 中，你仍能感到主播在某些时候语气有所犹豫，但相当短暂，那种令人感到尴尬的「卡壳」「空档」已经不复存在了；而到了 Pocket Casts 中，主播们则似乎都成了雄辩家，语句之间过渡利索得令人叹服，《ATP》中的三位主播的衔接听起来更是几乎都有「抢台词」之嫌了。至于哪种策略更好，就是见仁见智的选择了。

## Voice Boost/Volume Boost

在进行这一部分的测试之前，我们有必要对个别音频相关概念做一些铺垫。正如 Adobe 在[文档](https://helpx.adobe.com/cn/audition/using/monitoring-recording-playback-levels.html)中所述，Audition 界面上纵轴指示的是音频的**振幅**（amplitude）。作为一个数字领域的概念，振幅与人耳所最终感受到的**响度**（loudness）并非同一概念，后者还会受到音频的时延、频率等其他因素的影响。不过，这并不影响我们将振幅作为响度的一个主要度量标准。基于此、也为简便起见，下文不会刻意区分这两个概念。

容易观察到，Audition 纵轴上的振幅是以分贝（dB）为单位的，多数人对这个单位并不陌生，但为什么在图中其数值都是**负数**呢？事实上，**分贝在不同语境下可能有着不同的含义。**我们日常所说的「60 分贝的声音可以将人唤醒」「某工地的噪音高达 110 分贝」，其中的「分贝」指的是**「dBSPL」**（Decibel Sound Pressure Level）。正如其名称所体现的，dBSPL 度量的其实是**压强**，即声波压力压迫耳鼓膜的强度。

与此不同，数字音频中的「分贝」指的是**「dBFS」**（Decibel Full Scale），它所体现的是**音频输出与设备能够到达的最高响度水平之比。**又因为分贝是用对数定义的，因此，**当音频输出达到最大值时，其分贝数为 0 dB**（因为 lg(100%)=0）；而当输出未达到最大时，其分贝数为负值（因为 x<1 时，lg(x)<0），输出音量越小，分贝数越远离 0。

![对数函数](http://ww1.sinaimg.cn/large/73403117ly1fdrxck0u0ij216m10ugrj.jpg)

在此基础上，我们来看 Overcast 和 Pocket Casts 在音量增益功能上的表现。还是先从宏观上看：《ATP》原始音频的响度基本在 -6 dB 以内，经 Overcast 处理后，响度普遍提升到 -3 dB 左右，而 Pocket Casts 则更是一举将其提升到 0 dB；对《一天世界》处理结果的分析可以得出同样的结论。

![](http://ww1.sinaimg.cn/large/73403117ly1fdrxckast9j21z4140dv0.jpg)

![](http://ww1.sinaimg.cn/large/73403117ly1fdrxck8ofdj21z4140nbs.jpg)

仅从数值上看，似乎 Pocket Casts 的处理更有成效：它把声音放得比 Overcast 更「响」了。但问题在于，怎样定义「有效」？这就要**回到 Voice Boost/Volume Boost 功能的目的上来分析。**与我们的直觉不同，Voice Boost/Volume Boost 的真正价值**并不在于提高播客的音量**——如果是那样的话，只要多按几下「音量 +」就好了，有什么必要单独做成一个功能，并且当作卖点大加宣传呢？相反，这一功能的存在目的其实是**减少不同播客间的音量差距**，它所要解决的是下面这种不愉快的体验：你点开一档播客节目，发现主播的声音很小，于是手动提高了音量；过了一会，你又点开另外一档节目，不幸的是，它的主播是个大嗓门，于是刚才让你觉得正合适的音量，现在听起来却刺耳到疼痛了——没错，这正是上文所引 Overcast 宣传文案中所描述的情景。换句话说，**在播客音量的问题上，「不患贫而患不均」才是真正要解决的痛点。**

理解了这一点，我们再来仔细观察一下上面的频谱图：不难发现，Pocket Casts 的输出其实就是对原始音频的直接放大，其波形的高低起伏与后者是完全一致的——事实上，如果你用 Audition 给原始音频加上 +6 dB 的增益效果，就会得到和 Pocket Casts 输出几乎完全相同的结果。Overcast 则不然，它的处理策略可以用**「削高平低」**来形容：原来的波峰在处理后的波形中没有那么突出了，而原来的波谷现在看起来也变得平缓。一句话，音频的**动态**被削减了。

如果我们讨论的对象是一段音乐，动态的减弱将是致命的——这会让乐曲听起来缺乏感染力和对比，因而索然无味；但对于以人声为主的播客节目来说，这反倒成了求之不得的结果，不仅使得不同播客节目间的音量差异得以减弱，也弥补了同一期节目中因设备和主播个人因素导致的声音忽大忽小的瑕疵。

由此看来，Overcast 对 Voice Boost 的理解是更为精准到位的；而 Pocket Casts 那种直接增益的处理方式，虽然也能奏效，但未免略显「暴力」，更何况拉高到 0 dB 的最大电平，本身就是一件很危险的事情——这会使输出处于失真的边缘。事实上，Pocket Casts 输出频谱图在 0dB 的线上已经能看到**明显的裁切痕迹**，这也是其增益策略不足之处的例证。

观察 Voice Boost/Volume Boost 的另一个视角是它们**如何处理音频在各个频段上的输出**——这其实就是所有音乐播放器都具备的「均衡器」（equalizer）功能做的事情。正如我们所知道的，**人声的频率一般在 1 kHz 以下**，因此，要让人声更加清晰可闻，就应该放大这一频段的输出。在下面的 Audition 截图中，纵轴为频率（单位 Hz），红色的亮度表示输出在该频率上的强度。

![](http://ww1.sinaimg.cn/large/73403117ly1fdrxckqdatj21z4140e81.jpg)

![](http://ww1.sinaimg.cn/large/73403117ly1fdrxcksatij21z4140e81.jpg)

可以看出，两款 app 的输出效果基本类似，在 1 kHz 以下都比原始音频「明亮」了许多。如果非要作出一些区分的话，**Overcast 的输出似乎更有针对性一些**，而 Pocket Casts 的增强则延伸到了 1 kHz 以上、与人声基本无涉的频段。这也进一步强化了我们在了上一部分的印象：Overcast 的优化更为细致一些。

### \[Update\] Castro 2.4 中的 Enhanced Audio

5 月 26 日，播客客户端 [Castro](http://castro.fm/) 发布了 2.4 版更新，新加入了呼声较高的 Enhanced Audio 功能。[官方博客](http://blog.supertop.co/post/161095313797/enhanced-audio)对其介绍称：

> Enhanced Audio helps when playing a show where voices are at different levels and makes it much easier to listen to podcasts in a car, on public transit, or in a busy noisy place.
> 
> 「音频增强」功能在播放语音音量参差的节目时十分有用。该功能可让你在车中、公共交通工具或嘈杂场所中更容易地聆听播客。

可见，该功能与 Overcast 和 Pocket Casts 中的 Voice Boost/Volume Boost 是类似的。那么，其具体表现如何呢？

我们使用与之前相同的方法进行了简单的测试，音频素材为 [《ATP》 第 223 期](http://atp.fm/episodes/223)和[《比特新声》第 146 期](https://banlan.show/bitvoice/146)，三款客户端均为测试时的最新版本。

![各客户端音频增强功能输出的 ATP 频谱图](http://ww1.sinaimg.cn/large/73403117ly1ffzoctgdeaj21jk2bc465.jpg)

![各客户端音频增强功能输出的《比特新声》频谱图](http://ww1.sinaimg.cn/large/73403117ly1ffzoctgfthj21jk2bcgtw.jpg)

从上图可见，Castro 的 Enhanced Audio 功能输出的音频频谱与 Pocket Casts 在观感上较为接近，表明两者采用了类似的实现机制，即直接在原音频的基础上进行增益。这反映在主观听感上，就是节目的音量有了显著的提高。不过，正如我们在之前比较 Overcast 和 Pocket Casts 时所述，这种机制的不足在于略显「暴力」，不能完全消除源文件中音量参差不齐的问题，同时还导致了一些溢出（注意频谱上下端因超出最大电平而被「削去」的部分）。在这方面，Overcast 的处理似乎还是更为成熟一些。

当然，正如原文所述，频谱上明显的差异，在实际中听起来并没有那么明显，其本身可能并不足以左右用户对客户端的偏好。就 Castro 而言，其主要优势仍在于独特的 triage 机制和优美的 UI 动效，新加入的 Enhanced Audio 只是补齐了之前短板的一次锦上添花而已。也期待 Supertop 能在今后继续打磨这一功能，带来更好的表现。

## 总结与反思

至此，对 Overcast 和 Pocket Casts 中两对功能重合的音频特效的对比就基本完成了。需要说明的是，由于个人设备和知识所限，上文中的对比是较为粗疏浅显的，也难免有不准确之处，只能对两款 app 音频功能的表现做一粗线条的描绘。整体上说，作为 Smart Speed 和 Voice Boost 功能的开拓者，**Overcast 在实际表现中确实体现出了较强的实力，而这种实力主要体现于对功能所针对痛点和使用场景的准确把握上**，即：Smart Speed 重在「smart」的压缩停顿而非为追求「speed」剪裁空白，Voice Boost 的处理重在让「voice」更清晰而非囫囵吞枣地「boost」所有频段。而作为跟进者的 Pocket Casts，其对应功能虽然也有较好的效果，但在实现细节上就显得不够成熟了。The Sweet Setup 在评测 iOS 播客客户端时曾[提到](http://thesweetsetup.com/apps/our-favorite-podcast-client-for-ios/)，「Overall, I just don’t find Pocket Cast’s silence removal as pleasing to use as Overcast. To my ears, Overcast seems like a more natural cut. / 总体来说，我就是觉得 Pocket Casts 去除空白没有 Overcast 来得舒服。Overcast 的裁剪在我的耳朵听起来更为自然。」这虽是一句主观评价，但根据我们的测试结果，他们的结论确实并非空穴来风。

必须指出，**虽然播放功能是播客客户端的核心所在，但仍然不是全部。**因此，即使得出了 Overcast 的音频特效略优于 Pocket Casts 的结论，这也不能构成你选择或放弃某一个客户端的全部理由。例如，我自己在测试后就仍然保留了 Pocket Casts 作为主力客户端，一方面是因为其设计在我看来比 Overcast 更为精致，另一方面是因为比起 Overcast 的订阅制收费、我暂时还是更喜欢直接付费使用的「一锤子买卖」。再如，如果你订阅了大量播客需要集中管理，Castro 的优势就会凸显出来，其缺少 Smart Speed 的遗憾则可以通过 1.1 倍速播放来弥补。总之，**在收集——管理——播放这个播客体验的完整链条中，市场上暂时还没有一个完美的解决方案，如何取舍取决于个人的偏好和需求。**或许，同时使用其中两个以取长补短会是更好的选择。

* * *

借本文的结尾，我还想讨论一个与主题有关、但更加「形而上」的问题：**作为听众，我们是否有必要/应该使用音频特效？**在我的记忆中，这个问题最早是由不鸟万如一在《IT 公论》时代提出的，他当时在评价 Overcast 时，表明自己并不喜欢 Smart Speed 这样的功能，理由大致是：播客中的空白和停顿也是节目的一部分，如果跳过，听到的节目就不再真实和完整了；况且，这种跳过空白来追求效率的做法本身与播客所倡导的「湿货」概念是相悖的。

我的观点是：首先，**音频特效并不会过分损害播客的真实性和完整性。**不可否认，有些时候语气中的留白可能是有意为之，是把控节奏和氛围的需要，承载着主播的言外之意。但那毕竟是少数人才能达到的境界；在更多数以「闲谈」为追求的播客中，空白仅仅是出于卡壳或停顿。因此，**打开 Smart Speed 所带来的收益是超过其潜在负面作用的**；况且，对于少数精心编制的播客，完全可以通过单独关闭该功能来避免不必要的信息丢失。相反，由于 Smart Speed 节约了时间、弥补了节目的瑕疵，听众更有可能完整地听完节目而非中途放弃，这其实也**有利于实现主播们最重要的诉求**——更完整地传递所想要表达的信息。

其次，**播客作为一种「湿货」的意义，并不在于只应将其作为消遣或背景音，而在于任何人在任何时候都可以用任何自己喜欢的方式去消费其内容。**因此，Smart Speed 或 Voice Boost 并不会害及播客的「湿货」属性；相反，它们的存在正是这一属性的**彰显**：用户有根据自己喜好选择加速或不加速、提高音量或不提高音量的权利，而这正是播客所颠覆（disrupt）的那些传统媒介（如广播）所不具备的。以自己为例，我会针对自己订阅的不同播客节目的特点，对其播放方式进行单独设置。对《一天世界》这种信息量较大，经常穿插引用音乐、录音的节目，我会关闭特效和加速，仔细聆听细节；而对于[《Mac Power Users》](https://www.relay.fm/mpu)这种技术导向较强、风格轻松的节目，我就会打开音频特效，并且以 1.3 倍速播放以提高效率；等等。在我看来，这种灵活性让我更加充分有效地利用碎片时间获取信息，也是吸引我不断加大播客消费量的主要动力。

我特别喜欢[《ATP》的结尾曲（ending theme）](https://www.youtube.com/watch?v=iCXItGrjqrw)，它不仅以打油诗的格式唱出了枯燥乏味的节目信息，更诙谐幽默地宣示了节目的由来和宗旨：

> Now the show is over / 节目到此为止

> They didn't even meant to begin / 他们甚至未曾有意开头

> Cause it was accidental / 因为一切纯属偶然

> It was accidental / 一切纯属偶然

> John didn't do any research / John 没做任何准备

> Marco and Casey wouldn't let him / Marco 和 Casey 拦住了他

> Cause it was accidental / 因为一切纯属偶然

> It was accidental / 一切纯属偶然

> …

> Accidental accidental / 纯属偶然 纯属偶然

> They didn't mean to / 他们未曾有意开头

> Accidental / 纯属偶然

> Accidental Tech Podcast

> So long / 回头见吧

这种幽默，与我常听的另一档节目[《迟早更新》](https://itunes.apple.com/us/podcast/chi-zao-geng-xin/id1129660186?mt=2)的标题不谋而合。在我看来，播客文化的精神莫过于如此：**主播随意展开、随性交流；听众随兴选择、随时聆听。**而播客客户端和 Smart Speed、Voice Boost 这样的的音频特效，正是帮助实现上述目标的必要工具。
