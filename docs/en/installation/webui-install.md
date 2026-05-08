---
title: "Hermes WebUI Installation Guide for Windows"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../../zh-CN/installation/webui-install.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# 🌐 Hermes WebUI Installation Guide

> Use Hermes Agent in your browser — three-panel interface with full CLI functionality

---

## What Is Hermes WebUI?

Hermes WebUI is a **lightweight browser-based interface** that provides the same complete feature set as the CLI:

| Feature | Description |
|---------|-------------|
| 💬 Chat Interface | Streaming output, Markdown rendering, code syntax highlighting |
| 📁 Workspace | File browsing, editing, Git integration |
| 📋 Session Management | Multi-session support, search, export/import |
| 🎨 7 Themes | Dark / Light / Nord / Monokai / OLED / Solarized / Slate |
| ⚙️ Settings Hub | Model selection, configuration management, theme switching |

> **No build step required. No framework dependencies.** Pure Python + vanilla JavaScript.

---

## Prerequisites

- ✅ [Agent installation](agent-install.md) completed
- ✅ Python 3.10+ virtual environment activated
- ✅ Browser (Chrome / Edge / Firefox)

---

## Installation Steps

### Step 1: Navigate to the WebUI Directory

```powershell
cd D:\hermes-windows-native\hermes-webui
```

### Step 2: Configure Environment Variables

Create an `.env` file (copy from the example):

```powershell
Copy-Item .env.example .env
```

Edit `.env` and set the key configuration items:

```bash
# ⚠️ REQUIRED: Path to your Agent directory (point to your hermes-agent)
HERMES_WEBUI_AGENT_DIR=D:\hermes-windows-native\hermes-agent

# OPTIONAL: Python path (auto-detected in most cases)
HERMES_WEBUI_PYTHON=D:\hermes-windows-native\hermes-agent\.venv\Scripts\python.exe

# OPTIONAL: Port (default: 8787)
HERMES_WEBUI_PORT=8787

# OPTIONAL: Bind address (default: 127.0.0.1, localhost only)
HERMES_WEBUI_HOST=127.0.0.1
```

### Step 3: Start WebUI

#### Method A: Using start.ps1 (Recommended)

```powershell
cd D:\hermes-windows-native
.\start.ps1
```

The script automatically handles:
- Detecting the Agent directory
- Loading `.env` configuration
- Starting the web server
- Opening your default browser

#### Method B: Manual Startup

```powershell
cd D:\hermes-windows-native\hermes-webui
$env:HERMES_WEBUI_AGENT_DIR="D:\hermes-windows-native\hermes-agent"
..\hermes-agent\.venv\Scripts\python.exe server.py
```

#### Method C: Using the hermes command (Recommended for Advanced Users)

```powershell
# Activate the virtual environment
cd D:\hermes-windows-native\hermes-agent
.\.venv\Scripts\Activate.ps1

# Launch WebUI
hermes webui

# Or specify custom port and host
hermes webui --port 8788 --host 127.0.0.1
```

### Step 4: Verify Successful Startup

You should see output similar to this:

```
✓ Hermes WebUI starting...
✓ Agent directory: D:\hermes-windows-native\hermes-agent
✓ Listening on http://127.0.0.1:8787
✓ Health check passed
```

Open `http://127.0.0.1:8787` in your browser. You should see:

- Left panel: Session list sidebar
- Center panel: Chat area
- Right panel: Workspace file browser
- Bottom bar: Input field + control buttons

![Hermes WebUI running](/screenshots/hermes-webui-start.png)

*Figure: Hermes WebUI three-panel layout — session list on the left, chat area in the center, workspace on the right*

---

## UI Feature Reference

### Main Layout

```
┌──────────────────────────────────────────────────┐
│  [☰] Hermes          [Session Search]   [⚙ Settings] │ ← Top Bar
├─────────┬────────────────────────┬───────────────┤
│ Sessions │                        │               │
│ ─────── │      Chat Area         │   Workspace    │
│ 🔵 Sess1│                        │               │
│ 📌 Sess2│   👤 User Message      │   📁 File Tree │
│ 📁 ProjA│   🤖 AI Reply          │   📄 Preview   │
│ 📁 ProjB│   [Tool Call Card]     │               │
│         │                        │               │
│ [+] New │                        │               │
├─────────┴────────────────────────┴───────────────┤
│  [📎] [🎤] Input...              [Model▼] [Send]  │ ← Bottom Bar
└──────────────────────────────────────────────────┘
```

### Quick Actions

| Action | How To |
|--------|--------|
| Send message | Press Enter or click Send |
| New session | Click [+ New] or type `/new` |
| Switch model | Use the [Model▼] dropdown at the bottom bar |
| Switch theme | Settings → Preferences → Theme |
| Export session | Right-click session → Download as Markdown |
| Upload files | Drag and drop onto input or click 📎 |

---

## Complete Environment Variable Reference

| Variable | Default | Description |
|----------|---------|-------------|
| `HERMES_WEBUI_AGENT_DIR` | Auto-detected | **Required** — Absolute path to hermes-agent directory |
| `HERMES_WEBUI_PYTHON` | Auto-detected | Path to Python executable |
| `HERMES_WEBUI_HOST` | `127.0.0.1` | Bind address (`0.0.0.0` allows LAN access) |
| `HERMES_WEBUI_PORT` | `8787` | Listening port |
| `HERMES_WEBUI_STATE_DIR` | `~/.hermes/webui-mvp` | State data storage directory |
| `HERMES_WEBUI_DEFAULT_WORKSPACE` | `~/workspace` | Default workspace directory |
| `HERMES_HOME` | `~/.hermes` | Hermes base directory |
| `HERMES_CONFIG_PATH` | `~/.hermes/config.yaml` | Configuration file path |
| `HERMES_WEBUI_BOT_NAME` | `Hermes` | Assistant display name |
| `HERMES_WEBUI_PASSWORD` | *(not set)* | Enables password authentication when set |

---

## Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| Blank page / fails to load | Incorrect Agent directory path | Verify `HERMES_WEBUI_AGENT_DIR` in `.env` |
| Port 8787 already in use | Another process is using it | Change `HERMES_WEBUI_PORT=8788` in `.env` |
| Python not found | Path not configured | Manually set `HERMES_WEBUI_PYTHON` |
| File upload failed | File too large | Default limit is 20MB; check file size |
| Mobile display issues | Browser compatibility | Use Chrome or Edge |
| Session data lost | State directory was cleaned up | Check that `HERMES_WEBUI_STATE_DIR` exists |

---

## Security Recommendations

| Scenario | Recommendation |
|----------|----------------|
| Local use only | Keep default `127.0.0.1`, no password needed |
| LAN access | Set `HERMES_WEBUI_PASSWORD=your-password-here` |
| Public exposure | ❌ Not recommended; if necessary, use HTTPS + strong password |

Enable password authentication:

```bash
# Add to .env
HERMES_WEBUI_PASSWORD=change-me-to-something-strong
```

---

## Next Steps

With WebUI installed, configure your AI models:

➡️ [Chat Model Configuration (Kimi K2.6)](../configuration/chat-config.md) — Up and running in 5 minutes
➡️ [Vision Model Configuration (GLM-4.6V)](../configuration/vision-config.md) — Local image recognition
➡️ [Speech-to-Text Configuration (Whisper)](../configuration/audio-config.md) — Local voice transcription
➡️ [Text Processing Configuration (GLM-4.6V)](../configuration/text-config.md) — Local file understanding
