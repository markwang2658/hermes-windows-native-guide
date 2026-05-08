# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-05-08

### Added

#### 文档结构
- 📁 初始化项目目录结构（docs / examples / screenshots / assets）
- 📝 创建中文文档导航页 `docs/zh-CN/index.md`
- 📝 创建英文文档导航页 `docs/en/index.md`

#### 安装指南
- 📝 Agent 安装指南（3 种安装方式：一键脚本 / 手动 / 开发者）
- 📝 WebUI 安装指南（3 种启动方式：start.ps1 / 手动 / hermes 命令）

#### 配置指南
- 💬 聊天模型配置 (Kimi K2.6) — API Key 获取、配置方法、成本控制
- 👁️ 视觉模型配置 (GLM-4.6V) — LM Studio 安装、量化选择、GPU 加速
- 🎤 语音转写配置 (faster-whisper) — 模型选择、CUDA 加速、多语言
- 📄 文本处理配置 (GLM-4.6V) — 文件类型支持、典型场景

#### 架构设计
- 🏗️ 四种模式分流架构文档（Chat / Vision / Audio / Text）
- 📊 ASCII 架构图 + 模式对比表 + 数据流详解
- 🪟 Windows 特殊处理说明

#### 故障排查
- 🔧 安装问题 (7 条)
- 🚀 启动问题 (6 条)
- 🌐 连接问题 (4 含 Git 代理完整配置)
- 🤖 模型问题 (6 条)
- ⚙️ 功能问题 (6 条)
- ⚡ 性能问题 (5 条 + 优化速查表)
- 🪟 Windows 特有问题 (8 条)

#### 工程化规范
- 📋 PR 模板 `.github/PULL_REQUEST_TEMPLATE.md`
- 🐛 Bug 报告模板 `.github/ISSUE_TEMPLATE/bug_report.md`
- ✨ 功能请求模板 `.github/ISSUE_TEMPLATE/feature_request.md`
- 🤝 贡献指南 `docs/zh-CN/contributing.md`
  - Commit 规范（Conventional Commits 格式）
  - 提交前 Checklist（7 大类 20+ 检查项）
  - 分支命名规范
  - PR 流程说明
  - 写作风格指南

#### 配置示例
- 📄 `.env.example` 环境变量示例（含安全警告）
- 📄 `config.yaml.example` 配置文件示例

### Documentation

- ✅ 所有 16 个文档文件添加 Front Matter（title / lang / version）
- ✅ 所有 16 个文档文件添加语言切换按钮（🇨🇳 / 🇺🇸）
- ✅ README.zh-CN.md 添加 Badge 徽章系统（4 个 shields.io）
- ✅ README.zh-CN.md 添加 Quick Start 内联（3 步启动）
- ✅ README.zh-CN.md 添加技术栈章节（8 项技术列表）
- ✅ README.zh-CN.md 添加文档结构树形图
- ✅ README.zh-CN.md 添加项目亮点表格
- ✅ index.md 添加完整文档结构树形导航
- ✅ troubleshooting 拆分为 7 个独立子文件（便于单独更新）

### Fixed

- 🔗 修复所有失效链接（`troubleshooting.md` → `troubleshooting/index.md`）
- 📍 统一路径前缀为 `D:\hermes-windows-native`
- 🔢 统一模型版本号：`kimi-k2.0711-preview` → `kimi-k2.6`
- 🔢 统一量化等级：`glm-4.6v-flash:q5` → `glm-4.6v-flash:q4`
- 🔢 重编 troubleshooting 子文件编号（从 1.1 开始）

---

## [Unreleased]

### Planned

- 🖼️ 制作核心截图（WebUI 主界面 / 架构图 / 配置界面）
- 🎬 制作 Quick Start GIF 动画
- 🌐 完善英文版文档（目前为占位内容）
- ⚙️ 完善 config.yaml.example 注释
- 📝 补充 .gitignore 规则
- 🤖 创建 CLAUDE.md AI 编程助手上下文文件
- 🔧 配置 GitHub Actions CI/CD（链接检查 / 格式校验）
- 💬 启用 GitHub Discussions
- 🏷️ 设置仓库 Topics 标签

---

## 版本说明

| 版本 | 类型 | 说明 |
|------|------|------|
| **1.0.0** | Major | 初始发布，包含完整的中文文档体系 |
| **1.1.0** | Minor | 计划：补充截图、完善英文版 |
| **2.0.0** | Major | 远期：社区贡献内容整合 |

---

**Changelog 格式参考**: [Keep a Changelog](https://keepachangelog.com/)
