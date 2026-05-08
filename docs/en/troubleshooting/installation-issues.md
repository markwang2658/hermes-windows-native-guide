---
title: "Installation Issues"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../../../zh-CN/troubleshooting/installation-issues.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# 🔧 Installation Issues

| # | Issue | Symptom | Diagnostic Command | Solution |
|---|-------|---------|--------------------|----------|
| 1.1 | Python not found | `'python' is not recognized` | `$env:PATH -split ";" \| Select-String "Python"` | Check **"Add to PATH"** during Python installation, or add it manually |
| 1.2 | pip timeout | `Read timed out` | `pip config list` | Use mirror source: `pip install xxx -i https://pypi.tuna.tsinghua.edu.cn/simple` |
| 1.3 | Permission error | `cannot run scripts` | `$env:ExecutionPolicy` | Run: `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` |
| 1.4 | Git clone failure | `Connection timed out` | `git config --global http.proxy` | Configure proxy: `git config --global http.proxy http://127.0.0.1:10808` |
| 1.5 | venv creation failed | `Error [Errno 2]` | `python --version` | Ensure Python 3.10+ and path contains no Chinese characters or spaces |
| 1.6 | Dependency conflict | `ModuleNotFoundError` | `pip list` | Delete and recreate: `Remove-Item .venv -Recurse; python -m venv .venv` |
| 1.7 | Insufficient disk space | `No space left on device` | `psdrive C \| Select-Object Free` | Clean up C drive, ensure >= 2GB free space available |
