---
title: "根据电源连接状态自动切换默认浏览器"
date: "2017-05-22"
categories: 
  - "post"
tags: 
  - "macos"
  - "tutorial"
---

Safari 和 Chrome 是 macOS 平台上最主流的两个浏览器，如何在它们之间取舍也一直是热门话题。虽然两者性能、速度孰优孰劣并无定论，但 **Safari 更加稳定省电、Chrome 在功能和扩展性上更优**则是没有疑问的。因此，对于 MacBook 而言，用电池供电时使用 Safari 是更经济的选择，而连接电源时则可放心使用 Chrome，享受其丰富的扩展程序带来的便利。但显然，**每次插拔电源后手动切换默认浏览器是十分麻烦的，如何将其自动化呢？**

我们可以使用一款名为 ControlPlane 的免费工具来达成上述目的。该软件的机制非常类似于 IFTTT，即当检测到一定条件发生时，自动触发相应的操作。据此，前述需求实际上可以表述为：如果连接电源适配器，则将默认浏览器设置为 Chrome；如果拔下电源适配器，则将默认浏览器设置为 Safari。下面介绍如何利用这套机制实现文首提出的需求。

首先[下载安装](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0ahUKEwiXv9aNo4PUAhVFrJQKHSIEDPgQFggmMAA&url=https://www.controlplaneapp.com/&usg=AFQjCNFrDQlphF3fIVpg35MyLqLzroU6gQ&sig2=K9uH5lVL2TeLM-n7ybXa_Q) ControlPlane。打开后，可以看到「通用」（General）、「情境」（Contexts）、「迹象」（Evidence Sources）、「规则」（Rules）、「动作」（Actions）、「高级」（Advanced）等选项卡。**上述几个概念的逻辑关系是：当特定的「迹象」出现时，触发相应的「规则」；软件将据此判断电脑当前处于何种「情境」，从而执行与其关联的「动作」。**

![软件主界面](http://ww1.sinaimg.cn/large/73403117ly1ffuce85v7kj20t60r6wiy.jpg)

首先在「通用」（General）选项卡中，勾选「登录时启动 ControlPlane」（Start ControlPlane at login），允许其随系统自启。

然后，切换到「情境」（Contexts）选项卡。点击「+」，新建一个名为「Battery」的情境。

![新建情境](http://ww1.sinaimg.cn/large/73403117ly1ffuce85sojj20s20s2tc0.jpg)

接着，在「迹象」（Evidence Sources）选项卡中，勾选「连接的电源适配器」（Attached Power Adapter），允许将电源连接情况作为判断情境的标准。

![允许将电源连接情况作为判断情境的标准](http://ww1.sinaimg.cn/large/73403117ly1ffuce86dnlj20ru0ratcq.jpg)

在「规则」（Rules）选项卡中，点击「+」>「添加『连接的电源适配器』规则…」（Add 'Attached Power Adapter' Rule…）。在弹出的窗口中，将「情境」（Context）指定为刚才创建的「Battery」，**并将「把握」（Confidence）滑杆向右拉动到超过 75%（软件默认的切换情境所需最低阈值），但不要拉到 100%。** \[^1\] 由于我们希望在断开电源时触发规则，还应勾选「反向适用」（Negate）选项。

![新建规则（是的，竟然还可以根据序列号指定某一个特定的电源……）](http://ww1.sinaimg.cn/large/73403117ly1ffuh7nus43j20xo0qcn26.jpg)

最后，切换到「动作」（Actions）选项卡，点击「+」>「网络动作」（Web Actions）>「默认浏览器」（Default Browser）。在弹出窗口的「将默认浏览器设置为」（Set default browser to）下拉菜单中选择 Chrome 浏览器，并在「情境」（Context）项下的两个下拉菜单中分别选择刚才创建的「Battery」情境和「情境开始时」（On arrival）。用同样的方法添加一个在「情境结束时」（On departure）将默认浏览器改回 Chrome 的动作。（注意：该功能的实现机制是将 ControlPlane 本身设定为系统默认浏览器，然后根据规则转发到对应浏览器，因此第一次做此操作时，会弹出修改系统默认浏览器的提示，同意其修改即可。如果不慎忽略了该提示，可以事后在「」>「系统偏好设置」>「通用」>「默认网页浏览器」中手动修改。）

![动作设置完毕后的界面](http://ww1.sinaimg.cn/large/73403117ly1ffuce87ls9j20xw0xi44o.jpg)

现在，只要断开电源，即可看到 ControlPlane 弹出通知，表明默认浏览器已经切换到 Safari，需求达成。（如果不需要该通知，可以取消「通用」（General）>「使用通知」（Use Notifications）选项的勾选。）

![切换情境时的通知](http://ww1.sinaimg.cn/large/73403117ly1ffuce84z54j20l005ejrr.jpg)

从上述操作中可以看出，ControlPlane 的功能相当丰富，其所能实现的效果远不止切换默认浏览器一种。除电源连接状况之外，该软件还支持以运行的程序、蓝牙状态、外置存储，以至 IP 地址、地理位置、光线强弱为情境触发条件；可以执行的动作则还有打开文件/应用、加载/推出设备、开关 WiFi 等。而且，由于其支持运行终端命令（Shell Script）和 Apple Script 脚本，理论上可以实现的效果几乎是无限的，读者可以按照自己的需求自行探索。

\[1\]: 「把握」（Confidence）是 ControlPlane 用于判断电脑当前处于何种情境的独特机制。简言之，**当两个或以上情境的条件同时成就时，ControlPlane 将优先切换到「把握」最高的情境。**因此，此处不将该值设定为 100% 的理由在于，某些情况下（如在家中可以随时充电时），即使不插电源，我们也希望继续使用 Chrome。这时，通过新建一个以连接家中 WiFi 为触发条件的情境「在家」，并将其「把握」设置得更高，即可在「断开电源」和「连接家中 WiFi」两个条件同时成就时，排除适用「Battery」情境，而适用「在家」情境，从而保持 Chrome 的默认浏览器身份。计算某个情境「把握」`C` 的方法是：将其下每个规则「把握」`c[i]` **不成立**的概率（`1-c[i]`）相乘，所得结果被 1 减，即 `C=1-∏(1-c[i])`。你可以在「通用」（General）>「切换情境所需的把握度」（Confidence required to switch）来调节适合需求的阈值。
