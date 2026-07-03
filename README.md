# Translator Float

Translator Float 是一个 Windows 桌面翻译浮窗工具，支持中文和英文自动互译。项目包含两个互相独立的版本：

- `translater_python`：Python / Tkinter 版本，可从源码运行，也可自行打包为 exe。
- `translater_powershell`：PowerShell / Windows Forms 版本，Windows 原生可用。

翻译接口使用硅基流动兼容 OpenAI Chat Completions 的 API。你可以通过这个邀请链接注册硅基流动：[https://cloud.siliconflow.cn/i/rxl9Pzih](https://cloud.siliconflow.cn/i/rxl9Pzih)。注册并实名后通常可获得 16 元额度，足够支撑本翻译器较长时间使用。

## 怎么使用

### 1. 获取硅基流动 API Key

在硅基流动控制台创建 API Key，并准备至少一个聊天模型 ID。

推荐先用较快模型，例如：

```text
tencent/Hunyuan-MT-7B
inclusionAI/Ling-flash-2.0
deepseek-ai/DeepSeek-V3.2
```

### 2. 配置 API.txt

在你要使用的版本目录中复制示例文件：

```text
API.example.txt -> API.txt
```

`API.txt` 格式如下：

```text
你的 API Key

模型 ID 1
模型 ID 2
```

第一行是 API Key，第二行留空，后续每行一个模型 ID。程序默认优先使用第一个模型。

### 3. 运行 Python 版

进入：

```text
translater_python
```

双击：

```text
launch_translator.bat
```

如果你自行打包了 exe，也可以直接运行 `TranslatorFloat.exe`。公开仓库默认不提交本地打包 exe。

### 4. 运行 PowerShell 版

进入：

```text
translater_powershell
```

双击：

```text
launch_powershell_translator.bat
```

也可以在当前目录执行：

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -STA -File .\translator_native.ps1
```

## 主要功能

- 输入中文自动翻译成英文，输入英文自动翻译成中文。
- 输入变化后即时翻译。
- 支持模型切换。
- 支持快速 / 思考模式。
- 支持上下文长度和推理强度设置。
- 支持配置/代码镜像输出，避免配置文本被模型错误翻译。
- 支持自定义快速/思考翻译提示词。
- 支持临时提示词：开启后，只有输入严格以小写 `oder:` 开头时才解析；`oder:` 到第一个中文句号 `。` 之间的内容只作为本次提示词，不作为原文翻译，可控制大小写、固定输出、格式等本次输出约束。
- 支持翻译缓存。
- 支持悬浮球模式：拖入文本或对悬浮球粘贴即可翻译。
- 悬浮球翻译过程中有动画反馈，避免不确定是否收到翻译指令。
- 翻译完成后可在悬浮球旁显示气泡，支持复制结果。

## 目录结构

```text
Translater
├─ translater_python
│  ├─ translator_app.py
│  ├─ launch_translator.bat
│  ├─ prompt_templates.json
│  ├─ API.example.txt
│  └─ vendor
├─ translater_powershell
│  ├─ translator_native.ps1
│  ├─ launch_powershell_translator.bat
│  ├─ prompt_templates.json
│  └─ API.example.txt
└─ memory
```

两个版本互相独立，不共用 `API.txt`、提示词、缓存或窗口设置文件。

## 不会提交到仓库的文件

公开仓库会忽略以下本地文件：

- `API.txt`：包含 API Key，不能公开。
- `translation_cache.json`：本地翻译缓存，可能包含私人文本。
- `window_settings.json`：本地窗口位置、模型和模式缓存。
- `TranslatorFloat.exe`：本地打包产物。
- `build`、`dist`、`__pycache__` 等临时产物。

## 打包 Python exe

如果需要重新打包 Python 版，可以安装 PyInstaller 后在项目根目录执行：

```powershell
python -m PyInstaller --noconfirm --onefile --windowed --name TranslatorFloat --icon .\translater_python\translator_girly_icon.ico --hidden-import platform --distpath .\translater_python --workpath .\translater_python\build --specpath .\translater_python .\translater_python\translator_app.py
```

生成的 `TranslatorFloat.exe` 会出现在 `translater_python` 目录中。

## 许可证

本项目使用 MIT License。详见 [LICENSE](LICENSE)。
