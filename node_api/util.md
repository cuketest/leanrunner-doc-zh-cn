### Util (常用工具函数）

提供自动化脚本常用的工具函数， 它通过引入“leanpro.common"中的Util对象获得：

```javascript
const { Util } = require('leanpro.win');
```


它的定义如下：

```javascript
class Util {
    static delay(milliseconds: number): Promise<void>;
    static launchProcess(exePath: string, ...args: string[]): any;
    static stopProcess(proc: ChildProcess): boolean;
    static takeScreenshot(filePath: string = null, monitor: number = 0): string | void;
    static loadCsvFile(filePath: string): Promise<RowCsv[]>;
}
```

* **delay**

指定延时的毫秒数。因为是异步调用，记住前面需要加上await。例如：

下面的代码打开计算器应用，等待一秒后，确保它初始化成功后，开始点击操作。

```javascript
async function run() {
    let calcPath = 'c:/windows/system32/calc.exe';
    await Util.launchProcess(calcPath);
    await Util.delay(1000); //wait for process to initialize
    await model.getButton("Two").click();
}

run();
```

* **launchProcess**
启动某个进程。一般用来启动被测应用。上述的例子显示了如何用launchProcess启动计算器应用。

* **stopProcess**
停止某个进程。将launchProcess返回值传递给proc，可关闭该进程。

```javascript
async function run() {
    let notepadPath = 'c:/windows/notepad.exe';
    let proc = await Util.launchProcess(notepadPath);
    //do some other operations...
    Util.stopProcess(proc);
}

run();
```

> **注意**：有些应用是多进程的。界面端窗体是由主进程打开的。这种情况下停止主进程不会关闭应用程序界面。Windows 10中的计算器应用即这种情况。

* **takeScreenshot**
截取整个屏幕图片，以png格式保存。
  * `filePath`是文件路径，应以`.png`后缀结尾。如果提供了文件名，返回值是空。如果`filePath`为null, 返回为图片的base64编码。
  * `monitor`是截取屏幕的编号，0是第一个，1是第二个，缺省为0。


* **loadCsvFile**
读取CSV文件，返回json对象的数组，每个对象的key是列名，value是数据。例如有下面的内容的data.csv文件：

```
first_name,last_name,company_name,state,zip
James,Butt,"Benton, John B Jr",LA,70116
Josephine,Darakjy,"Chanay, Jeffrey A Esq",MI,48116
Art,Venere,"Chemel, James L Cpa",NJ,8014
```

使用如下代码读取：
```javascript
(async function() {
    let data = await Util.loadCsvFile('C:\\temp\\data.csv');
    console.log(data);
})();
```

会返回如下的json:

```json
[
{ first_name: 'James',
  last_name: 'Butt',
  company_name: 'Benton, John B Jr',
  state: 'LA',
  zip: '70116' },
{ first_name: 'Josephine',
  last_name: 'Darakjy',
  company_name: 'Chanay, Jeffrey A Esq',
  state: 'MI',
  zip: '48116' },
{ first_name: 'Art',
  last_name: 'Venere',
  company_name: 'Chemel, James L Cpa',
  state: 'NJ',
  zip: '8014' } 
]
```
