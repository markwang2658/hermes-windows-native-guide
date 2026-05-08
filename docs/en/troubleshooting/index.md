---
title: "Troubleshooting Guide"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../../../zh-CN/troubleshooting/index.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# 🐛 Troubleshooting Guide

> 20+ common issues and solutions covering installation, startup, configuration, and runtime

---

## Quick Navigation

| Issue Type | Jump To |
|------------|---------|
| Installation failures | [Installation Issues](installation-issues.md) |
| Startup failures | [Startup Issues](startup-issues.md) |
| Connection / Network issues | [Connection & Network Issues](connection-issues.md) |
| Model / API issues | [Model & API Issues](model-issues.md) |
| Feature malfunctions | [Feature Issues](feature-issues.md) |
| Performance problems | [Performance Issues](performance-issues.md) |
| Windows-specific issues | [Windows-Specific Issues](windows-issues.md) |

---

## Diagnostic Toolkit

### hermes doctor

```powershell
hermes doctor
```

The most commonly used diagnostic command — performs a comprehensive check of all critical items in one pass.

### Health Check List

```powershell
# 1. Python environment
python --version                    # >= 3.10

# 2. Dependency integrity
pip check                            # Should produce no output (no conflicts)

# 3. Agent availability
hermes --version                     # Should output version number

# 4. WebUI availability
curl http://127.0.0.1:8787/health   # Should return {"status": "ok"}
Test-Path "$env:USERPROFILE\.hermes\webui-mvp"    # WebUI state directory exists

# 5. Configuration files
Test-Path "$env:USERPROFILE\.hermes\config.yaml"    # True
Test-Path "$env:USERPROFILE\.hermes\.env"            # True

# 6. LM Studio (if using local models)
Invoke-RestMethod http://127.0.0.1:1234/v1/models    # Should return model list

# 7. Port occupation
netstat -ano | findstr ":8787"       # python.exe should be listening

# 8. Log inspection
Get-Content "$env:USERPROFILE\.hermes\logs\errors.log" -Tail 20  # Recent errors
```

### Log Locations

| Log | Path | Purpose |
|-----|------|---------|
| Agent log | `~/.hermes/logs/agent.log` | Runtime information |
| Error log | `~/.hermes/logs/errors.log` | Exception stack traces |
| Gateway log | `~/.hermes/logs/gateway.log` | Web service logs |

---

## Getting Help

If none of the solutions above resolve your issue:

| Channel | When to Use |
|---------|-------------|
| 🐛 [GitHub Issues](https://github.com/markwang2658/hermes-windows-native/issues) | Bug reports, feature requests |
| 💬 [GitHub Discussions](https://github.com/markwang2658/hermes-windows-native/discussions) | Usage questions, experience sharing |
| 🧠 [Upstream Agent Issues](https://github.com/NousResearch/hermes-agent/issues) | Core component bugs |
| 🌐 [Upstream WebUI Issues](https://github.com/nesquena/hermes-webui/issues) | Web interface bugs |

### Please Include When Submitting an Issue

- [ ] Windows version (`winver`)
- [ ] Python version (`python --version`)
- [ ] Full error message (do not truncate)
- [ ] Reproduction steps (minimal reproducible case)
- [ ] Output of `hermes doctor`
- [ ] Relevant log excerpts (sanitized)

---

## Common Error Codes Quick Reference

| Error Message | Meaning | Quick Fix |
|---------------|---------|-----------|
| `EADDRINUSE` | Port already in use | Change port or kill process |
| `ECONNREFUSED` | Service not started | Start the corresponding service |
| `ETIMEDOUT` | Connection timed out | Check network / proxy settings |
| `ENOENT` | File not found | Check path spelling |
| `EACCES` | Insufficient permissions | Run as Administrator or check permissions |
| `OOM` / `CUDA OOM` | Insufficient GPU memory | Lower quantization or use smaller model |
| `401 Unauthorized` | Invalid API Key | Check / update key |
| `429 Too Many Requests` | Rate limit exceeded | Reduce frequency or upgrade plan |
| `500 Internal Server Error` | Server-side error | Retry later or report bug |
