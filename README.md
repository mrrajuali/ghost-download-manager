<div align="center">

<img src="assets/icon.png" alt="Ghost Download Manager Logo" width="110" height="110">

# Ghost Download Manager

**A high-speed, modern, and lightweight multi-threaded download manager with intelligent browser integration.**

Segmented parallel downloads, native Windows H.264/AAC media playback, YouTube & 1,000+ sites, dynamic queue scheduling, fluid 60 FPS UI, and a smart browser extension that catches media other tools miss.

<br>

[![Latest Release](https://img.shields.io/github/v/release/mrrajuali03112008/ghost-download-manager?label=latest&style=for-the-badge&color=7C3AED)](https://github.com/mrrajuali03112008/ghost-download-manager/releases/latest)
[![Windows](https://img.shields.io/badge/Platform-Windows%2010%20%7C%2011-0078D6?style=for-the-badge&logo=windows&logoColor=white)](https://github.com/mrrajuali03112008/ghost-download-manager/releases/latest)
[![Language](https://img.shields.io/badge/Made%20with-Rust-DEA584?style=for-the-badge&logo=rust&logoColor=white)](https://www.rust-lang.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-a78bfa?style=for-the-badge)](LICENSE)

<br>

[![Download Installer](https://img.shields.io/badge/Download-Windows%20Installer-0078D4?style=for-the-badge&logo=windows&logoColor=white)](https://github.com/mrrajuali03112008/ghost-download-manager/releases/latest)
&nbsp;
[![Download Portable](https://img.shields.io/badge/Download-Portable%20ZIP-6B7280?style=for-the-badge&logo=archive&logoColor=white)](https://github.com/mrrajuali03112008/ghost-download-manager/releases/latest)

<br>

<img src="assets/preview.png" alt="Ghost Download Manager Preview" width="94%" style="border-radius: 12px; box-shadow: 0 10px 40px rgba(0,0,0,0.35);">

</div>

---

## 📖 Overview

**Ghost Download Manager** is an advanced, ultra-fast download acceleration system engineered in **Rust**. Built for speed, stability, and elegance, it merges high-concurrency segmented downloading with a sleek, modern 60 FPS dark interface and seamless browser extension capture.

Whether downloading large archives, ISO images, or streaming media from YouTube, Facebook, and thousands of other video platforms, Ghost Download Manager maximizes your network throughput with zero bloat and absolute stability.

---

## 🚀 Key Features

### ⚡ Turbo Multi-Threaded Engine
- **Dynamic Segment Stealing:** Splits downloads across up to 32 adaptive connections. When one thread finishes, it splits the remaining portion of the slowest connection, preventing idle bandwidth.
- **Single Pre-allocated File:** Allocates file space upfront to eliminate slow file stitching and duplicate disk I/O at the end of transfers.
- **Crash-Safe Resume:** Missing ranges are continuously journaled; safely resume interrupted, paused, or severed downloads anytime.
- **Speed Limiter & Scheduler:** Limit speeds in KB/s or MB/s globally or per download, and schedule queue completion triggers (Shutdown, Sleep, Hibernate, or Exit).

### 🎬 Universal Video & Stream Downloader
- **YouTube & 1,000+ Platforms:** Built-in video engine captures 720p, 1080p, 1440p, 2K, and 4K streams with instant audio-video multiplexing.
- **Native Windows Playback (No 0xc00d5212 Codec Errors):** Automatically prioritizes standard **H.264 (AVC)** video and **AAC** audio streams so downloaded files play immediately out-of-the-box in Windows Media Player and Movies & TV without needing third-party codec packs.
- **HLS & DASH Acceleration:** Native stream parser for `.m3u8` playlists and MPEG-DASH manifests with multi-segment parallel caching.

### 🌐 Intelligent Browser Integration
- **Universal Floating Download Bar:** Hover over any playing HTML5 video on YouTube, Facebook, or web players to reveal the sleek IDM-style *Download this video* bar.
- **Deep Browser Support:** First-class extension compatibility for **Google Chrome**, **Microsoft Edge**, **Brave**, **Opera**, and **Mozilla Firefox**.
- **Smart Hand-Off:** Seamlessly pauses browser downloads, transfers headers, authentication cookies, and proxies to Ghost Download Manager, and safely falls back if needed.

### 🎨 Fluid 60 FPS Dark UI
- **Precision Progress Indicator:** Real-time 60 FPS animated barber-pole progress bars with high-contrast text and zero visual artifacts.
- **Live Throughput Visualizer:** Real-time bandwidth graph displaying current download velocity and peak speeds.
- **Segment Inspector:** Live view of individual thread chunks, byte boundaries, and connection health.

---

## ⚡ The Engine Architecture

The core downloader utilizes a high-efficiency async pipeline built in Rust on top of `tokio` and `reqwest`:

- **Work Stealing:** A free connection immediately takes over half of whatever will finish last, dynamically balancing work according to measured transfer speeds.
- **Probe on First Request:** The initial byte-range request determines whether the remote host supports multi-range streaming before spawning worker threads.
- **Self-Healing Connections:** Detects HTTP 429/503 rate limits, network drops, or expired media tokens and refreshes connections automatically.

```rust
// Core Engine Download Flow
let downloader = Downloader::new(client)
    .max_connections(16)
    .speed_limit(None);

downloader.download(job, progress_tx, cancel_rx).await?;
```

---

## 📦 Download & Installation

Get the latest official release from the [**Releases Page**](https://github.com/mrrajuali03112008/ghost-download-manager/releases).

| Distribution | Package File | Description |
| :--- | :--- | :--- |
| **Windows Installer** *(Recommended)* | `Ghost_Download_Manager_Installer.exe` | Complete setup wizard. Installs application binaries, registers system paths, desktop shortcuts, and auto-configures browser native messaging. |
| **Portable Edition** | `Ghost_Download_Manager_Portable.zip` | Standalone zero-install archive. Extract anywhere and launch `ghost_download_manager.exe` directly. Clean package with no batch scripts required. |

---

## 🧩 Browser Extension Setup

To enable universal in-page video detection and download interception:

1. Open your browser extension manager:
   - **Chrome / Brave:** Navigate to `chrome://extensions`
   - **Microsoft Edge:** Navigate to `edge://extensions`
2. Toggle on **Developer mode** in the top-right corner.
3. Click **Load unpacked** and select the extension folder:
   - For Installer:
     ```
     %LOCALAPPDATA%\ghost_download_manager\extensions\browser-extension
     ```
   - For Portable:
     ```
     <Extracted_Folder>\extensions\browser-extension
     ```
4. Click the Ghost Download Manager icon in your browser toolbar to confirm successful communication with the desktop app.

---

## 🛠️ Building from Source

### Prerequisites
- [Rust](https://rustup.rs/) (edition 2021 or later)
- Visual Studio C++ Build Tools (MSVC)
- [Inno Setup 6](https://jrsoftware.org/isdl.php) *(optional, for compiling the Windows installer)*

### Build Steps

```powershell
# 1. Clone the repository
git clone https://github.com/mrrajuali03112008/ghost-download-manager.git
cd ghost-download-manager

# 2. Compile release binary
cargo build --release

# 3. Output binary location:
# target\release\ghost_download_manager.exe
```

---

## 🤝 Community & Developer Support

- 👨‍💻 **Developer:** [Mr Raju Ali](https://t.me/mrrajuali) (Telegram)
- 🏢 **Organization:** [Skill Up Agency LTD](https://t.me/+5LQRN1HAckhjZjBl)
- 🐛 **Issue Tracker:** [GitHub Issues](https://github.com/mrrajuali03112008/ghost-download-manager/issues)
- 🌐 **Project Repository:** [mrrajuali03112008/ghost-download-manager](https://github.com/mrrajuali03112008/ghost-download-manager)

---

## 📄 License

This project is open-source software licensed under the **[MIT License](LICENSE)**.

```
MIT License

Copyright (c) 2026 Mr Raju Ali (Skill Up Agency LTD)
Telegram: https://t.me/mrrajuali | Agency: https://t.me/+5LQRN1HAckhjZjBl
```
