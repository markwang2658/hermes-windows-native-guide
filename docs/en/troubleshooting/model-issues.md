---
title: "Model & API Issues"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../../../zh-CN/troubleshooting/model-issues.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# 🤖 Model & API Issues

| # | Issue | Symptom | Diagnostic Command | Solution |
|---|-------|---------|--------------------|----------|
| 1.1 | Invalid Kimi API Key | `Invalid API Key` | `echo $env:KIMI_API_KEY` | Verify key in `.env` is correct; regenerate if necessary |
| 1.2 | Kimi quota exhausted | `Insufficient quota` | Visit platform.moonshot.cn | Top up balance or wait for free tier refresh |
| 1.3 | Local model not loaded | Image / file processing unresponsive | `curl http://127.0.0.1:1234/v1/models` | Launch LM Studio and load a model |
| 1.4 | GPU out of memory (OOM) | `CUDA out of memory` | `nvidia-smi` | Use lower quantization (Q4) or a smaller model (base variant) |
| 1.5 | Whisper slow on first run | Appears stuck / frozen | Check Task Manager CPU/Memory usage | First run downloads the model (~142MB); wait for completion |
| 1.6 | Garbled model output | Chinese text displays as question marks | Check terminal encoding | Ensure terminal is UTF-8: `chcp 65001` |
