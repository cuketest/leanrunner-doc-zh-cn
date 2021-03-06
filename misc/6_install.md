# LeanRunner的安装

本文描述LeanRunner客户端的安装，包括设计器和机器人。如要了解控制器的安装，请参考[LeanRunner控制器的安装](/server/controller_install.md)

## LeanRunner Lite
从Windows 10的应用商店安装。Windows应用商店也会自动安装程序的更新版本。

## LeanRunner

LeanRunner桌面版可在各个版本的Windows 上运行，包括Windows 7、8、10等系统。它的安装包是msi文件。

安装程序通过定义选项，可以安装不同部分：

![](/assets/02-install-01.png)

其中安装模块有：

•	基础部分：必装，包括LeanRunner设计器、Model Manager(应用模型管理器)、执行引擎、机器人等
•	帮助文档
•	样例：演示的被测样例程序、及测试脚本

安装程序结束时可以选择 “启动LeanRunner”去启动应用程序：

![](/assets/02-install-02.png)

## 启动LeanRunner设计器

安装好之后，可以在开始菜单中点击 “LeanRunner设计器”启动应用，开始编辑脚本。

另一种方式是在命令行窗口中直接输入“leanrunner"命令启动。该应用已配置在PATH环境变量中，意味着打开命令行窗口，在任意路径下执行 “leanrunner”，都可以执行LeanRunner应用。在命令行中，如果该命令后带上一个目录作为参数，则会在LeanRunner中将这个目录作为项目打开。例如“leanrunner .”将当前目录作为项目打开。

