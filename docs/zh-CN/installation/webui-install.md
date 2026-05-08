---
title: "Hermes WebUI Windows 原生安装指南"
lang: zh-CN
version: "1.0"
---

<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../../en/installation/webui-install.md">🇺🇸 English</a>
</div>

# 🌐 Hermes WebUI 安装指南

> 在浏览器中使用 Hermes Agent — 三面板界面，完整 CLI 功能

---

## 一、WebUI 是什么？

Hermes WebUI 是一个**轻量级浏览器界面**，提供与 CLI 完全相同的功能：

| 功能 | 说明 |
|------|------|
| 💬 聊天界面 | 流式输出、Markdown 渲染、代码高亮 |
| 📁 工作区 | 文件浏览、编辑、Git 集成 |
| 📋 会话管理 | 多会话、搜索、导出/导入 |
| 🎨 7 种主题 | Dark / Light / Nord / Monokai / OLED / Solarized / Slate |
| ⚙️ 设置中心 | 模型选择、配置管理、主题切换 |

> **无需构建步骤，无框架依赖。** 纯 Python + 原生 JS。

---

## 二、前置条件

- ✅ 已完成 [Agent 安装](agent-install.md)
- ✅ Python 3.10+ 虚拟环境已激活
- ✅ 浏览器（Chrome / Edge / Firefox）

---

## 三、安装步骤

### Step 1：进入 WebUI 目录

```powershell
cd D:\hermes-windows-native\hermes-webui
```

### Step 2：配置环境变量

创建 `.env` 文件（从示例复制）：

```powershell
Copy-Item .env.example .env
```

编辑 `.env` 文件，关键配置项：

```bash
# ⚠️ 必填：Agent 目录路径（指向你的 hermes-agent）
HERMES_WEBUI_AGENT_DIR=D:\hermes-windows-native\hermes-agent

# 可选：Python 路径（通常自动检测）
HERMES_WEBUI_PYTHON=D:\hermes-windows-native\hermes-agent\.venv\Scripts\python.exe

# 可选：端口（默认 8787）
HERMES_WEBUI_PORT=8787

# 可选：绑定地址（默认 127.0.0.1，仅本机访问）
HERMES_WEBUI_HOST=127.0.0.1
```

### Step 3：启动 WebUI

#### 方式 A：使用 start.ps1（推荐）

```powershell
cd D:\hermes-windows-native
.\start.ps1
```

脚本自动完成：
- 检测 Agent 目录
- 加载 .env 配置
- 启动 Web 服务器
- 打开浏览器

#### 方式 B：手动启动

```powershell
cd D:\hermes-windows-native\hermes-webui
$env:HERMES_WEBUI_AGENT_DIR="D:\hermes-windows-native\hermes-agent"
..\hermes-agent\.venv\Scripts\python.exe server.py
```

#### 方式 C：使用 hermes 命令（推荐进阶用户）

```powershell
# 激活虚拟环境
cd D:\hermes-windows-native\hermes-agent
.\.venv\Scripts\Activate.ps1

# 启动 WebUI
hermes webui

# 或指定端口
hermes webui --port 8788 --host 127.0.0.1
```

### Step 4：验证成功

看到以下输出说明启动成功：

```
✓ Hermes WebUI starting...
✓ Agent directory: D:\hermes-windows-native\hermes-agent
✓ Listening on http://127.0.0.1:8787
✓ Health check passed
```

打开 `http://127.0.0.1:8787`，你应该看到：

- 左侧：会话列表栏
- 中间：聊天区域
- 右侧：工作区文件浏览器
- 底部：输入框 + 控制按钮

![Hermes WebUI 启动效果](/screenshots/hermes-webui-start.png)

*图：Hermes WebUI 三面板界面 — 左侧会话列表、中间聊天区域、右侧工作区*

---

## 四、界面功能速查

### 4.1 主布局

```
┌──────────────────────────────────────────────────┐
│  [☰] Hermes          [会话搜索]    [⚙️ 设置]     │ ← 顶栏
├─────────┬────────────────────────┬───────────────┤
│ 会话列表 │                        │               │
│ ─────── │      聊天区域           │   工作区       │
│ 🔵 会话1 │                        │               │
│ 📌 会话2 │   👤 用户消息           │   📁 文件树    │
│ 📁 项目A │   🤖 AI 回复            │   📄 预览      │
│ 📁 项目B │   [工具调用卡片]        │               │
│         │                        │               │
│ [+]新建 │                        │               │
├─────────┴────────────────────────┴───────────────┤
│  [📎] [🎤] 输入框...              [模型▼] [发送]  │ ← 底栏
└──────────────────────────────────────────────────┘
```

### 4.2 快捷操作

| 操作 | 方式 |
|------|------|
| 发送消息 | Enter 或点击发送 |
| 新建会话 | 点击 [+新建] 或 `/new` |
| 切换模型 | 底栏 [模型▼] 下拉菜单 |
| 切换主题 | 设置 → Preferences → Theme |
| 导出会话 | 右键会话 → Download as Markdown |
| 上传文件 | 拖拽到输入框或点击 📎 |

---

## 五、环境变量完整参考

| 变量名 | 默认值 | 说明 |
|--------|--------|------|
| `HERMES_WEBUI_AGENT_DIR` | 自动检测 | **必填** — hermes-agent 目录绝对路径 |
| `HERMES_WEBUI_PYTHON` | 自动检测 | Python 可执行文件路径 |
| `HERMES_WEBUI_HOST` | `127.0.0.1` | 绑定地址（`0.0.0.0` 允许局域网访问） |
| `HERMES_WEBUI_PORT` | `8787` | 监听端口 |
| `HERMES_WEBUI_STATE_DIR` | `~/.hermes/webui-mvp` | 状态数据存储目录 |
| `HERMES_WEBUI_DEFAULT_WORKSPACE` | `~/workspace` | 默认工作区目录 |
| `HERMES_HOME` | `~/.hermes` | Hermes 基础目录 |
| `HERMES_CONFIG_PATH` | `~/.hermes/config.yaml` | 配置文件路径 |
| `HERMES_WEBUI_BOT_NAME` | `Hermes` | 助手显示名称 |
| `HERMES_WEBUI_PASSWORD` | *(未设置)* | 设置后启用密码登录 |

---

## 六、常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 页面空白 / 无法加载 | Agent 目录路径错误 | 检查 `.env` 中 `HERMES_WEBUI_AGENT_DIR` 是否正确 |
| 端口 8787 被占用 | 其他程序占用 | 修改 `.env` 中 `HERMES_WEBUI_PORT=8788` |
| 找不到 Python | 路径未设置 | 手动设置 `HERMES_WEBUI_PYTHON` |
| 文件上传失败 | 文件过大 | 默认限制 20MB，检查文件大小 |
| 移动端显示异常 | 浏览器兼容性 | 使用 Chrome / Edge |
| 会话数据丢失 | 状态目录被清理 | 检查 `HERMES_WEBUI_STATE_DIR` 是否存在 |

---

## 七、安全建议

| 场景 | 建议 |
|------|------|
| 仅本地使用 | 保持默认 `127.0.0.1`，无需密码 |
| 局域网访问 | 设置 `HERMES_WEBUI_PASSWORD=你的密码` |
| 公网暴露 | ❌ 不推荐，如必须请配合 HTTPS + 强密码 |

启用密码认证：

```bash
# 在 .env 中添加
HERMES_WEBUI_PASSWORD=change-me-to-something-strong
```

---

## 八、下一步

WebUI 安装完成后，配置 AI 模型：

➡️ [聊天模型配置 (Kimi K2.6)](../configuration/chat-config.md) — 最快上手，5 分钟可用
➡️ [视觉模型配置 (GLM-4.6V)](../configuration/vision-config.md) — 本地图片识别
➡️ [语音转写配置 (Whisper)](../configuration/audio-config.md) — 本地语音转文字
➡️ [文本处理配置 (GLM-4.6V)](../configuration/text-config.md) — 本地文件解读
