# 模拟按键输入pressKeys方法

在自动化文本框或类似接收键盘输入的控件的时候，需要模拟键盘输入。`pressKeys()`方法是{{ book.product }}中各个控件类型都支持的操作API，经常用来在输入框中输入字符串。每个控件都有这个方法，它有下面的签名

```
  pressKeys(keys: string): Promise<void>;
```

这个方法是通过模拟键盘信号来实现字符串的输入，因此其同样可以用来进行复杂的键盘操作。比如使用以下代码能够快速完成登录：

```js
    await input.pressKeys("username{TAB}password~");
```  

其中，`{TAB}`代表按下Tab键，`~`代表按下回车键，在支持Tab键切换输入框和回车键登录的前提下，该语句能够顺利的完成账号密码的输入和登录，而这些模拟按键的指令，就叫做键指令（keycode），更多相关的内容可以查看[附录：输入键对应表](/misc/key_codes.md)。

## 样例1：输入特殊字符

假设现在需要输入文本，当然啦，可能是复杂一点的文本，这些文本里包含了可能与keycode冲突的特殊字符怎么办？比如想要输入波浪号`~`，然而担心会被解析为回车键？答案是使用花括号来消除歧义，如下：  

```js
    let textarea = model.getDocument("文本编辑器"); // 以下样例同
    //需求：输入特殊符号"+^%~()[]{}"
    await textarea.pressKeys("{+}");
    await textarea.pressKeys("{^}");
    await textarea.pressKeys("{%}");
    await textarea.pressKeys("{~}");
    await textarea.pressKeys("{(}");
    await textarea.pressKeys("{)}");
    await textarea.pressKeys("{[}");
    await textarea.pressKeys("{]}");
    await textarea.pressKeys("{{}");
    await textarea.pressKeys("{}}");
    await textarea.pressKeys("\""); // 对于引号仍需要转义
```

## 样例2：插入换行符和制表符

文本可以输入了，但是现在需要换行呢？或者是输入的文本需要插入制表符来排版呢？自然是使用回车键和Tab键，如下：  

```js
    //需求：输入回车键换行，输入Tab插入制表符
    await textarea.pressKeys("{ENTER}");
    await textarea.pressKeys("~");  // 回车键的另一个keycode
    await textarea.pressKeys("{TAB}");
```

## 样例3：使用组合键进行操作

或许现在有这样一个情况，你希望使用关闭当前窗口的组合快捷键来代替点击右上角的叉号。这个快捷键也许是`ctrl+w`也可能是`alt+F4`，取决于窗口支持哪个。如下  

```js
    //需求：使用Shift键加方向键选中5个字符
    await textarea.pressKeys("+{LEFT 5}");
    //需求：使Ctrl键加x剪切选中字符
    await textarea.pressKeys("^x");
    //需求：使用Ctrl键加v粘贴字符
    await textarea.pressKeys("^v");
    //需求：使用Ctrl键加w关闭窗口
    await textarea.pressKeys("^w");
    //需求：使用Alt键加F4关闭窗口
    await textarea.pressKeys("%{F4}");
```

也许你会注意到，在传入多个指令的时候，`pressKeys()`方法如何分辨这些指令是分开执行还是组合执行呢？事实上，只有`Shift`、`Ctrl`、`Alt`这三个控制键是会被当作组合键执行的，当出现这三个键的指令时，会自动的等待与下个指令一起执行（如果下个指令仍为控制键，那么会顺延至下下个指令）。

因此，如果要实现类似按住`Shift`键输入的效果，只需要将`Shift`指令后的指令用括号包裹起来即可。可以借助以下两行代码理解：
```js
    await textarea.pressKeys("+abc");   // 输入结果为Abc
    await textarea.pressKeys("+(abc)"); // 输入结果为ABC
```

## 总结

以上就是在实际场景中使用输入键指令的介绍样例，需要特别注意的是，`pressKeys()`方法是一个测试对象的实例方法，需要指定键盘输入的对象。比如在某个窗口中按下组合键、在某个输入框中输入字符串，必须指定对象才能够使用`pressKeys()`方法。