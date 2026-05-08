---
title: "Speech-to-Text Configuration (faster-whisper)"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../../zh-CN/configuration/audio-config.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# 🎤 Speech-to-Text Configuration (Default: faster-whisper)

> Enable Hermes to **understand voice** — automatically transcribe voice messages into text

---

## Why Use Local Speech-to-Text?

| Aspect | Cloud API (Whisper API) | **Local faster-whisper** ⭐ |
|--------|------------------------|---------------------------|
| Privacy | Audio uploaded to server | ✅ Data never leaves your machine |
| Cost | ~$0.006/minute | **Free** |
| Latency | 2-5s | 1-3s (short audio) |
| Offline | ❌ Requires internet | ✅ Fully offline |
| Language Support | 99 languages | 99 languages |

**Ideal use cases:**
- 🎙️ Voice message transcription
- 📝 Meeting recording summarization
- 🎵 Audio content summarization
- 🌐 Multilingual audio translation

---

## Hardware Requirements

| Requirement | CPU Mode | GPU Mode (CUDA) |
|-------------|----------|-----------------|
| Minimum RAM | 4GB | 8GB |
| Recommended RAM | 8GB | 16GB |
| GPU | Not required | NVIDIA GPU (VRAM >= 4GB) |
| Processing speed (1 min audio) | ~30-60s | ~3-10s |

---

## Installing faster-whisper

### Step 1: Activate the Virtual Environment

```powershell
cd D:\hermes-windows-native\hermes-agent
.\.venv\Scripts\Activate.ps1
```

### Step 2: Install faster-whisper

```powershell
pip install faster-whisper
```

> 💡 If network is slow, use a mirror:
> ```powershell
> pip install faster-whisper -i https://pypi.tuna.tsinghua.edu.cn/simple
> ```

### Step 3: Verify Installation

```powershell
python -c "from faster_whisper import WhisperModel; print('OK')"
```

Outputting `OK` confirms successful installation.

---

## Configuring Hermes

Edit `~/.hermes/config.yaml`:

```yaml
stt:
  enabled: true                          # Enable speech-to-text
  local:
    model: "base"                        # Model size
    # language: ""                       # Leave blank = auto-detect language
    # device: "cuda"                     # Optional: cuda / cpu / auto
    # compute_type: "int8"               # Optional: int8 / float16 / float32
```

### Model Selection Guide

| Model | Size | VRAM Needed | Speed (GPU) | Accuracy | **Recommended For** |
|-------|------|-------------|-------------|----------|--------------------|
| `tiny` | 75MB | ~1GB | ⚡⚡⚡ | ★☆☆ | Quick testing |
| `base` | 142MB | ~2GB | ⚡⚡ | ★★☆ | **Daily use recommended** ✓ |
| `small` | 466MB | ~3GB | ⚡ | ★★★ | High accuracy needs |
| `medium` | 1.5GB | ~5GB | 🐢 | ★★☆ | Not recommended |
| `large-v3` | 3GB | ~10GB | 🐢🐢 | ★★★★ | Maximum accuracy |

> 💡 **Beginner tip**: Start with `base` — it offers the best balance of speed and accuracy.

---

## Testing & Verification

### Direct Python Test

```powershell
python -c "
from faster_whisper import WhisperModel
model = WhisperModel('base', device='cpu', compute_type='int8')
segments, info = model.transcribe('test.mp3')
for seg in segments:
    print(f'[{seg.start:.1f}s -> {seg.end:.1f}s] {seg.text}')
"
```

### Test via WebUI

1. Open `http://127.0.0.1:8787`
2. Click the **🎤 microphone icon** next to the input box to record
   - Or click **📎** to upload an `.mp3/.wav` file
3. Send the message

Expected results:
- ✅ Voice is automatically transcribed to text
- ✅ AI responds based on the transcribed content

![Audio transcription demo](../../screenshots/demo-audio.png)

*Figure: faster-whisper transcription — audio files are automatically converted to text with intelligent responses*

### Supported Audio Formats

| Format | Extension | Supported |
|--------|-----------|-----------|
| MP3 | `.mp3` | ✅ Recommended |
| WAV | `.wav` | ✅ Lossless |
| M4A | `.m4a` | ✅ Apple recordings |
| OGG | `.ogg` | ✅ |
| FLAC | `.flac` | ✅ |
| WebM | `.webm` | ✅ |

---

## Advanced Configuration

### GPU Acceleration (Strongly Recommended)

If you have an NVIDIA graphics card:

```yaml
stt:
  enabled: true
  local:
    model: "base"
    device: "cuda"                      # Use GPU
    compute_type: "float16"             # float16 recommended for GPU
```

**Speed comparison** (1 minute audio):

| Device | Time (base model) |
|--------|-------------------|
| CPU (i7) | ~40-60 seconds |
| GPU (GTX 1060) | ~5-8 seconds |
| GPU (RTX 3090) | ~2-3 seconds |
| GPU (RTX 4090) | ~1-2 seconds |

### Specifying Language

If you know the audio language in advance, specifying it improves accuracy:

```yaml
stt:
  local:
    model: "base"
    language: "zh"                     # Force Chinese
    # language: "en"                   # Force English
    # language: "ja"                   # Force Japanese
```

Supported language codes: `zh`(Chinese), `en`(English), `ja`(Japanese), `ko`(Korean), `fr`(French), `de`(German), and 99 more.

### Performance vs. Accuracy Trade-off

```yaml
stt:
  local:
    model: "small"                     # Higher accuracy
    device: "cuda"
    compute_type: "int8"               # Lower VRAM usage
```

| compute_type | VRAM Usage | Speed | Accuracy Impact |
|--------------|-----------|-------|-----------------|
| `float32` | Highest | Slowest | Baseline |
| `float16` | Half | Fast | Nearly lossless |
| `int8` | Lowest | Fastest | Slight degradation |

---

## Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| `ModuleNotFoundError` | faster-whisper not installed | `pip install faster-whisper` |
| Empty transcription result | Unsupported audio format | Convert to MP3/WAV |
| Very slow processing | CPU inference | Set `device: "cuda"` |
| CUDA error | CUDA PyTorch not installed | `pip install torch torchvision --index-url https://download.pytorch.org/whl/cu121` |
| Chinese garbled text | Encoding issue | Ensure terminal uses UTF-8 encoding |
| Out of memory (OOM) | Model too large | Use `base` or `tiny` model |
| Slow first run | Downloading model files | First run auto-downloads (~142MB for base), then caches locally |

---

## Local vs. Cloud Speech-to-Text

| Scenario | Recommended | Reason |
|----------|-------------|--------|
| Daily use | Local faster-whisper | Free, private, fast |
| Long audio (>1h) | Local | No duration limits |
| Real-time transcription | Local | Low latency |
| Maximum accuracy needed | Cloud Whisper API | large-v3 model is stronger |
| Old PC without GPU | Cloud | Avoid slow CPU processing |

---

## Next Steps

➡️ [Text Processing Configuration (GLM-4.6V)](text-config.md) — Enable file reading
➡️ [Four-Mode Routing Architecture](../architecture/trimode-routing.md) — Understand the overall system design
➡️ [Troubleshooting Guide](../troubleshooting/index.md) — Reference when issues arise
