# 基本操作API

自动化Windows应用时对象的基本操作API通过引入"leanpro.win"包中导出的类对象获得，它导出对象包括“TestModel”和“Auto”两个类获得：

```javascript
const { TestModel, Auto } = require('leanpro.win');
```

### Auto

Auto对象用来通过[描述模式](descriptive_mode.md)获取测试对象，无需加载对象模型。

### TestModel

TestModel是对象模型，该类有下面的方法：

```javascript
class TestModel {
    static loadModel(modelPath: string): IModel;
    static bindToProcess(processId: number);
}
```

* **loadModel**

loadModel从文件加载对象模型文件并返回模型对象。对象模型是以*.tmodel为结尾的文件。下面是调用样例：

```javascript
const { TestModel } = require("leanpro.win");
var model = TestModel.loadModel(__dirname + "/simle_styles.tmodel");

async function run() {
    await model.getButton("Default").click();
}

run();
```

* **bindToProcess**

bindToProcess用来将模型绑定到一个被自动化应用的进程。在操作的时候即使有多个相同的应用实例，运行时也只会选择绑定的应用操作。



