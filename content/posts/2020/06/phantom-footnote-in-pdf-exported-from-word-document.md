---
title: "Word 文档导出为 PDF 时出现额外脚注"
date: "2020-06-10"
categories: 
  - "post"
tags: 
  - "microsoft-office"
  - "tips"
---

昨天在把一个合同从 Word 版本导出为 PDF 的时候，发现导出的 PDF 版总是会在页脚处多出一串代码（形如 `XY&Z\12345.67`），但在 Word 中并不能看到任何对应的文字。

![打印时页脚自动出现的编号（文件内容和代码都是我乱编的）](https://p178.p0.n0.cdn.getcloudapp.com/items/BluOpj7D/phantom_footnote.png?v=db61de0b8ccf3783bcb255519d749c52)

打印时页脚自动出现的编号（文件内容和代码都是我乱编的）

虽然暂时不知道这串代码的意思，但看外观像是某种格式的文件编号。于是首先尝试搜索其中的字母部分 `XY&Z`，发现是某个律所的简称（全称类似 **X**enos, **Y**anko & **Z**ais, LLP）。

看来，这串字符确实是文件编号。剩下的问题就是它是如何出现的，以及怎么去掉。

考虑到文件编号只在导出成 PDF 时才出现，而导出 PDF 的操作基本相当于打印，便联想到 Word 中域功能的特性——[打印时自动更新页眉和页脚中的域](https://support.microsoft.com/en-us/help/211629/which-fields-are-updated-when-you-open-repaginate-or-print-document)。于是再次进入脚注编辑界面并按 Option-F9 显示域代码，果然看到这串隐形文件编号的对应位置有一个域，代码为 `{ DOCPROPERTY"SWDocID" }`。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/mXuAE8dk/field_code_docproperty.png?v=39b8491169c4a675b382231e30e317d9)

查阅 Office 官方文档的[说明](https://support.microsoft.com/en-us/office/field-codes-docproperty-field-bf00526e-18cd-4515-8c8e-39d59094395a)，`DOCPROPERTY` 域的作用是显示当前文档的某个[属性](https://support.office.com/en-us/article/View-or-change-the-properties-for-an-Office-file-21D604C2-481E-4379-8E54-1DD4622C6B75)（property）。这个属性可能是内置的，例如文档的作者（`Author`）、创建时间（`CreateTime`）等；也可以是用户或者第三方软件后续添加的。进一步搜索发现，`SWDocID` 是 Litera 公司开发的法律文件自动化软件 Innova 创建的属性，正是起到给文件编号的作用。

![Innova 文档关于 SWDocID 属性的说明](https://p178.p0.n0.cdn.getcloudapp.com/items/d5uWzBBv/innova_swdocid.png?v=9097ff06c6f582127f119cf449db7dda)

Innova 文档关于 SWDocID 属性的说明

既然了解了这串字符是通过域代码生成的，去除它的方法也很简单，直接删掉就行了。如果嫌这么做过于简单粗暴，或者出于一些原因必须保留，也可以选中这段代码，然后按 Command-F11 将其**锁定**，阻止该域在打印时自动更新。（虽然 Word 偏好设置里有「打印时更新域」的选项，且默认为禁用，但页眉和页脚中的域并不服从该设置，必须手动锁定才不会在打印时更新。）

问题解决后，顺手在 EDGAR 里搜了一下 `SWDocID`：

![](https://p178.p0.n0.cdn.getcloudapp.com/items/bLujJYY0/edgar_swdocid.png?v=fb7bd1dbd786eca97ce8ff3c6203c228)

……看起来被这个软件坑到的人还是挺多的。
