## Unity3D语音文档

##### 1.下载SDK
 1.[下载Unity3D SDK包 版本：1.0.0](http://cdn.mztgame.ztgame.com.cn/gavoice_rtchat/resource_zip/GiantSDK_Voice_2.8.2.zip)

2.双击GiantSDK_Voice_1.0.0.unitypackage导入
或则直接复制 Unity3D/ 下内容到 Assets/下


##### 2.系统配置  
   1.在iOS ／android, Player setting 设置宏（RTCHAT_ENABLE）开关，否则无法调用语音功能。
   ![](http://cdn.mztgame.ztgame.com.cn/gavoice_rtchat/resource_img/gavoice_hong.png)

   2.初始化接口，注册回调事件接口，只能执行一次，使用状态值判定 或 是放至单例脚本的Awake或Start函数中.
   示例
   ```
   public static bool isStart = false;
   void Start()
   {
       if (!isStart)
       {
           isStart = true;
           GiantVoiceManager.OnPlayOverComplete += (int retCode) =>
                  {
                      Debug.Log(" startplayFinishResult  In C# Client re = " + retCode);
                  };
       }
   }
   ```
   3.**接口需要主线程调用。**

##### 3.基本API

###### 3.1初始化接口


  *1.接口说明  *

  初始化SDK,在其他接口之前调用。

 *2.函数原型 *

   ```
   //初始化sdk(appid ,appkey 可以联系我们，serverurl,xif,customip)
    void InitGASDK (string appId, string appKey, string  userId, string serverUrl, string xfid,string customip)

   ```
| 参数        | 类型           | 意义   |
| ------------- |:-------------:| -----:|
| appId      | string | 应用标识,可以联系我们申请 |
| appKey     | string      |   应用标识,可以联系我们申请|
| userId     | string      |   用户标识|
| serverUrl | string     |  录音上传地址 |
| xfid | string     |    录音ID(Android 和iOS 会不一样) |
| customip | string     |  自定义实时语音地址 |

*3.示例代码*
```
GiantVoiceManager.Instance.InitGASDK (appid, appKey, userId,uploadserver,"58536195","192.168.1.1:8081");
```

###### 3.2加入房间接口


  *1.接口说明  *

   实时语音，加入房间

 *2.函数原型 *

   ```
   //进入房间（roomid:房间id，cb加入房间回调）
  void JoinRoom (string roomId)；


   ```
| 参数        | 类型           | 意义   |
| ------------- |:-------------:| -----:|
| roomId      | string | 房间号 |
| retCode      | int |加入房间状态：1成功，0失败 |



*3.示例代码*
```
GiantVoiceManager.Instance.JoinRoom (roomidValue);


```
###### 3.3退出房间接口


  *1.接口说明  *

   实时语音，退出房间

 *2.函数原型 *

   ```
  //退出房间（roomid:房间id，cb加入房间回调）
  void QuitRoom ()；

   ```


*3.示例代码*
```
GiantVoiceManager.Instance.QuitRoom ();

```

###### 3.4关闭扬声器


  *1.接口说明  *

   实时语音，关闭扬声器

 *2.函数原型 *

   ```
   //关闭扬声器外放功能
    void CloseLoudSpeaker ()

   ```

*3.示例代码*
```
GiantVoiceManager.Instance.CloseLoudSpeaker ();

```
###### 3.5打开扬声器


  *1.接口说明  *

   实时语音，打开扬声器

 *2.函数原型 *

   ```
   //打开扬声器外放功能
    void OpenLoudSpeaker ()

   ```

*3.示例代码*
```
GiantVoiceManager.Instance.OpenLoudSpeaker ();

```
###### 3.6打开麦克风


  *1.接口说明  *

   实时语音，打开麦克风

 *2.函数原型 *

   ```
   //打开麦克风
    void OpenMic ()

   ```

*3.示例代码*
```
GiantVoiceManager.Instance.OpenMic ();

```
###### 3.6关闭麦克风


  *1.接口说明  *

   实时语音，关闭麦克风

 *2.函数原型 *

   ```
   //关闭麦克风
    void CloseMic ()

   ```

*3.示例代码*
```
GiantVoiceManager.Instance.CloseMic ();

```
###### 3.7 设置语音外放音量调节


  *1.接口说明  *

   实时语音，设置语音波形外放（默认系统音量）

 *2.函数原型 *

   ```
   //设置语音外放音量调节（取值范围为0-10的整数，最大值请根据回音情况做调节）
   public void SpeakerVolum (float volume)；

   ```
   | 参数        | 类型           | 意义   |
   | ------------- |:-------------:| -----:|
   | volume     | float      |   音量调节，范围（0，10）|


*3.示例代码*
```
GiantVoiceManager.Instance.SpeakerVolum (4.0);

```
---
###### 3.8 开始录制语音消息


  *1.接口说明  *

   语音消息，开始录制语音消息

 *2.函数原型 *

   ```
   //开始录制语音消息（true 需要， false 不需要）
    void StartRecordVoice (bool needConvertWord)；

   ```
   | 参数        | 类型           | 意义   |
   | ------------- |:-------------:| -----:|
   | needConvertWord     | bool      |   是否需要翻译为文字 true 需要， false 不需要|


*3.示例代码*
```
GiantVoiceManager.Instance.StartRecordVoice (true);

```
###### 3.9 停止录制语音消息


  *1.接口说明  *

   语音消息，停止录制语音消息

 *2.函数原型 *

   ```
   //停止录制语音消息（录制回调）
   void StopRecordVoice ()

   ```


*3.示例代码*
```
GiantVoiceManager.Instance.StopRecordVoice ();

```
###### 3.10 播放录制语音消息


  *1.接口说明  *

   语音消息，播放录制语音消息

 *2.函数原型 *

   ```
   //播放录制语音消息
   void StartPlayVoice (string voiceUrl)；

   ```
   | 参数        | 类型           | 意义   |
   | ------------- |:-------------:| -----:|
   | voiceUrl     | string      |   语音上传地址 （录音完成回调 取得）|


*3.示例代码*
```
GiantVoiceManager.Instance.StartPlayVoice ("http://xxxxxxx");

```
###### 3.11 取消录制语音消息


  *1.接口说明  *

   语音消息，取消录制语音消息

 *2.函数原型 *

   ```
   //取消录制语音消息
   void CancelRecordVoice ()；
  ```

*3.示例代码*
```
GiantVoiceManager.Instance.CancelRecordVoice ();

```
###### 3.11 停止播放语音消息


  *1.接口说明  *

   语音消息，停止播放语音消息

 *3.函数原型 *

   ```
   //停止播放语音消息
   void StopPlayVoice ()；
  ```

*3.示例代码*
```
GiantVoiceManager.Instance.StopPlayVoice ();

```
###### 3.12 设置用户消息


  *1.接口说明  *

   语音消息，设置用户消息

 *2.函数原型 *

   ```
   //停止播放语音消息
  public void SetUserInfo (string username, string userkey)；
  ```
  | 参数        | 类型           | 意义   |
  | ------------- |:-------------:| -----:|
  | username     | string      |   用户名|
  | userkey     | string      |   可为空|


*3.示例代码*
```
GiantVoiceManager.Instance.SetUserInfo ("username","");

```
###### 3.13 加入房间回调
*1.接口说明  *

  加入房间回调接口

*2.函数原型 *

 ```
 //回调
 public delegate void JoinRoomCompleteHandler (int retCode);
```
| 参数        | 类型           | 意义   |
| ------------- |:-------------:| -----:|
| retCode      | int |加入房间状态：1成功，0失败 |

*3.示例代码*
```
GiantVoiceManager.OnJoinRoomComplete += (int retCode) =>
{
    Debug.Log(" joinroomResult  In C# Client re = " + retCode);
};

```
###### 3.14 退出房间回调
*1.接口说明  *

  退出房间回调

*2.函数原型 *

 ```
 //回调
 public delegate void QuitRoomCompleteHandler (int retCode);
```
| 参数        | 类型           | 意义   |
| ------------- |:-------------:| -----:|
| retCode      | int |加入房间状态：1成功，0失败 |

*3.示例代码*
```
GiantVoiceManager.OnQuitRoomComplete += (int retCode) =>
        {
            Debug.Log(" quitroomResult  In C# Client re = " + retCode);
        };

```
###### 3.15 播放完成回调
*1.接口说明  *

  播放完成回调

*2.函数原型 *

 ```
 //回调
 public delegate void PlayFinishCompleteHandler (int retCode);
```
| 参数        | 类型           | 意义   |
| ------------- |:-------------:| -----:|
| retCode      | int |加入房间状态：1成功，0失败 |

*3.示例代码*
```
GiantVoiceManager.OnPlayOverComplete += (int retCode) =>
       {
           Debug.Log(" startplayFinishResult  In C# Client re = " + retCode);
       };

```
###### 3.16 录制完成回调
*1.接口说明  *

  录制完成回调

*2.函数原型 *

 ```
 //回调
 public delegate void VoiceRecordCompleteHandler (int retCode, string url, string text,float duration);

```
| 参数        | 类型           | 意义   |
| ------------- |:-------------:| -----:|
| retCode     | int      |   停止录制状态 1 成功， 0 失败|
| url     | string      |   语音上传地址|
| text     | string      |   翻译的文字|
| duration     | float      |   语音时间长度|

*3.示例代码*
```
GiantVoiceManager.OnVoiceRecordComplete += (int retCode, string url, string text, float duration) =>
       {
           Debug.Log(" voiceRecordResult  In C# Client re = " + retCode + ",url = " + url + ",duration = " + duration);
           if (url != null)
           {
               voiceRecordUrl = url;
           }
       };


```
