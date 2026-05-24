
# JadeView
> 面向 Windows 的轻量高性能 WebView 宿主框架，基于 Rust + WebView2 底层实现，提供标准 C 调用接口，支持多语言无缝接入，借助前端技术高效构建原生质感桌面应用。

## ✨ 核心特性
- **原生高性能**：Rust 底层编写，依托 WebView2 内核，体积轻巧、运行低耗稳定
- **全量窗口管控**：支持窗口创建、尺寸位置调节、置顶、缩放、显隐切换等操作
- **完善事件回调**：监听窗口状态、页面导航、通信交互等事件，灵活拦截业务行为
- **自定义标题栏**：兼容系统原生标题栏与完全自定义样式，适配窗口布局规则
- **系统级视觉特效**：深浅色/跟随系统主题，支持 Mica、Acrylic 等 Windows 磨砂材质
- **双向安全 IPC**：前端与本地业务代码自由收发数据，跨层交互便捷可靠
- **本地资源托管**：内置本地服务与自定义协议，轻松加载本地网页静态资源
- **多语言兼容**：原生 C API 对外暴露，配套易语言、Python、JS 等多端 SDK
- **内存安全可靠**：Rust 内存机制规避泄漏、野指针问题，程序运行更稳健

## 🚨 核心强制规则（必看）
1. 框架初始化完成后，**必须注册 `app-ready` 事件**
2. **窗口创建、页面加载等操作，只能在 `app-ready` 事件触发后执行**
3. 遵循：创建实例 → 注册事件 → 运行消息循环 → 事件回调中创建窗口

## 🖥️ 适配平台
- Windows x86 32位
- Windows x64 64位
- Windows ARM64 (ARM 架构)

## 🛠️ 技术架构
- 底层内核：Rust、Microsoft WebView2、标准 C FFI
- 前端技术：HTML5 / CSS3 / TS、React、Vue、Tailwind 等任意主流框架
- 接入语言：C/C++、Python、易语言、火山视窗

## 📦 快速上手
### 1. 环境准备
前往 [GitHub Releases](https://github.com/JadeViewDocs/JadeView/releases) 下载：
- 对应系统位数的 `JadeView.dll`
- 头文件 `jadeview.h`
- 放置到项目目录中

### 2. 官方标准极简示例（100% 匹配文档）
```c
#include "jadeview.h"
#include <stdio.h>

// app-ready 事件回调函数：框架初始化完成，在此处创建窗口
void on_app_ready(JvInstance inst, void* user_data) {
    printf("JadeView 初始化完成，开始创建窗口\n");

    // 1. 配置窗口参数
    JvWindowConfig cfg = {0};
    cfg.width = 900;
    cfg.height = 600;
    cfg.title = "JadeView 官方示例";

    // 2. 创建窗口（必须在 app-ready 事件中执行）
    JvWindow win = jv_create_window(inst, &cfg);

    // 3. 加载网页（支持在线地址 / 本地文件）
    jv_navigate(win, "https://jade.run");
}

int main(void)
{
    // 1. 创建 JadeView 实例
    JvInstance inst = jv_create_instance();
    if (!inst) {
        printf("实例创建失败\n");
        return -1;
    }

    // 2. 【核心】注册 app-ready 事件回调
    // 窗口创建逻辑必须放在此事件触发后执行
    jv_set_event_callback(inst, JV_EVENT_APP_READY, on_app_ready, NULL);

    // 3. 启动消息循环（阻塞运行）
    jv_run_loop(inst);

    // 4. 程序退出，释放资源
    jv_destroy_instance(inst);

    return 0;
}
```

## 📚 完整 API 文档
官方规范文档：https://jade.run/spec/quickstart
- 实例生命周期：创建、事件注册、消息循环、销毁
- 窗口配置：尺寸、标题、样式、系统特效
- 页面操控：地址跳转、执行 JS、资源加载
- 事件体系：`app-ready`、窗口、导航、IPC 事件
- 主题美化：Mica/Acrylic 特效、明暗主题

## 📂 项目信息
- 源码仓库：https://github.com/JadeViewDocs/JadeView
- 官方主页：https://jade.run
- 问题反馈：[GitHub Issues](https://github.com/JadeViewDocs/JadeView/issues)

## 🤝 贡献指南
欢迎提交 PR、反馈 BUG 或提出功能建议，共同完善框架生态。
