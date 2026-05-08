---
title: "Hermes Windows Native Guide — English Navigation"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../zh-CN/index.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# 📚 Hermes Windows Native Guide

> **Run AI Agents Natively on Windows — No Docker · No WSL2 · Zero Overhead**

This guide complements the [hermes-windows-native](https://github.com/markwang2658/hermes-windows-native) code repository, providing complete tutorials from zero to advanced configuration.

---

## 📂 Document Structure

```
docs/en/
├── index.md                          # Main navigation (this file)
├── architecture/
│   └── trimode-routing.md            # Four-mode routing architecture
├── installation/
│   ├── agent-install.md              # Agent installation guide
│   └── webui-install.md              # WebUI installation guide
├── configuration/
│   ├── chat-config.md                # Chat model config (Kimi K2.6)
│   ├── vision-config.md              # Vision model config (GLM-4.6V)
│   ├── audio-config.md               # Speech-to-text config (Whisper)
│   └── text-config.md                # Text processing config (GLM-4.6V)
└── troubleshooting/
    ├── index.md                      # Troubleshooting navigation
    ├── installation-issues.md        # Installation issues
    ├── startup-issues.md             # Startup issues
    ├── connection-issues.md          # Connection issues
    ├── model-issues.md               # Model/API issues
    ├── feature-issues.md             # Feature issues
    ├── performance-issues.md         # Performance issues
    └── windows-issues.md             # Windows-specific issues
```

## 🎯 Who Is This For?

| You Are | Is This Guide Right? |
|---------|---------------------|
| Windows user wanting AI Agents | ✅ Perfect fit, no Linux experience needed |
| Have GPU for local models | ✅ GLM-4.6V + Whisper fully covered |
| Privacy-conscious | ✅ Local models keep data on your machine |
| Older PC with 8GB RAM | ✅ Native runs save ~750MB memory |

---

## ⚡ Quick Navigation

### 🔧 Installation Guides (Required)

| Document | Description | Time | Difficulty |
|----------|-------------|------|------------|
| [Agent Installation](installation/agent-install.md) | Install Hermes Agent core from scratch | 10 min | ⭐⭐ |
| [WebUI Installation](installation/webui-install.md) | Set up browser interface | 5 min | ⭐ |

### ⚙️ Configuration Guides (As Needed)

| Document | Default Model | Use Case | Difficulty |
|----------|---------------|----------|------------|
| [Chat Model Config](configuration/chat-config.md) | Kimi K2.6 ☁️ | AI chat, code writing | ⭐ |
| [Vision Model Config](configuration/vision-config.md) | GLM-4.6V 🔒 | Image recognition, screenshot analysis | ⭐⭐ |
| [Speech-to-Text Config](configuration/audio-config.md) | faster-whisper 🔒 | Voice message transcription | ⭐⭐ |
| [Text Processing Config](configuration/text-config.md) | GLM-4.6V 🔒 | File summarization, code reading | ⭐⭐ |

> ☁️ = Cloud API (requires network) | 🔒 = Local inference (privacy-safe)

### 🏗️ Architecture Design (Advanced)

| Document | Description | Difficulty |
|----------|-------------|------------|
| [Four-Mode Routing Architecture](architecture/trimode-routing.md) | Understand how input routes to different models | ⭐⭐⭐ |

### 🐛 Troubleshooting

| Document | Description |
|----------|-------------|
| [Common Issues & Solutions](troubleshooting/index.md) | 20+ common problems and fixes |

---

## 🗺️ Recommended Reading Paths

```
New Users:       Agent Install → WebUI Install → Chat Config → Start Using
Privacy-First:   Agent Install → WebUI Install → Vision/Audio/Text Config (all local)
Advanced Users:  Full Install → Architecture Design → Custom Tuning
```

---

## 📋 Prerequisites

Before starting, verify your environment meets these requirements:

```powershell
# Check Windows version (needs 1809+, October 2018 update)
[Environment]::OSVersion.VersionString

# Check Python version (needs 3.10+)
python --version

# Check Git
git --version

# Check disk space (recommend ≥ 2GB free)
psdrive C | Select-Object Used, Free
```

| Requirement | Minimum | Recommended |
|-------------|---------|-------------|
| OS | Windows 10 (1809+) | Windows 11 |
| Python | 3.10+ | 3.11 or 3.12 |
| Git | Any version | Latest |
| Disk Space | 500MB | 2GB+ |
| RAM | 4GB | 8GB+ (recommended for local models) |

---

## 🔗 Related Links

| Link | Description |
|------|-------------|
| 📦 [Code Repository](https://github.com/markwang2658/hermes-windows-native) | hermes-windows-native |
| 🧠 [Upstream Agent](https://github.com/NousResearch/hermes-agent) | NousResearch/hermes-agent |
| 🌐 [Upstream WebUI](https://github.com/nesquena/hermes-webui) | nesquena/hermes-webui |
| 💬 [Discussions](https://github.com/markwang2658/hermes-windows-native/discussions) | Q&A and discussions |
| 🐛 [Issues](https://github.com/markwang2658/hermes-windows-native/issues) | Bug reports |

---

## 📄 License

This project is licensed under the [MIT License](../../LICENSE).
