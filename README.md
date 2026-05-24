# JadeView
> 面向 Windows 的轻量、高性能 WebView 宿主库，基于 Rust 与 WebView2 构建，提供标准 C 语言 API，支持多语言集成，用前端技术快速开发流畅的桌面应用。

## ✨ 核心特性
- **原生高性能**：底层基于 Rust 开发，依托 WebView2 内核，轻量无冗余，运行高效稳定
- **灵活窗口管理**：支持窗口创建、大小/位置配置、最大化/最小化/置顶、显示/隐藏等全量操作
- **丰富事件系统**：内置窗口、导航、IPC 通信等事件，通过回调函数可拦截与控制行为
- **自定义标题栏**：支持内置 `title-overlay` 模式或完全自定义，兼容 Windows Snap Layout
- **现代化视觉效果**：适配 Light/Dark/System 主题，支持 Mica、MicaAlt、Acrylic 等 Windows 原生背景
- **安全 IPC 通信**：提供双向通信能力，实现前端与宿主语言的数据交互
- **内置本地服务器**：支持自定义协议，便捷加载本地前端资源
- **多语言友好**：提供 JS、Python、易语言、火山视窗等官方 SDK，开箱即用
- **安全内存管理**：Rust 底层保障，严格内存管控，避免内存泄漏

## 🖥️ 支持平台
- Windows x86（32 位系统）
- Windows x64（64 位系统）
- Windows x64（ARM 64 位系统）
## 🛠️ 技术栈
### 底层核心
- Rust、WebView2、标准 C 语言 API
### 前端技术（任意选择）
- 基础：HTML5、CSS3、TypeScript
- 框架：React、Vue.js、Angular、Next.js
- 工具：Tailwind CSS、Sass、Webpack、Three.js

## 📦 快速集成
### 1. 获取预编译库
从 [GitHub Releases](https://github.com/JadeViewDocs/JadeView/releases) 下载最新版本（当前最新：v2.1.1），包含：
- 动态库：`JadeView_x86.dll`、`JadeView_x64.dll`
- 调试文件：`.pdb`、`.lib`、`.exp`
- 多语言 SDK 与示例代码

### 2. 多语言集成
支持直接集成以下语言，共享同一原生能力：
- C/C++（原生 API）
- Python（官方 SDK）
- 易语言（官方 SDK，含调用示例）
- 火山视窗（官方 SDK）
- JavaScript（Web SDK）

### 3. 极简示例（C 语言）
```c
#include "jade_view.h"

int main() {
    // 初始化 JadeView
    jade_init();
    
    // 创建 WebView 窗口
    WebViewWindow window = create_webview_window(
        "JadeView 示例", 800, 600, false
    );
    
    // 加载前端页面
    webview_navigate(window, "https://localhost:3000");
    
    // 启动消息循环
    jade_run_loop();
    
    // 释放资源
    jade_destroy(window);
    return 0;
}
```

## 📚 API 概览
完整文档：[JadeView 官网 API](https://jade.run/)
- **核心 API**：初始化、消息循环、资源清理
- **窗口管理 API**：创建/关闭窗口、配置标题/大小/位置
- **WebView API**：页面导航、执行 JavaScript、资源加载
- **事件系统 API**：事件订阅、回调注册、行为拦截
- **主题与样式 API**：主题切换、背景效果配置
- **IPC 通信 API**：消息发送/接收、数据交互
- **本地服务器 API**：自定义协议、本地资源托管

## 🤝 贡献与社区
- 仓库地址：[GitHub](https://github.com/JadeViewDocs/JadeView) | [Gitee 镜像](https://gitee.com/jadeview/JadeView)
- 问题反馈：提交 [Issues](https://github.com/JadeViewDocs/JadeView/issues)
- 交流社群：QQ 群 `703623743`
- 贡献指南：参考仓库 `CONTRIBUTING.md`

## 📝 更新日志
详细变更见 [Releases](https://github.com/JadeViewDocs/JadeView/releases)

---
**JadeView** —— 让 Windows WebView 桌面开发更简单！

要不要我帮你把这个README适配成仓库直传版本，补充徽章和目录跳转链接？
