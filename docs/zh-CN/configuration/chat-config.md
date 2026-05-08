---
title: "聊天模型配置指南 (Kimi K2.6)"
lang: zh-CN
version: "1.0"
---

<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../../en/configuration/chat-config.md">🇺🇸 English</a>
</div>

# 💬 聊天模型配置（默认：Kimi K2.6）

> 配置云端对话模型，让 Hermes 能和你正常聊天、写代码、回答问题

---

## 一、为什么选择 Kimi K2.6？

| 特性 | Kimi K2.6 | 说明 |
|------|-----------|------|
| 中文能力 | ⭐⭐⭐⭐⭐ | 当前最强中文大模型之一 |
| 上下文长度 | 128K+ | 支持超长对话和大型文件 |
| 响应速度 | ~2s | 快速响应，体验流畅 |
| 价格 | ¥0.02/千 Token | 性价比极高 |
| API 兼容性 | OpenAI 兼容 | 无缝接入 Hermes |

---

## 二、获取 API Key

### Step 1：注册 Moonshot 账号

1. 访问 [platform.moonshot.cn](https://platform.moonshot.cn)
2. 注册 / 登录账号
3. 进入控制台

### Step 2：创建 API Key

1. 点击左侧 **API Keys**
2. 点击 **Create New Key**
3. 复制生成的 Key（格式：`sk-xxxx...`）

> ⚠️ **安全提醒**: API Key 只显示一次，请立即保存！

### Step 3：充值（可选）

新用户有免费额度。用完后在 **计费管理** 中充值。

---

## 三、配置方法

### 方法 A：通过 hermes setup 向导（推荐）

```powershell
hermes setup
```

按提示选择：
1. Provider → 选择 `kimi-coding`
2. 输入 API Key → 粘贴你的 Key
3. 完成验证

### 方法 B：手动编辑配置文件

编辑 `~/.hermes/config.yaml`：

```yaml
model:
  default: "kimi-k2.6"    # 最新版本
  provider: "kimi-coding"             # Moonshot AI 提供商
  base_url: "https://api.moonshot.cn/v1"

# 或者使用 kimi-k2.5（稳定版）
# model:
#   default: "kimi-k2.5"
#   provider: "kimi-coding"
#   base_url: "https://api.moonshot.cn/v1"
```

### 方法 C：通过 .env 文件（推荐用于敏感信息）

编辑 `~/.hermes/.env`：

```bash
# === Kimi API 密钥 ===
KIMI_API_KEY=sk-your-real-api-key-here
```

> ✅ **推荐**: 使用 `.env` 存储密钥，避免提交到 Git。

---

## 四、可用模型列表

| 模型 ID | 名称 | 上下文长度 | 适用场景 |
|---------|------|------------|----------|
| `kimi-k2.6` | K2.6 最新版 | 128K+ | **默认推荐**，最新能力 |
| `kimi-k2.5` | K2.5 稳定版 | 128K | 生产环境稳定选择 |
| `moonshot-v1-8k` | V1 旧版 | 8K | 简单任务，成本低 |
| `moonshot-v1-32k` | V1 长上下文 | 32K | 中等长度文档 |

---

## 五、测试验证

### 5.1 使用 CLI 测试

```powershell
hermes
```

进入交互界面后输入：

```
你好，请介绍一下你自己
```

预期回复包含：
- ✅ 自称是 Hermes/Kimi
- ✅ 回复流畅自然
- ✅ 无报错信息

![Hermes Agent 聊天效果](/screenshots/hermes-agent-chat.png)

*图：Hermes Agent CLI 聊天界面 — 流式输出、Markdown 渲染*

### 5.2 使用 WebUI 测试

1. 打开 `http://127.0.0.1:8787`
2. 输入任意问题
3. 观察流式输出是否正常

![Hermes WebUI 聊天效果](/screenshots/hermes-webui-chat.png)

*图：Hermes WebUI 聊天界面 — 三面板布局、流式输出、代码高亮*

![聊天对话效果演示](/screenshots/demo-chat.png)

*图：Kimi K2.6 实际聊天效果 — 中文对话流畅、支持多轮上下文*

### 5.3 诊断命令

```powershell
hermes doctor
```

确认输出包含：
```
✓ Model config: OK (kimi-k2.6)
✓ API connection: OK
✓ Provider: kimi-coding
```

---

## 六、进阶配置

### 6.1 调整响应参数

```yaml
model:
  default: "kimi-k2.6"
  provider: "kimi-coding"
  base_url: "https://api.moonshot.cn/v1"
  # max_tokens: 4096         # 单次最大输出 Token 数（可选）
  # context_length: 131072   # 上下文窗口大小（通常自动检测）
```

### 6.2 配置代理（国内网络）

如果无法直接连接 Moonshot API：

```yaml
model:
  base_url: "https://api.moonshot.cn/v1"
  # 通过环境变量设置代理
```

在 `.env` 中添加：

```bash
HTTP_PROXY=http://127.0.0.1:7890
HTTPS_PROXY=http://127.0.0.1:7890
```

### 6.3 切换到其他云服务商

Hermes 支持 **10+ 云端提供商**，随时可切换：

| 提供商 | Provider 值 | 需要 | 特色 |
|--------|-------------|------|------|
| OpenRouter | `openrouter` | OPENROUTER_API_KEY | 200+ 模型选择 |
| OpenAI | `openai-codex` | OPENAI_API_KEY | GPT 系列 |
| Anthropic | `anthropic` | ANTHROPIC_API_KEY | Claude 系列 |
| Google | `gemini` | GOOGLE_API_KEY | Gemini 系列 |
| DeepSeek | `custom` | DEEPSEEK_API_KEY | 高性价比 |
| 智谱 GLM | `zai` | GLM_API_KEY | 国产模型 |

切换示例（DeepSeek）：

```yaml
model:
  default: "deepseek-chat"
  provider: "custom"
  base_url: "https://api.deepseek.com/v1"
```

---

## 七、成本控制

### 7.1 定价参考（Kimi K2.6）

| 用量 | 大约费用 |
|------|----------|
| 1000 条日常对话 | ~¥2-5 |
| 100 次代码生成 | ~¥1-3 |
| 每日轻度使用 | < ¥1/天 |
| 重度开发者 | ~¥5-15/天 |

### 7.2 省钱技巧

| 技巧 | 效果 |
|------|------|
| 本地模型处理图片/文件 | 省掉视觉 API 费用 |
| 压缩上下文 (`/compress`) | 减少每次请求的 Token 数 |
| 合理设置 max_tokens | 避免过长回复浪费 |
| 使用 `/new` 开启新会话 | 避免历史累积 |

---

## 八、常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| `Invalid API Key` | Key 错误或过期 | 检查 `.env` 中的 `KIMI_API_KEY` |
| `Rate limit exceeded` | 请求过于频繁 | 降低使用频率或升级套餐 |
| `Connection timeout` | 网络问题 | 检查代理设置或网络连接 |
| 回复内容为空 | 模型过载 | 稍后重试或切换模型 |
| 中文乱码 | 编码问题 | 确保终端使用 UTF-8 编码 |

---

## 九、下一步

聊天模型配置完成后，根据需要继续配置其他模式：

➡️ [视觉模型配置 (GLM-4.6V)](vision-config.md) — 让 AI 能看图
➡️ [语音转写配置 (Whisper)](audio-config.md) — 让 AI 能听懂语音
➡️ [文本处理配置 (GLM-4.6V)](text-config.md) — 让 AI 能读文件
