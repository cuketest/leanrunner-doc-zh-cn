## Excel文件操作

#### 加载Excel表数据  

在日常使用中接触到的表格文件经常是Excel表格文件(*.xlsx)，工具箱中的`leanpro.xlsx`库提供了Excel文件的数据读取和写入等支持。它提供的是`xlsx`的npm包的简单封装，更多的详细的调用方法可以查看[xlsx npm包](https://www.npmjs.com/package/xlsx)。

按照下面步骤添加Excel的读取：

  * 拖拽`加载Excel数据`工具到代码中
  * 在工具对话框中，选择Excel文件
  * 设定Excel数据表的变量名，缺省为"workbook"
  * 选择读取的工作表名称或索引（默认为0，即第一张工作表）
  * 完成Excel数据读取

生成代码如下：  

```js
    const xlsx = require('leanpro.xlsx');
    let workbook = xlsx.readFile("C:\\temp\\data.xlsx");
    let worksheetData = xlsx.utils.sheet_to_json(workbook.Sheets[workbook.SheetNames[0]]);
    console.log(worksheetData); // 输出工作簿内容，默认为注释状态
```

运行结果如下，它应与工作表内容一致：  

```json
[
  { "first_name": "James",
    "last_name": "Butt",
    "company_name": "Benton, John B Jr",
    "state": "LA",
    "zip": "70116" },
  { "first_name": "Josephine",
    "last_name": "Darakjy",
    "company_name": "Chanay, Jeffrey A Esq",
    "state": "MI",
    "zip": "48116" },
  { "first_name": "Art",
    "last_name": "Venere",
    "company_name": "Chemel, James L Cpa",
    "state": "NJ",
    "zip": "8014" } 
]
```

如果要通过工作表的名称访问工作表，比如"sheet1"，那么代码会变为：

```js
    const xlsx = require('leanpro.xlsx');
    let workbook = xlsx.readFile("C:\\temp\\data.xlsx");
    let worksheetData = xlsx.utils.sheet_to_json(workbook.Sheets["sheet1"]); // 变为直接使用工作簿名称来索引
```