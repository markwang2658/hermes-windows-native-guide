---
title: "Four-Mode Input Routing Architecture"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../../zh-CN/architecture/trimode-routing.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# 🏗️ Four-Mode Input Routing Architecture

> Understand how Hermes automatically selects the best AI model based on **input type**

---

## 1. Architecture Overview

![Four-Mode Routing Architecture](../../screenshots/architecture-en.png)

*Figure: Hermes four-mode automatic routing architecture — selects AI model based on input type*

```
┌─────────────────────────────────────────────────────────────┐
│                    WebUI / CLI Input                          │
│                  (User sends message/file)                    │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
        ┌──────────────┴──────────────┐
        │   Input Type Auto-Detection │
        │ (File extension / Content)  │
        └───┬──────┬──────┬──────┬────┘
            │      │      │      │
     ┌──────┘      │      │      └──────┐
     ▼             ▼      ▼             ▼
┌─────────┐  ┌─────────┐┌─────────┐ ┌─────────┐
│  Chat   │  │ Vision  ││ Audio   │ │  Text   │
│ Default │  │ Image   ││ Speech  │ │ File    │
├─────────┤  ├─────────┤├─────────┤ ├─────────┤
│Kimi K2.6│  │GLM-4.6V ││Whisper  │ │GLM-4.6V │
│  Cloud  │  │  Local  ││  Local  │ │  Local  │
│  ~2s    │  │  ~3-5s  ││  ~1-3s  │ │  ~2-4s  │
│   $     │  │  Free   ││  Free   │ │  Free   │
│  ☁️     │  │  🔒     ││  🔒     │ │  🔒     │
└─────────┘  └─────────┘└─────────┘ └─────────┘
```

---

## 2. Four Modes Explained

### 2.1 Chat Mode (Default Dialog)

| Attribute | Value |
|-----------|-------|
| **Trigger** | Plain text message, no attachments |
| **Default Model** | Kimi K2.6 (Cloud) |
| **Response Time** | ~2 seconds |
| **Cost** | Per-token billing |
| **Use Cases** | Daily conversation, coding, Q&A |

**Why does chat use cloud?**
- Kimi K2.6 is one of the strongest Chinese language models available
- Cloud inference offers fast response and strong capabilities
- Cost is predictable and affordable for typical usage

```yaml
# cli-config.yaml core configuration
model:
  default: "kimi-k2.6"           # or kimi-k2.0711-preview
  provider: "kimi-coding"         # Moonshot AI provider
  base_url: "https://api.moonshot.cn/v1"
```

---

### 2.2 Vision Mode (Image Recognition)

| Attribute | Value |
|-----------|-------|
| **Trigger** | Upload image file (.png, .jpg, .jpeg, .gif, .webp) |
| **Default Model** | GLM-4.6V-Flash (Local) |
| **Runtime** | LM Studio / Ollama |
| **Response Time** | 3-5 seconds (GPU-dependent) |
| **Cost** | Free (local inference) |
| **Privacy** | ✅ Data never leaves your machine |

**Why do images run locally?**
- Privacy protection: Screenshots may contain sensitive information
- Zero cost: No per-image API fees
- No network dependency: Works offline
- Unlimited batch processing: No rate limits

```yaml
# cli-config.yaml vision auxiliary model config
auxiliary:
  vision:
    provider: "lmstudio"           # or "custom"
    model: "glm-4.6v-flash:q4"     # Quantized version saves VRAM
    base_url: "http://127.0.0.1:1234/v1"  # LM Studio default port
    timeout: 30                    # Image analysis timeout (seconds)
```

---

### 2.3 Audio Mode (Speech-to-Text)

| Attribute | Value |
|-----------|-------|
| **Trigger** | Upload audio file (.mp3, .wav, .m4a, .ogg) |
| **Default Model** | faster-whisper (Local) |
| **Runtime** | Python local + GPU acceleration (optional) |
| **Response Time** | 1-3s (short audio) / 10-30s (long audio) |
| **Cost** | Free |
| **Privacy** | ✅ Voice data stays on your machine |

**Supported Audio Formats & Languages:**

| Format | Supported | Notes |
|--------|-----------|-------|
| MP3 | ✅ | Most common format |
| WAV | ✅ | Lossless, but larger files |
| M4A | ✅ | Apple device recordings |
| OGG | ✅ | Open source format |

```yaml
# cli-config.yaml speech-to-text config
stt:
  enabled: true
  local:
    model: "base"                 # tiny/base/small/medium/large-v3/turbo
    # model: "small"              # Recommended: speed vs accuracy balance
    # language: ""                # Optional: force language (default auto-detect)
```

**Model Selection Guide:**

| Model | VRAM Usage | Speed | Accuracy | Recommended For |
|------|-----------|-------|----------|----------------|
| `tiny` | ~1GB | ⚡⚡⚡ | ★☆☆ | Quick testing |
| `base` | ~2GB | ⚡⚡ | ★★☆ | **Daily use** ✓ |
| `small` | ~3GB | ⚡ | ★★★ | High accuracy needs |
| `medium` | ~5GB | 🐢 | ★★☆ | Not recommended (poor value) |
| `large-v3` | ~10GB | 🐢🐢 | ★★★★ | Maximum accuracy |

---

### 2.4 Text Mode (File Processing)

| Attribute | Value |
|-----------|-------|
| **Trigger** | Upload text file (.md, .py, .js, .txt, .json, .yaml, etc.) |
| **Default Model** | GLM-4.6V-Flash (Local) |
| **Runtime** | LM Studio / Ollama |
| **Response Time** | 2-4 seconds (depends on file size) |
| **Cost** | Free |
| **Privacy** | ✅ Code/documents stay local |

**Typical Use Cases:**

| File Type | Use Case | Example |
|-----------|----------|---------|
| `.md` | Document summarization, Q&A | README analysis |
| `.py/.js` | Code explanation, bug diagnosis | Function logic walkthrough |
| `.json/.yaml` | Config file interpretation | config.yaml explanation |
| `.txt` | Log analysis, text summary | Error log troubleshooting |

```yaml
# cli-config.yaml text processing via auxiliary.web_extract or main model
auxiliary:
  web_extract:
    provider: "lmstudio"           # Reuse local model
    model: "glm-4.6v-flash:q4"
    base_url: "http://127.0.0.1:1234/v1"
```

---

## 3. Mode Comparison Summary

| Dimension | Chat (Cloud) | Vision (Local) | Audio (Local) | Text (Local) |
|-----------|-------------|---------------|--------------|-------------|
| **Model** | Kimi K2.6 | GLM-4.6V | Whisper | GLM-4.6V |
| **Location** | ☁️ Cloud | 🔒 Local | 🔒 Local | 🔒 Local |
| **Latency** | ~2s | 3-5s | 1-30s | 2-4s |
| **Cost** | $ | Free | Free | Free |
| **Privacy** | Medium | High | High | High |
| **Offline** | ❌ | ✅ | ✅ | ✅ |
| **GPU Required** | No | Recommended | Optional | Recommended |
| **VRAM Needed** | 0 | 4-8GB | 2-8GB | 4-8GB |

---

## 4. Technical Decision Rationale

### Why Hybrid Cloud + Local Architecture?

```
Traditional Approach (All Cloud):
  User → Cloud API → Result
  Issues: Privacy risk, cost accumulation, network dependency

Traditional Approach (All Local):
  User → Local Model → Result
  Issues: Requires GPU, limited model capabilities, slow cold start

Hermes Approach (Hybrid Smart Routing):
  Text → Kimi K2.6 (Cloud - Strong Model)
  Images → GLM-4.6V (Local - Privacy Protection)
  Audio → Whisper (Local - Zero Cost)
  Files → GLM-4.6V (Local - Security)

  Benefits: Balances capability, cost, and privacy
```

### Windows-Specific Handling

| Issue | Solution | Notes |
|-------|----------|-------|
| WinError 5 Permission Error | Auto-retry mechanism | Waits and retries on file lock conflicts |
| CUDA DLL Version Mismatch | Auto-downgrade | cublas64_13 → cublas64_12 |
| Path Separator | Unified conversion | `/` → `\` auto-handled |
| Long Path Limit (>260 chars) | Enable long path support | `\\?\` prefix |

---

## 5. Data Flow Deep Dive

```
User Action Example: Send a screenshot + text description

Step 1: WebUI Receives Input
  ├── Detects image attachment → Marks as Vision mode
  └── Detects text content → Passes as context

Step 2: Agent Routing Decision
  ├── auxiliary.vision.provider = "lmstudio"
  ├── Calls http://127.0.0.1:1234/v1/chat/completions
  └── Model: glm-4.6v-flash:q4

Step 3: Local Model Inference (LM Studio)
  ├── Loads model into GPU VRAM
  ├── Executes visual understanding task
  └── Returns recognition result

Step 4: Agent Assembles Response
  ├── Combines image recognition result
  ├── Combines user's text question
  └── Generates final response (may call main model for polish)
```

---

## 6. Performance Tuning Recommendations

### 6.1 Reduce VRAM Usage

```yaml
# Use quantized models (Q4/Q5 vs FP16)
model: "glm-4.6v-flash:q4"    # 4-bit quantization, saves VRAM
```

| Quantization Level | VRAM Usage | Accuracy Loss | Recommendation |
|--------------------|-----------|---------------|----------------|
| FP16 (no quantization) | 100% | 0% | GPU ≥ 12GB |
| Q5 | ~60% | < 2% | ⭐⭐⭐ **Recommended** |
| Q4 | ~45% | 3-5% | ⭐⭐ GPU ≤ 8GB |
| Q3 | ~35% | > 10% | ❌ Not recommended |

### 6.2 Improve Response Speed

| Method | Effect | Use Case |
|--------|--------|----------|
| Keep model in memory | Cold start from 30s → 2s | Frequent local model usage |
| GPU acceleration (CUDA) | 5-10x speedup | Have NVIDIA GPU |
| Batch processing | Parallel multi-file | Bulk analysis scenarios |

---

## 7. Common Questions

| Question | Cause | Solution |
|----------|-------|----------|
| No response after image upload | LM Studio not started or wrong port | Check if `http://127.0.0.1:1234` is accessible |
| Speech transcription error | faster-whisper not installed | `pip install faster-whisper` |
| Local model is very slow | Using CPU instead of GPU | Install CUDA version of PyTorch |
| Model switch not taking effect | Cache issue | Restart Agent or clear session |

> For more troubleshooting, see [Troubleshooting Guide](../troubleshooting/index.md)
