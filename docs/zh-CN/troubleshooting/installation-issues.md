---
title: "安装问题"
lang: zh-CN
version: "1.0"
---

<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../../../en/troubleshooting/installation-issues.md">🇺🇸 English</a>
</div>

# 🔧 安装问题

| # | 问题 | 症状 | 诊断命令 | 解决方案 |
|---|------|------|----------|----------|
| 1.1 | Python 找不到 | `'python' 不是内部命令` | `$env:PATH -split ";" \| Select-String "Python"` | 安装 Python 时勾选 "Add to PATH"，或手动添加 |
| 1.2 | pip 超时 | `Read timed out` | `pip config list` | 使用镜像源: `pip install xxx -i https://pypi.tuna.tsinghua.edu.cn/simple` |
| 1.3 | 权限错误 | `cannot run scripts` | `$env:ExecutionPolicy` | 执行: `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` |
| 1.4 | Git 克隆失败 | `Connection timed out` | `git config --global http.proxy` | 配置代理: `git config --global http.proxy http://127.0.0.1:10808` |
| 1.5 | venv 创建失败 | `Error [Errno 2]` | `python --version` | 确保 Python 3.10+，且路径无中文/空格 |
| 1.6 | 依赖冲突 | `ModuleNotFoundError` | `pip list` | 删除重建: `Remove-Item .venv -Recurse; python -m venv .venv` |
| 1.7 | 磁盘空间不足 | `No space left on device` | `psdrive C \| Select-Object Free` | 清理 C 盘，确保 ≥ 2GB 可用 |
