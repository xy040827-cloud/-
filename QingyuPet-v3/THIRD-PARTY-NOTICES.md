# 青语 3.0 开源组件与来源

语音在本机合成。未加入游戏台词音频、真人克隆声音或有未核实来源的商业语音包。所列许可分别适用于各自上游组件，不将整个语音依赖概括为单一 MIT 或 Apache 许可。

| 组件 | 来源及版本 | 许可文件 |
| --- | --- | --- |
| MeloTTS 中文 ONNX 模型、词典及规则 | MyShell.ai；sherpa 官方 tts-models 发布的 vits-melo-tts-zh_en | licenses/MELO-LICENSE.txt，MIT；模型目录也保留 LICENSE |
| sherpa-onnx 原生 C API | k2-fsa/sherpa-onnx v1.13.7，Windows x64 shared MT Release | licenses/SHERPA-LICENSE.txt，Apache-2.0 |
| ONNX Runtime | Microsoft v1.27.1，来自上述官方 Windows 压缩包 | licenses/ONNXRUNTIME-LICENSE.txt，MIT；第三方声明见同目录 ThirdPartyNotices |
| eSpeak NG for Piper | csukuangfj/espeak-ng ed530aa113046142eb5115cf2fc9157854d0ffe1 | licenses/ESPEAK-NG-COPYING.txt，GPL-3.0；该依赖随 sherpa TTS 构建链接，Melo 采用自身词典 |
| piper-phonemize | csukuangfj/piper-phonemize f3ff95afc03640bc1399e113e83361192a2fafb4 | licenses/PIPER-PHONEMIZE-LICENSE.txt，MIT；保留 uni-algo 许可 |
| Kaldi decoder / native fbank | v0.3.0 / v1.22.3，sherpa 构建依赖 | licenses/KALDI-*-LICENSE.txt，Apache-2.0 |
| simple-sentencepiece | pkufool v0.7 | licenses/SENTENCEPIECE-LICENSE.txt，Apache-2.0 |
| nlohmann JSON | v3.12.0 | licenses/JSON-LICENSE.txt，MIT |

上游地址：

- https://github.com/myshell-ai/MeloTTS
- https://github.com/k2-fsa/sherpa-onnx/tree/v1.13.7
- https://k2-fsa.github.io/sherpa/onnx/tts/pretrained_models/vits.html
- https://github.com/microsoft/onnxruntime/tree/v1.27.1
- https://github.com/csukuangfj/espeak-ng/tree/ed530aa113046142eb5115cf2fc9157854d0ffe1
- https://github.com/csukuangfj/piper-phonemize/tree/f3ff95afc03640bc1399e113e83361192a2fafb4

下载归档的原始 URL 与 SHA-256 见 voice/DOWNLOADS.json；其他许可证与源代码下载记录见 licenses/sources.json。程序未修改上游 DLL 或模型。3.0 通过常驻原生 C API 调用 TTS；native 配置结构从上游 scripts/dotnet 改为 C# 5 工厂初始化，并使用 UTF-8 字符串封送。

对应源代码压缩包保留在 upstream-source：sherpa-onnx v1.13.7、eSpeak NG 固定提交、piper-phonemize 固定提交。sherpa 源码中的 CMakeLists.txt、cmake/*.cmake、cmake/download-all-deps.py 和 .github/workflows 保留原有构建说明、依赖 URL 与固定校验值，可用于获取其余依赖并重建上游工具。各上游源码包含自己的版权声明；重新分发请同时保留这些文件。

桌宠自身源码在单独的“青语桌宠-3.0-源码.zip”中，运行不需要源码压缩包。AI 生成角色图及表达素材的来源记录见该源码包的 ART_PROMPT*.md。青语不是 OpenAI 官方产品。
