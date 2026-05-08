---
title: "贡献指南"
lang: zh-CN
version: "1.0"
---

<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../en/contributing.md">🇺🇸 English</a>
</div>

# 🤝 贡献指南

> 感谢你对 Hermes Windows Native Guide 的贡献！

---

## 📋 贡献方式

| 方式 | 适用场景 | 难度 |
|------|----------|------|
| 🐛 报告 Bug | 发现文档错误/链接失效 | ⭐ |
| ✨ 提交功能请求 | 建议新内容/改进 | ⭐ |
| 📝 补充翻译 | 中英互译 | ⭐⭐ |
| ✏️ 修改文档 | 直接修复问题 | ⭐⭐ |
| 🖼️ 提供截图 | 补充操作截图/GIF | ⭐⭐ |

---

## 🔧 开发环境设置

### 克隆仓库

```powershell
git clone https://github.com/markwang2658/hermes-windows-native-guide.git
cd hermes-windows-native-guide
```

### 配置 Git 代理（国内用户）

```powershell
git config http.proxy http://127.0.0.1:10808
git config https.proxy http://127.0.0.1:10808

# 验证
git config --get http.proxy
# 应输出: http://127.0.0.1:10808

# 测试连接
git ls-remote --heads https://github.com/markwang2658/hermes-windows-native-guide.git
# 应返回 refs/heads/main
```

### 取消代理（如需要）

```powershell
git config --unset http.proxy
git config --unset https.proxy
```

---

## 📝 Commit 规范

### 格式要求

采用 **Conventional Commits** 格式：

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Type 类型

| Type | 说明 | 示例 |
|------|------|------|
| `docs` | 文档新增或修改 | `docs: add chat configuration guide` |
| `fix` | Bug 修复 | `fix: broken link in troubleshooting` |
| `style` | 格式调整（不影响内容） | `style: adjust table alignment` |
| `i18n` | 国际化更新 | `i18n: update English translation for vision-config` |
| `chore` | 工程化文件更新 | `chore: add .gitignore rules for venv` |

### Scope 范围（可选）

| Scope | 说明 |
|-------|------|
| `readme` | README.md / README.zh-CN.md |
| `installation` | 安装指南 |
| `configuration` | 配置指南 (chat/vision/audio/text) |
| `architecture` | 架构设计 |
| `troubleshooting` | 故障排查 |
| `examples` | 配置示例文件 |
| `assets` | 截图/资源文件 |

### Subject 标题规则

- 使用中文（与文档语言一致）
- 不超过 50 字符
- 不以句号结尾
- 使用命令语气（不是过去式）

**✅ 正确示例**:
```
docs(chat-config): 添加 Kimi K2.6 API Key 过期处理说明
fix(troubleshooting): 修复 connection-issues.md 代理端口号错误
i18n(vision-config): 更新英文版 LM Studio 安装步骤
```

**❌ 错误示例**:
```
update some files
fixed bug
修改了一些东西
```

### Body 正文（可选但推荐）

```markdown
docs(chat-config): 添加 Kimi K2.6 API Key 过期处理说明

## 变更内容
- 新增"API Key 过期"常见问题条目
- 更新成本控制章节，添加免费额度说明
- 修正模型列表中 kimi-k2.0711-preview 为 kimi-k2.6

## 关联 Issue
Closes #12
```

---

## ✅ 提交前 Checklist

### 内容质量（必须全部通过）

- [ ] 所有 `.md` 文件内容已审核，无敏感信息泄露
- [ ] 中英文链接双向可用（`zh-CN ↔ en` 切换正常）
- [ ] 新增内容与现有文档无矛盾
- [ ] PowerShell 命令可直接复制执行（已测试）

### 格式规范（必须全部通过）

- [ ] Front Matter 包含 `title` / `lang` / `version`
- [ ] 每个页面顶部有语言切换按钮（🇨🇳 / 🇺🇸）
- [ ] 表格格式正确（对齐、无溢出）
- [ ] 代码块标注语言（`powershell` / `yaml` / `bash`）

### 示例文件安全（如涉及）

- [ ] `examples/.env.example` 无真实密钥（使用占位符）
- [ ] `examples/config.yaml.example` 注释充分
- [ ] 如有截图，已脱敏（无 API Key / 个人路径 / IP 地址）

### 链接验证（必须全部通过）

- [ ] 内部链接（`../xxx.md`）指向正确文件
- [ ] 外部链接（GitHub Issues/Discussions）可访问
- [ ] 锚点链接（`#章节名`）跳转正确

---

## 🌿 分支策略

```
main (主分支，受保护)
  │
  ├── feature/docs-xxx    # 功能分支
  ├── fix/link-broken     # 修复分支
  └── i18n/en-update      # 国际化分支
```

### 分支命名规范

```
<type>-<short-description>

示例:
- feature/vision-screenshots
- fix/troubleshooting-link-404
- i18n/chat-config-en-translation
```

---

## 🔄 PR 流程

### 1. 创建分支

```powershell
git checkout -b feature/your-feature-name
```

### 2. 修改文件

按照上述规范编辑 `.md` 文件。

### 3. 本地预览

```powershell
# 使用 VS Code 预览 Markdown
code .

# 或使用在线工具
# https://markdownlivepreview.com/
```

### 4. 提交变更

```powershell
git add .
git commit -m "docs(scope): 简短描述"
git push origin feature/your-feature-name
```

### 5. 创建 Pull Request

在 GitHub 上创建 PR，填写模板中的各项内容。

### 6. 等待审核

维护者会检查：
- [ ] 内容准确性
- [ ] 格式规范性
- [ ] 链接有效性
- [ ] 无敏感信息泄露

### 7. 合并后

PR 合并后会自动触发以下操作（如有配置 CI）：
- 链接检查
- 格式校验
- 自动部署到 GitHub Pages

---

## 📂 目录结构约定

```
hermes-guide/
├── .github/
│   ├── PULL_REQUEST_TEMPLATE.md    # PR 模板
│   └── ISSUE_TEMPLATE/
│       ├── bug_report.md          # Bug 报告模板
│       └── feature_request.md     # 功能请求模板
├── docs/
│   ├── zh-CN/                     # 中文文档（主版本）
│   │   ├── index.md              # 总导航
│   │   ├── installation/         # 安装指南
│   │   ├── configuration/        # 配置指南
│   │   ├── architecture/         # 架构设计
│   │   └── troubleshooting/       # 故障排查
│   └── en/                        # 英文文档（镜像结构）
├── examples/                      # 配置示例
│   ├── .env.example
│   └── config.yaml.example
├── screenshots/                   # 截图资源
├── assets/                        # 其他静态资源
├── README.md                      # 英文门面
├── README.zh-CN.md                # 中文门面
├── LICENSE                        # MIT 许可证
└── .gitignore                     # 忽略规则
```

---

## 🎨 写作风格

### 语言

- 中文：简体中文，专业术语保留英文（如 API / GPU / CUDA）
- 英文：美式英语，简洁明了

### 格式

- 标题层级：最多 4 级（`#` → `####`）
- 列表：优先使用有序列表（步骤）和无序表格（对比）
- 代码块：标注具体语言（`powershell` / `yaml` / `bash`）
- 表格：对齐列宽，避免横向滚动

### Emoji 使用规范

| 场景 | 推荐 Emoji | 示例 |
|------|-----------|------|
| 章节标题 | 🎯🔧⚙️📚💬👁️🎤📄🏗️🐛 | `## 🎯 适用人群` |
| 状态标记 | ✅❌⚠️ | `✅ 已完成` / `❌ 不支持` |
| 难度标识 | ⭐ | `⭐` `⭐⭐` `⭐⭐⭐` |
| 语言标识 | 🇨🇳🇺🇸 | 切换按钮 |
| 模型类型 | ☁️🔒 | 云端 / 本地 |

**禁止**: 正文中每行都加 Emoji（过度使用影响专业感）

---

## ❓ 常见问题

### Q: 我可以只翻译不写新内容吗？

A: 当然可以！国际化贡献同样重要。

### Q: 我发现一个错别字，需要开 PR 吗？

A: 小问题可以直接提 Issue，标注 `[typo]` 标签即可。

### Q: 我想添加截图，有什么要求？

A: 请参考 `screenshots/README.md` 中的制作规范。截图需脱敏处理。

### Q: Commit 写错了怎么办？

A: 如果还未推送，使用 `git commit --amend` 修改。如果已推送，请新建 Commit 修复。

---

## 💬 联系方式

| 渠道 | 用途 |
|------|------|
| 🐛 [Issues](https://github.com/markwang2658/hermes-windows-native-guide/issues) | Bug 反馈 |
| 💬 [Discussions](https://github.com/markwang2658/hermes-windows-native-guide/discussions) | 问题讨论 |
| 📧 其他 | 通过 Issues 联系 |

---

再次感谢你的贡献！🎉
