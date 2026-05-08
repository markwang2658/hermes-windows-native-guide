---
title: "视觉模型配置指南 (GLM-4.6V)"
lang: zh-CN
version: "1.0"
---

<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../../en/configuration/vision-config.md">🇺🇸 English</a>
</div>

# 👁️ 视觉模型配置（默认：GLM-4.6V-Flash）

> 让 Hermes 能**看懂图片** — 截图分析、图像识别、OCR 文字提取

---

## 一、为什么用本地视觉模型？

| 对比项 | 云端 API (GPT-4V) | **本地 GLM-4.6V** ⭐ |
|--------|-------------------|---------------------|
| 隐私 | 截图上传到服务器 | ✅ 数据不出机器 |
| 成本 | ~¥0.1-0.5/张 | **免费** |
| 延迟 | 2-5s（网络波动） | 3-5s（稳定） |
| 离线 | ❌ 需要网络 | ✅ 完全离线 |
| 批量处理 | 按量计费 | 无限制 |

**适用场景：**
- 📸 截图分析（报错信息、界面问题）
- 📊 图表解读（数据可视化）
- 📄 OCR 文字提取（图片转文字）
- 🔍 图片内容问答

---

## 二、硬件要求

### 最低要求

| 组件 | 最低配置 | 推荐配置 |
|------|----------|----------|
| GPU | 无（CPU 也可运行） | NVIDIA GTX 1060+ (6GB) |
| 显存 | 0 (CPU) / 4GB (GPU) | 8GB+ |
| 内存 | 8GB | 16GB |
| 磁盘 | 5GB（模型文件） | SSD 推荐 |

### GPU 支持列表

| 显卡 | 显存 | 推荐量化 | 体验 |
|------|------|----------|------|
| RTX 4090 | 24GB | FP16 | ⭐⭐⭐⭐⭐ 完美 |
| RTX 3090 | 24GB | FP16 | ⭐⭐⭐⭐⭐ 完美 |
| RTX 4070 | 12GB | Q5 | ⭐⭐⭐⭐ 流畅 |
| RTX 3060 | 12GB | Q5/Q4 | ⭐⭐⭐ 可用 |
| GTX 1660 | 6GB | Q4 | ⭐⭐ 勉强 |
| 无 GPU | 0 | Q4 (CPU) | ⭐ 很慢 |

---

## 三、安装 LM Studio

LM Studio 是 Windows 上最简单的本地模型推理工具。

![LM Studio 模型加载界面](/screenshots/lm-studio-loading.png)

*图：LM Studio 界面 — 搜索、下载、加载本地 AI 模型*

### Step 1：下载安装

1. 访问 [lmstudio.ai](https://lmstudio.ai)
2. 下载 Windows 版本
3. 运行安装程序

### Step 2：下载 GLM-4.6V 模型

1. 打开 LM Studio
2. 点击左侧 **🔍 搜索图标**
3. 搜索 `glm-4.6v-flash`
4. 选择量化版本（推荐 `Q5` 或 `Q4`）
5. 点击 **Download**

> 💡 **推荐版本**: `glm-4.6v-flash:q4_K_M` — 精度与速度的最佳平衡

### Step 3：启动服务

1. 点击顶部 **💻 Local Server** 标签
2. 确认端口为 `1234`（默认）
3. 点击 **Start Server**

验证服务运行：

```powershell
curl http://127.0.0.1:1234/v1/models
```

预期输出包含 `glm-4.6v-flash`。

---

## 四、配置 Hermes 使用 GLM-4.6V

编辑 `~/.hermes/config.yaml`：

```yaml
auxiliary:
  vision:
    provider: "lmstudio"               # LM Studio 提供商
    model: "glm-4.6v-flash:q4"         # 你下载的模型名称
    base_url: "http://127.0.0.1:1234/v1"
    timeout: 30                         # 图片分析超时（秒）
    download_timeout: 30                # 图片下载超时（秒）
```

> ⚠️ 确保 LM Studio 的 **Server 已启动**，否则图片识别会失败。

---

## 五、测试验证

### 5.1 WebUI 测试

1. 打开 `http://127.0.0.1:8787`
2. 点击输入框旁的 **📎 回形针图标**
3. 选择一张图片（截图、照片等）
4. 输入描述："请描述这张图片的内容"

预期结果：
- ✅ AI 正确描述图片内容
- ✅ 能识别文字（如有）
- ✅ 能回答关于图片的问题

![图片识别效果演示](/screenshots/demo-vision.png)

*图：GLM-4.6V 图片识别效果 — 上传截图后自动识别并回答问题*

### 5.2 CLI 测试

```powershell
hermes
```

发送带图片的消息，观察是否调用 vision 模型。

---

## 六、进阶配置

### 6.1 切换量化等级

| 量化 | 显存占用 | 速度 | 精度 | 适用场景 |
|------|----------|------|------|----------|
| FP16 | ~10GB | 中 | 最高 | 高端显卡 |
| Q5 | ~6GB | 快 | 95%+ | **推荐默认** |
| Q4 | ~4GB | 很快 | 90% | 中低端显卡 |
| Q3 | ~3GB | 最快 | 80% | 不推荐 |

在 LM Studio 中搜索时选择不同量化版本即可。

### 6.2 替代方案：Ollama

如果你更喜欢 Ollama：

```powershell
ollama pull glm-4.6v-flash:q4
```

```yaml
auxiliary:
  vision:
    provider: "custom"
    model: "glm-4.6v-flash:q4"
    base_url: "http://127.0.0.1:11434/v1"
```

### 6.3 多模型切换

可以随时切换到其他视觉模型：

| 模型 | 来源 | 特点 |
|------|------|------|
| `llava-v1.6` | LM Studio | 开源经典，社区大 |
| `bakllava` | LM Studio | 轻量快速 |
| `gpt-4o-mini` | OpenAI | 云端备选 |

---

## 七、常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 图片上传后无反应 | LM Studio 未启动 | 启动 LM Studio → Start Server |
| 识别结果不准确 | 量化等级太低 | 切换到 Q5 或 FP16 |
| 速度很慢 | 使用 CPU 推理 | 安装 CUDA 版本的 LM Studio |
| 显存不足 (OOM) | 模型太大 | 使用更低量化 (Q4) |
| 连接被拒绝 | 端口错误 | 确认 LM Studio 端口为 1234 |
| 中文识别乱码 | 模型不支持中文 | GLM-4.6V 原生支持中文，检查模型是否正确 |

---

## 八、性能优化

| 方法 | 效果 | 操作难度 |
|------|------|----------|
| GPU 加速 | 速度提升 5-10x | ⭐ LM Studio 自动检测 |
| 模型常驻内存 | 冷启动从 30s → 2s | ⭐ 保持 LM Studio 开启 |
| 图片压缩 | 减少传输时间 | ⭐⭐ 预处理图片 |
| 批量处理 | 并行多张图片 | ⭐⭐⭐ 编程实现 |

---

## 九、下一步

➡️ [语音转写配置 (Whisper)](audio-config.md) — 让 AI 能听懂语音
➡️ [文本处理配置 (GLM-4.6V)](text-config.md) — 让 AI 能读文件
➡️ [故障排查大全](../troubleshooting/index.md) — 遇到问题时查阅
