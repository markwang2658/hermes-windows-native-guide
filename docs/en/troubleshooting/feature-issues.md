---
title: "Feature Issues"
lang: en
version: "1.0"
---

<div align="right">
  <a href="../../../zh-CN/troubleshooting/feature-issues.md">🇨🇳 中文</a> |
  <strong>🇺🇸 English</strong>
</div>

# ⚙️ Feature Issues

| # | Issue | Symptom | Diagnostic Command | Solution |
|---|-------|---------|--------------------|----------|
| 1.1 | Image upload not working | No response after sending | Browser F12 -> Network tab | Verify LM Studio is running on port 1234 |
| 1.2 | Speech-to-text fails | Error after uploading audio | `python -c "from faster_whisper import..."` | Install faster-whisper: `pip install faster-whisper` |
| 1.3 | File content not displayed | Only filename shown | Try uploading a .txt file | Some binary formats are not supported; convert to plain text |
| 1.4 | Session data lost | History disappears after page refresh | Check `~/.hermes/webui-mvp/` | Confirm state directory exists and has write permissions |
| 1.5 | Tool call failure | AI unable to execute commands | `hermes doctor` | Check tool permissions and configuration |
| 1.6 | Memory function not working | AI does not recall previous conversations | Check `~/.hermes/memory/` | Confirm memory directory exists |
