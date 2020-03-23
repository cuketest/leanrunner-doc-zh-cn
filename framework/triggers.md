## 触发器

触发器可以触发某个特定的流程的执行。

在无人值守的流程中，触发器可以由网络事件触发，如收到某个邮件，检测到某个上传文件，或者应用程序弹出某个窗口等。
有人值守流程中，除了以上可能的触发条件外，触发器还可以由用户事件触发，如菜单点击、热键等，然后在人工监督下运行。

根据触发流程运行的方式不同，有以下几种触发器：
* [菜单项触发器](#menu_trigger)
* [热键触发器](#hotkey_trigger)
* [自定义触发器](#custom_trigger)

你可以定义好流程的触发器。当流程执行时，会等待这些触发器的执行，触发条件满足时，会执行相应的函数或流程。

<a id="menu_trigger"></a>

#### 菜单项触发器

菜单触发器创建后，会在浮动图标的右键菜单上创建菜单项。用户点击菜单项后，相应的函数被执行。菜单触发器通过`registerMenuTrigger`创建。它有如下的函数签名：


```js
registerMenuTrigger({
    label: '导入数据',
    accelerator: 'CmdOrCtrl+I',
    click() {
        //TODO：执行导入操作
    }
}): () => void
```

例如下面的操作注册了一个"导入数据"的流程，点击它或按"Ctrl-i"快捷键会导入触发导入数据的流程：

```js

registerMenuTrigger({
    label: '导入数据',
    accelerator: 'CmdOrCtrl+I',
    click() {
        //TODO：执行导入操作
    }
})

```

它的返回值是一个方法，相当于dispose操作，调用它可以从菜单中释放这个注册的菜单。

如需要一次性注册多个菜单，可以传入菜单定义的数组。可以用 `{ type: 'separator' }`加入分隔符，分隔不同的菜单分组。

下面是样例：
```js

registerMenuTrigger([
    {
        label: '导入数据',
        accelerator: 'CmdOrCtrl+I',
        click() {
            //TODO：执行导入操作
        }
    },
    { type: 'separator' },
    {
        label: '停止流程数据',
        accelerator: 'CmdOrCtrl+I',
        click() {
            //TODO：执行退出操作
        }
    }
]);

```


<a id="hotkey_trigger"></a>

#### 热键触发器

注册全局热键

例如：
```js
    registerHotkeyTrigger('CmdOrCtrl+Shift+C', () => {
        
    })
```

<a id="custom_trigger"></a>

#### 自定义触发器

如果有自定义的触发条件，例如收到一个邮件，或者是某个特定的对话框出现，你可以注册自定义触发器

```js
registerCustomTrigger(conditionFunc(), callback());
```
