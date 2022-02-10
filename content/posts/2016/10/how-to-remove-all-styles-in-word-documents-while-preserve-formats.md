---
title: "在移除 Word 文档样式的同时保留格式"
date: "2016-10-13"
categories: 
  - "post"
tags: 
  - "microsoft-office"
  - "tips"
---

有时，我们需要将他人传过来的多份 Word 文档进行整合。这种情况下，他人文档中预设的样式可能会给排版造成不便。但是，如果一刀切地将其粘贴为纯文本，又会导致文本层级难以辨识。本文介绍一种利用 Office 中的 VBA 脚本，在移除样式的同时保留文本格式的方法。

### A. 如果你使用 macOS 和 Office 2016 for Mac 

1. 正常使用样式功能来编排文档；
2. 依次点击菜单中的「工具」–「宏」–「Visual Basic 编辑器…」；
    
    ![](http://ww1.sinaimg.cn/large/73403117gy1feq2snwaiij21js1e0k0g.jpg)
3. 在弹出的窗口右侧粘贴如下脚本：
    
    ```
    Sub DirectFormat()
                Dim para As Paragraph
                Dim fnt As Font
                Dim pfmt As ParagraphFormat
                For Each para In ActiveDocument.Paragraphs
                    With para
                        If .Style <> ActiveDocument.Styles("Normal") Then
                        Set fnt = .Style.Font
                        Set pfmt = .Style.ParagraphFormat
                        .Style = ActiveDocument.Styles("Normal")
                        .Range.Font = fnt
                        .Range.ParagraphFormat = pfmt
                        End If
                    End With
                Next
            End Sub
            
    ```
    
4. 点击下方的「运行程序」按钮，执行上述命令；
    
    ![](http://ww1.sinaimg.cn/large/73403117gy1feq2sns0h6j217e0ww0v1.jpg)
5. 所有的样式现在已经被清除。

要检查是否运行成功，在「主页」选项卡中点击打开「样式面板」，然后试着在之前设置有样式的段落中单击。如果右侧的样式面板中始终显示为「Normal」样式，则表明已经运行成功。

![](http://ww1.sinaimg.cn/large/73403117gy1feq2sny3klj21pc1k8qd3.jpg)

### B. 如果你使用 Windows 和 Office 2016

1. 正常使用样式功能来编排文档；
2. 按下 Alt + F11 组合键；
3. 在弹出的窗口中，双击左侧的「ThisDocument」选项，并在右侧弹出的空白窗口中粘贴如下脚本：
    
    ```
    Sub DirectFormat()
                Dim para As Paragraph
                Dim fnt As Font
                Dim pfmt As ParagraphFormat
                For Each para In ActiveDocument.Paragraphs
                    With para
                        If .Style <> ActiveDocument.Styles("Normal") Then            Set fnt = .Style.Font
                        Set pfmt = .Style.ParagraphFormat
                        .Style = ActiveDocument.Styles("Normal")
                        .Range.Font = fnt
                        .Range.ParagraphFormat = pfmt
                        End If
                    End With
                Next
            End Sub
            
    ```
    
4. 点击上方工具栏中的「运行」按钮，执行上述命令；
    
    ![](http://ww1.sinaimg.cn/large/73403117gy1feq2snrj4pj21fa1060y7.jpg)
5. 所有的样式现在已经被清除。

要检查是否运行成功，在「主页」选项卡中，点击「样式」区域右下角的展开按钮，展开样式窗格，然后试着在之前设置有样式的段落中单击。如果右侧的样式窗格中始终显示为「Normal」样式，则表明已经运行成功。

![](http://ww1.sinaimg.cn/large/73403117gy1feq30ib6i5j21xi1c2qet.jpg)

### C. 如果你使用早期版本的 Office（如 Office 2011 for Mac、Office 2007）

不知道。

### 备注

需要注意的是，如果你同时打开了多份 Word 文档，那么在上述 VBA 编辑器的左侧，也会出现多个文档的选项。这种场合，请保证选中了 `Project(需要去除样式的文档)-Microsoft Word Objects-ThisDocument` 并使其高亮，然后再在右侧粘贴并执行代码。

### Facts for Nerds

上述命令的作用如下：遍历文档中所有段落并检查其样式，如果某一段落的样式不是「Normal（正文）」，则记住其当前格式设置，然后清除该段落的样式，最后将先前记住的格式重新应用到该段落上。
