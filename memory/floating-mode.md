# 悬浮按钮与目录拆分

## 2026-06-04

- 项目根目录只保留版本文件夹与项目记忆，Python 版放在 `translater_python`，PowerShell 版放在 `translater_powershell`。
- 两个版本不共用 `API.txt`、`prompt_templates.json`、`translation_cache.json`、`window_settings.json` 或启动文件。
- Python 版新增悬浮按钮模式：主界面点“悬浮”隐藏主窗口并显示可拖动按钮，靠边半隐藏，鼠标移近伸出。
- PowerShell 版新增同等悬浮按钮模式，使用 WinForms 原生拖放接收文本。
- 悬浮按钮接收拖入文本后，使用当前模型、快速/深度、配置镜像、上下文和思考设置翻译。
- 悬浮气泡只显示本次译文，不写入新的输入事件；左键关闭气泡，右键复制译文。
- 关闭气泡或在气泡/窗口之间切换不会重新触发翻译。
- 2026-06-04 修复拖动误判：松开鼠标时只记录是否拖动，真正还原窗口只走独立 Click 事件；拖动超过阈值后的 Click 会被忽略。
- 2026-06-04 悬浮按钮和气泡改为粉色可爱样式；Python 版使用 Canvas 绘制圆形按钮，PowerShell 版使用 WinForms 椭圆 Region 和粉色气泡面板。
- 2026-06-04 删除靠近边缘自动隐藏/伸出功能和对应代码；悬浮球默认置顶，拖到哪里就停在哪里。
- 2026-06-04 新增显示形态缓存：`window_settings.json` 中保存 `display_mode` / `displayMode`，下次启动按上次关闭或切换时的窗口/悬浮球形态打开。
- 2026-06-04 调整悬浮球鼠标规则：左键只负责按住拖动位置，不再切换窗口；右键点击悬浮球才还原主窗口。
- 2026-06-04 修复 PowerShell 版双击无反应：启动阶段模型下拉框可能尚未选中，`Update-ModeAvailability` 必须先处理空模型，不能直接调用思考支持检测。
- 2026-06-04 修复 PowerShell 版悬浮球切换 JIT 报错：WinForms `Paint/OnPaint` 回调可能没有 PowerShell 默认运行空间，悬浮球样式不能再依赖 `Add_Paint` 脚本块自绘。
- 2026-06-04 PowerShell 版主消息循环从 `ShowDialog()` 改为 `Application.Run($form)`；否则启动时恢复到悬浮球并隐藏主窗会导致模态窗口返回、进程退出。
- 2026-06-05 Python/EXE 版悬浮球新增右上角迷你“拜拜”退出键：鼠标移入悬浮球显示、移出隐藏，左键命中退出键时调用现有 `on_close()` 关闭整个程序。
- 2026-06-05 Python/EXE 版打包补充 `platform` 导入和 PyInstaller `--hidden-import platform`，避免外置 `vendor\tkinterdnd2` 运行时导入 `platform` 失败。
- 2026-06-16 Python/EXE 与 PowerShell 版悬浮图标新增粘贴翻译：悬浮图标获得焦点后，`Ctrl+V` 或 `Shift+Insert` 读取剪贴板文本，并复用拖入文本的翻译流程显示气泡。
- 2026-06-16 Python/EXE 与 PowerShell 版悬浮图标新增翻译中动画：接收到拖入或粘贴文本后立即进入忙碌态，翻译完成、缓存命中、取消或报错后恢复默认样式。
- 2026-06-16 Python/EXE 版悬浮粘贴补强：悬浮模式下主窗口隐藏时绑定全局粘贴快捷键，并在创建悬浮按钮后主动聚焦 Canvas，避免快捷键没有落到悬浮球。
- 2026-06-16 PowerShell 版悬浮粘贴补强：按钮控件也绑定 `KeyDown`，鼠标进入时让按钮获取焦点，避免只有 Form 接收快捷键导致粘贴无响应。
