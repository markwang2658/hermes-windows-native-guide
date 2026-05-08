---
title: "Chat Model Configuration (Kimi K2.6)"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../../zh-CN/configuration/chat-config.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# 💬 Chat Model Configuration (Default: Kimi K2.6)

> Configure the cloud-based conversational model so Hermes can chat, write code, and answer questions

---

## Why Kimi K2.6?

| Feature | Kimi K2.6 | Details |
|---------|-----------|---------|
| Chinese Language | ⭐⭐⭐⭐⭐ | Among the top Chinese LLMs available today |
| Context Length | 128K+ | Supports ultra-long conversations and large files |
| Response Speed | ~2s | Fast response, smooth experience |
| Pricing | ~¥0.02/1K tokens | Exceptional value for money |
| API Compatibility | OpenAI-compatible | Seamless integration with Hermes |

---

## Obtaining an API Key

### Step 1: Register a Moonshot Account

1. Visit [platform.moonshot.cn](https://platform.moonshot.cn)
2. Sign up / log in to your account
3. Navigate to the console dashboard

### Step 2: Create an API Key

1. Click **API Keys** in the left sidebar
2. Click **Create New Key**
3. Copy the generated key (format: `sk-xxxx...`)

> ⚠️ **Security Note**: API keys are displayed only once. Save it immediately!

### Step 3: Top Up Balance (Optional)

New accounts include free credits. Recharge via **Billing** when credits are depleted.

---

## Configuration Methods

### Method A: Using the hermes setup wizard (Recommended)

```powershell
hermes setup
```

Follow the prompts:
1. Provider → Select `kimi-coding`
2. Enter API Key → Paste your key
3. Complete verification

### Method B: Manual config file editing

Edit `~/.hermes/config.yaml`:

```yaml
model:
  default: "kimi-k2.6"    # Latest version
  provider: "kimi-coding"             # Moonshot AI provider
  base_url: "https://api.moonshot.cn/v1"

# Or use kimi-k2.5 (stable release)
# model:
#   default: "kimi-k2.5"
#   provider: "kimi-coding"
#   base_url: "https://api.moonshot.cn/v1"
```

### Method C: Via .env file (Recommended for sensitive data)

Edit `~/.hermes/.env`:

```bash
# === Kimi API Key ===
KIMI_API_KEY=sk-your-real-api-key-here
```

> ✅ **Recommended**: Store keys in `.env` to prevent accidental commits to Git.

---

## Available Models

| Model ID | Name | Context Length | Use Case |
|----------|------|----------------|----------|
| `kimi-k2.6` | K2.6 Latest | 128K+ | **Default recommended**, latest capabilities |
| `kimi-k2.5` | K2.5 Stable | 128K | Stable choice for production |
| `moonshot-v1-8k` | V1 Legacy | 8K | Simple tasks, low cost |
| `moonshot-v1-32k` | V1 Long Context | 32K | Medium-length documents |

---

## Testing & Verification

### Test via CLI

```powershell
hermes
```

Type into the interactive prompt:

```
Hello, please introduce yourself.
```

Expected response includes:
- ✅ Identifies as Hermes/Kimi
- ✅ Natural, fluent reply
- ✅ No error messages

![Hermes Agent chat interface](/screenshots/hermes-agent-chat.png)

*Figure: Hermes Agent CLI chat — streaming output with Markdown rendering*

### Test via WebUI

1. Open `http://127.0.0.1:8787`
2. Type any question
3. Verify streaming output works correctly

![Hermes WebUI chat interface](/screenshots/hermes-webui-chat.png)

*Figure: Hermes WebUI chat — three-panel layout, streaming output, syntax highlighting*

![Demo chat conversation](/screenshots/demo-chat.png)

*Figure: Kimi K2.6 live chat demo — fluent Chinese conversation with multi-turn context*

### Diagnostic Command

```powershell
hermes doctor
```

Confirm the output contains:
```
✓ Model config: OK (kimi-k2.6)
✓ API connection: OK
✓ Provider: kimi-coding
```

---

## Advanced Configuration

### Adjusting Response Parameters

```yaml
model:
  default: "kimi-k2.6"
  provider: "kimi-coding"
  base_url: "https://api.moonshot.cn/v1"
  # max_tokens: 4096         # Max output tokens per response (optional)
  # context_length: 131072   # Context window size (usually auto-detected)
```

### Configuring a Proxy (China Network)

If you cannot connect directly to the Moonshot API:

```yaml
model:
  base_url: "https://api.moonshot.cn/v1"
  # Proxy set via environment variables
```

Add to `.env`:

```bash
HTTP_PROXY=http://127.0.0.1:7890
HTTPS_PROXY=http://127.0.0.1:7890
```

### Switching to Other Cloud Providers

Hermes supports **10+ cloud providers** and you can switch anytime:

| Provider | Provider Value | Required Key | Highlights |
|----------|---------------|--------------|-----------|
| OpenRouter | `openrouter` | OPENROUTER_API_KEY | 200+ model selection |
| OpenAI | `openai-codex` | OPENAI_API_KEY | GPT series |
| Anthropic | `anthropic` | ANTHROPIC_API_KEY | Claude series |
| Google | `gemini` | GOOGLE_API_KEY | Gemini series |
| DeepSeek | `custom` | DEEPSEEK_API_KEY | High cost-performance ratio |
| Zhipu GLM | `zai` | GLM_API_KEY | Chinese domestic model |

Switch example (DeepSeek):

```yaml
model:
  default: "deepseek-chat"
  provider: "custom"
  base_url: "https://api.deepseek.com/v1"
```

---

## Cost Control

### Pricing Reference (Kimi K2.6)

| Usage Level | Approximate Cost |
|-------------|------------------|
| 1,000 daily conversations | ~¥2-5 |
| 100 code generation requests | ~¥1-3 |
| Light daily usage | < ¥1/day |
| Heavy developer usage | ~¥5-15/day |

### Money-Saving Tips

| Technique | Effect |
|-----------|--------|
| Use local models for images/files | Eliminates vision API costs |
| Compress context (`/compress`) | Reduces token count per request |
| Set reasonable max_tokens | Avoids waste from overlong replies |
| Start new sessions with `/new` | Prevents history accumulation |

---

## Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| `Invalid API Key` | Wrong or expired key | Check `KIMI_API_KEY` in `.env` |
| `Rate limit exceeded` | Too many requests | Reduce frequency or upgrade plan |
| `Connection timeout` | Network issue | Check proxy settings or connection |
| Empty response content | Model overloaded | Retry later or switch model |
| Chinese character garbling | Encoding issue | Ensure terminal uses UTF-8 encoding |

---

## Next Steps

Once the chat model is configured, continue setting up other modes as needed:

➡️ [Vision Model Configuration (GLM-4.6V)](vision-config.md) — Enable image understanding
➡️ [Speech-to-Text Configuration (Whisper)](audio-config.md) — Enable voice recognition
➡️ [Text Processing Configuration (GLM-4.6V)](text-config.md) — Enable file reading
