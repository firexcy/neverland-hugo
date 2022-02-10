---
title: "用自定义属性功能管理 Word 文档中的「待定内容」"
date: "2021-01-26"
categories: 
  - "post"
tags: 
  - "microsoft-office"
  - "tutorial"
---

在使用 Word 制作合同等格式文本的过程中，经常会需要处理一些「待定内容」，例如签署方的全称、签署日期等。对此，常见的处理方法是用「\[\*\]」、下划线等方式做标记，等确认后再填上。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/xQun4bOp/101cb06e-5678-4d8b-95c4-9ce5ef66ba0d.png?v=bb150dc257a28092160e2cde709d84a1)

这种方法是有很多缺陷的。如果待定内容很多，逐个输入这些「标记」和事后查找替换都很麻烦，而且容易遗漏（更别提它们真的很丑）。有什么办法可以更方便地插入、管理和更新这些待定内容呢？换种问法，Word 文档中有没有什么合适的地方存放这些信息呢？

Word 文档的[「属性」](https://support.microsoft.com/en-us/office/view-or-change-the-properties-for-an-office-file-21d604c2-481e-4379-8e54-1dd4622c6b75)（properties）功能就是这样一个理想的容器。

提到 Word 文档属性，我们一般会想到创建日期、修改日期这些文件系统属性，或者作者、标题这些文档标准属性。但实际上，**Word 也支持用户创建「自定义属性」，其名称和值都可以自由设定。**不仅如此，Word 还提供了专门的文档属性设置界面，相当于附赠了「待定信息管理器」的功能。

进一步想到，域（Field）功能可以读取文档属性的值、插入到正文中，并且具有自动更新的特性；两者结合，就是我们需要的解决方案。

假定我们正在起草一份协议，其中甲乙双方的名称和签署日期都是待定的，并且将在协议中反复出现。我们先尝试手动将这些信息添加为自定义属性，然后通过域插入到文档中。

首先，单击「文件」>「信息」>「属性」>「高级属性」（对于 Mac，单击「文件」>「属性」），然后切换到「自定义」选项卡。

然后，在「名称」框中，为自定义属性键入一个名称。例如，对于甲乙双方的名称，可以分别命名为「partyA」「partyB」等；对于签署日期，可以命名为「ExeDate」。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/nOulzoJZ/828ffe9d-f198-411e-a1c9-5ced8d1043fc.png?v=932787ec74b34b0b6e37ecc5f2b0bc37)

接着，在「类型」列表中选择数据的类型，然后在「值」框中输入属性的值。例如，甲乙方的名称应该是文本，而签署日期应该选为日期。

需要注意，日期类型的数据**必须以系统当前区域设置对应的日期格式输入**。对于简体中文系统，这个格式一般是 `yyyy-MM-dd`（形如 2021-01-10），而英文系统则一般是 `M/d/yyyy`（形如 1/10/2021）。如果你不能确定，可以到 Windows 系统的「设置」>「时间和语言」>「地区」下的「地区格式」，或 macOS 的「系统偏好设置」>「语言和地区」中查看。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/rRukwGDx/0ef21ebb-1bee-4808-9083-aebd6e5c4bd5.png?v=f68037e6f68d043fc35ef426f1aaeae1)

接下来，我们通过域将自定义属性插入到正文中。点击「插入」>「域」，然后在弹出的对话框中选择 `DocProperty` 域，并在域代码输入框中通过 `DOCPROPERTY "自定义属性名称"` 的格式指定要插入到正文的属性。例如，如果要插入甲方的名称，对应的域代码应是 `DOCPROPERTY partyA`。

点击确定，就可以看到相应的文本被插入到了正文中。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/jkuegLjO/b08ded19-c220-4316-b92e-c4f6edd4b568.png?v=dfa11c7e71166c95932ad15f2b8e4c81)

对于日期类型的属性，我们还可以进一步指定其格式，只要在域代码的结尾追加 `\@ <格式>` 即可。

例如，对于中文合同，我们希望插入形如「2021年1月10日」这样的日期：

```
{ DOCPROPERTY ExeDate \@ "yyyy年M月d日" }
```

而对于英文合同，我们希望得到的格式就是「January 10, 2021」：

```
{ DOCPROPERTY ExeDate \@ "MMMM d, yyyy" }
```

更多日期格式的表达方式可以参考 [VBA 文档的说明](https://docs.microsoft.com/en-us/office/vba/api/access.format.propertydate.time)。

如果日后需要修改这些待定内容，只要回到自定义属性对话框，更新相应的属性值，然后全选文档内容按 F9 键更新域，就可以看到所有用上述方法插入的信息都被统一更新了。此外，在 Word 的默认设置下，域也会在打印（包括打印为 PDF）时自动更新。

![](https://p178.p0.n0.cdn.getcloudapp.com/items/E0u92AoK/fd43a1cd-528e-4539-a2b3-087ec0859d9a.gif?v=1ca225663fe4f5cd168ca36118567ed5)

当然，如果只是用上面的手动方法插入自定义属性和域代码，似乎并没有快捷到哪里去。但属性和域功能的优点就在于可以方便地**通过 VBA 实现自动化**。

与本文相关的 VBA 接口有两个。首先是 [`CustomDocumentProperties` 对象](https://docs.microsoft.com/en-us/office/vba/api/word.document.customdocumentproperties)，它的 `Add` 方法可以向文档追加自定义属性：

```
.Add (Name, Type, Value)
```

其中，`Name` 参数和 `Value` 参数分别为自定义属性的名称和值。`Type` 参数为自定义属性的类型（[`MsoDocProperties`](https://docs.microsoft.com/en-us/office/vba/api/office.msodocproperties)），与本文相关的主要为 `msoPropertyTypeString`（文本类型）和 `msoPropertyTypeDate`（日期类型）。例如，如果要追加一个名为 `partyA` 的文本自定义属性，则执行：

```
ActiveDocument.CustomDocumentProperties.Add _ 
    Name:=newPropName, _
    Type:=msoPropertyTypeString, _
    Value:="Acme Co."
```

其次是与域相关的 [`Fields` 对象](https://docs.microsoft.com/en-us/office/vba/api/word.fields.add)，它的 `Add` 方法可以在选定位置插入域代码：

```
.Add (Range, Type, Text)
```

其中，`Type` 参数用于指定域的类型（[`WdFieldType`](https://docs.microsoft.com/en-us/office/vba/api/Word.WdFieldType)），本文用到的 `DocProperty`域对应的类型是 `wdFieldDocProperty`。`Text` 参数用于附加设定，即域代码中域名称之后的部分，如本文用到的自定义属性名称和日期格式。因此，如果要在光标位置插入一个「ExeDate」自定义属性域，则应该运行：

```
ActiveDocument.Fields.Add _
    Range:=Selection.Range, _
    Type:=wdFieldDocProperty, _
    Text:="ExeDate"
```

我已经预先写好了一些本文操作相关的 VBA 函数供使用。在 Word 中按 Alt-F11 组合键（对于 Mac，按 Option-F11）打开 VBA 编辑器。在左侧边栏中双击 Normal > Microsoft Word Objects > ThisDocument，然后粘贴如下代码：

```
Sub newCustomProp()
Dim newPropName As String
Dim newPropVal As String
newPropName = InputBox("New Property Name", "New Property Name")
newPropVal = InputBox("New Property Value", "New Property Value", "[*]")
' If same property already exists, delete and update it
For Each Prop In ActiveDocument.CustomDocumentProperties
    If Prop.Name = newPropName Then
        Prop.Delete
    End If
Next Prop
With ActiveDocument.CustomDocumentProperties
    .Add Name:=newPropName, _
        LinkToContent:=False, _
        Type:=msoPropertyTypeString, _
        Value:=newPropVal
End With
End Sub

Sub insCustomProp()
Dim propName As String
Dim propNameDoesExist As Boolean
propName = InputBox("Insert Custom Property", "Property Name")
propNameDoesExist = False
For Each Prop In ActiveDocument.CustomDocumentProperties
    If Prop.Name = propName Then
        propNameDoesExist = True
    End If
Next Prop
' Complain if no such property exists
If propNameDoesExist = False Then
    MsgBox ("Property Not Found.")
    Else
    ActiveDocument.Fields.Add Range:=Selection.Range, Type:=wdFieldDocProperty, Text:=propName
End If
End Sub

Sub setAgtExeDate()
Dim newExeDate As Date
' Get user-input execution date, default to today
newExeDate = InputBox("Execution Date", "Set execution date to: ", Date)
' Delete old ExeDate
For Each Prop In ActiveDocument.CustomDocumentProperties
    If Prop.Name = "ExeDate" Then
        Prop.Delete
    End If
Next Prop
With ActiveDocument.CustomDocumentProperties
    .Add Name:="ExeDate", _
        LinkToContent:=False, _
        Type:=msoPropertyTypeDate, _
        Value:=newExeDate
End With
End Sub

Sub insAgtExeDateFmtC()
Dim dateFmtC As String
' Use ChrW() to insert CJK chars properly
dateFmtC = "yyyy" & ChrW(&H5E74) & "M" & ChrW(&H6708) & "d" & ChrW(&H65E5)
ActiveDocument.Fields.Add Range:=Selection.Range, _
 Type:=wdFieldDocProperty, Text:="ExeDate \@ " & """" & dateFmtC & """"
End Sub

Sub insAgtExeDateFmtE()
Dim dateFmtE As String
dateFmtE = "MMMM d, yyyy"
ActiveDocument.Fields.Add Range:=Selection.Range, _
 Type:=wdFieldDocProperty, Text:="ExeDate \@ " & """" & dateFmtE & """"
End Sub
```

上述代码中，前两个函数分别用来创建/更新和插入自定义属性：

- `newCustomProp`：创建一个新的文本型自定义属性，依次提示输入属性名称和值（默认为「\[\*\]」，如果该属性已存在，则更新为新输入的值
- `insCustomProp`：插入指定名称的自定义属性到正文

我日常工作中要处理签署日的情况尤其多，所以专门写了几个处理签署日的函数：

- `setAgtExeDate`：创建一个名为「ExeDate」的自定义函数用于存放签署日（默认为今天），如果「ExeDate」已存在，则更新为新输入的值
- `insAgtExeDateFmtC`（`insAgtExeDateFmtE`）：插入「ExeDate」属性中存储的签署日到正文，并修改为中文（英文）的常见日期格式

此后，点击「视图」>「宏」>「查看宏」（对于 Mac，「工具」>「宏」>「宏…」），在弹出的对话框中双击相应函数名，就可以快速运行相关功能。对于 Windows 版的 Word，还可以进入「文件」>「选项」>「自定义功能区」，将上述函数创建为工具栏中的按钮。

Mac 版 Word 没有这种功能，但可以通过 KeyboardMaestro、Alfred 等工具实现类似效果，只要将如下格式的 Apple Script 创建为 Marco/Workflow 并分配快捷键即可：

```
tell application "Microsoft Word"
    activate
    run VB macro macro name "<宏名称>"
end tell
```
