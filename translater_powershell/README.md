# Translator Float (PowerShell)

一个基于 `Windows PowerShell / PowerShell` 与 `Windows Forms` 的桌面翻译浮窗。

这个文件夹本身就是一份完整的 PowerShell 版本。需要备份或分发时，直接压缩整个 `translater_powershell` 文件夹即可。

## 文件夹内容

- `translator_native.ps1`：主程序
- `launch_powershell_translator.bat`：启动脚本
- `API.txt`：API Key 与模型列表
- `prompt_templates.json`：可调提示词
- `translation_cache.json`：翻译缓存
- `window_settings.json`：窗口与模型/思考支持缓存

## 功能

- 输入中文自动翻译成英文
- 输入英文自动翻译成中文
- 输入变化后即时翻译
- 支持流式输出
- 支持模型切换
- 支持“预制模型”弹窗拉取硅基流动最新聊天模型，并勾选保存到当前文件夹的 `API.txt`
- 主模型下拉框只显示当前已保存/勾选的模型
- 支持“快速 / 思考”模式
- 支持上下文与推理强度设置
- 支持配置/代码镜像输出
- 支持复制结果和清空
- 支持悬浮图标拖入文本翻译；悬浮图标获得焦点后，按 `Ctrl+V` 或 `Shift+Insert` 会读取剪贴板文本并触发同样的翻译流程
- 支持临时提示词：勾选后，只有输入严格以小写 `oder:` 开头时才解析；`oder:` 到第一个中文句号 `。` 之间的内容只作为本次翻译额外要求，模型会把它作为高优先级翻译约束自主理解，可控制目标语、术语、风格、大小写、固定输出、格式、替换、后处理等复杂输出要求；无法作用于译文的聊天/闲聊内容会被忽略
- 对 `tencent/Hunyuan-MT-7B`、`inclusionAI/Ling-flash-2.0` 等紧凑翻译模型，程序会使用短提示和纯原文 user message，减少边界标记泄漏。
- 开启临时提示词时，如果当前模型是紧凑翻译模型，程序会自动改用当前模型列表中更适合理解复杂要求的非紧凑模型处理本次请求。

## 配置

`API.txt` 格式：

```text
你的 API Key

模型 ID 1
模型 ID 2
```

- 第一行：API Key
- 第二行：留空
- 后续每行：一个模型 ID

程序默认优先使用第一个模型 ID。
点击模型右侧的“预制模型”可以拉取硅基流动最新聊天模型列表；弹窗默认勾选当前下拉框可选模型，点击保存后才会写回 `API.txt`。

## 运行

双击：

```text
launch_powershell_translator.bat
```

或在当前目录执行：

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -STA -File .\translator_native.ps1
```

如果系统安装了 `pwsh`，也可以用：

```powershell
pwsh -NoProfile -ExecutionPolicy Bypass -STA -File .\translator_native.ps1
```

## 说明

- 这个 PowerShell 版本只依赖当前文件夹内的配置与缓存文件，不再依赖外层目录。
- 不同版本的翻译器应各自维护自己的 `API.txt`、提示词、缓存与窗口设置文件。
