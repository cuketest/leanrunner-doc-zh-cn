# Node.js自动化API

本软件内置了下面的自动化库：

1. "leanpro.win"

   "leanpro.win"包内置了Windows自动化的Node.js API，下面针对API的不同类别做相应的介绍：

   * [基本操作API](node_basic.md)
   * [对象操作API](node_operations.md)
     * [模拟按键输入pressKeys方法](pressKeys.md)
   * [获取对象API](node_container.md)
   * [虚拟控件API](virtual_api.md)
   * [描述模式](descriptive_mode.md)

2. "leanpro.common"

   "leanpro.common"包内置了Node.js的工具类API函数：
   * [Util (常用工具函数）](util.md)

3. "leanpro.visual"

   这个包内置了图像、OCR识别、PDF操作等相关功能：
   * [图像字符识别(OCR)](ocr.md)
   * [图像操作API](image.md)
   * [Pdf文件操作](/shared/pdf.md)

4. 其它互操作API
   
   1. "leanpro.got"
      封装了got库，提供了API自动化的操作，具体API帮助文档可参考[API自动化库-gott](api_got.md)

   2. "leanpro.mail"
      提供了邮件发送的功能。参考[邮件发送](/shared/mailer.md)。

   3. "leanpro.xlsx"
      提供了[Excel文件操作](/shared/excel.md)的功能。

   4. 数据库操作
      
      提供了[数据库访问](/shared/database.md)的功能，它包括：
      1. "leanpro.mysql" 提供了MySQL的数据库访问
      2. "leanpro.sqlserver" 提供了SqlServer的数据库访问



   

