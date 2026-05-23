# 此目录为火山视窗SDK存放路径

> 更新时间 2026/05/23 16:45

- 修复了 `创建窗口` 函数 JadeView_视图选项 参数节点下 `预加载脚本`  参数传递错误的问题
- 完善了部分函数注释
- 使用流程
  - 申明 JadeView 类  如 Jade  |  JadeView
  - 在 `启动方法` 函数内使用申明的类 Jade.初始化 () 函数  初始化前可手动订阅部分可拦截系统事件
  - 使用 Jade.置IPC频道回调 (本对象, "ipcChannelMessageCallback") 设置订阅IPC回调函数，内有模板
  - 设置完回调函数后进行订阅 如：Jade.注册IPC通道 ("setTitlebarOverlayStyle") 
  - Jade.运行消息循环 ()
  - 在 申明变量处点击 JadeView > 点击闪电图标 > 选择 `应用就绪` 事件
  - 在应用就绪事件下面创建窗口
