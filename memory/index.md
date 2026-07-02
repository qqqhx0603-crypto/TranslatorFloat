# Translator Float 记忆索引

## 项目目标

- 做一个 Windows 桌面翻译浮窗，支持中文/英文自动互译。
- 翻译接口使用硅基流动 API，`API.txt` 第一行为密钥，第二行留空，后续每行一个模型 ID。
- 维护两个完全分离的版本：`translater_python` Python 自包含版、`translater_powershell` PowerShell 自包含版。

## 重要约束

- 不泄露 API Key。
- 不随意删除或重置 `translation_cache.json`、`window_settings.json`。
- Python 版本相关文件必须留在 `translater_python` 文件夹内，PowerShell 版本相关文件必须留在 `translater_powershell` 文件夹内，便于任一文件夹直接压缩分发。
- 临时提示词格式固定为 `oder:提示词。待翻译文本`；只有勾选“临时提示词”且输入以 `oder:` 开头时才解析，第一个中文句号 `。` 前的内容作为本次 system prompt，不作为原文。

## 详细记录

- [模型列表与预制模型](model-presets.md)
- [悬浮按钮与目录拆分](floating-mode.md)
