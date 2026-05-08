---
title: "Windows 特有问题"
lang: zh-CN
version: "1.0"
---

<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../../../en/troubleshooting/windows-issues.md">🇺🇸 English</a>
</div>

# 🪟 Windows 特有问题

| # | 问题 | 症状 | 原因 | 解决方案 |
|---|------|------|------|----------|
| 1.1 | 路径分隔符错误 | `FileNotFoundError` | Windows 用 `\`，代码用 `/` | Hermes 内部自动处理，手动路径用 `\` |
| 1.2 | 长路径名错误 (>260 字符) | `文件名过长` | Windows 路径长度限制 | 启用长路径支持或将项目放在短路径下 |
| 1.3 | 文件锁冲突 | `PermissionError: [Errno 13]` | 另一个进程正在使用文件 | 关闭占用文件的程序（编辑器、预览等） |
| 1.4 | PowerShell 执行策略 | `无法加载文件` | 安全策略禁止执行脚本 | `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` |
| 1.5 | 中文目录/文件名 | 编码错误 | GBK vs UTF-8 冲突 | 项目路径避免中文，文件内容不受影响 |
| 1.6 | 权限不足 (WinError 5) | 写入失败 | UAC 或 NTFS 权限 | 以管理员身份运行或检查文件夹权限 |
| 1.7 | 防火墙拦截 | 外部无法访问 | Windows Defender | 添加防火墙例外或保持默认 127.0.0.1 |
| 1.8 | 杀毒软件干扰 | 文件被隔离/删除 | Defender/第三方杀毒 | 将项目目录加入白名单 |
