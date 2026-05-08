---
title: "性能问题"
lang: zh-CN
version: "1.0"
---

<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../../../en/troubleshooting/performance-issues.md">🇺🇸 English</a>
</div>

# ⚡ 性能问题

| # | 问题 | 症状 | 诊断命令 | 解决方案 |
|---|------|------|----------|----------|
| 1.1 | 响应很慢 (>10s) | 打字机效果卡顿 | `nvidia-smi` (GPU) 或任务管理器 | 使用 GPU 加速；降低模型大小 |
| 1.2 | 内存占用过高 | Windows 变慢 | `tasklist \| Sort-Object WorkingSet64 -Descending` | 关闭其他程序；使用更低量化模型 |
| 1.3 | CPU 占用 100% | 风扇狂转 | 同上 | 说明在使用 CPU 推理，安装 CUDA 加速 |
| 1.4 | 冷启动慢 | 首次请求 30s+ | 正常现象 | 模型首次加载到内存，后续请求会快很多 |
| 1.5 | 上下文过长导致慢 | 对话越聊越慢 | `/usage` 命令 | 使用 `/compress` 压缩历史或 `/new` 新建会话 |

### 性能优化速查表

| 你的情况 | 优化方案 | 预期效果 |
|----------|----------|----------|
| 有 NVIDIA GPU 但没用上 | 安装 CUDA 版 PyTorch | 速度提升 5-10x |
| 显存只有 6GB | 使用 Q4 量化模型 | 减少 50% 显存占用 |
| 内存只有 8GB | 关闭不必要的程序 | 避免 Windows 使用页面文件 |
| 对话历史太长 | `/compress` 或 `/new` | 恢复初始速度 |
