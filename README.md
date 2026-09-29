# 妙啊播放器 MiaoA

一款用 [aardio](https://www.aardio.com/) 编写的 Windows 桌面直播 / 点播播放器。打开即看——首页一键进入直播或点播，自带天气与实时时钟，任意位置右键即可管理播放源。

> 绿色单文件 exe，无需安装。

## 功能特性

### 直播播放

- 内置 **5 个可配置的 m3u 直播源**，首页点一下直接观看
- 直播窗口采用**左侧画面 + 右侧节目单**布局
- 节目单支持**频道分组切换**（点击顶部分组头）、滚轮滚动、点击切台
- 基于 Edge WebView2 内嵌 HTML5 `<video>` + hls.js 播放 HLS(m3u8) 流，画面流畅

### 点播影视

- 接入 **TVBox 接口**的 5 个点播源
- 点播首页为**网格式影视卡片**（封面 + 片名 + 简介），顶部**分类导航条**可切换分类
- 选中剧集 → 异步加载详情 → 进入**选集页** → 解析真实地址 → 打开播放窗口
- HTML5 video 原生控制条：播放 / 暂停、音量、全屏、进度条（点播有固定时长，可拖动进度）

### 首页信息

- 自动 **IP 定位 + 天气**：显示城市、温度、天气状况、风向风速（异步加载，不阻塞界面）
- **实时时钟**：秒级刷新，同时显示日期与星期

### 播放源管理

- 在窗口**任意位置右键** → 打开「设置 - 播放源管理」
- 可编辑 5 个直播源与 5 个点播源的**名称**和**接口地址**
- 保存前**自动校验地址**（须以 `http://` 或 `https://` 开头；留空表示该源未配置）
- 配置以 JSON 持久化到 `%AppData%\LivePlayer\config.json`

### 其他

- **启动清理**：启动时尽力清理播放缓存，失败不影响运行

## 使用说明

1. 下载 `妙啊播放器.exe`，双击运行（无需安装）
2. 在窗口任意位置**右键** → 打开「设置 - 播放源管理」
3. 填写直播源（m3u 地址）与点播源（TVBox 接口地址）的**名称**和**地址**
4. 点「保存」，首页按钮名称会同步更新
5. 点击首页「直播源」按钮 → 进入直播播放（左侧画面 + 右侧节目单）
6. 点击首页「点播源」按钮 → 进入影视列表，分类浏览、选集后播放

## 界面说明

| 区域 | 说明 |
| --- | --- |
| 时钟 / 日期 | 左上角，秒级刷新，显示日期与星期 |
| 天气 | 右上角，显示城市、温度、天气状况、风向风速 |
| 【直播】区 | 5 个按钮，对应 5 个 m3u 直播源 |
| 【点播】区 | 5 个按钮，对应 5 个 TVBox 点播源 |

## 技术说明

- 开发语言：[aardio](https://www.aardio.com/)
- 运行平台：Windows（依赖 Microsoft Edge WebView2 运行时，Win10 / Win11 通常已内置）
- 播放方案：`web.view`（WebView2）内嵌 HTML5 `<video>`，用 hls.js 播放 m3u8
- 配置文件：`%AppData%\LivePlayer\config.json`

### 目录结构

```
MiaoA/
├── main.aardio                 主程序（首页：时钟 / 天气 / 直播与点播入口）
├── MiaoA.aproj                 aardio 工程文件
├── forms/                      窗口
│   ├── livePlay.aardio             直播播放窗口（画面 + 节目单）
│   ├── tvboxIndex.aardio           点播首页（分类导航 + 网格卡片）
│   ├── vodPlay.aardio              点播播放窗口
│   └── setting.aardio              设置窗口（播放源管理）
├── lib/                        自研模块
│   ├── configMgr.aardio            配置读写（JSON）
│   ├── m3uParser.aardio            M3U / M3U8 解析
│   ├── tvboxApi.aardio             TVBox 接口
│   ├── netApi.aardio               网络 / 天气（异步执行）
│   ├── cacheCleaner.aardio         缓存清理
│   ├── customCateBar.aardio        分类导航条（GDI 自绘）
│   ├── customGridList.aardio       网格卡片列表（GDI 自绘）
│   └── customProgramList.aardio    节目单控件（GDI 自绘）
└── res/                        资源
    ├── logo.ico                    应用图标
    └── html/
        ├── livePlayer.html         HTML5 播放页
        └── hls.min.js              hls.js 播放库
```

## 下载

前往 [发行版页面](https://gitee.com/powerclub/MiaoA/releases) 下载最新的 `妙啊播放器.exe`，双击即可运行。

## 开发说明

- 本仓库仅包含**工程源码**；`Publish/`（发布产物）、`.build/`（编译临时）、`_tools/`（第三方工具）均已通过 `.gitignore` 忽略
- 用 aardio IDE 打开 `MiaoA.aproj` 即可开发调试

## 注意事项

- 直播源 / 点播源均为**用户自行配置**的第三方接口，请自行确保使用合规
- 播放 HLS 流需要联网

## 许可证

MIT License
