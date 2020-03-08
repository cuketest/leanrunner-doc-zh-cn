# LeanRunner机器人

### 配置和运行

LeanRunner机器人随着桌面版一起安装。安装好以后，可在安装目录下(缺省为"C:\Program Files (x86)\LeanPro\LeanRunner")，可以看到agent_config.json, 它是LeanRunner机器人的配置文件。

例如：

```json
{
    "agentUniqueId": "<unique_id>",
    "server": "localhost:80",
    "rootDir": "c:/leanrunner/agent",
    "logLevel": "info",
}
```

其中：

* agentUniqueId为本机器人唯一的ID，默认为TBD，请手动修改。
* server是LeanRunner控制器的网址，注意格式为"服务器:端口号"，不包含http://部分。
* rootDir是机器人的工作目录，下载的流程包、数据文件和执行的中间结果会放在这个目录
* logLevel为日志级别，可设成error、warn、info。缺省是warn。当执行时会生成leanrunner_robot.log的日志文件，输出目录在rootDir配置的工作目录中。


通过下面的命令在命令行启动机器人：

```
leanrunner --robot
```

启动机器人后，它会根据配置自动连接LeanRunner控制器。

首次连接到控制器时，安全考虑，缺省情况下是此机器人是禁用的，即不会被分配自动化任务执行。如需要执行，请在控制器中启用此机器人。详情请查看[机器人管理](workbench.md#robot_manage)

### 执行流程

当在控制器上的一个任务被分配到某个机器人后，会按照下面流程执行：

1. 机器人先下载流程包到工作目录，如有数据文件也会同时下载
2. 启动新的LeanRunner实例，执行流程，执行过程中反馈执行状态到LeanRunner控制器
3. 执行结束后，上传执行日志及其它相关文件到控制器


