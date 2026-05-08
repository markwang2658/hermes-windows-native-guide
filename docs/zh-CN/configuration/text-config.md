---
title: "文本处理配置指南 (GLM-4.6V)"
lang: zh-CN
version: "1.0"
---

<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../../en/configuration/text-config.md">🇺🇸 English</a>
</div>

# 📄 文本处理配置（默认：GLM-4.6V-Flash）

> 让 Hermes 能**读懂文件** — 代码解释、文档摘要、日志分析

---

## 一、为什么用本地模型处理文本？

| 对比项 | 云端 API (Claude/GPT) | **本地 GLM-4.6V** ⭐ |
|--------|----------------------|---------------------|
| 隐私 | 代码/文档上传服务器 | ✅ 数据不出机器 |
| 成本 | 按 Token 计费 | **免费** |
| 文件大小限制 | 通常 < 10MB | 无限制 |
| 离线 | ❌ 需要网络 | ✅ 完全离线 |
| 批量处理 | 按量计费 | 无限制 |

**适用场景：**
- 📝 README / 文档摘要
- 🔍 代码逻辑解释
- 🐛 错误日志分析
- 📊 配置文件解读
- 📋 大段文本总结

---

## 二、前置条件

文本处理复用**视觉模型**（GLM-4.6V），因此需要先完成：

1. ✅ [安装 LM Studio](vision-config.md#step-1安装-lm-studio)
2. ✅ [下载 GLM-4.6V 模型](vision-config.md#step-2下载-glm-46v-模型)
3. ✅ [启动 LM Studio Server](vision-config.md#step-3启动服务)

![LM Studio 模型加载界面](/screenshots/lm-studio-loading.png)

*图：LM Studio 界面 — Text 模式与 Vision 模式共用同一个 GLM-4.6V 实例*

---

## 三、配置方法

编辑 `~/.hermes/config.yaml`：

```yaml
auxiliary:
  web_extract:
    provider: "lmstudio"               # 复用 LM Studio
    model: "glm-4.6v-flash:q4"         # 与视觉模型相同
    base_url: "http://127.0.0.1:1234/v1"
    timeout: 30                         # 处理超时（秒）
```

> 💡 如果已配置 [视觉模型](vision-config.md)，**无需重复下载模型**，直接复用即可。

---

## 四、支持的文件类型

### 4.1 自动识别的文件类型

| 类型 | 扩展名 | 处理方式 |
|------|--------|----------|
| Markdown | `.md` | 内容摘要、问答 |
| Python | `.py` | 代码解释、Bug 排查 |
| JavaScript | `.js/.ts/.jsx/.tsx` | 代码解释 |
| JSON/YAML | `.json/.yaml/.yml` | 结构化解读 |
| 文本 | `.txt/.log/.csv` | 内容分析 |
| Shell 脚本 | `.ps1/.sh/.bat` | 命令解释 |
| 配置文件 | `.ini/.toml/.conf` | 配置说明 |

### 4.2 使用方式

#### WebUI 中使用：

1. 点击输入框旁的 **📎 回形针图标**
2. 选择文件（支持多选）
3. 输入你的问题，例如：
   - "请总结这个文件的内容"
   - "这段代码的作用是什么？"
   - "帮我找出这个日志中的错误"

#### CLI 中使用：

```powershell
hermes
# 然后粘贴文件路径或拖拽文件到终端
```

---

## 五、典型使用场景

### 场景 1：README 摘要

**操作**: 上传 `README.md`，提问："这个项目是做什么的？"

**预期输出**:
```
这是一个 AI Agent 项目（Hermes），主要功能：
1. 持久化记忆 — 跨会话记住上下文
2. 多模型支持 — OpenAI/Anthropic/本地模型
3. 工具调用 — 终端/浏览器/文件操作
4. 定时任务 — Cron 调度自动化
```

![文件摘要效果演示](/screenshots/demo-text.png)

*图：GLM-4.6V 文本处理效果 — 上传文件后自动摘要并回答问题*

### 场景 2：代码解释

**操作**: 上传 `utils.py`，提问："这个函数的逻辑是什么？"

**预期输出**: 函数级别的逐行解释，包含：
- 输入参数说明
- 执行流程图
- 返回值含义
- 可能的边界情况

### 场景 3：错误日志分析

**操作**: 上传 `error.log`，提问："找出所有错误并给出解决方案"

**预期输出**:
```
发现 3 个错误：

❌ Error 1 (第 23 行): ConnectionRefusedError
   原因: 端口 8787 被占用
   解决: 修改端口或关闭占用进程

⚠️ Warning 2 (第 56 行): DeprecationWarning
   原因: 使用了废弃的 API
   解决: 更新到新版本 API

💡 建议: 第 89 行的配置可能导致性能问题...
```

---

## 六、进阶技巧

### 6.1 批量文件处理

可以一次上传多个文件进行对比分析：

```
上传: config.yaml, config.prod.yaml, config.dev.md
提问: 这三个配置文件有什么不同？
```

### 6.2 结合图片和文件

同时上传截图 + 代码文件：

```
上传: error-screenshot.png, main.py
提问: 截图中的报错对应代码的哪一行？如何修复？
```

### 6.3 大文件处理

对于超大文件（>10MB）：

| 方法 | 操作 |
|------|------|
| 分片上传 | 将文件拆分为多个小文件 |
| 先压缩 | 先让 AI 总结关键部分 |
| 指定行范围 | 提问："只分析前 100 行" |

---

## 七、常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 文件上传后无反应 | LM Studio 未启动 | 启动 LM Studio → Start Server |
| 只显示文件名无内容 | 文件格式不支持 | 转换为 .txt 或 .md 后重试 |
| 分析结果不准确 | 模型上下文窗口不够 | 减小文件大小或分批处理 |
| 中文文件乱码 | 编码问题 | 确保 UTF-8 编码 |
| 处理超时 | 文件过大 | 减小文件或增加 timeout 值 |
| 无法读取二进制文件 | 格式不支持 | .exe/.dll/.pdf 等二进制文件需先转换 |

---

## 八、与其他模式的关系

```
用户输入判断逻辑:

纯文字消息 → Chat 模式 (Kimi K2.6 云端)
     │
     ├── 包含图片 → Vision 模式 (GLM-4.6V 本地)
     ├── 包含音频 → Audio 模式 (Whisper 本地)
     └── 包含文件 → Text 模式 (GLM-4.6V 本地) ← 本文档
```

> **注意**: Text 模式和 Vision 模型共用同一个 GLM-4.6V 实例，无需额外资源。

---

## 九、下一步

至此，四种模式全部配置完成！

| 模式 | 状态 | 文档 |
|------|------|------|
| 💬 Chat (Kimi K2.6) | ☑️ 已配置 | [聊天配置](chat-config.md) |
| 👁️ Vision (GLM-4.6V) | ☑️ 已配置 | [视觉配置](vision-config.md) |
| 🎤 Audio (Whisper) | ☑️ 已配置 | [语音配置](audio-config.md) |
| 📄 Text (GLM-4.6V) | ☑️ 已配置 | **本文档** |

➡️ [故障排查大全](../troubleshooting/index.md) — 遇到问题时查阅
➡️ [架构设计](../architecture/trimode-routing.md) — 深入理解系统设计
