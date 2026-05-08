# 🚀 Hermes Windows Native Guide

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Platform: Windows](https://img.shields.io/badge/Windows-10%2B-0078D6?logo=windows&logoColor=white)]
[![No Docker](https://img.shields.io/badge/No_Docker-required-green)]
[![Docs: English](https://img.shields.io/badge/Docs-English-blue)]

<div align="right">
  <strong>🇺🇸 English</strong> |
  <a href="./README.zh-CN.md">🇨🇳 中文</a>
</div>

> **AI Agent running natively on your Windows — No Docker · No WSL2 · Zero overhead**

---

## ⚡ Quick Start — 3 Commands, 3 Minutes

```powershell
# Step 1: Clone the repository
git clone https://github.com/markwang2658/hermes-windows-native.git
cd hermes-windows-native

# Step 2: One-click install
.\install.ps1

# Step 3: Start the service
.\start.ps1
```

Open http://127.0.0.1:8787 in your browser to get started.

<details>
<summary>📖 Detailed Installation Instructions (click to expand)</summary>

### Prerequisites

| Requirement | Minimum Version | Check Command |
|-------------|-----------------|---------------|
| Windows | 10 (1809+) | `[Environment]::OSVersion.VersionString` |
| Python | 3.10+ | `python --version` |
| Git | Any version | `git --version` |

### Three Installation Methods

| Method | Best For | Time Required |
|--------|----------|---------------|
| **A. One-Click Script** ⭐ Recommended | Beginners, quick start | 3 minutes |
| **B. Manual Install** | Advanced users who want details | 10 minutes |
| **C. Developer Setup** | Contributors, code modification | 15 minutes |

See: [Agent Installation Guide](docs/en/installation/agent-install.md) | [WebUI Installation Guide](docs/en/installation/webui-install.md)

</details>

---

## 🛠️ Tech Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| **Python** | 3.10+ | Runtime environment |
| **PowerShell** | 5.1+ / 7+ | Installation scripts / automation |
| **Kimi K2.6** | Latest | Cloud chat model (Moonshot API) |
| **GLM-4.6V-Flash** | Q4 quantized | Local vision model (LM Studio) |
| **faster-whisper** | latest | Local speech-to-text |
| **LM Studio** | latest | Local model inference engine |
| **CUDA** | 12.x / 13.x | GPU acceleration (optional) |

---

## 📁 Document Structure

```
docs/en/
├── index.md                          # Main navigation (this file)
├── installation/
│   ├── agent-install.md              # Agent installation guide
│   └── webui-install.md              # WebUI installation guide
├── configuration/
│   ├── chat-config.md                # Chat model config (Kimi K2.6)
│   ├── vision-config.md              # Vision model config (GLM-4.6V)
│   ├── audio-config.md               # Speech-to-text config (Whisper)
│   └── text-config.md                # Text processing config (GLM-4.6V)
├── architecture/
│   └── trimode-routing.md            # Four-mode routing architecture
├── troubleshooting/
│   ├── index.md                      # Troubleshooting navigation
│   ├── installation-issues.md        # Installation issues (7 items)
│   ├── startup-issues.md             # Startup issues (6 items)
│   ├── connection-issues.md          # Connection issues (4 items)
│   ├── model-issues.md               # Model & API issues (6 items)
│   ├── feature-issues.md             # Feature issues (6 items)
│   ├── performance-issues.md         # Performance issues (5 items)
│   └── windows-issues.md             # Windows-specific issues (8 items)
└── contributing.md                   # Contributing guide
```

**Total**: 16 documents, 42+ troubleshooting entries

---

## 📚 Document Navigation

### 🔧 Installation Guides (Required)

| Document | Description | Est. Time | Difficulty |
|----------|-------------|-----------|------------|
| [Agent Installation](docs/en/installation/agent-install.md) | Install Hermes Agent from scratch | 10 min | ⭐⭐ |
| [WebUI Installation](docs/en/installation/webui-install.md) | Set up browser interface | 5 min | ⭐ |

### ⚙️ Configuration Guides (As Needed)

| Document | Default Model | Use Case | Difficulty |
|----------|---------------|----------|------------|
| [Chat Config (Kimi K2.6)](docs/en/configuration/chat-config.md) | Kimi K2.6 ☁️ | AI chat, code writing | ⭐ |
| [Vision Config (GLM-4.6V)](docs/en/configuration/vision-config.md) | GLM-4.6V 🔒 | Image recognition, screenshot analysis | ⭐⭐ |
| [Audio Config (Whisper)](docs/en/configuration/audio-config.md) | faster-whisper 🔒 | Voice message transcription | ⭐⭐ |
| [Text Config (GLM-4.6V)](docs/en/configuration/text-config.md) | GLM-4.6V 🔒 | File summarization, code reading | ⭐⭐ |

> ☁️ = Cloud API (requires network) | 🔒 = Local inference (privacy-safe)

### 🏗️ Architecture Design (Advanced)

| Document | Description | Difficulty |
|----------|-------------|------------|
| [Four-Mode Routing Architecture](docs/en/architecture/trimode-routing.md) | Understand how input routes to different models | ⭐⭐⭐ |

### 🐛 Troubleshooting

| Document | Description |
|----------|-------------|
| [Common Issues & Solutions](docs/en/troubleshooting/index.md) | 42+ common problems and fixes |

### 🤝 Contributing

| Document | Description |
|----------|-------------|
| [Contributing Guide](docs/en/contributing.md) | Commit convention / PR workflow / Checklist |

---

## 🗺️ Recommended Reading Paths

```
New Users:       Agent Install → WebUI Install → Chat Config → Start Using
Privacy-First:    Agent Install → WebUI Install → Vision/Audio/Text Config (all local)
Advanced Users:  Full documentation → Architecture Design → Custom Tuning
Contributors:     Contributing Guide → Pick an Issue → Fork → Modify → Submit PR
```

---

## 🔗 Related Links

| Link | Description |
|------|-------------|
| 📦 [Code Repository](https://github.com/markwang2658/hermes-windows-native) | hermes-windows-native |
| 🧠 [Upstream Agent](https://github.com/NousResearch/hermes-agent) | NousResearch/hermes-agent |
| 🌐 [Upstream WebUI](https://github.com/nesquena/hermes-webui) | nesquena/hermes-webui |
| 💬 [Discussions](https://github.com/markwang2658/hermes-windows-native/discussions) | Q&A and discussions |
| 🐛 [Issues](https://github.com/markwang2658/hermes-windows-native/issues) | Bug reports |
| 🤝 [Contributing Guide](docs/en/contributing.md) | How to contribute |

---

## 📊 Project Highlights

| Feature | Description |
|---------|-------------|
| 🪟 **Windows Native** | No Docker, no WSL2, no virtualization overhead |
| 🔒 **Privacy First** | Images/audio/text processed locally — data never leaves your machine |
| 💰 **Cost Effective** | Chat uses cloud (affordable), everything else is free (local) |
| 📚 **Comprehensive Docs** | 16 documents + 42+ troubleshooting entries |
| 🌐 **Bilingual Support** | Full internationalization (Chinese + English) |

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

Why MIT? Maximum community participation — allows both commercial and personal use.
