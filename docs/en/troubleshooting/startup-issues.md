---
title: "Startup Issues"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../../../zh-CN/troubleshooting/startup-issues.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# 🚀 Startup Issues

| # | Issue | Symptom | Diagnostic Command | Solution |
|---|-------|---------|--------------------|----------|
| 1.1 | Port already in use | `Address already in use` | `netstat -ano \| findstr :8787` | Change port: `HERMES_WEBUI_PORT=8788` or kill process: `taskkill /PID <pid> /F` |
| 1.2 | Agent directory not found | `Agent directory not found` | `Test-Path D:\hermes-windows-native\hermes-agent` | Verify `HERMES_WEBUI_AGENT_DIR` path in `.env` is correct |
| 1.3 | Python path incorrect | `Python executable not found` | `Test-Path .\.venv\Scripts\python.exe` | Set `HERMES_WEBUI_PYTHON` to the correct path |
| 1.4 | WebUI blank page | Page loads empty with no content | Browser F12 -> Console | Check Console for errors; usually an Agent path issue |
| 1.5 | Exits immediately after startup | Process flashes and closes | Manually run `.\start.ps1` | Review error messages in PowerShell output |
| 1.6 | Missing dependencies | `ImportError: No module named xxx` | `pip list \| Select-String "xxx"` | Install missing dependency: `pip install xxx` |
