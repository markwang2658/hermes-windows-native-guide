---
title: "故障排查大全"
lang: zh-CN
version: "1.0"
---

<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../../../en/troubleshooting/index.md">🇺🇸 English</a>
</div>

# 🐛 故障排查大全

> 20+ 常见问题及解决方案，覆盖安装、启动、配置、运行全流程

---

## 快速定位

| 你遇到的问题类型 | 跳转到 |
|------------------|--------|
| 安装失败 | [安装问题](installation-issues.md) |
| 启动失败 | [启动问题](startup-issues.md) |
| 连接/网络问题 | [连接问题](connection-issues.md) |
| 模型/API 问题 | [模型问题](model-issues.md) |
| 功能异常 | [功能问题](feature-issues.md) |
| 性能问题 | [性能问题](performance-issues.md) |
| Windows 特有问题 | [Windows 问题](windows-issues.md) |

---

## 诊断工具箱

### hermes doctor

```powershell
hermes doctor
```

最常用的诊断命令，一次性检查所有关键项。

### 健康检查清单

```powershell
# 1. Python 环境
python --version                    # ≥ 3.10

# 2. 依赖完整性
pip check                            # 应无输出（无冲突）

# 3. Agent 可用性
hermes --version                     # 应输出版本号

# 4. WebUI 可用性
curl http://127.0.0.1:8787/health   # 应返回 {"status": "ok"}
Test-Path "$env:USERPROFILE\.hermes\webui-mvp"    # WebUI 状态目录存在

# 5. 配置文件
Test-Path "$env:USERPROFILE\.hermes\config.yaml"    # True
Test-Path "$env:USERPROFILE\.hermes\.env"            # True

# 6. LM Studio (如使用本地模型)
Invoke-RestMethod http://127.0.0.1:1234/v1/models    # 应返回模型列表

# 7. 端口占用
netstat -ano | findstr ":8787"       # 应有 python.exe 监听

# 8. 日志检查
Get-Content "$env:USERPROFILE\.hermes\logs\errors.log" -Tail 20  # 最近错误
```

### 日志位置

| 日志 | 路径 | 用途 |
|------|------|------|
| Agent 日志 | `~/.hermes/logs/agent.log` | 运行信息 |
| 错误日志 | `~/.hermes/logs/errors.log` | 异常堆栈 |
| Gateway 日志 | `~/.hermes/logs/gateway.log` | Web 服务日志 |

---

## 获取帮助

如果以上方案都无法解决你的问题：

| 渠道 | 适用场景 |
|------|----------|
| 🐛 [GitHub Issues](https://github.com/markwang2658/hermes-windows-native/issues) | Bug 报告、功能请求 |
| 💬 [GitHub Discussions](https://github.com/markwang2658/hermes-windows-native/discussions) | 使用问题、经验分享 |
| 🧠 [上游 Agent Issues](https://github.com/NousResearch/hermes-agent/issues) | 核心组件 Bug |
| 🌐 [上游 WebUI Issues](https://github.com/nesquena/hermes-webui/issues) | Web 界面 Bug |

### 提交 Issue 时请包含

- [ ] Windows 版本 (`winver`)
- [ ] Python 版本 (`python --version`)
- [ ] 完整的错误信息（不要截断）
- [ ] 复现步骤（最小可复现案例）
- [ ] `hermes doctor` 的输出
- [ ] 相关日志片段（脱敏后）

---

## 常见错误码速查

| 错误信息 | 含义 | 快速修复 |
|----------|------|----------|
| `EADDRINUSE` | 端口被占用 | 换端口或杀进程 |
| `ECONNREFUSED` | 服务未启动 | 启动对应服务 |
| `ETIMEDOUT` | 连接超时 | 检查网络/代理 |
| `ENOENT` | 文件不存在 | 检查路径拼写 |
| `EACCES` | 权限不足 | 管理员运行或检查权限 |
| `OOM` / `CUDA OOM` | 显存不足 | 降低量化或换小模型 |
| `401 Unauthorized` | API Key 无效 | 检查/更新密钥 |
| `429 Too Many Requests` | 请求频率过高 | 降低频率或升级套餐 |
| `500 Internal Server Error` | 服务端错误 | 稍后重试或报告 Bug |
