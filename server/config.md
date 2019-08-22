
# 资源配置
用来配置平台的相关资源信息。主要提供如下部分:

## 部门管理

管理公司部门，设定部门信息列表

![](assets/dept_manage.png)

* 新建部门: 创建新的部门。
* 编辑: 编辑修改部门情况。
* 删除: 删除此部门信息。

## 邮箱服务器

配置邮件服务器信息:

![](assets/email_manage.png)

配置的邮件服务器会用来发送通知邮件，如果某个执行设定了邮件通知，当LeanRunner任务执行成功后，会发送通知邮件给启动任务执行的用户，用户可以点击邮件的中的链接，查看任务执行详情。

## 代理服务器管理

针对RPA运行过程中使用到的服务器代理进行配置。

* 新建代理: 创建新的代理配置。
* 序列: 代理的序号。
* 代理名: 代理设置别名。
* 代理服务器: 代理服务器IP地址。
* 编辑: 配置服务器代理。
* 删除: 删除代理。

LeanRunner提供的用户定制的能力，客户可以用来管理自定制配置信息列表，此部分为定制列表，可提供给脚本执行时获得服务器配置的信息。

## 许可证书管理

通过安装LeanRunner服务器的许可证书，可以获得服务器的完全版的功能。

LeanRunner证书包括两种类型，
1. 服务器证书
2. 执行机证书

服务器证书用来解锁LeanRunner服务器的完全版功能。

![](assets/license_manage.png)

在没有安装服务器证书时，服务器可以启用一台执行机，如果有多台执行机连接到服务器，其它连接的服务器将被禁用。

执行机证书用来解锁LeanRunner可管理的执行机数量。例如，当LeanRunner服务器安装了一个2个执行机许可，可同时使用两台执行机执行任务，提高并发性。