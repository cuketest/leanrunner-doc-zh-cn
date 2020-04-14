# 错误代码及解释

| 错误代码 |           错误名称          | 错误解释                                                                                                         |
|:--------:|:---------------------------:|------------------------------------------------------------------------------------------------------------------|
| 1001     | ObjectNotExist              | 没有找到对象，或者对象不存在。通常是由于目标控件不可见引起的。比如未展开的下拉框选项、树形图节点、子菜单栏等等。 |
| 1002     | ObjectIsOutOfScreen         | 控件超出屏幕。通常是由于目标控件不在屏幕中，可能由于目标窗口没有全屏运行或者多屏幕的问题。                   |
| 1003     | CannotPerformThisOperation  | 无法执行该操作。                                                                                                 |
| 1004     | ObjectIsReadOnly            | 对象是只读的无法修改。                                                                                           |
| 1005     | ItemNotExistInList          | 项目不存在。在使用项目名索引List、ComboBox等存在多个子控件的控件时，使用控件名字没有匹配到合适的项目。           |
| 1006     | OutOfRange                  | 索引超出数组长度。                                                                                               |
| 1007     | Others                      | 其它原因。                                                                                                       |
| 1008     | InvalidArgument             | 不合法的参数。                                                                                                   |
| 1009     | CannotFindTestObjectInModel | 在模型文件中无法找到相关的{{book.test_object}}。通常是对象名词拼错，或者模型文件中的更改未保存。                             |
| 1010     | InvalidRunContext           | 不合法的运行上下文。                                                                                             |
| 1011     | InvalidObjectType           | 不合法的对象类型。                                                                                               |
| 1012     | NoLicenseAndOutOfFreeQuota  | 到达许可版本的最大限制。即对象识别、图像识别等API的调用次数到达上限，需要升级许可类型来解除限制。                |
| 1013     | DuplicateTestObjectFound    | 找到多个对象。通常是由于对象存在重名，或者对象的识别属性匹配到了多个控件。                                       |
| 1014     | InvalidTestObjectType       | 不合法的{{book.test_object}}类型。通常是由于获取对象的方法与对象的类型不一致。                                               |
| 1015     | InvalidConditionString      | 不合法的条件字符串。                                                                                             |