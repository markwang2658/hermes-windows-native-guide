---
title: "启动问题"
lang: zh-CN
version: "1.0"
---

<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../../../en/troubleshooting/startup-issues.md">🇺🇸 English</a>
</div>

# 🚀 启动问题

| # | 问题 | 症状 | 诊断命令 | 解决方案 |
|---|------|------|----------|----------|
| 1.1 | 端口被占用 | `Address already in use` | `netstat -ano \| findstr :8787` | 修改端口: `HERMES_WEBUI_PORT=8788` 或杀进程: `taskkill /PID <pid> /F` |
| 1.2 | Agent 目录未找到 | `Agent directory not found` | `Test-Path D:\hermes-windows-native\hermes-agent` | 检查 `.env` 中 `HERMES_WEBUI_AGENT_DIR` 路径是否正确 |
| 1.3 | Python 路径错误 | `Python executable not found` | `Test-Path .\.venv\Scripts\python.exe` | 设置 `HERMES_WEBUI_PYTHON` 为正确路径 |
| 1.4 | WebUI 白屏 | 页面空白无内容 | 浏览器 F12 → Console | 检查 Console 报错，通常是 Agent 路径问题 |
| 1.5 | 启动后立即退出 | 进程闪退 | 手动运行 `.\start.ps1` | 查看 PowerShell 输出的错误信息 |
| 1.6 | 缺少依赖包 | `ImportError: No module named xxx` | `pip list \| Select-String "xxx"` | 安装缺失依赖: `pip install xxx` |
