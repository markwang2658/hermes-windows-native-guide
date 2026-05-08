---
title: "Hermes Agent Windows 原生安装指南"
lang: zh-CN
version: "1.0"
---

<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../../en/installation/agent-install.md">🇺🇸 English</a>
</div>

# 🔧 Hermes Agent 安装指南

> 从零在 Windows 上安装 Hermes Agent 核心，无需 Docker，无需 WSL2

---

## 一、前置条件检查

在开始安装前，请逐项确认以下环境：

```powershell
# ✅ 1. 检查 Windows 版本（需要 1809+，即 2018 年 10 月更新）
[Environment]::OSVersion.VersionString
# 预期输出: Microsoft Windows NT 10.0.xxxxx 或更高

# ✅ 2. 检查 Python 版本（需要 3.10+）
python --version
# 预期输出: Python 3.11.x 或 3.12.x

# ✅ 3. 检查 Git
git --version
# 预期输出: git version 2.x.x

# ✅ 4. 检查 PowerShell 版本（推荐 7+）
$PSVersionTable.PSVersion
# 预期输出: Major 7 (或 5.1 兼容模式)

# ✅ 5. 检查磁盘空间（建议 ≥ 2GB 可用）
psdrive C | Select-Object @{N='Free(GB)';E={[math]::Round($_.Free/1GB,2)}}
```

### 环境要求汇总

| 要求 | 最低版本 | 推荐版本 | 如何获取 |
|------|----------|----------|----------|
| 操作系统 | Windows 10 (1809+) | Windows 11 | [Windows 更新](https://www.microsoft.com/software-download/windows10) |
| Python | 3.10+ | 3.11 或 3.12 | [python.org](https://www.python.org/downloads/) |
| Git | 任意版本 | 最新版 | [git-scm.com](https://git-scm.com/download/win) |
| 磁盘空间 | 500MB | 2GB+ | 清理 C 盘 |
| 内存 | 4GB | 8GB+ | 本地模型推荐 |

> ⚠️ **重要**: 安装 Python 时**务必勾选 "Add Python to PATH"**

---

## 二、安装方式

提供 **3 种安装方式**，根据你的需求选择：

| 方式 | 适用场景 | 耗时 | 难度 |
|------|----------|------|------|
| **A. 一键脚本** ⭐ 推荐 | 新手、快速体验 | 3 分钟 | ⭐ |
| **B. 手动安装** | 进阶用户、想了解细节 | 10 分钟 | ⭐⭐ |
| **C. 开发者安装** | 贡献代码、修改源码 | 15 分钟 | ⭐⭐⭐ |

---

## 三、方式 A：一键安装（推荐）

### Step 1：克隆代码仓库

```powershell
cd F:\Hermes-Agent
git clone https://github.com/markwang2658/hermes-windows-native.git
cd hermes-windows-native
```

### Step 2：执行一键安装脚本

```powershell
.\install.ps1
```

脚本会自动完成以下操作：
- ✅ 检测 Python 环境
- ✅ 创建虚拟环境 (`venv`)
- ✅ 安装所有依赖包
- ✅ 配置基础设置
- ✅ 验证安装成功

### Step 3：验证安装

```powershell
.\start.ps1
```

看到以下输出说明安装成功：

```
✓ Hermes Agent v.x.x started successfully
✓ Listening on http://127.0.0.1:8787
✓ Open browser to start chatting
```

打开浏览器访问 `http://127.0.0.1:8787` 即可使用。

![Hermes Agent 启动效果](../../screenshots/hermes-agent-start.png)

*图：Hermes Agent CLI 启动成功界面 — 显示可用工具和模型信息*

---

## 四、方式 B：手动安装

### Step 1：克隆代码仓库

```powershell
cd D:\hermes-windows-native
git clone https://github.com/NousResearch/hermes-agent.git hermes-agent
cd hermes-agent
```

### Step 2：创建 Python 虚拟环境

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

如果遇到执行策略错误：

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
.\.venv\Scripts\Activate.ps1
```

### Step 3：安装依赖

```powershell
pip install -e ".[all]"
```

> 💡 **提示**: 如果网络慢，可使用国内镜像源：
> ```powershell
> pip install -e ".[all]" -i https://pypi.tuna.tsinghua.edu.cn/simple
> ```

### Step 4：初始化配置

```powershell
hermes setup
```

按照向导提示完成初始配置（选择模型提供商、输入 API Key 等）。

### Step 5：验证安装

```powershell
hermes doctor
```

预期输出显示所有检查项为绿色 ✓：

```
✓ Python version: OK (3.11.x)
✓ Dependencies: OK (all installed)
✓ Config file: OK (~/.hermes/config.yaml)
✓ Memory store: OK (SQLite ready)
✓ Agent binary: OK (hermes command available)
```

---

## 五、方式 C：开发者安装

适用于想要贡献代码或深度定制的用户。

### Step 1：Fork 并克隆

```powershell
# 在 GitHub 上 Fork https://github.com/NousResearch/hermes-agent
git clone https://github.com/<your-username>/hermes-agent.git
cd hermes-agent
git upstream add https://github.com/NousResearch/hermes-agent.git
```

### Step 2：创建开发环境

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -e ".[all,dev]"
```

### Step 3：运行测试

```powershell
scripts\run_tests.bat
```

> ⚠️ Windows 上部分测试可能因 POSIX 依赖而跳过，这是正常现象。

### Step 4：开始开发

```powershell
hermes              # 启动交互式 CLI
hermes --tui        # 启动 TUI 界面（实验性）
```

---

## 六、目录结构说明

安装完成后，你的目录结构如下：

```
D:\hermes-windows-native\
├── hermes-agent/              # Agent 核心代码
│   ├── run_agent.py           # 主入口
│   ├── cli.py                 # CLI 交互
│   ├── config.yaml.example    # 配置示例
│   ├── .venv/                 # Python 虚拟环境
│   └── ...
├── hermes-webui/              # Web UI 界面
│   ├── server.py              # Web 服务器
│   ├── static/                # 前端资源
│   └── ...
├── install.ps1                # 一键安装脚本
├── start.ps1                  # 一键启动脚本
├── README.md                  # 项目说明
└── LICENSE                    # MIT 许可证
```

### 用户数据目录

Hermes 的运行时数据存储在用户目录下：

```
~/.hermes/
├── config.yaml               # 主配置文件
├── .env                       # API 密钥等敏感信息
├── logs/                      # 日志文件
│   ├── agent.log             # Agent 运行日志
│   └── errors.log            # 错误日志
├── skills/                    # 自定义技能
├── memory/                    # 持久化记忆
└── webui-mvp/                 # WebUI 状态数据
```

---

## 七、常见安装问题

| 问题 | 症状 | 解决方案 |
|------|------|----------|
| Python 找不到 | `'python' 不是内部命令` | 安装 Python 时勾选 "Add to PATH"，或手动添加到 PATH |
| pip 超时 | `Read timed out` | 使用国内镜像源 `-i https://pypi.tuna.tsinghua.edu.cn/simple` |
| 权限错误 | `cannot run scripts` | 执行 `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` |
| 端口被占用 | `Address already in use` | 修改端口：`.\start.ps1 -Port 8788` 或关闭占用端口的进程 |
| 依赖冲突 | `ModuleNotFoundError` | 删除 venv 重建：`Remove-Item .venv -Recurse; python -m venv .venv` |
| Git 克隆失败 | `Connection timed out` | 配置代理或使用镜像站 |
| 虚拟环境激活失败 | `无法加载文件` | 见上方 Set-ExecutionPolicy 命令 |
| 内存不足 | Windows 变慢/卡顿 | 关闭其他程序，确保可用内存 ≥ 4GB |

---

## 八、卸载

如需完全卸载 Hermes Agent：

```powershell
# 1. 停止运行中的进程
Stop-Process -Name python -ErrorAction SilentlyContinue

# 2. 删除虚拟环境（可选）
Remove-Item .venv -Recurse -ErrorAction SilentlyContinue

# 3. 删除用户数据（⚠️ 会删除所有配置和记忆）
Remove-Item $env:USERPROFILE\.hermes -Recurse -ErrorAction SilentlyContinue
```

---

## 九、下一步

Agent 安装完成后，继续安装 WebUI 浏览器界面：

➡️ [WebUI 安装指南](webui-install.md)

或者直接配置 AI 模型：

➡️ [聊天模型配置 (Kimi K2.6)](../configuration/chat-config.md) — 最快上手
➡️ [视觉模型配置 (GLM-4.6V)](../configuration/vision-config.md) — 本地图片识别
➡️ [语音转写配置 (Whisper)](../configuration/audio-config.md) — 本地语音转文字
➡️ [文本处理配置 (GLM-4.6V)](../configuration/text-config.md) — 本地文件解读
