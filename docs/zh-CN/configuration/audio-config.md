---
title: "语音转写配置指南 (faster-whisper)"
lang: zh-CN
version: "1.0"
---

<div align="right">
  <strong>🇨🇳 中文</strong> |
  <a href="../../en/configuration/audio-config.md">🇺🇸 English</a>
</div>

# 🎤 语音转写配置（默认：faster-whisper）

> 让 Hermes 能**听懂语音** — 语音消息自动转写为文字

---

## 一、为什么用本地语音转写？

| 对比项 | 云端 API (Whisper API) | **本地 faster-whisper** ⭐ |
|--------|------------------------|---------------------------|
| 隐私 | 语音数据上传服务器 | ✅ 数据不出机器 |
| 成本 | ~$0.006/分钟 | **免费** |
| 延迟 | 2-5s | 1-3s（短音频） |
| 离线 | ❌ 需要网络 | ✅ 完全离线 |
| 语言支持 | 99 种语言 | 99 种语言 |

**适用场景：**
- 🎙️ 语音消息转文字
- 📝 会议录音整理
- 🎵 音频内容摘要
- 🌐 多语言音频翻译

---

## 二、硬件要求

| 配置 | CPU 模式 | GPU 模式 (CUDA) |
|------|----------|-----------------|
| 最低内存 | 4GB | 8GB |
| 推荐内存 | 8GB | 16GB |
| GPU | 不需要 | NVIDIA GPU (显存 ≥ 4GB) |
| 处理速度 (1分钟音频) | ~30-60s | ~3-10s |

---

## 三、安装 faster-whisper

### Step 1：激活虚拟环境

```powershell
cd D:\hermes-windows-native\hermes-agent
.\.venv\Scripts\Activate.ps1
```

### Step 2：安装 faster-whisper

```powershell
pip install faster-whisper
```

> 💡 如果网络慢，使用镜像源：
> ```powershell
> pip install faster-whisper -i https://pypi.tuna.tsinghua.edu.cn/simple
> ```

### Step 3：验证安装

```powershell
python -c "from faster_whisper import WhisperModel; print('OK')"
```

输出 `OK` 表示安装成功。

---

## 四、配置 Hermes

编辑 `~/.hermes/config.yaml`：

```yaml
stt:
  enabled: true                          # 启用语音转写
  local:
    model: "base"                        # 模型大小
    # language: ""                       # 留空 = 自动检测语言
    # device: "cuda"                     # 可选: cuda / cpu / auto
    # compute_type: "int8"               # 可选: int8 / float16 / float32
```

### 模型选择指南

| 模型 | 大小 | 显存需求 | 速度 (GPU) | 精度 | **推荐场景** |
|------|------|----------|------------|------|-------------|
| `tiny` | 75MB | ~1GB | ⚡⚡⚡ | ★☆☆ | 快速测试 |
| `base` | 142MB | ~2GB | ⚡⚡ | ★★☆ | **日常推荐** ✓ |
| `small` | 466MB | ~3GB | ⚡ | ★★★ | 高精度需求 |
| `medium` | 1.5GB | ~5GB | 🐢 | ★★☆ | 不推荐 |
| `large-v3` | 3GB | ~10GB | 🐢🐢 | ★★★★ | 最高精度 |

> 💡 **新手建议**: 从 `base` 开始，速度与精度的最佳平衡点。

---

## 五、测试验证

### 5.1 Python 直接测试

```powershell
python -c "
from faster_whisper import WhisperModel
model = WhisperModel('base', device='cpu', compute_type='int8')
segments, info = model.transcribe('test.mp3')
for seg in segments:
    print(f'[{seg.start:.1f}s -> {seg.end:.1f}s] {seg.text}')
"
```

### 5.2 WebUI 测试

1. 打开 `http://127.0.0.1:8787`
2. 点击输入框旁的 **🎤 麦克风图标** 录音
   - 或点击 **📎** 上传 `.mp3/.wav` 文件
3. 发送消息

预期结果：
- ✅ 语音自动转写为文字显示
- ✅ AI 根据转写内容回复

![语音转写效果演示](/screenshots/demo-audio.png)

*图：faster-whisper 语音转写效果 — 音频文件自动转为文字并智能回复*

### 5.3 支持的音频格式

| 格式 | 扩展名 | 支持 |
|------|--------|------|
| MP3 | `.mp3` | ✅ 推荐 |
| WAV | `.wav` | ✅ 无损 |
| M4A | `.m4a` | ✅ Apple 录音 |
| OGG | `.ogg` | ✅ |
| FLAC | `.flac` | ✅ |
| WebM | `.webm` | ✅ |

---

## 六、进阶配置

### 6.1 GPU 加速（强烈推荐）

如果你有 NVIDIA 显卡：

```yaml
stt:
  enabled: true
  local:
    model: "base"
    device: "cuda"                      # 使用 GPU
    compute_type: "float16"             # GPU 推荐使用 float16
```

**加速效果对比**（1 分钟音频）：

| 设备 | base 模型耗时 |
|------|---------------|
| CPU (i7) | ~40-60 秒 |
| GPU (GTX 1060) | ~5-8 秒 |
| GPU (RTX 3090) | ~2-3 秒 |
| GPU (RTX 4090) | ~1-2 秒 |

### 6.2 指定语言

如果知道音频是特定语言，可以指定以提升准确率：

```yaml
stt:
  local:
    model: "base"
    language: "zh"                     # 强制中文
    # language: "en"                   # 强制英文
    # language: "ja"                   # 强制日文
```

支持的语言代码：`zh`(中文), `en`(英文), `ja`(日文), `ko`(韩文), `fr`(法文), `de`(德文) 等 99 种。

### 6.3 性能与精度权衡

```yaml
stt:
  local:
    model: "small"                     # 更高精度
    device: "cuda"
    compute_type: "int8"               # 更低显存占用
```

| compute_type | 显存占用 | 速度 | 精度影响 |
|--------------|----------|------|----------|
| `float32` | 最大 | 最慢 | 基准 |
| `float16` | 半量 | 快 | 几乎无损 |
| `int8` | 最小 | 最快 | 轻微下降 |

---

## 七、常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| `ModuleNotFoundError` | 未安装 faster-whisper | `pip install faster-whisper` |
| 转写结果为空 | 音频格式不支持 | 转换为 MP3/WAV 格式 |
| 速度很慢 | 使用 CPU 推理 | 配置 `device: "cuda"` |
| CUDA 错误 | 未安装 CUDA 版 PyTorch | `pip install torch torchvision --index-url https://download.pytorch.org/whl/cu121` |
| 中文乱码 | 编码问题 | 确保终端 UTF-8 编码 |
| 显存不足 (OOM) | 模型太大 | 使用 `base` 或 `tiny` 模型 |
| 首次运行很慢 | 正在下载模型文件 | 首次会自动下载 (~142MB for base)，之后会缓存 |

---

## 八、语音转写 vs 云端 API

| 场景 | 推荐 | 原因 |
|------|------|------|
| 日常使用 | 本地 faster-whisper | 免费、隐私、快速 |
| 超长音频 (>1h) | 本地 | 无时长限制 |
| 实时转录 | 本地 | 延迟低 |
| 需要最高精度 | 云端 Whisper API | large-v3 模型更强 |
| 无 GPU 的老电脑 | 云端 | 避免 CPU 过慢 |

---

## 九、下一步

➡️ [文本处理配置 (GLM-4.6V)](text-config.md) — 让 AI 能读文件
➡️ [四种模式分流架构](../architecture/trimode-routing.md) — 理解整体架构
➡️ [故障排查大全](../troubleshooting/index.md) — 遇到问题时查阅
