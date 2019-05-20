# Visual Studio 集成

## 菜单集成
LeanRunner提供了Visual Studio  IDE环境的集成，支持Visual Studio 2012, 2013, 2015等。使用方法如下：
用户可以在Visual Studio的LeanRunner菜单选择 “Launch LeanRunner”去启动应用模型管理器，如下图所示：

![](/assets/5.1_vs_menu.png)

这会打开模型管理器，然后你就可以识别对象，新建、编辑测试模型之类的操作了。

## C#项目模板
LeanRunner安装时还在Visual Studio中安装了C#测试脚本的项目模板，这可让用户在Visual Studio中更方便的创建C#自动化测试项目。点击“新建”=> “项目“，然后这个模板可以在“Test”项目文件夹下面找到，如下图。

![](/assets/5.1_vs_dialog.png)

用这个模板创建项目后，你就可以编辑自动化测试代码了。可以在Solution Explorer中看到，创建的项目已经为用户添加了比较的引用和第一个源代码文件。

![](/assets/5.1_vs_sln_explore.png)

打开LeanRunnerTest.cs文件，看到项目模板已经生成了如下代码：

![](/assets/5.1_vs_code.png)

如要了解如何开发测试代码，请参见文档的[代码生成](/4_code_generation.md)和[运行](/1_2_run.md)两节。



