---
title: "连接问题"
lang: zh-CN
version: "1.0"
---

<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../../../en/troubleshooting/connection-issues.md">🇺🇸 English</a>
</div>

# 🌐 连接问题

| # | 问题 | 症状 | 诊断命令 | 解决方案 |
|---|------|------|----------|----------|
| 1.1 | 无法访问 GitHub | `git clone` 超时 | `git ls-remote https://github.com` | 设置代理: 见下方代理配置 |
| 1.2 | API 连接超时 | `Connection timeout` | `curl https://api.moonshot.cn/v1/models` | 检查网络/代理设置 |
| 1.3 | LM Studio 连接失败 | `Connection refused` | `curl http://127.0.0.1:1234/v1/models` | 启动 LM Studio → Start Server |
| 1.4 | 代理设置无效 | 仍然超时 | `git config --get http.proxy` | 确认代理软件正在运行，端口正确 |

### Git 代理完整配置

```powershell
# 设置代理（仅在当前仓库生效）
cd D:\hermes-windows-native\hermes-agent
git config http.proxy http://127.0.0.1:10808
git config https.proxy http://127.0.0.1:10808

# 验证
git config --get http.proxy
# 应输出: http://127.0.0.1:10808

# 测试连接
git ls-remote --heads https://github.com/markwang2658/hermes-windows-native-guide.git
# 应返回 refs/heads/main

# 取消代理（如需要）
git config --unset http.proxy
git config --unset https.proxy
```
