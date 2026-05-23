# 此目录易语言SDK存放路径

> 更新时间 2026/05/23 21:13

- 修复 【JadeView创建本地服务】 路径编码问题
- 修正 【应用包_加载JAPK包】 错误代码提示文本
- 完善了部分函数注释
- 使用流程
  - 创建无窗口易语言程序，申明 变量类型为 JadeView 类  如 Jade  |  JadeView
  - 在 `_启动子程序` 函数内使用申明的变量调用 Jade.初始化 () 函数  初始化前可手动订阅部分可拦截系统事件
  - 使用 Jade.注册程序事件 ("事件名称", "ipcChannelMessageCallback") 设置订阅IPC回调函数，内有模板
  - 设置完回调函数后进行订阅 如：Jade.ipc_订阅 ("setTitlebarOverlayStyle") 
  - JadeView消息循环 ()
  - 在 JadeView.注册程序事件 (“app-ready”, &JadeView准备就绪)
  - 在【JadeView准备就绪】事件下面创建窗口
