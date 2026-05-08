---
title: "Performance Issues"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../../../zh-CN/troubleshooting/performance-issues.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# ⚡ Performance Issues

| # | Issue | Symptom | Diagnostic Command | Solution |
|---|-------|---------|--------------------|----------|
| 1.1 | Slow response (>10s) | Typewriter effect stuttering | `nvidia-smi` (GPU) or Task Manager | Enable GPU acceleration; reduce model size |
| 1.2 | High memory usage | Windows becomes sluggish | `tasklist \| Sort-Object WorkingSet64 -Descending` | Close other applications; use lower quantization model |
| 1.3 | CPU at 100% | Fans spinning at max speed | Same as above | Indicates CPU-only inference; install CUDA acceleration |
| 1.4 | Slow cold start | First request takes 30s+ | Normal behavior | Initial model load into memory; subsequent requests will be much faster |
| 1.5 | Long context causing slowdowns | Conversation gets progressively slower | `/usage` command | Use `/compress` to compress history or `/new` to start fresh session |

### Performance Optimization Quick Reference

| Your Situation | Optimization Strategy | Expected Result |
|----------------|----------------------|-----------------|
| NVIDIA GPU available but not utilized | Install CUDA-enabled PyTorch | 5-10x speed improvement |
| Only 6GB VRAM available | Use Q4 quantized model | ~50% reduction in VRAM usage |
| Only 8GB RAM available | Close unnecessary programs | Avoid Windows using page file |
| Long conversation history | `/compress` or `/new` | Restore initial response speed |
