# 妙啊播放器 MiaoA

一个用 [aardio](https://www.aardio.com/) 写的 Windows 桌面直播 / 点播播放器。打开即看——首页一键进入直播或点播，自带天气与实时时钟，任意位置右键即可管理播放源。

## 功能特性

- **直播播放**：内置 5 个可配置的 m3u 直播源，点一下直接观看。左侧播放画面 + 右侧节目单，支持频道分组切换、滚轮滚动、点选切台
- **点播影视**：接入 TVBox 接口的 5 个点播源，网格式影视卡片浏览（封面 / 片名 / 简介），支持分类切换与选集播放
- **流畅播放**：基于 Edge WebView2 内嵌 HTML5 `<video>` + hls.js 播放 HLS(m3u8) 流，使用原生控制条（播放 / 暂停、音量、全屏、进度）
- **首页信息**：自动 IP 定位并异步加载当地天气（不阻塞界面），以及秒级刷新的实时时钟
- **播放源管理**：任意位置右键 → 打开「设置」，编辑每个直播源 / 点播源的名称与接口地址，保存前自动校验地址合法性
- **配置持久化**：配置以 JSON 保存在 `%AppData%\LivePlayer\config.json`
- **启动清理**：启动时尽力清理播放缓存（失败不影响运行）

## 使用说明

1. 用 aardio IDE 打开 `MiaoA.aproj` 直接运行，或运行发布后的 `妙啊播放器.exe`
2. 首页点击任意「直播源」按钮 → 进入直播播放（左侧画面 + 右侧节目单）
3. 首页点击任意「点播源」按钮 → 进入影视列表，分类浏览、选集后播放
4. 在窗口任意位置**右键** → 打开「设置 - 播放源管理」
5. 填写直播源（m3u 地址）与点播源（TVBox 接口地址）的名称和地址，点「保存」立即生效

## 界面说明

- **时钟 / 日期**：左上角，秒级刷新
- **天气**：右上角，显示城市、温度、天气状况、风向风速
- **【直播】区**：5 个按钮，对应 5 个 m3u 直播源
- **【点播】区**：5 个按钮，对应 5 个 TVBox 点播源

## 技术说明

- 开发语言：[aardio](https://www.aardio.com/)
- 运行平台：Windows（依赖 Edge WebView2 运行时）
- 播放方案：`web.view`（WebView2）内嵌 HTML5 `<video>` + hls.js 播放 m3u8
- 模块划分：
  - `main.aardio`：主程序（首页）
  - `forms/`：窗口 —— `livePlay`（直播播放）、`tvboxIndex`（点播首页）、`vodPlay`（点播播放）、`setting`（设置）
  - `lib/`：自研模块 —— `configMgr`（配置读写）、`m3uParser`（m3u 解析）、`tvboxApi`（TVBox 接口）、`netApi`（网络 / 天气）、`cacheCleaner`（缓存清理）、`customCateBar` / `customGridList` / `customProgramList`（GDI 自绘控件）
  - `res/`：图标与 HTML 播放页（`html/hls.min.js`）

## 开发说明

- 本仓库仅包含工程源码；`Publish/`（发布产物）、`.build/`（编译临时）、`_tools/`（第三方工具）均已通过 `.gitignore` 忽略

## 许可证

MIT License
