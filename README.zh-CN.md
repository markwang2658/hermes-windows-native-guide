# 🚀 Hermes Windows Native Guide

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Platform: Windows 10+](https://img.shields.io/badge/Windows-10%2B-0078D6?logo=windows&logoColor=white)]
[![No Docker](https://img.shields.io/badge/No_Docker-required-green)]
[![Docs: zh-CN](https://img.shields.io/badge/Docs-中文-blue)]

<div align="right">
  <a href="./README.md">🇺🇸 English</a> |
  <strong>🇨🇳 中文</strong>
</div>

> **AI Agent 原生运行在你的 Windows 上 —— 无 Docker · 无 WSL2 · 零开销**

---

## ⚡ Quick Start（3 步启动）

```powershell
# Step 1: 克隆代码仓库
git clone https://github.com/markwang2658/hermes-windows-native.git
cd hermes-windows-native

# Step 2: 一键安装
.\install.ps1

# Step 3: 启动服务
.\start.ps1
```

打开浏览器访问 **http://127.0.0.1:8787** 即可使用。

<details>
<summary>📖 详细安装说明（点击展开）</summary>

### 前置条件

| 要求 | 最低版本 | 检查命令 |
|------|----------|----------|
| Windows | 10 (1809+) | `[Environment]::OSVersion.VersionString` |
| Python | 3.10+ | `python --version` |
| Git | 任意版本 | `git --version` |

### 三种安装方式

| 方式 | 适用场景 | 耗时 |
|------|----------|------|
| **A. 一键脚本** ⭐ 推荐 | 新手、快速体验 | 3 分钟 |
| **B. 手动安装** | 进阶用户、想了解细节 | 10 分钟 |
| **C. 开发者安装** | 贡献代码、修改源码 | 15 分钟 |

详见：[Agent 安装指南](docs/zh-CN/installation/agent-install.md) | [WebUI 安装指南](docs/zh-CN/installation/webui-install.md)

</details>

---

## 🛠️ 技术栈

| 技术 | 版本 | 用途 |
|------|------|------|
| **Python** | 3.10+ | 运行环境 |
| **PowerShell** | 5.1+ / 7+ | 安装脚本 / 自动化 |
| **Kimi K2.6** | 最新版 | 云端对话模型 (Moonshot API) |
| **GLM-4.6V-Flash** | Q4 量化 | 本地视觉模型 (LM Studio) |
| **faster-whisper** | latest | 本地语音转写 |
| **LM Studio** | latest | 本地模型推理引擎 |
| **CUDA** | 12.x / 13.x | GPU 加速（可选） |

---

## 📁 文档结构

```
docs/zh-CN/
├── index.md                          # 总导航（当前文件）
├── installation/
│   ├── agent-install.md              # Agent 安装指南
│   └── webui-install.md              # WebUI 安装指南
├── configuration/
│   ├── chat-config.md                # 聊天模型配置 (Kimi K2.6)
│   ├── vision-config.md              # 视觉模型配置 (GLM-4.6V)
│   ├── audio-config.md               # 语音转写配置 (Whisper)
│   └── text-config.md                # 文本处理配置 (GLM-4.6V)
├── architecture/
│   └── trimode-routing.md            # 四种模式分流架构
├── troubleshooting/
│   ├── index.md                      # 故障排查导航
│   ├── installation-issues.md        # 安装问题 (7 条)
│   ├── startup-issues.md             # 启动问题 (6 条)
│   ├── connection-issues.md          # 连接问题 (4 条)
│   ├── model-issues.md               # 模型问题 (6 条)
│   ├── feature-issues.md             # 功能问题 (6 条)
│   ├── performance-issues.md         # 性能问题 (5 条)
│   └── windows-issues.md             # Windows 问题 (8 条)
└── contributing.md                   # 贡献指南
```

**总计**: 16 个文档，42+ 个故障排查条目

---

## 📚 文档导航

### 🔧 安装指南（必读）

| 文档 | 说明 | 预计耗时 | 难度 |
|------|------|----------|------|
| [Agent 安装](docs/zh-CN/installation/agent-install.md) | 从零安装 Hermes Agent 核心 | 10 分钟 | ⭐⭐ |
| [WebUI 安装](docs/zh-CN/installation/webui-install.md) | 安装浏览器界面 | 5 分钟 | ⭐ |

### ⚙️ 配置指南（按需）

| 文档 | 默认模型 | 用途 | 难度 |
|------|----------|------|------|
| [聊天模型配置](docs/zh-CN/configuration/chat-config.md) | Kimi K2.6 ☁️ | AI 对话、代码编写 | ⭐ |
| [视觉模型配置](docs/zh-CN/configuration/vision-config.md) | GLM-4.6V 🔒 | 图片识别、截图分析 | ⭐⭐ |
| [语音转写配置](docs/zh-CN/configuration/audio-config.md) | faster-whisper 🔒 | 语音消息转文字 | ⭐⭐ |
| [文本处理配置](docs/zh-CN/configuration/text-config.md) | GLM-4.6V 🔒 | 文件摘要、代码阅读 | ⭐⭐ |

> ☁️ = 云端 API（需要网络） | 🔒 = 本地推理（隐私安全）

### 🏗️ 架构设计（进阶）

| 文档 | 说明 | 难度 |
|------|------|------|
| [四种模式分流架构](docs/zh-CN/architecture/trimode-routing.md) | 理解输入如何路由到不同模型 | ⭐⭐⭐ |

### 🐛 故障排查

| 文档 | 说明 |
|------|------|
| [常见问题解决方案](docs/zh-CN/troubleshooting/index.md) | 42+ 常见问题及解决方法 |

### 🤝 参与贡献

| 文档 | 说明 |
|------|------|
| [贡献指南](docs/zh-CN/contributing.md) | Commit 规范 / PR 流程 / Checklist |

---

## 🗺️ 推荐阅读路径

```
新手用户:     Agent 安装 → WebUI 安装 → 聊天配置 → 开始使用
隐私优先:     Agent 安装 → WebUI 安装 → 视觉/语音/文本配置（全本地）
进阶用户:     全部文档阅读 → 架构设计 → 自定义配置调优
贡献者:      贡献指南 → 选择 Issue → Fork → 修改 → 提交 PR
```

---

## 🔗 相关链接

| 链接 | 说明 |
|------|------|
| 📦 [代码仓库](https://github.com/markwang2658/hermes-windows-native) | hermes-windows-native |
| 🧠 [上游 Agent](https://github.com/NousResearch/hermes-agent) | NousResearch/hermes-agent |
| 🌐 [上游 WebUI](https://github.com/nesquena/hermes-webui) | nesquena/hermes-webui |
| 💬 [Discussions](https://github.com/markwang2658/hermes-windows-native/discussions) | 问题讨论 |
| 🐛 [Issues](https://github.com/markwang2658/hermes-windows-native/issues) | Bug 反馈 |
| 🤝 [贡献指南](docs/zh-CN/contributing.md) | 如何参与贡献 |

---

## 📊 项目亮点

| 特性 | 说明 |
|------|------|
| 🪟 **Windows 原生** | 无 Docker、无 WSL2、无虚拟机开销 |
| 🔒 **隐私优先** | 图片/语音/文本本地处理，数据不出机器 |
| 💰 **成本可控** | 聊天走云端（便宜），其他走本地（免费） |
| 📚 **文档完善** | 16 篇文档 + 42+ 故障排查条目 |
| 🌐 **中英双语** | 完整的国际化支持 |

---

## 📄 许可证

本项目采用 [MIT License](LICENSE) 开源。

选择 MIT 的原因：最大化社区参与度，允许商业和个人自由使用。
