# Translator Float 记忆索引

## 项目目标

- 做一个 Windows 桌面翻译浮窗，支持中文/英文自动互译。
- 翻译接口使用硅基流动 API，`API.txt` 第一行为密钥，第二行留空，后续每行一个模型 ID。
- 维护两个完全分离的版本：`translater_python` Python 自包含版、`translater_powershell` PowerShell 自包含版。

## 重要约束

- 不泄露 API Key。
- 不随意删除或重置 `translation_cache.json`、`window_settings.json`。
- Python 版本相关文件必须留在 `translater_python` 文件夹内，PowerShell 版本相关文件必须留在 `translater_powershell` 文件夹内，便于任一文件夹直接压缩分发。
- 临时提示词格式固定为 `oder:本次翻译额外要求。待翻译文本`；只有勾选“临时提示词”且输入严格以小写 `oder:` 开头时才解析，`oder:` 到第一个中文句号 `。` 之间的内容作为本次 system 输出约束，不作为原文；模型需要把它作为高优先级翻译约束自主理解，可控制固定输出、大小写、格式、术语、替换、后处理等复杂要求，但无法作用于译文的聊天/闲聊内容必须忽略，不能输出或回应。紧凑模型使用短英文 system 和纯原文 user message，避免复杂边界标记泄漏；开启临时提示词且当前选择紧凑模型时，自动路由到当前列表中更适合理解复杂要求的非紧凑模型处理本次请求。

## 详细记录

- [模型列表与预制模型](model-presets.md)
- [悬浮按钮与目录拆分](floating-mode.md)
