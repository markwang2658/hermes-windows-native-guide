# 📸 Screenshots 截图目录

> 本目录存放文档所需的所有截图和视频
>
> **中英文文档共用**此目录资源

---

## 📋 截图清单（12 张 + 1 视频）

### 架构图（2 张）

| # | 文件名 | 说明 | 使用位置 |
|---|--------|------|----------|
| 1 | `architecture-zh.png` | 四种模式分流架构图（中文版） | [trimode-routing.md](../docs/zh-CN/architecture/trimode-routing.md) |
| 2 | `architecture-en.png` | 四种模式分流架构图（英文版） | [trimode-routing.md](../docs/en/architecture/trimode-routing.md) |

### 启动演示（3 张）

| # | 文件名 | 说明 | 使用位置 |
|---|--------|------|----------|
| 3 | `quick-start.gif` | 3 步快速启动演示动画 | [README.zh-CN.md](../README.zh-CN.md) Quick Start 章节 |
| 4 | `hermes-agent-start.png` | Hermes Agent 启动效果 | [agent-install.md](../docs/zh-CN/installation/agent-install.md) |
| 5 | `hermes-webui-start.png` | Hermes WebUI 启动效果 | [webui-install.md](../docs/zh-CN/installation/webui-install.md) |

### 聊天效果（4 张）

| # | 文件名 | 说明 | 使用位置 |
|---|--------|------|----------|
| 6 | `hermes-agent-chat.png` | Hermes Agent 聊天效果 | [chat-config.md](../docs/zh-CN/configuration/chat-config.md) |
| 7 | `hermes-webui-chat.png` | Hermes WebUI 聊天效果 | [chat-config.md](../docs/zh-CN/configuration/chat-config.md) |
| 8 | `demo-chat.png` | 聊天对话效果演示 | [chat-config.md](../docs/zh-CN/configuration/chat-config.md) |

### 功能演示（3 张）

| # | 文件名 | 说明 | 使用位置 |
|---|--------|------|----------|
| 9 | `demo-vision.png` | 图片识别效果演示 | [vision-config.md](../docs/zh-CN/configuration/vision-config.md) |
| 10 | `demo-audio.png` | 语音转写效果演示 | [audio-config.md](../docs/zh-CN/configuration/audio-config.md) |
| 11 | `demo-text.png` | 文件摘要效果演示 | [text-config.md](../docs/zh-CN/configuration/text-config.md) |

### 工具界面（1 张）

| # | 文件名 | 说明 | 使用位置 |
|---|--------|------|----------|
| 12 | `lm-studio-loading.png` | LM Studio 模型加载界面 | [vision-config.md](../docs/zh-CN/configuration/vision-config.md) / [text-config.md](../docs/zh-CN/configuration/text-config.md) |

---

## 📊 统计总览

| 类型 | 数量 | 状态 |
|------|------|------|
| PNG 静态图 | **11** | ✅ 100% |
| **GIF 动画** | **1** | ✅ 100% |
| **总计** | **12** | ✅ 全部完成 |

---

## 🔗 文档引用语法

### 图片引用

```markdown
<!-- 相对路径：从 docs/zh-CN 或 docs/en 目录引用 -->
![3 步快速启动](../../screenshots/quick-start.gif)
```

### GIF 动画引用（GitHub 原生支持）

```markdown
<video src="../../screenshots/quick-start.gif" controls width="100%" style="max-width:800px;">
  <source src="../../screenshots/quick-start.gif" type="image/gif">
  您的浏览器不支持 GIF 标签。
</video>
```

### 带说明的引用（推荐）

```markdown
<figure style="text-align: center;">
  <img src="../../screenshots/demo-vision.png" alt="图片识别效果演示">
  <figcaption>图：GLM-4.6V 图片识别效果 — 上传图片后自动识别内容</figcaption>
</figure>
```

---

## 🎨 截图规范

### 技术参数

| 属性 | 要求 | 说明 |
|------|------|------|
| 分辨率 | 1920×1080 或 2560×1440 (16:9) | GitHub 渲染友好比例 |
| 静态图格式 | PNG (无损压缩) | ❌ 禁用 JPG |
| 视频格式 | GIF (帧率 10fps, 时长 < 15s) | GitHub 原生支持 |
| 文件大小 | PNG < 500KB / GIF < 2MB | 超过需压缩 |

### 脱敏检查清单

- [ ] **API Key** → 用 `sk-xxxx...xxxx` 占位符
- [ ] **个人路径** → 用 `D:\hermes-windows-native\` 统一占位符
- [ ] **IP 地址** → 用 `127.0.0.1` 或 `localhost`
- [ ] **用户名/计算机名** → 打码或隐藏

### 推荐工具

| 工具 | 用途 |
|------|------|
| **Snipaste** | 截图 + 标注（免费） |
| **ShareX** | 录屏 / GIF / 视频（开源） |
| **OBS Studio** | 高质量录屏（开源） |

---

## 📁 命名规范

```
<功能>-<场景>.<扩展名>

架构图:
  architecture-zh.png    -- 中文版
  architecture-en.png    -- 英文版

启动类:
  hermes-agent-start.png   -- Agent 启动界面
  hermes-webui-start.png   -- WebUI 启动界面
  quick-start.gif           -- 快速启动动画

功能演示:
  demo-chat.png            -- 聊天效果
  demo-vision.png          -- 图片识别效果
  demo-audio.png           -- 语音转写效果
  demo-text.png            -- 文本摘要效果

第三方工具:
  lm-studio-loading.png    -- LM Studio 模型加载
```

---

## ✅ 提交前自检

- [ ] 所有截图已脱敏（无真实 API Key / 个人路径）
- [ ] 文件名符合 kebab-case 格式
- [ ] 文件大小符合限制（PNG < 500KB）
- [ ] 分辨率为 16:9 比例
- [ ] 引用路径正确（相对路径从 docs 目录出发）

---

**最后更新**: 2026-05-08  
**截图总数**: 12 (11 PNG + 1 GIF)
