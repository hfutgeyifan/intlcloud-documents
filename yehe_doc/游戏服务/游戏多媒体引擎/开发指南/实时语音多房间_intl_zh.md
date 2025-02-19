为方便 Unity 开发者调试和接入腾讯云游戏多媒体引擎客户端 API，本文为您介绍适用于 Unity 实时语音多房间功能的开发接入流程指引。

## 使用 GME 重要事项

GME 提供实时语音服务、语音消息服务及转文本服务，使用 GME 服务都依赖 Init 和 Poll 等核心接口。多房间功能相比普通 GME 进房，有以下几点改动：

1. 使用实时语音多房间功能需要联系 GME 开发者获得该功能的 GME 版本 SDK。
2. 在 Init 前需要调用高级接口开启多房间功能。
3. 进房及房间内操作的接口需要使用 ITMGContext.GetSubInstance(“roomid”) 进行调用。
4. ITMGContext.GetSubInstance(“roomid”)  实例中的 roomid 代表要操作的房间。
5. 所有的回调统一在 OnEvent 事件中返回。
6. 多房间功能的计费方式请参考 [购买指南](https://intl.cloud.tencent.com/document/product/607/50009)。



## 接入 SDK

### 准备工作
- 已完成 GME 应用创建，并获取 SDK AppID 和 Key。请参考 [服务开通指引](https://intl.cloud.tencent.com/document/product/607/10782)。
- 已开通 **GME 实时语音服务、语音消息服务以及转文本服务**。请参考 [服务开通指引](https://intl.cloud.tencent.com/document/product/607/10782)。
- GME 使用前请对工程进行配置，否则 SDK 不生效。

### 注意事项
- GME 的接口调用成功后返回值为 QAVError.OK，数值为 0。
- GME 的接口调用要在同一个线程下。
- GME 需要周期性的调用 Poll 接口触发事件回调。
- 错误码详情可参考 <dx-tag-link link="https://intl.cloud.tencent.com/document/product/607/33223" tag="ErrorCode">错误码 </dx-tag-link>。

### 重要步骤

接入 SDK 重要流程如下：

<img src="https://qcloudimg.tencent-cloud.cn/raw/a69ce208fb05dd336ad6618264caf6c2.jpg"  width="70%" /></img>

<dx-steps>
-<dx-tag-link link="#Init" tag="接口：Init">初始化 GME</dx-tag-link>
-<dx-tag-link link="#Poll" tag="接口：Poll">周期性调用 Poll 触发回调</dx-tag-link>
-<dx-tag-link link="#EnterRoom" tag="接口：EnterRoom">进入实时语音房间</dx-tag-link>
-<dx-tag-link  tag="回调：QAVEnterRoomComplete">进房回调处理</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="接口：EnableMic">打开麦克风</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="接口：EnableSpeaker">打开扬声器</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="接口：ExitRoom">退出语音房间</dx-tag-link>
-<dx-tag-link link="#UnInit" tag="接口：UnInit">反初始化 GME</dx-tag-link>
</dx-steps>

### C# 类

| 类                  |        含义        |
| ------------------- | :----------------: |
| ITMGContext         |      核心接口      |
| ITMGRoom            |    房间相关接口    |
| ITMGRoomManager     |    房间管理接口    |
| ITMGAudioCtrl       |    音频相关接口    |
| ITMGAudioEffectCtrl | 音效及伴奏相关接口 |

## 核心接口

| 接口   |   接口含义   |
| ------ | :----------: |
| Init   |  初始化 GME  |
| Poll   | 触发事件回调 |
| Pause  |   系统暂停   |
| Resume |   系统恢复   |
| Uninit | 反初始化 GME |

### 引用头文件

```
using TencentMobileGaming;
```

### 获取实例

请使用 ITMGContext.GetInstance() 的方法获取 Context 实例，不要直接使用 QAVContext.GetInstance() 去获取实例。

当使用多房间功能的时候，需要通过 ITMGContext.GetSubInstance(sRoomID) 获取实例，不同的 Roomid 代表不同的实例，进入不同的房间。例如：获取 A 实例用于进入房间 A，并通过此实例打开在 A 房间中的麦克风扬声器；获取 B 实例用于进入房间 B，并通过此实例打开在 B 房间中的麦克风扬声器。

>!一个实例只能进去一个房间。例如 ITMGContext.GetSubInstance(“1”) 只能进去房间号码为 1 的房间。

### 使用多房间功能

使用多房间功能，需要在 Init 之前调用高级接口。

```
ITMGContext.GetInstance().SetAdvanceParams("enableMulRoom", "1");
```

### [初始化 SDK](id:Init)

未初始化前，SDK 处于未初始化阶段，**需要通过接口 Init 初始化 SDK**，才可以使用实时语音服务、语音消息服务及转文本服务。

#### 函数原型

```
//class ITMGContext
public abstract int Init(string sdkAppID, string openID);
```

| 参数     |  类型  | 含义                                                         |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | string | 来自 [腾讯云控制台](https://console.cloud.tencent.com/gamegme) 的 GME 服务提供的 AppID，获取方法请参考 [语音服务开通指引](https://intl.cloud.tencent.com/document/product/607/10782#.E9.87.8D.E7.82.B9.E5.8F.82.E6.95.B0)。 |
| openID   | string | openID 只支持 Int64 类型（转为 string 传入）。规则由 App 开发者自行制定，App 内不重复即可。 |

#### 返回值

| 返回值                          | 处理                                          |
| ------------------------------- | --------------------------------------------- |
| QAVError.OK= 0                  | 初始化 SDK 成功                               |
| AV_ERR_SDK_NOT_FULL_UPDATE=7015 | 检查 SDK 文件是否完整，建议删除后重新导入 SDK |

出现返回值 AV_ERR_SDK_NOT_FULL_UPDATE 时，此返回值**只有提示作用**，并不会造成初始化失败。

<dx-alert infotype="notice" title="关于7015错误提示">
<ul style="margin:0;">
<li> 7015错误码是通过 md5 进行判断，在接入过程中若出现此错误，请根据提示检查 SDK 文件是否完整、SDK 文件版本是否一致。</li>
<li> 由于第三方加固、Unity 打包机制等因素会影响库文件 md5，造成误判，所以<b>正式发布请在逻辑中忽略此错误</b>，并尽量不在 UI 中提示。</li>
</ul>
</dx-alert>

#### 示例代码 

```
int ret = ITMGContext.GetInstance().Init(sdkAppId, openID);
//通过返回值判断是否初始化成功
if (ret != QAVError.OK)
    {
        Debug.Log("SDK初始化失败:"+ret);
        return;
    }
```

<dx-alert infotype="notice" title="关于 Init 接口">
<ul style="margin:0;">
<li> 例如使用了实时语音服务，同时也需要使用语音消息服务，<b>只需要调用一次 Init 初始化接口</b>。</li>
<li> Init 之后不会开始计费，调用 <dx-tag-link link="#EnterRoom" tag="接口：EnterRoom">进入实时语音房间</dx-tag-link> 接口成功进入实时语音房间后才会开始计费。</li>
<li> 应用内用户同时进入两个房间，会累计用户在两个房间的时长进行计费。例如：若 A 用户在 12:00 时进入语音房间 X，同时在 12:00 时进入房间 Y，A 用户在 12:40 时同时离开2个房间房间，则语音时长合计为80分钟（A 用户在语音房间 X 40分钟，在语音房间 Y 40分钟）。</li>
<li> 初始化 SDK 之后才可以进入实时语音房间。</li>
<li> 调用 Init 接口的线程必须于其他接口在同一线程。建议都在主线程调用接口。</li>
</ul>
</dx-alert>

### [触发事件回调](id:Poll)

通过在 update 里面周期的调用 Poll 可以触发事件回调。Poll 是 GME 的消息泵，GME 需要周期性的调用 Poll 接口触发事件回调。如果没有调用 Poll ，将会导致整个 SDK 服务运行异常。详情请参见 [Sample Project](https://intl.cloud.tencent.com/document/product/607/18521)  中的 EnginePollHelper 文件。

<dx-alert infotype="alarm" title="务必周期性调用 Poll 接口">
务必周期性调用 Poll 接口且在主线程调用，以免接口回调异常。
</dx-alert>

#### 函数原型

```
ITMGContext public abstract int Poll();
```

#### 示例代码

```
public void Update()
    {
        ITMGContext.GetInstance().Poll();
    }
```

### 系统暂停

当系统发生 Pause 事件时，需要同时通知引擎进行 Pause。例如：在应用退后台时候（OnApplicationPause, isPause=True），如果不需要后台播放房间内声音，请调用 Pause 接口暂停整个 GME 服务。

#### 函数原型

```
ITMGContext public abstract int Pause()
```

### 系统恢复

当系统发生 Resume 事件时，需要同时通知引擎进行 Resume。Resume 接口只恢复实时语音。

#### 函数原型

```
ITMGContext  public abstract int Resume()
```

### [反初始化 SDK](id:UnInit)

反初始化 SDK，进入未初始化状态。**如果游戏业务侧账号与 openid 是绑定的，那切换游戏账号需要反初始化 GME，再用新的 openid 初始化**。

#### 函数原型

```
ITMGContext public abstract int Uninit()

```

## 实时语音房间相关接口

初始化之后，SDK 调用进房后进去了房间，才可以进行实时语音通话。
使用问题可参考 [实时语音相关问题](https://intl.cloud.tencent.com/document/product/607/39524)。

| 接口           |       接口含义       |
| -------------- | :------------------: |
| GenAuthBuffer  |      初始化鉴权      |
| EnterRoom      |       加入房间       |
| IsRoomEntered  |   是否已经进入房间   |
| ExitRoom       |       退出房间       |
| ChangeRoomType | 修改用户房间音频类型 |
| GetRoomType    | 获取用户房间音频类型 |

### 多房间调用流程图
<img src="https://qcloudimg.tencent-cloud.cn/raw/7e13766f5c8fcc2c314f650f67cee420.png" width="70%"/>


### 鉴权信息

生成 AuthBuffer，用于相关功能的加密和鉴权，如正式发布请使用后台部署密钥，后台部署请参考 [鉴权密钥](https://intl.cloud.tencent.com/document/product/607/12218)。    

#### 函数原型

```
QAVAuthBuffer GenAuthBuffer(int appId, string roomId, string openId, string key)
```

| 参数   |  类型  | 含义                                                         |
| ------ | :----: | ------------------------------------------------------------ |
| appId  |  int   | 来自腾讯云控制台的 AppID 号码。                              |
| roomId | string | 房间号，最大支持127字符。                                    |
| openId | string | 用户标识。与 Init 时候的 openID 相同。                       |
| key    | string | 来自腾讯云 [控制台](https://console.cloud.tencent.com/gamegme) 的权限密钥。 |

#### 示例代码  

```
public static byte[] GetAuthBuffer(string AppID, string RoomID,string OpenId, string AuthKey){
        return QAVAuthBuffer.GenAuthBuffer(int.Parse(AppID), RoomID, OpenId, AuthKey);
}

```

### [加入房间](id:EnterRoom)

请使用 GetSubInstance 调用接口，用生成的鉴权信息进房，加入房间默认不打开麦克风及扬声器。返回值为 AV_OK 的时候代表调用成功，不代表进房成功。

#### 函数原型

```
ITMGContext EnterRoom(string roomId, int roomType, byte[] authBuffer)

```

| 参数       |     类型     | 含义                                       |
| ---------- | :----------: | ------------------------------------------ |
| roomId     |    string    | 房间号，最大支持127字符                    |
| roomType   | ITMGRoomType | 只需填 ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY |
| authBuffer |    Byte[]    | 鉴权码                                     |

#### 示例代码  

```
//进入第一个房间
ITMGContext.GetSubInstance("room1").EnterRoom("room1", ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);
//进入第二个房间
ITMGContext.GetSubInstance("room2").EnterRoom("room2", ITMGRoomType.ITMG_ROOM_TYPE_FLUENCY, byteAuthbuffer);

```

### 加入房间事件的回调

加入房间完成后会通过 OnEvent 回调返回进房结果，结果中带有事件发生的房间号，可以通过房间号判读是哪个房间发生的事件，监听进房结果事件后进行处理。如果回调为成功，即此时进房成功，开始进行**计费**。

<dx-fold-block title="计费问题参考">
[多房间功能，如何计费？参考购买指南。](https://intl.cloud.tencent.com/document/product/607/50009)
[计费相关问题。](https://intl.cloud.tencent.com/document/product/607/30255)
[使用实时语音后，如果客户端掉线了，是否还会继续计费？](https://intl.cloud.tencent.com/document/product/607/30255#.E4.BD.BF.E7.94.A8.E5.AE.9E.E6.97.B6.E8.AF.AD.E9.9F.B3.E5.90.8E.EF.BC.8C.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E7.AB.AF.E6.8E.89.E7.BA.BF.E4.BA.86.EF.BC.8C.E6.98.AF.E5.90.A6.E8.BF.98.E4.BC.9A.E7.BB.A7.E7.BB.AD.E8.AE.A1.E8.B4.B9.EF.BC.9F)
</dx-fold-block>

#### 示例代码  

```
//对事件进行监听：
ITMGContext.GetInstance().onEventCallBack += new QAVOnEventCallBack(OnEvent);

//进房回调 JsonData 格式
string roomID = string.Empty;
JsonData root = JsonMapper.ToObject(data);
if (root != null && root.ContainsKey("roomID")) 

//处理监听
void OnEvent(int eventType, int subEventType, string data)
{
	string roomID = string.Empty;
	JsonData root = JsonMapper.ToObject(data);
	if (root != null && root.ContainsKey("roomID"))
	{
		if (root["roomID"] != null)
		{
			roomID = root["roomID"].ToString();
		}
	}
		
	switch (eventType)
	{
		case (int)ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
		{
			OnEnterRoomComplete(0, "");
		}
		break;
	}
}

```

#### Data 详情

| 消息                                 |        Data        | 例子                                                         |
| ------------------------------------ | :----------------: | ------------------------------------------------------------ |
| ITMG_MAIN_EVENT_TYPE_ENTER_ROOM      | result; error_info | {"error_info":"","result":0,"roomID":""}                     |
| ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT | result; error_info | {"error_info":"waiting timeout, please check your network","result":0} |

如果断网，将会有断网的回调提示 `ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_ROOM_DISCONNECT`，此时 SDK 会自动进行重连，回调是  `ITMG_MAIN_EVENT_TYPE_RECONNECT_START`，当重连成功时，会有 `ITMG_MAIN_EVENT_TYPE_RECONNECT_SUCCESS` 回调。

#### 错误码

| 错误码值 | 原因及建议方案                                               |
| -------- | ------------------------------------------------------------ |
| 7006     | 鉴权失败原因：<ul style="margin:0;"><li>AppID 不存在或者错误</li><li>authbuff 鉴权错误</li><li>鉴权过期 </li><li>OpenId 不符合规范</li></ul> |
| 7007     | 已经在其它房间                                               |
| 1001     | 已经在进房过程中，然后又重复了此操作。建议在进房回调返回之前不要再调用进房接口 |
| 1003     | 已经进房了在房间中，又调用一次进房接口                       |
| 1101     | 确保已经初始化 SDK，确保 OpenId 是否符合规则，或者确保在同一线程调用接口，以及确保 Poll 接口正常调用 |

### [退出房间](id:ExitRoom)

通过调用此接口可以退出所在房间。这是一个异步接口，返回值为 AV_OK 的时候代表异步投递成功。

如果应用中有退房后立即进房的场景，在接口调用流程上，开发者无需要等待 ExitRoom 的回调 RoomExitComplete 通知，只需直接调用接口。

#### 函数原型  

```
ITMGContext ExitRoom()

```

#### 示例代码  

```
ITMGContext.GetSubInstance("room1").ExitRoom();

```

### 退出房间回调

退出房间完成回调，通过委托传递消息。

#### 示例代码  

```
//对事件进行监听：
ITMGContext.GetInstance().onEventCallBack += new QAVOnEventCallBack(OnEvent);

//处理监听
void OnEvent(int eventType, int subEventType, string data)
{
	string roomID = string.Empty;
	JsonData root = JsonMapper.ToObject(data);
	if (root != null && root.ContainsKey("roomID"))
	{
		if (root["roomID"] != null)
		{
			roomID = root["roomID"].ToString();
		}
	}
		
	case (int)ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
	{
		if (mMulForbiddedMembers.ContainsKey(roomID))
		{
			mMulForbiddedMembers.Remove(roomID);
		}

		if (mMulSpeakingMembers.ContainsKey(roomID))
		{
			mMulSpeakingMembers.Remove(roomID);
		}
	}
	break;
}

```

### 成员进房、说话状态通知

此接口适用于获取房间中说话的人并在 UI 中展示，以及有人进入、退出语音房间的一个通知。

该事件在状态变化才通知，状态不变化的情况下不通知。如需实时获取成员状态，请在上层收到通知时缓存，事件消息为 ITMG_MAIN_EVNET_TYPE_USER_UPDATE，包含 event_id、count 及 openIdList，在 OnEvent 函数中对事件消息进行判断。
音频事件的通知有一个阈值，超过这个阈值才会发送通知。超过两秒没有收到音频包才通知“有成员停止发送音频包”消息。此事件只会返回成员说话事件，没有返回具体的音量。如需房间内成员具体音量可使用接口 GetVolumeById 进行获取。

| event_id                    |                          含义                           | 应用侧维护内容         |
| --------------------------- | :-----------------------------------------------------: | ---------------------- |
| EVENT_ID_ENDPOINT_ENTER     |         有成员进入房间，返回房间内所有的 openid         | 应用侧维护成员列表     |
| EVENT_ID_ENDPOINT_EXIT      |         有成员退出房间，返回房间内所有的 openid         | 应用侧维护成员列表     |
| EVENT_ID_ENDPOINT_HAS_AUDIO |     有成员发送音频包，返回房间内说话的所有的 openid     | 应用侧维护通话成员列表 |
| EVENT_ID_ENDPOINT_NO_AUDIO  | 有成员停止发送音频包，返回房间内停止说话的所有的 openid | 应用侧维护通话成员列表 |

#### 维护房间成员流程图

![](https://main.qcloudimg.com/raw/33eecfcd9e18a361aa0b732ffd0fb7dd.png)

#### 示例代码

```
//对事件进行监听：
ITMGContext.GetInstance().onEventCallBack += new QAVOnEventCallBack(OnEvent);

//处理监听
void OnEvent(int eventType, int subEventType, string data)
{
	string roomID = string.Empty;
	JsonData root = JsonMapper.ToObject(data);
	if (root != null && root.ContainsKey("roomID"))
	{
		if (root["roomID"] != null)
		{
			roomID = root["roomID"].ToString();
		}
	}
		
	case (int)ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_USER_UPDATE:
	{
		UserListInfo userListInfo = JsonUtility.FromJson<UserListInfo>(data);
		if (userListInfo.event_id == QAVContext.EVENT_ID_ENDPOINT_HAS_AUDIO)
		{
			foreach (string openId in userListInfo.user_list)
			{
				if (!mMulSpeakingMembers.ContainsKey(roomID))
                      {
					mMulSpeakingMembers.Add(roomID, new HashSet<string>());
				}
				mMulSpeakingMembers[roomID].Add(openId);
			}
		}
		else if (userListInfo.event_id == QAVContext.EVENT_ID_ENDPOINT_NO_AUDIO)
		{
			foreach (string openId in userListInfo.user_list)
			{
				if (mMulSpeakingMembers.ContainsKey(roomID)
					&& mMulSpeakingMembers[roomID]!= null
					&& mMulSpeakingMembers[roomID].Contains(openId))
				{
					mMulSpeakingMembers[roomID].Remove(openId);
				}
			}
		}
	}
	break;

}

```

### 房间中禁言

将某个 ID 加入音频数据黑名单，即不接受某人的语音， 只对本端生效，不会影响其他端。返回值为 0 表示调用成功。例如 ：A、B、C 都在同一个房间开麦说话： 

- 如果 A 设置了 C 的黑名单， 则 A 只能听见 B 的声音。
- B 因为没有设置黑名单， 仍旧可以听见 A 和 C 的声音。
- C 同样因为没有设置黑名单， 可以听见 A 和 B 的声音。

此接口适用于在语音房间中将某用户禁言的场景。

#### 函数原型  

```
ITMGContext ITMGAudioCtrl AddAudioBlackList(String openId)

```

| 参数   |  类型  | 含义                      |
| ------ | :----: | ------------------------- |
| openId | String | 需添加黑名单的用户 openid |

#### 示例代码  

```
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl ().AddAudioBlackList (openId);

```

### 移除禁言

将某个 ID 移除音频数据黑名单。返回值为0表示调用成功。

#### 函数原型  

```
ITMGContext ITMGAudioCtrl RemoveAudioBlackList(string openId)


```

| 参数   |  类型  | 含义                      |
| ------ | :----: | ------------------------- |
| openId | String | 需移除黑名单的用户 openid |

#### 示例代码  

```
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl ().RemoveAudioBlackList (openId);


```



## 实时语音采集相关接口

### [开启或关闭麦克风](id:EnableMic)

此接口用来开启关闭麦克风。加入房间默认不打开麦克风及扬声器。

**EnableMic = EnableAudioCaptureDevice + EnableAudioSend**

#### 函数原型  

```
ITMGAudioCtrl EnableMic(bool isEnabled)
```

| 参数      |  类型   | 含义                                                         |
| --------- | :-----: | ------------------------------------------------------------ |
| isEnabled | boolean | 如果需要打开麦克风，则传入的参数为 true，如果关闭麦克风，则参数为 false |

#### 示例代码  

```
//打开麦克风
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().EnableMic(true);
```

### 麦克风状态获取

此接口用于获取麦克风状态，返回值0为关闭麦克风状态，返回值1为打开麦克风状态。

#### 函数原型  

```
ITMGAudioCtrl GetMicState()
```

#### 示例代码  

```
micToggle.isOn = ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().GetMicState();
```

### 开启或关闭采集设备

此接口用来开启/关闭采集设备。加入房间默认不打开设备。

- 只能在进房后调用此接口，退房会自动关闭设备。
- 在移动端，打开采集设备通常会伴随权限申请，音量类型调整等操作。

#### 函数原型  

```
ITMGAudioCtrl int EnableAudioCaptureDevice(bool isEnabled)


```

| 参数      | 类型 | 含义                                                         |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | 如果需要打开采集设备，则传入的参数为 true，如果关闭采集设备，则参数为 false |

#### 示例代码

```
//打开采集设备
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().EnableAudioCaptureDevice(true);


```

### 采集设备状态获取

此接口用于采集设备状态获取。

#### 函数原型

```
ITMGAudioCtrl bool IsAudioCaptureDeviceEnabled()


```

#### 示例代码

```
bool IsAudioCaptureDevice = ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().IsAudioCaptureDeviceEnabled();


```

### 打开或关闭音频上行

此接口用于打开/关闭音频上行。如果采集设备已经打开，那么会发送采集到的音频数据。如果采集设备没有打开，那么仍旧无声。采集设备的打开关闭请参见接口 EnableAudioCaptureDevice。

#### 函数原型

```
ITMGAudioCtrl int EnableAudioSend(bool isEnabled)


```

| 参数      | 类型 | 含义                                                         |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | 如果需要打开音频上行，则传入的参数为 true，如果关闭音频上行，则参数为 false |

#### 示例代码  

```
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().EnableAudioSend(true);


```

### 音频上行状态获取

此接口用于音频上行状态获取。

#### 函数原型  

```
ITMGAudioCtrl bool IsAudioSendEnabled()


```

#### 示例代码  

```
bool IsAudioSend = ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().IsAudioSendEnabled();


```

### 获取麦克风实时音量

此接口用于获取麦克风实时音量，返回值为 int 类型。建议20ms获取一次。值域为0 - 100，通过此接口可以获取到麦克风采集到的实时音量情况。

**此接口不适用于语音消息服务。**

#### 函数原型  

```
ITMGAudioCtrl int GetMicLevel


```

#### 示例代码  

```
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().GetMicLevel();


```

### 获取音频上行实时音量

此接口用于获取自己音频上行实时音量，返回值为 int 类型，取值范围为0 - 100。

**此接口不适用于语音消息服务。**

#### 函数原型  

```
ITMGAudioCtrl int GetSendStreamLevel()
```

#### 示例代码  

```
int Level = ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().GetSendStreamLevel();
```

### 设置麦克风软件音量

此接口用于设置麦克风的音量。参数 volume 用于设置麦克风的音量，相当于对采集的声音做衰减或增益，当数值为0的时候表示静音，当数值为100的时候表示音量不增不减，默认数值为100。

**此接口不适用于语音消息服务。**

#### 函数原型  

```
ITMGAudioCtrl SetMicVolume(int volume)
```

| 参数   | 类型 | 含义                  |
| ------ | :--: | --------------------- |
| volume | int  | 设置音量，范围0 - 200 |

#### 示例代码  

```
int micVol = (int)(value * 100);
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().SetMicVolume (micVol);
```

### 获取麦克风软件音量

此接口用于获取麦克风的音量。返回值为一个int类型数值，返回值为101代表没调用过接口 SetMicVolume。

**此接口不适用于语音消息服务。**

#### 函数原型  

```
ITMGAudioCtrl GetMicVolume()
```

#### 示例代码  

```
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().GetMicVolume();
```

## 实时语音播放相关接口

### [开启或关闭扬声器](id:EnableSpeaker)

此接口用于开启关闭扬声器。
**如果有使用伴奏的情况，请参考 [实时语音伴奏流程图](https://intl.cloud.tencent.com/document/product/607/31504) 进行调用。**

**EnableSpeaker = EnableAudioPlayDevice +  EnableAudioRecv**

#### 函数原型  

```
ITMGAudioCtrl EnableSpeaker(bool isEnabled)
```

| 参数      | 类型 | 含义                                                         |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | 如果需要关闭扬声器，则传入的参数为 false，如果打开扬声器，则参数为 true |

#### 示例代码  

```
//打开扬声器
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().EnableSpeaker(true);
```

### 扬声器状态获取

此接口用于扬声器状态获取。返回值0为关闭扬声器状态，返回值1为打开扬声器状态。

#### 函数原型  

```
ITMGAudioCtrl GetSpeakerState()
```

#### 示例代码  

```
speakerToggle.isOn = ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().GetSpeakerState();
```



### 开启或关闭播放设备

此接口用于开启关闭播放设备。

#### 函数原型  

```
ITMGAudioCtrl EnableAudioPlayDevice(bool isEnabled)
```

| 参数      | 类型 | 含义                                                         |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | 如果需要关闭播放设备，则传入的参数为 false，如果打开播放设备，则参数为 true |

#### 示例代码  

```
//打开播放设备
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().EnableAudioPlayDevice(true);
```

### 播放设备状态获取

此接口用于播放设备状态获取。

#### 函数原型

```
ITMGAudioCtrl bool IsAudioPlayDeviceEnabled()
```

#### 示例代码  

```
bool IsAudioPlayDevice = ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().IsAudioPlayDeviceEnabled();
```

### 打开或关闭音频下行

此接口用于打开/关闭音频下行。如果播放设备已经打开，那么会播放房间里其他人的音频数据。如果播放设备没有打开，那么仍旧无声。播放设备的打开关闭参见接口请参见 EnableAudioPlayDevice。

#### 函数原型  

```
ITMGAudioCtrl int EnableAudioRecv(bool isEnabled)
```

| 参数      | 类型 | 含义                                                         |
| --------- | :--: | ------------------------------------------------------------ |
| isEnabled | bool | 如果需要打开音频下行，则传入的参数为 true，如果关闭音频下行，则参数为 false |

#### 示例代码  

```
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().EnableAudioRecv(true);
```



### 音频下行状态获取

此接口用于音频下行状态获取。

#### 函数原型  

```
ITMGAudioCtrl bool IsAudioRecvEnabled()
```

#### 示例代码  

```
bool IsAudioRecv = ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().IsAudioRecvEnabled();
```

### 获取扬声器实时音量

此接口用于获取扬声器实时音量。返回值为 int 类型数值，表示扬声器实时音量。建议20ms获取一次。

#### 函数原型  

```
ITMGAudioCtrl GetSpeakerLevel()
```

#### 示例代码  

```
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().GetSpeakerLevel();
```

### 获取房间内其他成员下行实时音量

此接口用于获取房间内其他成员下行实时音量，返回值为 int 类型，取值范围为0 - 200。

#### 函数原型  

```
ITMGAudioCtrl int GetRecvStreamLevel(string openId)
```

| 参数   |  类型  | 含义                  |
| ------ | :----: | --------------------- |
| openId | string | 房间其他成员的 openId |

#### 示例代码  

```
int Level = ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().GetRecvStreamLevel(openId);
```

### 设置扬声器的音量

此接口用于设置扬声器的音量。
参数 volume 用于设置扬声器的音量，当数值为0时，表示静音，当数值为100时，表示音量不增不减，默认数值为100。

#### 函数原型  

```
ITMGAudioCtrl SetSpeakerVolume(int volume)
```

| 参数   | 类型 | 含义                  |
| ------ | :--: | --------------------- |
| volume | int  | 设置音量，范围0 - 200 |

#### 示例代码  

```
int speVol = (int)(value * 100);
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().SetSpeakerVolume(speVol);
```

### 获取扬声器的音量

此接口用于获取扬声器的音量。返回值为 int 类型数值，代表扬声器的音量，返回值为101代表没调用过接口 SetSpeakerVolume。
Level 是实时音量，Volume 是扬声器的音量，最终声音音量 =  Level × Volume %。例如实时音量是数值是100，此时 Volume 的数值是60，那么最终发出来的声音数值也是60。

#### 函数原型  

```
ITMGAudioCtrl GetSpeakerVolume()
```

#### 示例代码  

```
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().GetSpeakerVolume();
```



## 高级 API

### 启动耳返

此接口用于启动耳返，需要 EnableLoopBack+EnableSpeaker 才可以听到自己声音。

#### 函数原型  

```
ITMGContext GetAudioCtrl EnableLoopBack(bool enable)
```

| 参数   | 类型 | 含义         |
| ------ | :--: | ------------ |
| enable | bool | 设置是否启动 |

#### 示例代码  

```
ITMGContext.GetSubInstance(sRoomID).GetAudioCtrl().EnableLoopBack(true);
```

### 房间通话质量监控事件

质量监控事件，在进房后触发，2秒回调一次，事件消息为 ITMG_MAIN_EVENT_TYPE_CHANGE_ROOM_QUALITY，返回的参数为 weight、loss 及 delay，代表的信息如下，在 OnEvent 函数中对事件消息进行判断。

此接口适用于监听网络质量，如果用户网络差的话，业务层将通过 UI 提醒用户切换网络。

| 参数   | 类型   | 含义                                                         |
| ------ | ------ | ------------------------------------------------------------ |
| weight | int    | 范围是1 - 50，数值为50是音质评分极好，数值为1是音质评分很差，几乎不能使用，数值为0代表初始值，无含义。一般数值在30以下就可以提醒用户网络较差，建议切换网络。 |
| loss   | double | 上行丢包率。                                                 |
| delay  | int    | 音频触达延迟时间（ms）。                                     |

### 获取版本号

获取 SDK 版本号，用于分析。

#### 函数原型

```
ITMGContext  abstract string GetSDKVersion()
```

#### 示例代码  

```
ITMGContext.GetInstance().GetSDKVersion();
```





### 设置打印日志等级

用于设置打印日志等级。建议保持默认等级。需要在 Init 之前调用。

#### 函数原型

```
ITMGContext  SetLogLevel(ITMG_LOG_LEVEL levelWrite, ITMG_LOG_LEVEL levelPrint)
```

#### 参数含义

| 参数       | 类型           | 含义                                                         |
| ---------- | -------------- | ------------------------------------------------------------ |
| levelWrite | ITMG_LOG_LEVEL | 设置写入日志的等级，TMG_LOG_LEVEL_NONE 表示不写入，默认为 TMG_LOG_LEVEL_INFO |
| levelPrint | ITMG_LOG_LEVEL | 设置打印日志的等级，TMG_LOG_LEVEL_NONE 表示不打印，默认为 TMG_LOG_LEVEL_ERROR |

TMG_LOG_LEVEL_NONE 说明：

| ITMG_LOG_LEVEL        | 含义                 |
| --------------------- | -------------------- |
| TMG_LOG_LEVEL_NONE    | 不打印日志           |
| TMG_LOG_LEVEL_ERROR   | 打印错误日志（默认） |
| TMG_LOG_LEVEL_INFO    | 打印提示日志         |
| TMG_LOG_LEVEL_DEBUG   | 打印开发调试日志     |
| TMG_LOG_LEVEL_VERBOSE | 打印高频日志         |

#### 示例代码  

```
ITMGContext.GetInstance().SetLogLevel(TMG_LOG_LEVEL_INFO,TMG_LOG_LEVEL_INFO);

```



### 设置打印日志路径

用于设置打印日志路径。默认路径如下。需要在 Init 之前调用。

| 平台    | 路径                                                         |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName                            |
| iOS     | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents   |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files                       |
| Mac     | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |

#### 函数原型

```
ITMGContext  SetLogPath(string logDir)

```

| 参数   |  类型  | 含义 |
| ------ | :----: | ---- |
| logDir | String | 路径 |

#### 示例代码  

```
ITMGContext.GetInstance().SetLogPath(path);

```

### 获取诊断信息

获取音视频通话的实时通话质量的相关信息。该接口主要用来查看实时通话质量、排查问题等，业务侧可以忽略。

#### 函数原型  

```
ITMGRoom GetQualityTips()

```

#### 示例代码  

```
string tips = ITMGContext.GetInstance().GetRoom().GetQualityTips();

```
