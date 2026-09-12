# 青语桌宠 3.0

Windows x64 / .NET Framework 4.8 / C# 5 / WPF。双击 build.cmd 编译，再运行 bin/QingyuPet.exe。
运行需要旁边的 voice/engine 和 voice/melo，可从便携包复制，或用 Python 3.12+ 运行 download-voice.py。下载固定官方归档并校验 SHA-256，不安装云端语音依赖。

## 结构

- QingyuPet.cs：偏好设置、WPF 工具、透明桌宠窗口。
- PetApp.cs / Program.cs：生命周期、设置迁移、托盘、情绪联动与入口。
- CompanionWindow.cs：互动、AI 聊天、语音/连接、外观四页。
- ChatService.cs / ChatProtocol.cs：TLS 1.2、模型列表、DeepSeek 名称纠正、SSE、元数据解析和动作白名单。
- VoiceService.cs：文本/音频两个异步队列、分句播放、取消、缓存、MediaPlayer 与音量包络。
- ResidentVoice.cs：常驻 sherpa C API、初始化预热、后台串行合成、温和语调处理。
- native/*Config.cs：对应 sherpa-onnx 1.13.7 的上游结构，改为 C# 5 工厂初始化并使用 UTF-8 字符串；版权保留。
- AnimatedRig.cs：18 个互动及三形象，原图表情贴片和新形象面部坐标驱动图形。
- assets/outfits：最终旗袍与赛博形象。弃用稿未打包。
- V3Tests.cs / ServiceTests.cs：模拟接口、原生界面、语音及密钥验证。

旧版 FocusSession 和专注控制窗口已移出 v3 运行代码；旧实现保留在 2.0 备份源码。

## 测试

用 Start-Process -Wait 等待 GUI 测试结束，例如：
Start-Process ./bin/QingyuPet.exe -ArgumentList '--v3-test --data-dir "C:/temp/qingyu-v3"' -Wait

--v3-test 检查模拟 SSE -> 实际聊天状态/动作、白名单、四页面、连接页滚动、服装 alpha、六种表情、缩放、常驻语音速度、静音两句流水播放与打断。
--services-test 检查错误返回、请求字段、取消、DPAPI 与实际语音合成。此项要求已加载 Windows 当前用户配置。
--playback-test 检查真实 MediaPlayer 和嘴部开合。
--smoke-test 走正式托盘/单实例启动路径，6 秒后退出；使用前先退出正式桌宠。

测试均可用独立 --data-dir，避免改动个人设置。测试工具没有内置真实 Key。实际 DeepSeek 验证只使用用户在桌宠中已保存的 Key，对其选择的官方服务做了模型列表和短句调用；Key 未记录在输出中。

## 说明

模型常驻以更多内存换取较短等待；两句队列并行生成和播放。Melo 本身没有本项目所需的原生情感控制，当前按情绪调整语速、轻微音高和文字节奏。不是逐音素口型，不是 Live2D。
远程 AI 为用户配置服务，SSE 首行元数据只选择内置动作，不执行任意指令。DeepSeek 默认 thinking.disabled；其他服务不强加该参数。对话上下文仅内存保存，音频缓存受上限约束。

## 文档来源

- [DeepSeek 官方调用说明](https://api-docs.deepseek.com/)
- [DeepSeek Chat Completions](https://api-docs.deepseek.com/api/create-chat-completion/)
- [DeepSeek 思考模式](https://api-docs.deepseek.com/guides/thinking_mode/)
- [sherpa-onnx C API](https://k2-fsa.github.io/sherpa/onnx/c-api/html/c-api_8h.html)
- [MeloTTS](https://github.com/myshell-ai/MeloTTS)

完整开源许可与上游对应源码位于 licenses 和 upstream-source，详见 THIRD-PARTY-NOTICES.md；形象生成提示词见 ART_PROMPT-v3.md。
