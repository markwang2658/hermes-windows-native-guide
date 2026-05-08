# CLAUDE.md

> **AI 编程助手上下文文件** — 帮助 AI 更好地理解本项目

---

## 项目信息

| 属性 | 值 |
|------|-----|
| **项目名称** | Hermes Windows Native Guide |
| **项目类型** | 技术文档仓库（Markdown + PowerShell） |
| **目标读者** | Windows 用户 / AI Agent 初学者 / 隐私关注者 |
| **配套代码** | [hermes-windows-native](https://github.com/markwang2658/hermes-windows-native) |
| **文档语言** | 中文（主版本）+ 英文（镜像） |

---

## 技术栈

| 技术 | 用途 | 版本要求 |
|------|------|----------|
| Markdown | 文档编写 | GitHub Flavored Markdown |
| PowerShell | 脚本/命令示例 | 5.1+ / 7+ |
| YAML | 配置示例 | 1.2+ |
| shields.io | Badge 徽章 | - |
| ASCII art | 架构图 | - |

---

## 目录结构约定

```
hermes-guide/
├── docs/
│   ├── zh-CN/              # 中文文档（主版本，先写）
│   │   ├── index.md       # 总导航页
│   │   ├── installation/  # 安装指南
│   │   ├── configuration/ # 配置指南（按模型分类）
│   │   ├── architecture/  # 架构设计
│   │   ├── troubleshooting/# 故障排查（按问题类型分子文件）
│   │   └── contributing.md  # 贡献指南
│   └── en/                 # 英文文档（与中文结构对称）
├── examples/              # 配置示例（中英共用）
│   ├── .env.example      # 环境变量
│   └── config.yaml.example
├── screenshots/           # 截图资源（中英共用）
├── assets/                # 其他静态资源
├── .github/              # 工程化模板
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── ISSUE_TEMPLATE/
├── README.md              # 英文门面
├── README.zh-CN.md        # 中文门面
├── CHANGELOG.md           # 更新日志
├── LICENSE                # MIT 许可证
└── .gitignore             # 忽略规则
```

---

## 关键约定

### 文件命名

- 使用 `kebab-case`（小写 + 连字符）
- 示例：`agent-install.md`、`chat-config.md`、`connection-issues.md`
- 禁止：`AgentInstall.md`、`Chat_Config.md`

### 图片路径

- 截图统一放在 `screenshots/` 目录
- 引用方式：相对路径 `../../screenshots/xxx.png`
- 禁止使用绝对路径或外部链接

### 代码块语言标注

```markdown
# PowerShell 命令
```powershell
Get-Process python
```

# YAML 配置
```yaml
model:
  default: "kimi-k2.6"
```

# Bash 环境变量
```bash
export KIMI_API_KEY=sk-xxx
```
```

### Front Matter 格式

**每个 `.md` 文件都必须包含**：

```yaml
---
title: "文档标题"
lang: zh-CN          # 或 en
version: "1.0"       # 与项目版本一致
---
```

### 语言切换按钮

**每个页面顶部都必须有**：

```html
<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../../en/xxx.md">🇺🇸 English</a>
</div>
```

路径规则：
- 从 `docs/zh-CN/yyy/zzz.md` 到 `docs/en/yyy/zzz.md` → `../../en/yyy/zzz.md`
- 从 `docs/zh-CN/zzz.md` 到 `docs/en/zzz.md` → `../en/zzz.md`

---

## 写作风格

### 语言规范

- **中文文档**: 简体中文，专业术语保留英文
  - ✅ API / GPU / CUDA / Docker / WSL2 / Token
  - ❌ 应用程序接口 / 图形处理器 / 计算统一设备架构

- **英文文档**: 美式英语，简洁明了

### 标题层级

```markdown
# 一级标题 (每个文件只有一个)
## 二级标题 (主要章节)
### 三级标题 (子章节)
#### 四级标题 (细节说明)
```

禁止超过 4 级。

### Emoji 使用

| 场景 | 推荐 | 示例 |
|------|------|------|
| 章节标题 | ✅ | `## 🎯 适用人群` |
| 状态标记 | ✅❌⚠️ | `✅ 已完成` / `❌ 不支持` |
| 难度标识 | ⭐ | `⭐` `⭐⭐` `⭐⭐⭐` |
| 语言标识 | 🇨🇳🇺🇸 | 切换按钮 |
| 模型类型 | ☁️🔒 | 云端 / 本地 |

**禁止**: 正文中每行都加 Emoji

### 表格格式

- 对齐列宽
- 避免横向滚动（手机端）
- 表头使用加粗

### 代码示例

- 所有命令必须可直接复制执行
- 敏感值使用占位符：`sk-your-key-here` / `D:\your-path`
- 添加预期输出注释

---

## 配置关键信息

### 默认模型配置

| 模式 | 默认模型 | 提供商 | 类型 |
|------|----------|--------|------|
| Chat | kimi-k2.6 | Moonshot (kimi-coding) | ☁️ 云端 |
| Vision | glm-4.6v-flash:q4 | LM Studio | 🔒 本地 |
| Audio | base (faster-whisper) | 本地 Python | 🔒 本地 |
| Text | glm-4.6v-flash:q4 | LM Studio | 🔒 本地 |

### 关键端口

| 服务 | 端口 | 说明 |
|------|------|------|
| WebUI | 8787 | 主界面 |
| LM Studio | 1234 | 本地模型推理 |

### 关键路径

| 用途 | 路径 |
|------|------|
| 代码根目录 | `D:\hermes-windows-native\` |
| Agent 目录 | `D:\hermes-windows-native\hermes-agent\` |
| WebUI 目录 | `D:\hermes-windows-native\hermes-webui\` |
| 用户数据 | `%USERPROFILE%\.hermes\` |

---

## Commit 规范

采用 **Conventional Commits** 格式：

```
<type>(<scope>): <subject>

<body>
```

### Type 类型

| Type | 说明 |
|------|------|
| `docs` | 文档新增或修改 |
| `fix` | Bug 修复 |
| `style` | 格式调整（不影响内容） |
| `i18n` | 国际化更新 |
| `chore` | 工程化文件更新 |

### Scope 范围

| Scope | 说明 |
|-------|------|
| `readme` | README.md / README.zh-CN.md |
| `installation` | 安装指南 |
| `configuration` | 配置指南 |
| `architecture` | 架构设计 |
| `troubleshooting` | 故障排查 |
| `examples` | 配置示例文件 |

---

## 常见任务

### 新增一篇配置文档

1. 在 `docs/zh-CN/configuration/` 创建 `xxx-config.md`
2. 添加 Front Matter（title / lang / version）
3. 添加语言切换按钮
4. 按照模板编写内容：
   - 为什么选这个技术
   - 如何获取/安装
   - 配置示例（带注释）
   - 测试验证步骤
   - 性能调优建议
   - 常见问题表格
5. 在 `index.md` 中添加导航链接
6. 创建对应的英文版 `docs/en/configuration/xxx-config.md`

### 新增故障排查条目

1. 确定问题类型（安装/启动/连接/模型/功能/性能/Windows）
2. 在对应的 `troubleshooting/xxx-issues.md` 中添加一行
3. 格式：`| 编号 | 问题 | 症状 | 诊断命令 | 解决方案 |`
4. 编号延续现有最大值 + 1

### 更新截图

1. 截图放入 `screenshots/` 目录
2. 命名规范：`<功能名>-<场景>.png`
3. 分辨率：1920×1080 或 2560×1440
4. 格式：PNG（静态）/ GIF（动画）
5. **必须脱敏**：模糊 API Key / 个人路径 / IP 地址
6. 压缩：< 500KB/张

---

## 禁止事项

- ❌ 不要在文档中包含真实 API Key 或密码
- ❌ 不要使用个人路径（如 `C:\Users\YourName`），使用占位符
- ❌ 不要提交 `venv/` 或 `node_modules/` 到 Git
- ❌ 不要修改 `.env.example` 中的占位符为真实值
- ❌ 不要在正文中过度使用 Emoji（每行都加）
- ❌ 不要创建超过 4 级的标题层级
- ❌ 不要使用已废弃的语法或过时的工具名称

---

## 有用的命令

```powershell
# 检查所有内部链接（手动）
Get-ChildItem -Recurse -Filter *.md | Select-String -Pattern "\]\(\.\." | Measure-Object

# 统计文档字数
(Get-ChildItem -Recurse -Filter *.md | Get-Content | Measure-Object -Word).Words

# 检查 Front Matter 完整性
Get-ChildItem -Recurse -Filter *.md | Select-String -Pattern "^---$" | Measure-Object
```

---

**最后更新**: 2026-05-08  
**维护者**: @markwang2658
