---
title: "功能问题"
lang: zh-CN
version: "1.0"
---

<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../../../en/troubleshooting/feature-issues.md">🇺🇸 English</a>
</div>

# ⚙️ 功能问题

| # | 问题 | 症状 | 诊断命令 | 解决方案 |
|---|------|------|----------|----------|
| 1.1 | 图片上传无效 | 发送后无反应 | 浏览器 F12 → Network | 检查 LM Studio 是否运行在 1234 端口 |
| 1.2 | 语音转写失败 | 上传音频后报错 | `python -c "from faster_whisper import..."` | 安装 faster-whisper: `pip install faster-whisper` |
| 1.3 | 文件内容不显示 | 只显示文件名 | 尝试上传 .txt 文件 | 某些二进制文件不支持，转换为文本格式 |
| 1.4 | 会话数据丢失 | 刷新页面后历史消失 | 检查 `~/.hermes/webui-mvp/` | 确认状态目录存在且有写入权限 |
| 1.5 | 工具调用失败 | AI 无法执行命令 | `hermes doctor` | 检查工具权限和配置 |
| 1.6 | 记忆功能不工作 | AI 不记得之前对话 | 检查 `~/.hermes/memory/` | 确认 memory 目录存在 |
