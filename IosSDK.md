## Ios集成文档

工程配置:
####
	1.导入全部静态库和thirdpard目录下的文件到xcode工程。导入include文件夹下的头文件到xcode源码目录。
	2.确认工程的Build Settings->Other Linker Flags下有-ObjC配置，如无请自行添加
	注:请在Build Phases下检查是否有增加了如下静态链接库，如无请添加
####

<img src="http://cdn.mztgame.ztgame.com.cn/gavoice_rtchat/resource_img/iso1.png" width="430">

####
	检查录音和使用摄像头权限，请在info.plist文件中添加如下两个键值，
	Privacy – Microphone Usage Description
	Privacy – Camera Usage Description


接口使用

	1.注册消息回调(主线程), MsgCallBackFunc函数定义见头文件
    void registerMsgCallback(const MsgCallBackFunc& func);

	2.sdk初始化，只能调用一次, appid,appkey从官方网站注册获取
    SdkErrorCode initSDK(const char* appid, const char* key);

	3.设置IM上传地址参数，如需使用IM翻译成文字模块还需输入从讯飞官方网站注册的appid
    void setParams(const char* voiceUploadUrl, const char* xunfeiAppID);

	4.设置房间平台连接地址，地址从官方网站获取
	void customRoomServerAddr(const char* roomServerAddr);

	5.设置聊天登录用户信息，请自行保证带入用户名的唯一性，userkey目前可以输入””
    SdkErrorCode setUserInfo(const char* username, const char* userkey);

####

####
IM消息模块部分接口

	1.开始录制麦克风数据(主线程), needConvertWord为true表示录音完成后自动翻译为文字返回给应用层
    SdkErrorCode startRecordVoice(bool needConvertWord = false);
	
	2.停止录制麦克风数据(主线程)
    SdkErrorCode stopRecordVoice();

	3.取消当前录音
    SdkErrorCode cancelRecordedVoice();

	4.开始播放录制数据(主线程)
    SdkErrorCode startPlayLocalVoice(const char* voiceUrl);
    
    5.停止播放数据(主线程)
    SdkErrorCode stopPlayLocalVoice();

####

####
实时语音模块部分接口

	1.加入房间(主线程), roomid为任意32位长度字母数字组合字符串，需进入同一房间聊天的用户请使用相同的roomid登入, enMediaType见头文件定义说明
    SdkErrorCode requestJoinPlatformRoom(const char* roomid_p, enMediaType meida_type = kVoiceOnly);

	2.向平台请求退出房间(主线程)
    SdkErrorCode requestLeavePlatformRoom();

	3.调整通道外放音量(主线程)(0.0f-10.0f)
    SdkErrorCode adjustSpeakerVolume(float volume);
    
    4.设置是否用外放扬声器，该接口仅在收到进入房间成功回调后调用有效
    SdkErrorCode setLoudSpeaker(bool enable);


####