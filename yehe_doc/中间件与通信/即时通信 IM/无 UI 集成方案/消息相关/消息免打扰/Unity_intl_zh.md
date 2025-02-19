## 功能描述
通过设置**单聊和群聊**的消息接收选项，可以实现消息免打扰的功能。
IM SDK 支持三种类型的消息接收选项，消息接收选项在 `TIMReceiveMessageOpt` 中定义：

| 消息接收选项                                    | 功能描述                                     |
| ----------------------------------------------- | -------------------------------------------- |
| TIMReceiveMessageOpt.kTIMRecvMsgOpt_Receive     | 在线时正常接收消息，离线时接收离线推送通知   |
| TIMReceiveMessageOpt.kTIMRecvMsgOpt_Not_Receive | 在线和离线都不接收消息                       |
| TIMReceiveMessageOpt.kTIMRecvMsgOpt_Not_Notify  | 在线时正常接收消息，离线时不接收离线推送通知 |

使用不同的 `TIMReceiveMessageOpt` 可以实现群消息免打扰：
**完全不接收消息**
消息接收选项设置为 `kTIMRecvMsgOpt_Not_Receive` 后，单聊/群聊的任何消息都收不到，会话列表也不会更新。

**接收消息但不提醒，在会话列表界面显示小圆点（不显示未读数）**
1. 消息接收选项设置为 `kTIMRecvMsgOpt_Not_Notify`。
2. 当单聊/群聊收到新消息，会话列表需要更新时，可以通过设置会话未读消息总数变更的回调 `SetConvTotalUnreadMessageCountChangedCallback` 中的 `total_unread_count` ([Details](https://comm.qq.com/im/doc/unity/en/callback/ConvTotalUnreadMessageCountChangedCallback.html)) 获取到消息未读数。
3. 根据 `ConvInfo` 的 `conv_recv_opt` ([Details](https://comm.qq.com/im/doc/unity/en/types/ConvAttributes/ConvInfo.html)) 判断获取到的消息接收选项为 `kTIMRecvMsgOpt_Not_Notify` 时显示小红点而非消息未读数。

> ? 此方式需使用未读计数功能，因此仅适用于好友工作群（Work）和陌生人社交群（Public）。群组类型详见 群组介绍。


## 设置单聊的消息接收选项
通过调用 `MsgSetC2CReceiveMessageOpt`([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgSetC2CReceiveMessageOpt.html)) 接口，设置单聊的消息接收选项。
您可以通过参数 userIDList 设置一批用户，但一次最大允许设置 30 个用户。

>! 该接口调用频率被限制为 1 秒内最多调用 5 次。

示例代码如下：


```c#
// 设置在线和离线都不接收消息
TIMResult res = TencentIMSDK.MsgSetC2CReceiveMessageOpt(user_id_list, TIMReceiveMessageOpt.kTIMRecvMsgOpt_Not_Receive, (int code, string desc, string user_data)=>{
 // 处理异步逻辑
});
```


## 获取单聊的消息接收选项
通过调用 `MsgGetC2CReceiveMessageOpt`([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgGetC2CReceiveMessageOpt.html)) 接口，获取单聊的消息接收选项。

示例代码如下：


```c#
TIMResult res = TencentIMSDK.MsgGetC2CReceiveMessageOpt(user_id_list, (int code, string desc, List<GetC2CRecvMsgOptResult> msg_opts, string user_data)=>{
 // 处理异步逻辑
});
```



## 设置群聊的消息接收选项
通过调用 `MsgSetGroupReceiveMessageOpt`([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgSetGroupReceiveMessageOpt.html)) 接口，设置群聊的消息接收选项。

示例代码如下：


```c#
TIMResult res = TencentIMSDK.MsgSetGroupReceiveMessageOpt(group_id, TIMReceiveMessageOpt.kTIMRecvMsgOpt_Not_Receive, (int code, string desc, string user_data)=>{
 // 处理异步逻辑
});
```




