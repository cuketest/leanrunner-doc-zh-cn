## Pdf文件操作

"leanpro.visual"中的Pdf类提供了Pdf文件内容提取的功能。

Pdf类有如下的定义

```javascript

interface PdfExtractOptions {
        fontSize?: number,
        password?: string
    }

class Pdf {
    static fromFile(inputFile: string): Pdf;
    async extract(pageNum: number, options: PdfExtractOptions): Promise<string>;
}
```


其中：

#### fromFile

静态方法，可从Pdf文件中生成Pdf对象实例。这个实例可用来执行后继的操作。

#### extract

传入页号和其它提取参数，提取Pdf实例对象中的第几页内容。页码从1开始。


举例：

```javascript
let { Pdf } = require('leanpro.visual')
async function test() {

    let inputFile = __dirname + '/sample.pdf';
    let pageNum = 1;

    let pdf  = Pdf.fromFile(inputFile);
    let content = await pdf.extract(pageNum);
    console.log(content);
}

test();
```

上述例子提取sample.pdf文件中的第一页内容并输出。