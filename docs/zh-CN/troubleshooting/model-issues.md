---
title: "模型问题"
lang: zh-CN
version: "1.0"
---

<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../../../en/troubleshooting/model-issues.md">🇺🇸 English</a>
</div>

# 🤖 模型问题

| # | 问题 | 症状 | 诊断命令 | 解决方案 |
|---|------|------|----------|----------|
| 1.1 | Kimi API Key 无效 | `Invalid API Key` | `echo $env:KIMI_API_KEY` | 检查 `.env` 中 Key 是否正确，重新生成 |
| 1.2 | Kimi 额度用完 | `Insufficient quota` | 访问 platform.moonshot.cn | 充值或等待免费额度刷新 |
| 1.3 | 本地模型未加载 | 图片/文件处理无响应 | `curl http://127.0.0.1:1234/v1/models` | 启动 LM Studio 并加载模型 |
| 1.4 | 显存不足 (OOM) | `CUDA out of memory` | `nvidia-smi` | 使用更低量化 (Q4) 或更小模型 (base) |
| 1.5 | Whisper 首次很慢 | 卡住不动 | 任务管理器查看 CPU/内存 | 首次运行会下载模型 (~142MB)，等待完成 |
| 1.6 | 模型返回乱码 | 中文显示为问号 | 终端编码检查 | 确保终端 UTF-8: `chcp 65001` |
