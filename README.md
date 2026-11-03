# ⚡ Taskbar Pulse

<p align="center">
  <img src="app_icon.ico" alt="Taskbar Pulse Logo" width="96" height="96">
</p>

<p align="center">
  <strong>Ultra-Compact Real-Time Windows Taskbar Hardware Monitor</strong><br>
  <em>Displays live CPU and RAM telemetry seamlessly on the Windows 10 & 11 taskbar with a 100% transparent background.</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%20%7C%20Windows%2011-0078D6?logo=windows" alt="Platform">
  <img src="https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python" alt="Python">
  <img src="https://img.shields.io/badge/License-MIT-green" alt="License">
  <img src="https://img.shields.io/badge/Architecture-x64-orange" alt="Architecture">
  <img src="https://img.shields.io/badge/Release-v1.0.0-blue" alt="Release">
</p>

---

## 📌 Overview

**Taskbar Pulse** is a lightweight, high-performance Windows desktop monitor designed to sit directly on the Windows Taskbar—next to your internet speed meter and system tray icons. 

Unlike conventional hardware monitoring utilities that take up entire desktop screens or hide away in menus, Taskbar Pulse provides instant, at-a-glance visibility into your PC's real-time resource consumption while consuming virtually zero CPU (<0.1%) and minimal RAM.

---

## ✨ Key Features

- **✨ 100% Transparent Background:** Blends seamlessly into any taskbar theme, accent color, or desktop wallpaper. No opaque black boxes or borders.
- **⚡ Internet Speed-Meter Style Layout:** Clean 2-line vertical layout displaying real-time CPU percentage and RAM consumption side-by-side.
- **💯 100% CPU Overflow Fix:** Formats CPU utilization smoothly up to 100% without truncation, text clipping, or frame overflow.
- **🧠 3 Dynamic RAM Modes:**
  - **Used RAM:** `RAM  2.2G` (Default)
  - **Available / Free RAM:** `FREE 1.0G`
  - **Percentage:** `RAM  68%`
  - *Double-click the widget anytime to instantly toggle between modes.*
- **⚡ Live Dynamic Hover Tooltip:** Hovering over the meter reveals an expanded hardware card with real-time per-core CPU load, processor clock frequency, physical/logical core counts, total/free RAM, and C: drive storage capacity—updating live every 1 second without flickering.
- **🔒 Strict Taskbar Docking & Z-Order Persistence:**
  - Automatically docks on the Windows taskbar vertically centered and horizontally positioned next to the notification tray.
  - Reject-out-of-bounds safety: automatically rejects accidental desktop coordinates and pulls the widget back to the taskbar.
  - Vertical movement is constrained to the taskbar track so it can never be accidentally dragged up onto the desktop wallpaper.
  - Native Win32 `SetWindowPos(HWND_TOPMOST)` keeps the widget firmly visible above the Windows taskbar without getting buried when Explorer gains focus.
- **🛡️ Single-Instance Win32 Mutex:** Named Mutex (`Local\TaskbarPulseSingleInstance_AiMonitor`) guarantees only one instance runs at any given time.
- **🚀 Windows Auto-Start:** Integrated Windows Startup registry manager (`HKCU\Software\Microsoft\Windows\CurrentVersion\Run`) for seamless auto-start on PC boot.
- **📦 Interactive Setup Installer & Portable Editions:**
  - Includes `TaskbarPulse_Setup.exe` with an interactive setup wizard that prompts for permission to dock on the taskbar and enable autostart.
  - Registers cleanly in Windows **Settings > Apps (Add or Remove Programs)** with a self-contained uninstaller.
  - Also includes a single-file `TaskbarPulse_Portable.exe` for instant plug-and-play use.

---

## 🎮 Controls & Shortcuts

| Action | Function |
|---|---|
| **Left Click + Drag** | Smoothly slides widget horizontally along the taskbar |
| **Double Click** | Cycle RAM display modes (`Used` ➔ `Available` ➔ `Percent`) |
| **Hover (Mouse Over)** | Displays live dynamic telemetry card (CPU, Cores, Frequency, RAM, SSD) |
| **Right Click** | Context Menu (Lock position, Transparency, Color themes, Speeds, Settings) |

---

## 🎨 Color Themes

Choose your preferred aesthetic directly from the right-click menu:
- 💎 **Electric Sky Cyan (`#38bdf8`)** — Default unified theme matching modern internet speed meters.
- ⚪ **Crisp White (`#ffffff`)** — High-contrast minimalist white.
- 🟢 **Emerald / Lime Green (`#34d399`)** — Subtle eco-green.
- 🟡 **Amber Gold (`#fbbf24`)** — Warm dashboard amber.
- 🌈 **Dual Color** — Cyan CPU + Green RAM.

---

## 📥 Installation & Download

### Option 1: Setup Wizard Installer (`TaskbarPulse_Setup.exe`) — *Recommended*
1. Download `TaskbarPulse_Setup.exe` from the [Releases](https://github.com) tab.
2. Run the installer. A setup wizard will appear with customizable permissions:
   - ☑ **Dock and keep monitor directly on Windows Taskbar**
   - ☑ **Start automatically when Windows boots (Auto-Start)**
   - ☑ **Create Desktop Shortcut**
   - ☑ **Add to Windows Start Menu Programs**
   - ☑ **Launch Taskbar Pulse immediately after installation**
3. Click **Install Now**. The app installs cleanly to `%LocalAppData%\Programs\TaskbarPulse` without requiring administrator privileges.
4. Easily uninstall anytime via Windows **Settings > Apps > Installed apps**.

### Option 2: Portable Edition (`TaskbarPulse_Portable.exe`)
- Download `TaskbarPulse_Portable.exe`.
- Double-click to run immediately from any folder or USB drive with zero installation.

### Option 3: Run from Source
```bash
# 1. Clone the repository
git clone https://github.com/your-username/taskbar-pulse.git
cd taskbar-pulse

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch application
python main.py
```

---

## 🏗️ Building from Source

To compile standalone executables yourself:

```bash
# Build Portable Edition (.exe)
python -m PyInstaller --noconfirm --onefile --windowed --icon=app_icon.ico --name "TaskbarPulse_Portable" main.py

# Build Setup Installer (.exe)
python build_installer.py
```

The resulting executables will be generated in the root directory:
- `TaskbarPulse_Setup.exe` (~34 MB)
- `TaskbarPulse_Portable.exe` (~21 MB)

---

## 🧪 Running Automated Tests

Run the built-in test suite to verify hardware telemetry, Windows registry operations, configuration management, and taskbar docking:

```bash
python test_suite.py
```

---

## 📁 Repository Structure

```
taskbar-pulse/
├── autostart.py          # Windows Startup registry manager (HKCU Run key)
├── build_installer.py    # Bundles payload.zip and compiles TaskbarPulse_Setup.exe
├── config.py             # User preferences & persistent settings manager
├── installer.py          # Interactive Setup Wizard with taskbar permission dialog
├── main.py               # Application entry point, Single-Instance Mutex, DPI awareness
├── monitor.py            # Real-time hardware telemetry engine (CPU, RAM, SSD)
├── tray.py               # System tray icon and background menu integration
├── ui_widget.py          # Tkinter transparent taskbar overlay & dynamic hover tooltip
├── test_suite.py         # 5/5 automated unit tests
├── app_icon.ico          # Multi-resolution application icon (16x16 to 256x256)
├── requirements.txt      # Python dependencies
├── .gitignore            # Git exclusion rules for clean repository
├── LICENSE               # MIT License
└── README.md             # Project documentation
```

---

## 📄 License

This project is licensed under the [MIT License](LICENSE) — feel free to use, modify, and distribute it freely.
