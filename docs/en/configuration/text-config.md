---
title: "Text Processing Configuration (GLM-4.6V-Flash)"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../../zh-CN/configuration/text-config.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# 📄 Text Processing Configuration (Default: GLM-4.6V-Flash)

> Enable Hermes to **read files** — code explanation, document summarization, log analysis

---

## Why Use a Local Model for Text Processing?

| Aspect | Cloud API (Claude/GPT) | **Local GLM-4.6V** ⭐ |
|--------|----------------------|---------------------|
| Privacy | Code/docs uploaded to server | ✅ Data never leaves your machine |
| Cost | Billed per token | **Free** |
| File size limit | Usually < 10MB | No limit |
| Offline | ❌ Requires internet | ✅ Fully offline |
| Batch processing | Pay-per-use | Unlimited |

**Ideal use cases:**
- 📝 README / document summarization
- 🔍 Code logic explanation
- 🐛 Error log analysis
- 📊 Configuration file interpretation
- 📋 Long-form text summarization

---

## Prerequisites

Text processing **reuses the vision model** (GLM-4.6V), so you must first complete:

1. ✅ [Install LM Studio](vision-config.md#installing-lm-studio)
2. ✅ [Download the GLM-4.6V model](vision-config.md#step-2-download-the-glm-46v-model)
3. ✅ [Start LM Studio Server](vision-config.md#step-3-start-the-server)

![LM Studio loading screen](../../screenshots/lm-studio-loading.png)

*Figure: LM Studio interface — Text mode shares the same GLM-4.6V instance with Vision mode*

---

## Configuration

Edit `~/.hermes/config.yaml`:

```yaml
auxiliary:
  web_extract:
    provider: "lmstudio"               # Reuse LM Studio
    model: "glm-4.6v-flash:q4"         # Same as vision model
    base_url: "http://127.0.0.1:1234/v1"
    timeout: 30                         # Processing timeout (seconds)
```

> 💡 If you have already [configured the vision model](vision-config.md), **no need to re-download the model** — just reuse the same instance.

---

## Supported File Types

### Automatically Recognized File Types

| Type | Extensions | Processing Method |
|------|-----------|-------------------|
| Markdown | `.md` | Content summary, Q&A |
| Python | `.py` | Code explanation, bug diagnosis |
| JavaScript | `.js/.ts/.jsx/.tsx` | Code explanation |
| JSON/YAML | `.json/.yaml/.yml` | Structured interpretation |
| Plain text | `.txt/.log/.csv` | Content analysis |
| Shell scripts | `.ps1/.sh/.bat` | Command explanation |
| Config files | `.ini/.toml/.conf` | Configuration description |

### How to Use

#### In WebUI:

1. Click the **📎 paperclip icon** next to the input box
2. Select files (multi-select supported)
3. Type your question, for example:
   - "Summarize the contents of this file."
   - "What does this code do?"
   - "Find all errors in this log."

#### In CLI:

```powershell
hermes
# Then paste the file path or drag-and-drop the file into the terminal
```

---

## Typical Use Cases

### Scenario 1: README Summary

**Action**: Upload `README.md`, ask: "What does this project do?"

**Expected output**:
```
This is an AI Agent project (Hermes). Key features include:
1. Persistent memory — remembers context across sessions
2. Multi-model support — OpenAI/Anthropic/local models
3. Tool calling — terminal/browser/file operations
4. Scheduled tasks — Cron-based automation
```

![File summarization demo](../../screenshots/demo-text.png)

*Figure: GLM-4.6V text processing — automatic file summarization and Q&A after upload*

### Scenario 2: Code Explanation

**Action**: Upload `utils.py`, ask: "What is the logic of this function?"

**Expected output**: Line-by-line function-level explanation including:
- Input parameter descriptions
- Execution flow diagram
- Return value meanings
- Potential edge cases

### Scenario 3: Error Log Analysis

**Action**: Upload `error.log`, ask: "Find all errors and provide solutions."

**Expected output**:
```
3 errors found:

❌ Error 1 (Line 23): ConnectionRefusedError
   Cause: Port 8787 is already in use
   Fix: Change port or kill the occupying process

⚠️ Warning 2 (Line 56): DeprecationWarning
   Cause: Deprecated API in use
   Fix: Update to the new API version

💡 Note: The configuration at line 89 may cause performance issues...
```

---

## Advanced Tips

### Batch File Processing

Upload multiple files for comparative analysis at once:

```
Upload: config.yaml, config.prod.yaml, config.dev.md
Question: What are the differences between these three configuration files?
```

### Combining Images and Files

Upload a screenshot alongside source code simultaneously:

```
Upload: error-screenshot.png, main.py
Question: Which line of code corresponds to the error in the screenshot? How do I fix it?
```

### Handling Large Files

For very large files (>10MB):

| Method | Action |
|--------|--------|
| Split upload | Break the file into smaller chunks |
| Summarize first | Ask AI to summarize key sections first |
| Specify line range | Ask: "Analyze only the first 100 lines" |

---

## Troubleshooting

| Problem | Cause | Solution |
|---------|-------|----------|
| No response after file upload | LM Studio not running | Launch LM Studio → Start Server |
| Shows filename but no content | Unsupported format | Convert to `.txt` or `.md` and retry |
| Inaccurate analysis results | Insufficient context window | Reduce file size or process in batches |
| Chinese file garbled text | Encoding issue | Ensure UTF-8 encoding |
| Processing timeout | File too large | Reduce file size or increase timeout value |
| Cannot read binary files | Format not supported | Binary files (.exe/.dll/.pdf etc.) must be converted first |

---

## Relationship With Other Modes

```
User input routing logic:

Plain text message → Chat mode (Kimi K2.6 cloud)
     │
     ├── Contains image → Vision mode (GLM-4.6V local)
     ├── Contains audio → Audio mode (Whisper local)
     └── Contains file → Text mode (GLM-4.6V local) ← This document
```

> **Note**: Text mode and Vision mode share the same GLM-4.6V instance — no additional resources required.

---

## Next Steps

All four modes are now fully configured!

| Mode | Status | Documentation |
|------|--------|---------------|
| 💬 Chat (Kimi K2.6) | ☑️ Configured | [Chat Config](chat-config.md) |
| 👁️ Vision (GLM-4.6V) | ☑️ Configured | [Vision Config](vision-config.md) |
| 🎤 Audio (Whisper) | ☑️ Configured | [Audio Config](audio-config.md) |
| 📄 Text (GLM-4.6V) | ☑️ Configured | **This document** |

➡️ [Troubleshooting Guide](../troubleshooting/index.md) — Reference when issues arise
➡️ [Architecture Design](../architecture/trimode-routing.md) — Deep dive into system architecture
