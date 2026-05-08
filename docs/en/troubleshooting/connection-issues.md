---
title: "Connection & Network Issues"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../../../zh-CN/troubleshooting/connection-issues.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# 🌐 Connection & Network Issues

| # | Issue | Symptom | Diagnostic Command | Solution |
|---|-------|---------|--------------------|----------|
| 1.1 | Cannot access GitHub | `git clone` times out | `git ls-remote https://github.com` | Set up proxy: see Git proxy configuration below |
| 1.2 | API connection timeout | `Connection timeout` | `curl https://api.moonshot.cn/v1/models` | Check network / proxy settings |
| 1.3 | LM Studio connection failed | `Connection refused` | `curl http://127.0.0.1:1234/v1/models` | Launch LM Studio and click **Start Server** |
| 1.4 | Proxy settings ineffective | Still timing out | `git config --get http.proxy` | Confirm proxy software is running and port is correct |

### Complete Git Proxy Configuration

```powershell
# Set proxy (applies to current repository only)
cd D:\hermes-windows-native\hermes-agent
git config http.proxy http://127.0.0.1:10808
git config https.proxy http://127.0.0.1:10808

# Verify
git config --get http.proxy
# Expected output: http://127.0.0.1:10808

# Test connection
git ls-remote --heads https://github.com/markwang2658/hermes-windows-native-guide.git
# Should return refs/heads/main

# Remove proxy (if needed)
git config --unset http.proxy
git config --unset https.proxy
```
