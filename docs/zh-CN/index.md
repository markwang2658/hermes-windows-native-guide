---
title: "Hermes Windows Native Guide — 中文导航"
lang: zh-CN
version: "1.0"
---

<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../en/index.md">🇺🇸 English</a>
</div>

# 📚 Hermes Windows Native Guide

> **AI Agent 在你的 Windows 上原生运行 — 无 Docker · 无 WSL2 · 零额外开销**

本指南配套 [hermes-windows-native](https://github.com/markwang2658/hermes-windows-native) 代码仓库，提供从零安装到高级配置的完整教程。

---

## 📂 文档结构

```
docs/zh-CN/
├── index.md                          # 总导航（当前文件）
├── architecture/
│   └── trimode-routing.md            # 四种模式分流架构
├── installation/
│   ├── agent-install.md              # Agent 安装指南
│   └── webui-install.md              # WebUI 安装指南
├── configuration/
│   ├── chat-config.md                # 聊天模型配置 (Kimi K2.6)
│   ├── vision-config.md              # 视觉模型配置 (GLM-4.6V)
│   ├── audio-config.md               # 语音转写配置 (Whisper)
│   └── text-config.md                # 文本处理配置 (GLM-4.6V)
└── troubleshooting/
    ├── index.md                      # 故障排查导航
    ├── installation-issues.md        # 安装问题
    ├── startup-issues.md             # 启动问题
    ├── connection-issues.md          # 连接问题
    ├── model-issues.md               # 模型问题
    ├── feature-issues.md             # 功能问题
    ├── performance-issues.md         # 性能问题
    └── windows-issues.md             # Windows 特有问题
```

## 🎯 适用人群

| 你是 | 这份指南适合你吗 |
|------|------------------|
| Windows 用户想用 AI Agent | ✅ 完全适合，无需 Linux 经验 |
| 有 GPU 想跑本地模型 | ✅ GLM-4.6V + Whisper 配置全覆盖 |
| 注重隐私保护 | ✅ 本地模型数据不出机器 |
| 8GB 内存的老电脑 | ✅ 原生运行省 ~750MB 内存 |

---

## ⚡ 快速导航

### 🔧 安装指南（必读）

| 文档 | 说明 | 预计耗时 | 难度 |
|------|------|----------|------|
| [Agent 安装](installation/agent-install.md) | 从零安装 Hermes Agent 核心 | 10 分钟 | ⭐⭐ |
| [WebUI 安装](installation/webui-install.md) | 安装浏览器界面 | 5 分钟 | ⭐ |

### ⚙️ 配置指南（按需）

| 文档 | 默认模型 | 用途 | 难度 |
|------|----------|------|------|
| [聊天模型配置](configuration/chat-config.md) | Kimi K2.6 ☁️ | AI 对话、代码编写 | ⭐ |
| [视觉模型配置](configuration/vision-config.md) | GLM-4.6V 🔒 | 图片识别、截图分析 | ⭐⭐ |
| [语音转写配置](configuration/audio-config.md) | faster-whisper 🔒 | 语音消息转文字 | ⭐⭐ |
| [文本处理配置](configuration/text-config.md) | GLM-4.6V 🔒 | 文件摘要、代码阅读 | ⭐⭐ |

> ☁️ = 云端 API（需要网络） | 🔒 = 本地推理（隐私安全）

### 🏗️ 架构设计（进阶）

| 文档 | 说明 | 难度 |
|------|------|------|
| [四种模式分流架构](architecture/trimode-routing.md) | 理解输入如何路由到不同模型 | ⭐⭐⭐ |

### 🐛 故障排查

| 文档 | 说明 |
|------|------|
| [常见问题解决方案](troubleshooting/index.md) | 20+ 常见问题及解决方法 |

---

## 🗺️ 推荐阅读路径

```
新手用户:     Agent 安装 → WebUI 安装 → 聊天配置 → 开始使用
隐私优先:     Agent 安装 → WebUI 安装 → 视觉/语音/文本配置（全本地）
进阶用户:     全部安装 → 架构设计 → 自定义配置调优
```

---

## 📋 前置要求

在开始之前，请确认你的环境满足以下条件：

```powershell
# 检查 Windows 版本（需要 1809+）
[Environment]::OSVersion.VersionString

# 检查 Python 版本（需要 3.10+）
python --version

# 检查 Git
git --version

# 检查磁盘空间（建议 ≥ 2GB 可用）
psdrive C | Select-Object Used, Free
```

| 要求 | 最低版本 | 推荐版本 |
|------|----------|----------|
| 操作系统 | Windows 10 (1809+) | Windows 11 |
| Python | 3.10+ | 3.11 或 3.12 |
| Git | 任意版本 | 最新版 |
| 磁盘空间 | 500MB | 2GB+ |
| 内存 | 4GB | 8GB+（本地模型推荐） |

---

## 🔗 相关链接

| 链接 | 说明 |
|------|------|
| 📦 [代码仓库](https://github.com/markwang2658/hermes-windows-native) | hermes-windows-native |
| 🧠 [上游 Agent](https://github.com/NousResearch/hermes-agent) | NousResearch/hermes-agent |
| 🌐 [上游 WebUI](https://github.com/nesquena/hermes-webui) | nesquena/hermes-webui |
| 💬 [Discussions](https://github.com/markwang2658/hermes-windows-native/discussions) | 问题讨论 |
| 🐛 [Issues](https://github.com/markwang2658/hermes-windows-native/issues) | Bug 反馈 |

---

## 📄 许可证

本项目采用 [MIT License](../../LICENSE) 开源。
