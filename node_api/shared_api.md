## 常见的API方法

#### click
```javascript
click(x?: number, y?: number, mousekey?: MouseKey): Promise<void>;
```

点击控件。mouseKey=1 是左键, 2是右键, 4是中键，缺省为1。x, y是点击区域，都为缺省值0 将点击中心区域。

其中MouseKey定义如下：
   ```javascript
   enum MouseKey {
       LButton = 1,
       RButton = 2,
       MButton = 4,
       Ctrl = 8,
       Shift = 16,
       Alt = 32
   }
   ```

使用MouseKey枚举无需记忆按键的值，下面是鼠标点击示例

```javascript
const { TestModel, MouseKey } = require("leanpro.win");
var model = TestModel.loadModel(__dirname + "yourModel.tmodel");

async function r(){
    //点击鼠标左键
    await model.getButton("button").click();
    //在图片的x = 10, y = 20部分点击右键
    await model.getImage("image1").click(10, 20, MouseKey.RButton);
    //点击左键同时按下Ctrl键
    await model.getImage("image1").click(10, 20, MouseKey.Ctrl | MouseKey.LButton);
}
```

#### dblClick
双击控件
```javascript
dblClick(x?: number, y?: number, mousekey?: MouseKey): Promise<void>;
```

`dblClick`所有的参数与`click`方法相同。


#### exists
```javascript
    exists(time: number): Promise<boolean>;
```

检查控件是否存在，其中time为重试时间，以秒为单位。缺省重试秒数为0，即只检查1次。

   ```javascript
   let isExists=model.getButton(‘button1’).exists(20)
   if (isExists) {
      //.... some operations
   }
   ```
上面的例子中exists里面20就是在20秒里自动循环等待，如果控件存在，会立刻返回true，如果控件不存在，在20秒超时后会返回false。用户可以根据控件出现的时间长短以及控件识别的时间，调整等待的秒数。

<a id="takeScreenshots"></a>

#### takeScreenshots

```javascript
takeScreenshot(filePath?: string): Promise<void | string> 
```

获得控件的截屏, 传入完整路径的文件名，以.png文件结尾。

filePath传入文件路径，即截图保存的位置，当传入实际路径时，截图会保存到文件中，同时方法返回null。
如果filePath传入null值，表示用户希望直接获取截图的数据，截图数据将作为base64编码的字符串返回。

可以比较一下控件上的这个方法和Util的takeScreenshots方法。两个方法的相似，不同的控件的这个方法只截取控件自己截图，而Util.takeScreenshots截取整个显示屏的截图。


#### pressKeys

```javascript
pressKeys(keys: string): Promise<void>;
```
按一个或多个按键，特殊按键值请参见附录：输入键对应表。例如：键值可以是"Good morning,{DELETE}"

pressKeys不切换中文输入法，直接输入中文或英文。但如果你是打开中文输入法，输英文会被中文输入法截获，可能造成混乱。请在自动化前关闭中文输入法。



