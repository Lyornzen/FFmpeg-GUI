# 🎬 FFmpeg GUI

> 跨平台 FFmpeg 桌面图形界面工具 — 视频/音频处理一站式解决方案  
> Cross-platform desktop GUI for FFmpeg — all-in-one video/audio processing tool

![Electron](https://img.shields.io/badge/Electron-33-blue?logo=electron)
![Platform](https://img.shields.io/badge/platform-Windows%20|%20macOS%20|%20Linux-lightgrey)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 📋 功能总览

### 1. 视频处理

| 工具 | 功能 |
|------|------|
| **视频裁剪** | 按时间段 / 起始结束 / 帧范围裁剪，支持快速无损与精确重编码两种模式 |
| **视频转码** | 7 种输出格式：MP4(H.264/H.265)、MKV、AVI、MOV、WEBM(VP9)、GIF |
| **调整分辨率** | 10 种预设 + 自定义宽高：1080p → 竖屏 9:16 → 正方形 1:1 |
| **压缩视频** | CRF 18/23/28/32 + 固定码率 1M/2.5M/5M + 仅压缩音频 |

### 2. 音频分离与替换

| 工具 | 功能 |
|------|------|
| **提取音频** | 8 种输出格式：MP3(320k/128k)、AAC(256k/128k)、FLAC、WAV、Opus、原样 |
| **替换音轨** | 替换 / 新增第二音轨 / 延迟同步 / 静音处理 |
| **静音视频** | 完全删除音轨 / 保留音轨设为零音量 |

### 3. 音频处理

| 工具 | 功能 |
|------|------|
| **音频转码** | 8 种输出格式转换 |
| **音频裁剪** | 按时间段 / 起始结束，支持快速无损与精确重编码 |
| **调整音量** | 0.5× → 3.0× + 最大化不失真 + 自定义倍数 |
| **合并音频** | 首尾拼接 / 混音叠加 / 混音降低背景音 |

### 4. 其他工具

| 工具 | 功能 |
|------|------|
| **查看媒体信息** | ffprobe 输出格式/流/帧信息，支持 JSON |
| **生成 GIF** | 标准/高清/低质量/调色板高质量 4 种模式 |


## 🚀 快速开始

### 前置要求

- [Node.js](https://nodejs.org/) ≥ 18
- FFmpeg 二进制 **自动打包**（使用 `@ffmpeg-installer`，无需手动安装）

### 运行

```bash
# 克隆
git clone https://github.com/your-username/ffmpeg-gui.git
cd ffmpeg-gui

# 安装依赖
npm install

# 启动
npm start
```

> **Windows 用户**：如果 `npm start` 提示 `'node' 不是内部命令`，试试：
> ```bash
> npm run start:win
> ```

### 打包

```bash
# Windows — NSIS 安装包 + 便携版
npm run dist:win

# macOS — DMG
npm run dist:mac

# Linux — AppImage + deb
npm run dist:linux

# 全平台
npm run dist:all
```

---

## 📦 体积优化

| 产物 | 体积 | 说明 |
|------|------|------|
| NSIS 安装包 | ~55 MB | LZMA 固实压缩 |
| Portable 便携版 | ~90 MB | 解压即用 |
| macOS DMG | ~70 MB | 双架构 (x64 + arm64) |
| Linux AppImage | ~80 MB | |

**裁剪策略**：
- 只打包 `@ffmpeg-installer` / `@ffprobe-installer` 两个运行时依赖
- `electron-builder` 等 300+ 个开发依赖全部排除
- 原生二进制解包到 asar 外，JS 代码打入 asar
- `compression: "maximum"` 使用最大压缩级别

---

## 🏗 项目结构

```
ffmpeg-gui/
├── main.js                     # Electron 主进程
├── preload.js                  # 安全预加载脚本 (contextBridge)
├── renderer/
│   ├── index.html              # 主页面结构
│   ├── style.css               # Fluent Design 样式 (~480 行)
│   └── renderer.js             # UI 逻辑 + 13 个工具配置 (~1360 行)
├── package.json                # 依赖 + 打包配置
├── .gitignore
├── .github/workflows/build.yml # CI: 合并到 main 自动构建
└── assets/                     # 图标
```

---

## 🛡 安全

- ✅ `nodeIntegration: false` — 渲染进程禁用 Node API
- ✅ `contextIsolation: true` — 上下文隔离
- ✅ `contextBridge` — 受控 IPC 通信
- ✅ `-y` / `-nostdin` — ffmpeg 安全参数
- ✅ 30 分钟超时保护 — 防止 ffmpeg 挂死

---

## 🧩 技术栈

| 层 | 技术 |
|----|------|
| 框架 | Electron 33 |
| 前端 | 原生 HTML/CSS/JS |
| 设计 | Fluent Design (Mica + WinUI) |
| 字体 | Segoe UI Variable + SF Mono |
| FFmpeg | `@ffmpeg-installer/ffmpeg` |
| 打包 | electron-builder 25 |
| CI | GitHub Actions (Windows) |

---

## 🖥 系统要求

| 平台 | 最低要求 |
|------|---------|
| Windows 10+ | x64 |
| macOS 11+ | Intel / Apple Silicon |
| Linux | x64 (GLIBC ≥ 2.28) |

---

## 📄 License

MIT © FFmpeg GUI
