---
title: "Windows-Specific Issues"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../../../zh-CN/troubleshooting/windows-issues.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# 🪟 Windows-Specific Issues

| # | Issue | Symptom | Cause | Solution |
|---|-------|---------|-------|----------|
| 1.1 | Path separator mismatch | `FileNotFoundError` | Windows uses `\`, code uses `/` | Hermes handles this internally; use `\` for manual paths |
| 1.2 | Long path name error (>260 chars) | Filename too long | Windows MAX_PATH limitation | Enable long path support or place project under a short path |
| 1.3 | File lock conflict | `PermissionError: [Errno 13]` | Another process holds the file lock | Close the program holding the file (editor, previewer, etc.) |
| 1.4 | PowerShell execution policy | `Cannot load file` | Security policy blocks script execution | `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` |
| 1.5 | Chinese characters in directory/filename | Encoding errors | GBK vs UTF-8 conflict | Avoid Chinese characters in project paths; file contents unaffected |
| 1.6 | Insufficient permissions (WinError 5) | Write operation failed | UAC or NTFS permission restrictions | Run as Administrator or check folder permissions |
| 1.7 | Firewall blocking access | Cannot access from external network | Windows Defender Firewall | Add firewall exception or keep default binding to 127.0.0.1 |
| 1.8 | Antivirus interference | Files quarantined or deleted | Defender or third-party antivirus | Add project directory to antivirus exclusion list |
