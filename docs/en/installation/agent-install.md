---
title: "Hermes Agent Installation Guide for Windows"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../../zh-CN/installation/agent-install.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# 🔧 Hermes Agent Installation Guide

> Install Hermes Agent core on Windows from scratch — No Docker, no WSL2

---

## 1. Prerequisites Check

Before starting installation, verify each item:

```powershell
# ✅ 1. Check Windows version (needs 1809+, October 2018 update)
[Environment]::OSVersion.VersionString
# Expected output: Microsoft Windows NT 10.0.xxxxx or higher

# ✅ 2. Check Python version (needs 3.10+)
python --version
# Expected output: Python 3.11.x or 3.12.x

# ✅ 3. Check Git
git --version
# Expected output: git version 2.x.x

# ✅ 4. Check PowerShell version (recommend 7+)
$PSVersionTable.PSVersion
# Expected output: Major 7 (or 5.1 in compatibility mode)

# ✅ 5. Check disk space (recommend ≥ 2GB free)
psdrive C | Select-Object @{N='Free(GB)';E={[math]::Round($_.Free/1GB,2)}}
```

### Environment Requirements Summary

| Requirement | Minimum Version | Recommended Version | Where to Get |
|-------------|-----------------|---------------------|--------------|
| Operating System | Windows 10 (1809+) | Windows 11 | [Windows Update](https://www.microsoft.com/software-download/windows10) |
| Python | 3.10+ | 3.11 or 3.12 | [python.org](https://www.python.org/downloads/) |
| Git | Any version | Latest | [git-scm.com](https://git-scm.com/download/win) |
| Disk Space | 500MB | 2GB+ | Free up C drive |
| RAM | 4GB | 8GB+ | Recommended for local models |

> ⚠️ **Important**: When installing Python, **make sure to check "Add Python to PATH"**

---

## 2. Installation Methods

We provide **3 methods** — choose based on your needs:

| Method | Best For | Time Required | Difficulty |
|--------|----------|---------------|------------|
| **A. One-Click Script** ⭐ Recommended | Beginners, quick start | 3 minutes | ⭐ |
| **B. Manual Installation** | Advanced users who want details | 10 minutes | ⭐⭐ |
| **C. Developer Setup** | Contributors, code modification | 15 minutes | ⭐⭐⭐ |

---

## 3. Method A: One-Click Installation (Recommended)

### Step 1: Clone the Repository

```powershell
cd D:\hermes-windows-native
git clone https://github.com/markwang2658/hermes-windows-native.git
cd hermes-windows-native
```

### Step 2: Run the One-Click Script

```powershell
.\install.ps1
```

The script automatically handles:
- ✅ Detects Python environment
- ✅ Creates virtual environment (`venv`)
- ✅ Installs all dependencies
- ✅ Configures basic settings
- ✅ Verifies successful installation

### Step 3: Verify Installation

```powershell
.\start.ps1
```

You should see this output:

```
✓ Hermes Agent v.x.x started successfully
✓ Listening on http://127.0.0.1:8787
✓ Open browser to start chatting
```

Open your browser and visit `http://127.0.0.1:8787` to get started.

![Hermes Agent Startup](../../screenshots/hermes-agent-start.png)

*Figure: Hermes Agent CLI startup screen showing available tools and model information*

---

## 4. Method B: Manual Installation

### Step 1: Clone the Repository

```powershell
cd D:\hermes-windows-native
git clone https://github.com/NousResearch/hermes-agent.git hermes-agent
cd hermes-agent
```

### Step 2: Create Python Virtual Environment

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If you encounter an execution policy error:

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
.\.venv\Scripts\Activate.ps1
```

### Step 3: Install Dependencies

```powershell
pip install -e ".[all]"
```

> 💡 **Tip**: If network is slow, use a mirror:
> ```powershell
> pip install -e ".[all]" -i https://pypi.tuna.tsinghua.edu.cn/simple
> ```

### Step 4: Initialize Configuration

```powershell
hermes setup
```

Follow the wizard prompts to complete initial configuration (select model provider, enter API key, etc.).

### Step 5: Verify Installation

```powershell
hermes doctor
```

Expected output shows all checks in green ✓:

```
✓ Python version: OK (3.11.x)
✓ Dependencies: OK (all installed)
✓ Config file: OK (~/.hermes/config.yaml)
✓ Memory store: OK (SQLite ready)
✓ Agent binary: OK (hermes command available)
```

---

## 5. Method C: Developer Setup

For users who want to contribute code or customize deeply.

### Step 1: Fork and Clone

```powershell
# Fork https://github.com/NousResearch/hermes-agent on GitHub first
git clone https://github.com/<your-username>/hermes-agent.git
cd hermes-agent
git remote add upstream https://github.com/NousResearch/hermes-agent.git
```

### Step 2: Create Development Environment

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -e ".[all,dev]"
```

### Step 3: Run Tests

```powershell
scripts\run_tests.bat
```

> ⚠️ Some tests may be skipped on Windows due to POSIX dependencies — this is normal.

### Step 4: Start Developing

```powershell
hermes              # Launch interactive CLI
hermes --tui        # Launch TUI interface (experimental)
```

---

## 6. Directory Structure Explained

After installation, your directory structure looks like this:

```
D:\hermes-windows-native\
├── hermes-agent/              # Agent core code
│   ├── run_agent.py           # Main entry point
│   ├── cli.py                 # CLI interaction
│   ├── config.yaml.example    # Config example
│   ├── .venv/                 # Python virtual environment
│   └── ...
├── hermes-webui/              # Web UI interface
│   ├── server.py              # Web server
│   ├── static/                # Frontend resources
│   └── ...
├── install.ps1                # One-click installation script
├── start.ps1                  # One-click startup script
├── README.md                  # Project description
└── LICENSE                    # MIT License
```

### User Data Directory

Hermes stores runtime data in your user directory:

```
~/.hermes/
├── config.yaml               # Main configuration file
├── .env                       # API keys and sensitive info
├── logs/                      # Log files
│   ├── agent.log             # Agent runtime logs
│   └── errors.log            # Error logs
├── skills/                    # Custom skills
├── memory/                    # Persistent memory
└── webui-mvp/                 # WebUI state data
```

---

## 7. Common Installation Issues

| Issue | Symptom | Solution |
|-------|---------|----------|
| Python not found | `'python' is not recognized` | Check "Add to PATH" when installing Python, or add it manually |
| pip timeout | `Read timed out` | Use a mirror source `-i https://pypi.tuna.tsinghua.edu.cn/simple` |
| Permission error | `cannot run scripts` | Run `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` |
| Port occupied | `Address already in use` | Change port: `.\start.ps1 -Port 8788` or kill the process using that port |
| Dependency conflict | `ModuleNotFoundError` | Delete venv and rebuild: `Remove-Item .venv -Recurse; python -m venv .venv` |
| Git clone fails | `Connection timed out` | Configure proxy or use a mirror |
| Virtual environment activation fails | `cannot load file` | See Set-ExecutionPolicy command above |
| Insufficient memory | Windows slows down/freezes | Close other programs, ensure ≥ 4GB RAM available |

---

## 8. Uninstallation

To completely uninstall Hermes Agent:

```powershell
# 1. Stop running processes
Stop-Process -Name python -ErrorAction SilentlyContinue

# 2. Delete virtual environment (optional)
Remove-Item .venv -Recurse -ErrorAction SilentlyContinue

# 3. Delete user data (⚠️ deletes all config and memory)
Remove-Item $env:USERPROFILE\.hermes -Recurse -ErrorAction SilentlyContinue
```

---

## 9. Next Steps

After installing Agent, continue with WebUI browser interface:

➡️ [WebUI Installation Guide](webui-install.md)

Or configure AI models directly:

➡️ [Chat Model Configuration (Kimi K2.6)](../configuration/chat-config.md) — Fastest way to start
➡️ [Vision Model Configuration (GLM-4.6V)](../configuration/vision-config.md) — Local image recognition
➡️ [Speech-to-Text Configuration (Whisper)](../configuration/audio-config.md) — Local voice transcription
➡️ [Text Processing Configuration (GLM-4.6V)](../configuration/text-config.md) — Local file reading
