---
title: "Vision Model Configuration (GLM-4.6V-Flash)"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../../zh-CN/configuration/vision-config.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# 👁️ Vision Model Configuration (Default: GLM-4.6V-Flash)

> Enable Hermes to **see images** — screenshot analysis, image recognition, OCR text extraction

---

## Why Use a Local Vision Model?

| Aspect | Cloud API (GPT-4V) | **Local GLM-4.6V** ⭐ |
|--------|-------------------|---------------------|
| Privacy | Screenshots uploaded to server | ✅ Data never leaves your machine |
| Cost | ~¥0.1-0.5/image | **Free** |
| Latency | 2-5s (network dependent) | 3-5s (stable) |
| Offline | ❌ Requires internet | ✅ Fully offline |
| Batch processing | Pay-per-use | Unlimited |

**Ideal use cases:**
- 📸 Screenshot analysis (error messages, UI issues)
- 📊 Chart interpretation (data visualization)
- 📄 OCR text extraction (image to text)
- 🔍 Image-based Q&A

---

## Hardware Requirements

### Minimum Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| GPU | None (CPU fallback) | NVIDIA GTX 1060+ (6GB VRAM) |
| VRAM | 0 (CPU) / 4GB (GPU) | 8GB+ |
| RAM | 8GB | 16GB |
| Storage | 5GB (model files) | SSD recommended |

### GPU Support Matrix

| Graphics Card | VRAM | Recommended Quantization | Experience |
|---------------|------|---------------------------|------------|
| RTX 4090 | 24GB | FP16 | ⭐⭐⭐⭐⭐ Perfect |
| RTX 3090 | 24GB | FP16 | ⭐⭐⭐⭐⭐ Perfect |
| RTX 4070 | 12GB | Q5 | ⭐⭐⭐⭐ Smooth |
| RTX 3060 | 12GB | Q5/Q4 | ⭐⭐⭐ Usable |
| GTX 1660 | 6GB | Q4 | ⭐⭐ Adequate |
| No GPU | 0 | Q4 (CPU) | ⭐ Very slow |

---

## Installing LM Studio

LM Studio is the simplest local model inference tool for Windows.

![LM Studio loading screen](../../screenshots/lm-studio-loading.png)

*Figure: LM Studio interface — search, download, and load local AI models*

### Step 1: Download and Install

1. Visit [lmstudio.ai](https://lmstudio.ai)
2. Download the Windows version
3. Run the installer

### Step 2: Download the GLM-4.6V Model

1. Open LM Studio
2. Click the **🔍 Search icon** in the left sidebar
3. Search for `glm-4.6v-flash`
4. Select a quantization level (recommended: `Q5` or `Q4`)
5. Click **Download**

> 💡 **Recommended version**: `glm-4.6v-flash:q4_K_M` — best balance of accuracy and speed.

### Step 3: Start the Server

1. Click the **💻 Local Server** tab at the top
2. Confirm port is set to `1234` (default)
3. Click **Start Server**

Verify the service is running:

```powershell
curl http://127.0.0.1:1234/v1/models
```

Expected output contains `glm-4.6v-flash`.

---

## Configuring Hermes to Use GLM-4.6V

Edit `~/.hermes/config.yaml`:

```yaml
auxiliary:
  vision:
    provider: "lmstudio"               # LM Studio as provider
    model: "glm-4.6v-flash:q4"         # Your downloaded model name
    base_url: "http://127.0.0.1:1234/v1"
    timeout: 30                         # Image analysis timeout (seconds)
    download_timeout: 30                # Image download timeout (seconds)
```

> ⚠️ Make sure LM Studio's **Server is started**, otherwise image recognition will fail.

---

## Testing & Verification

### Test via WebUI

1. Open `http://127.0.0.1:8787`
2. Click the **📎 paperclip icon** next to the input box
3. Select an image (screenshot, photo, etc.)
4. Type: "Describe what is in this image"

Expected results:
- ✅ AI correctly describes the image content
- ✅ Recognizes any text present
- ✅ Answers questions about the image

![Vision recognition demo](../../screenshots/demo-vision.png)

*Figure: GLM-4.6V image recognition — upload a screenshot and get automatic analysis with Q&A*

### Test via CLI

```powershell
hermes
```

Send a message with an attached image and observe whether the vision model is invoked.

---

## Advanced Configuration

### Switching Quantization Levels

| Quantization | VRAM Usage | Speed | Accuracy | Best For |
|--------------|-----------|-------|----------|----------|
| FP16 | ~10GB | Medium | Highest | High-end GPUs |
| Q5 | ~6GB | Fast | 95%+ | **Default recommended** |
| Q4 | ~4GB | Very fast | 90% | Mid-range GPUs |
| Q3 | ~3GB | Fastest | 80% | Not recommended |

Simply select a different quantization version when searching in LM Studio.

### Alternative: Ollama

If you prefer Ollama:

```powershell
ollama pull glm-4.6v-flash:q4
```

```yaml
auxiliary:
  vision:
    provider: "custom"
    model: "glm-4.6v-flash:q4"
    base_url: "http://127.0.0.1:11434/v1"
```

### Switching Between Vision Models

You can switch to other vision models at any time:

| Model | Source | Notes |
|-------|--------|-------|
| `llava-v1.6` | LM Studio | Classic open-source option, large community |
| `bakllava` | LM Studio | Lightweight and fast |
| `gpt-4o-mini` | OpenAI | Cloud-based fallback |

---

## Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| No response after image upload | LM Studio not running | Launch LM Studio → Start Server |
| Inaccurate recognition results | Quantization too low | Switch to Q5 or FP16 |
| Very slow processing | Running on CPU inference | Install CUDA-enabled LM Studio |
| Out of memory (OOM) | Model too large | Use lower quantization (Q4) |
| Connection refused | Wrong port | Confirm LM Studio port is 1234 |
| Chinese text garbled | Model lacks Chinese support | GLM-4.6V natively supports Chinese; verify correct model loaded |

---

## Performance Optimization

| Technique | Effect | Difficulty |
|-----------|--------|------------|
| GPU acceleration | 5-10x speedup | ⭐ LM Studio auto-detects GPU |
| Keep model in memory | Cold start drops from 30s → 2s | ⭐ Keep LM Studio open |
| Image compression | Reduces transfer time | ⭐⭐ Pre-process images |
| Batch processing | Parallel multi-image handling | ⭐⭐⭐ Programmatic implementation |

---

## Next Steps

➡️ [Speech-to-Text Configuration (Whisper)](audio-config.md) — Enable voice recognition
➡️ [Text Processing Configuration (GLM-4.6V)](text-config.md) — Enable file reading
➡️ [Troubleshooting Guide](../troubleshooting/index.md) — Reference when issues arise
