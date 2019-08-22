# VBScript API提示

**GetControls**方法是获取一个控件数组，它的调用无法由模型管理器自动生成，需要用户手写。

首先为SimpleStyles样例添加模型：

![](/node_api/assets/checkboxes.png)

下面是对应的模型

![](/node_api/assets/checkboxes_model.png)

执行如下代码:
```vbscript
Dim auto
Set auto = CreateObject("Win.Automation")
Dim model
Set model = auto.LoadModel("C:\\temp\\SimpleStyles\\Model1.tmodel")

Dim controls
controls = model.getControls("Normal")
Dim summary
MsgBox(LBound(controls) & " " & UBound(controls))
For i = 0 to UBound(controls)
summary = summary & vbCrLf & controls(i).name
Next

MsgBox(summary) 

```

打印出以下内容：
```
Normal
Checked
Indeterminate
CheckBox
```
可以看到所有的checkbox控件都被访问到了。