# Translator Float (Python)

这是 Python 版翻译器。这个文件夹是独立版本，配置、提示词、缓存、图标和可执行文件都只读取当前文件夹内的文件。

## 文件夹内容

- `TranslatorFloat.exe`: 打包后的主程序
- `translator_app.py`: Python 源码入口
- `launch_translator.bat`: 源码运行入口
- `API.txt`: API Key 与模型列表
- `prompt_templates.json`: 快速/深度提示词
- `translation_cache.json`: 翻译缓存
- `window_settings.json`: 窗口、模型、模式、上下文、思考等设置缓存
- `translator_girly_icon.ico` / `translator_girly_icon.png`: 图标资源
- `vendor`: Python 版独立依赖目录

## 运行

优先双击：

```text
TranslatorFloat.exe
```

如果需要从源码运行，双击：

```text
launch_translator.bat
```

## 浮窗

- 主界面点击“悬浮”可切换为悬浮按钮。
- 悬浮按钮可拖动；右键点击悬浮按钮会恢复主窗口。
- 鼠标移入悬浮按钮时，右上角会显示迷你“拜拜”退出键；点击该退出键会关闭程序。
- 将选中的文本拖到悬浮按钮上，会按当前模型、快速/深度、配置镜像、上下文和思考设置翻译。
- 鼠标移入或点击悬浮按钮后，按 `Ctrl+V` 或 `Shift+Insert` 会读取剪贴板文本，并按拖入文本同样流程翻译。
- 翻译完成后会在悬浮按钮旁显示气泡；左键气泡关闭显示，右键气泡复制译文。

## 临时提示词

- 主界面勾选“临时提示词”后，如果输入框为空，会自动显示可编辑的 `oder:`。
- 输入格式：`oder:本次翻译要求。待翻译文本`
- 第一个中文句号 `。` 前的内容只作为本次翻译提示词，不会作为原文翻译；句号后的内容才是待翻译文本。
