### 语音识别如何接入？
语音识别目前支持 API 和 SDK 接入，推荐 SDK 接入，详情可参见 [一分钟接入服务端 API](https://intl.cloud.tencent.com/document/product/1118/43356) 和 [ 一分钟跑通集成 SDK](https://intl.cloud.tencent.com/document/product/1118/43382)。

### 语音识别怎么进行功能体验？
可通过微信搜索“腾讯云 AI 语音”小程序，选择语音识别进行体验。也可在 [语音识别控制台](https://console.cloud.tencent.com/asr) 功能体验模块，通过上传文件或者 URL 进行体验。详情可参考 [体验功能](https://intl.cloud.tencent.com/document/product/1118/43359)。

### 语音识别控制台功能体验怎样上传大于 5M 的文件？
可在 [语音识别控制台-功能体验](https://console.cloud.tencent.com/asr/demonstrate) 中采用上传音频 URL 方式上传体验，**建议音频时长不能大于五个小时**。

### 不同使用场景对应的是语音识别哪种服务？
- 实时语音识别适用于有实时性要求的场景，例如语音输入、语音机器人、会议现场记录等场景。
- 一句话识别适用于对60秒之内的短音频文件进行识别的场景，例如语音短信、语音搜索等场景。
- 录音文件识别适用于语音时间较长、实时性要求低的场景，例如客服质检、视频字幕生成等场景。

### 支持远场和离线的语音识别吗？
录音文件识别、一句话识别和实时语音识别暂时不支持远场和离线的语音识别。

### 语音识别支持中英文混合场景和地方方言吗？
- 普通话引擎支持单词级别的中英文混合识别，且支持带口音的中文普通话语音识别。
- 实时语音识别支持中文普通话、英文、粤语、韩语、日语、泰语和上海话方言的识别。
- 一句话识别和录音文件识别支持中文普通话、英文、粤语、日语和上海话方言的识别。

>?若有四川话、南京话、南昌话及更多方言需求，可填写 [表单](https://cloud.tencent.com/apply/p/75h8nunsh9) 申请。

### 语音识别的支持的输入音频时长是多少？
- 一句话识别每次调用支持60秒之内的音频。
- 录音文件识别每次调用支持五小时之内的音频。
- 实时语音音频流中每个数据包的音频分片为200ms。

### 语音识别接口的 HTTP 请求返回鉴权失败？
请用户对照参数表检查自己的参数是否正确上传。如果想快速接入，推荐使用官网提供的 SDK。

### 语音识别接口会限制音频文件的采样率吗？
接口不会限制，但是采样率不符合标准，会影响到识别效果。

