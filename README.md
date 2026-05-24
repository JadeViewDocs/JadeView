
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
#include <stdio.h>
#include <string.h>
#include "jadeview.h"

// app-ready 事件回调函数
const char* app_ready_callback(uint32_t window_id, const char* event_data) {
    // 判断是否成功
    if (window_id == 1 && event_data && strcmp(event_data, "success") == 0) {
        printf("JadeView 准备就绪，现在可以创建窗口了\n");
        
        // 创建窗口选项
        WebViewWindowOptions options = {
            .title = "我的第一个窗口",
            .width = 800,
            .height = 600,
            .resizable = 1,
            .frame_style = "normal",  // normal, no-titlebar, borderless, title-overlay
            .transparent = 0,
            .theme = "System",  // Light, Dark, System
            .maximized = 0,
            .maximizable = 1,
            .minimizable = 1,
            .x = -1,  // -1, -1 表示居中
            .y = -1,
            .min_width = 0,
            .min_height = 0,
            .max_width = 0,
            .max_height = 0,
            .fullscreen = 0,
            .focus = 1,
            .hide_window = 0,
            .use_page_icon = 0,
            .content_protection = 0,
            .auto_save_state = 0
        };
        
        // 创建 WebView 设置
        WebViewSettings settings = {
            .autoplay = 0,
            .background_throttling = 0,
            .disable_right_click = 0,
            .ua = NULL,
            .preload_js = NULL,
            .allow_fullscreen = 0,
            .postmessage_whitelist = NULL
        };
        
        // 创建窗口
        uint32_t new_window_id = create_webview_window(
            "https://www.example.com",
            0,
            &options,
            &settings
        );
        
        if (new_window_id == 0) {
            printf("窗口创建失败\n");
        } else {
            printf("窗口创建成功，窗口 ID：%u\n", new_window_id);
        }
    } else {
        printf("JadeView 初始化失败：%s\n", event_data ? event_data : "未知错误");
    }
    
    return NULL;
}

int main() {
    // 先注册 app-ready 事件
    jade_on("app-ready", app_ready_callback);
    
    // 初始化
    int result = JadeView_init(
        1,
        NULL,
        NULL,
        "我的应用",
        "com.example.myapp",
        0
    );
    
    if (result == 0) {
        printf("初始化失败\n");
        return 1;
    }
    
    printf("初始化成功，等待 app-ready 事件...\n");
    
    // 运行消息循环（可选，在 DLL 嵌入场景下通常不需要
    // run_message_loop();
    
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
