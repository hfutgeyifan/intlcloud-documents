## 功能描述
* 发送消息方法在核心类 ` TencentImSDKPlugin.v2TIMManager.getMessageManager()`中。
* 支持发送文本、自定义、富媒体消息，消息类型都是 `V2TimMessage`。
* `V2TimMessage` 中可以携带不同类型子类，表示不同类型的消息。

## 重点接口说明
接口 `sendMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html)) 是发送消息中最核心的接口。该接口支持发送所有类型的消息。

> ? 下文中提到的发消息高级接口，指的都是 `sendMessage`。

接口说明如下：
```dart
Future<V2TimValueCallback<V2TimMessage>> sendMessage(
{
  required String id,
  required String receiver,
  required String groupID,
  int priority = 0,
  bool onlineUserOnly = false,
  bool needReadReceipt = false,
  bool isExcludedFromUnreadCount = false,
  bool isExcludedFromLastMessage = false,
  Map<String, dynamic>? offlinePushInfo,
  String? cloudCustomData,
  String? localCustomData,
}
)
```

参数说明：
<table>
   <tr>
      <th width="0px" style="text-align:center">参数</td>
      <th width="0px" style="text-align:center">含义</td>
      <th width="0px"  style="text-align:center">单聊有效</td>
      <th width="0px"  style="text-align:center">群聊有效</td>
			<th width="0px"  style="text-align:center">说明</td>
   </tr>
   <tr>
      <td>id</td>
      <td>创建消息返回的id</td>
      <td>YES</td>
      <td>YES</td>
			<td>需要通过对应的 `createXxxMessage` 接口先行创建</td>
   </tr>
   <tr>
      <td>receiver</td>
      <td>单聊消息接收者 userID</td>
      <td>YES</td>
      <td><b>NO</td>
			<td>如果是发送 C2C 单聊消息，只需要指定 receiver 即可</td>
   </tr>
	 <tr>
      <td>groupID</td>
      <td>群聊 groupID</td>
      <td><b>NO</td>
      <td>YES</td>
			<td>如果是发送群聊消息，只需要指定 groupID 即可</td>
   </tr>
	 <tr>
      <td>priority</td>
      <td>消息优先级</td>
      <td><b>NO</td>
      <td>YES</td>
			<td>请把重要消息设置为高优先级（例如红包、礼物消息），高频且不重要的消息设置为低优先级（例如点赞消息）</td>
   </tr>
	 <tr>
      <td>onlineUserOnly</td>
      <td>是否只有在线用户才能收到</td>
      <td>YES</td>
      <td>YES</td>
	    <td>如果设置为 YES ，接收方历史消息拉取不到，常被用于实现”对方正在输入”或群组里的非重要提示等弱提示功能</td>
   </tr>
	 <tr>
      <td>offlinePushInfo</td>
      <td>离线推送信息</td>
      <td>YES</td>
      <td>YES</td>
	    <td>离线推送时携带的标题和内容</td>
   </tr>
	 <tr>
      <td>needReadReceipt</td>
      <td>发送群消息是否支持已读</td>
      <td><b>NO</td>
      <td>YES</td>
	    <td>发送群消息是否支持已读</td>
   </tr>
 <tr>
      <td>isExcludedFromUnreadCount</td>
      <td>发送消息是否计入会话未读数</td>
      <td>YES</td>
      <td>YES</td>
	    <td>如果设置为 true，发送消息不会计入会话未读，默认为 false</td>
   </tr>
<tr>
      <td>isExcludedFromLastMessage</td>
      <td>发送消息是否计入会话 lastMessage</td>
      <td>YES</td>
      <td>YES</td>
	    <td>如果设置为 true，发送消息不会计入会话 lastMessage，默认为 false</td>
   </tr>
<tr>
      <td>cloudCustomData</td>
      <td>消息云端数据</td>
      <td>YES</td>
      <td>YES</td>
	    <td>消息附带的额外的数据，存云端，消息的接受者可以访问到</td>
   </tr>
<tr>
      <td>localCustomData</td>
      <td>消息本地数据</td>
      <td>YES</td>
      <td>YES</td>
	    <td>消息附带的额外的数据，存本地，消息的接受者不可以访问到，App 卸载后数据丢失</td>
   </tr></dx-tabs>
</table>

>?如果 groupID 和 receiver 同时设置，表示给 receiver 发送定向群消息。具体请参考 [群定向消息](https://intl.cloud.tencent.com/document/product/1047/48028)。


## 发送文本消息
文本消息区分单聊和群聊，涉及的接口、传参有所区别。

发送文本消息可以采用两种接口：普通接口和高级接口。高级接口比普通接口能设置更多的发送参数（例如优先级、离线推送信息等）。
普通接口参考下文具体描述，高级接口就是上文中提到的 `sendMessage`。

### 单聊文本消息


#### 高级接口

调用高级接口发送单聊文本消息分两步：
1. 调用 `createTextMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/createTextMessage.html)) 创建文本消息。
2. 调用 `sendMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html)) 发送消息。

示例代码如下：
```dart
// 创建文本消息
V2TimValueCallback<V2TimMsgCreateInfoResult> createTextAtMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createTextAtMessage(
    text: "test",
    atUserList: [],
  );
 if(createTextAtMessageRes.code == 0){
    String id =  createTextAtMessageRes.data.id;
   	
   	// 发送文本消息
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: id, receiver: "userID", groupID: "");
    if(sendMessageRes.code == 0){
      // 发送成功
    }
  }
```



### 群聊文本消息


#### 高级接口

调用高级接口发送群聊文本消息分两步：
1. 调用 `createTextMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/createTextMessage.html))  创建文本消息。
2. 调用 `sendMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html)) 发送消息。

示例代码如下：
```dart
// 创建文本消息
V2TimValueCallback<V2TimMsgCreateInfoResult> createTextAtMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createTextAtMessage(
    text: "test",
    atUserList: [],
  );
 if(createTextAtMessageRes.code == 0){
    String id =  createTextAtMessageRes.data.id;
   	
   	// 发送文本消息
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: id, receiver: "", groupID: "groupID");
    if(sendMessageRes.code == 0){
      // 发送成功
    }
  }
```


## 发送自定义消息

自定义消息区分单聊和群聊，涉及的接口或者传参有所区别。发送自定义消息可以采用两种接口：普通接口和高级接口。
高级接口即上文中已介绍过的 `sendMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html))，比普通接口能设置更多的发送参数（例如优先级、离线推送信息等）。


### 单聊自定义消息


#### 高级接口

调用高级接口发送单聊自定义消息分两步：
1. 调用 `createCustomMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/createCustomMessage.html))  创建自定义消息。
2. 调用 `sendMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html)) 发送消息。

示例代码如下：
```java
// 创建自定义消息
V2TimValueCallback<V2TimMsgCreateInfoResult> createCustomMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createCustomMessage(
    data: '自定义data',
    desc: '自定义desc',
    extension: '自定义extension',
  );
  if(createCustomMessageRes.code == 0){
    String id =  createCustomMessageRes.data.id;
    // 发送自定义消息
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: id, receiver: "userID", groupID: "");
    if(sendMessageRes.code == 0){
      // 发送成功
    }
  }
```



### 群聊自定义消息


#### 高级接口

调用高级接口发送群聊自定义消息分两步：
1. 调用 `createCustomMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/createCustomMessage.html)) 创建自定义消息。
2. 调用 `sendMessage` ([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html)) 发送消息。

代码示例如下：
```java
// 创建自定义消息
V2TimValueCallback<V2TimMsgCreateInfoResult> createCustomMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createCustomMessage(
    data: '自定义data',
    desc: '自定义desc',
    extension: '自定义extension',
  );
  if(createCustomMessageRes.code == 0){
    String id =  createCustomMessageRes.data.id;
    // 发送自定义消息
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(id: id, receiver: "", groupID: "groupID");
    if(sendMessageRes.code == 0){
      // 发送成功
    }
  }
```




## 发送富媒体消息

富媒体消息发送没有普通接口，都需要使用高级接口，步骤是：

1. 调用 `createXxxMessage` 创建指定类型的富媒体消息对象，其中 Xxx 表示具体的消息类型。
2. 调用 `sendMessage`([Details](https://comm.qq.com/im/doc/flutter/en/SDKAPI/Api/V2TIMMessageManager/sendMessage.html)) 发送消息。
3. 在消息回调中获取消息是否发送成功或失败。

### 图片消息

创建图片消息需要先获取到本地图片路径。
发送消息过程中，会先将图片文件上传至服务器，同时回调上传进度。上传成功后再发送消息。

示例代码如下：
```dart
V2TimValueCallback<V2TimMsgCreateInfoResult> createImageMessageRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createImageMessage(
        imagePath: "本地图片绝对路径", 
);
  if (createImageMessageRes.code == 0) {
    String id = createImageMessageRes.data.id;
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // 发送成功
    }
  }
```


### 语音消息

创建语音消息需要先获取到本地语音文件路径和语音时长，其中语音时长可用于接收端 UI 显示。
发送消息过程中，会先将语音文件上传至服务器，同时回调上传进度。上传成功后再发送消息。

示例代码如下：
```dart
V2TimValueCallback<V2TimMsgCreateInfoResult> createSoundMessageRes =
      await TencentImSDKPlugin.v2TIMManager.getMessageManager().createSoundMessage(
        soundPath: "本地录音文件绝对路径",
        duration: 10,// 录音时长
      );
  if (createSoundMessageRes.code == 0) {
    String id = createSoundMessageRes.data.id;
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // 发送成功
    }
  }
```


### 视频消息

创建视频消息需要先获取到本地视频文件路径、视频时长和视频快照，其中时长和快照可用于接收端 UI 显示。
发送消息过程中，会先将视频上传至服务器，同时回调上传进度。上传成功后再发送消息。

示例代码如下：
```dart
V2TimValueCallback<V2TimMsgCreateInfoResult> createVideoMessageRes =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createVideoMessage(
            videoFilePath: "本地视频文件绝对路径",
            type: "mp4", // 视频类型
            duration: 10,// 视频时长
            snapshotPath: "本地视频封面文件绝对路径",
          );
  if (createVideoMessageRes.code == 0) {
    String id = createVideoMessageRes.data.id;
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // 发送成功
    }
  }
```



### 文件消息

创建文件消息需要先获取到本地文件路径。
发送消息过程中，会先将文件上传至服务器，同时回调上传进度。上传成功后再发送消息。

示例代码如下：
```dart
V2TimValueCallback<V2TimMsgCreateInfoResult> createFileMessageRes =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createFileMessage(
            filePath: "本地文件绝对路径",
            fileName: "文件名",
          );
  if (createFileMessageRes.code == 0) {
    String id = createFileMessageRes.data.id;
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // 发送成功
    }
  }
```



### 定位消息

定位消息会直接发送经纬度，一般需要配合地图控件显示。

示例代码如下：
```dart
 V2TimValueCallback<V2TimMsgCreateInfoResult> createLocationMessage =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createLocationMessage(
            desc: "深圳市南山区深南大道",//位置信息摘要
            longitude: 34,// 经度
            latitude: 20, // 纬度
          );
  if (createLocationMessage.code == 0) {
    String id = createLocationMessage.data.id;
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // 发送成功
    }
  }
```


### 表情消息

定位消息会直接发送表情编码，通常接收端需要将其转换成对应的表情 icon。

示例代码如下：
```java
V2TimValueCallback<V2TimMsgCreateInfoResult> createFaceMessageRes =
      await TencentImSDKPlugin.v2TIMManager
          .getMessageManager()
          .createFaceMessage(
            index: 0,
            data: "",
          );
  if (createFaceMessageRes.code == 0) {
    String id = createFaceMessageRes.data.id;
    V2TimValueCallback<V2TimMessage> sendMessageRes = await TencentImSDKPlugin
        .v2TIMManager
        .getMessageManager()
        .sendMessage(id: id, receiver: "userID", groupID: "groupID");
    if (sendMessageRes.code == 0) {
      // 发送成功
    }
  }
```



