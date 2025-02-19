## 功能描述
* 通过 `addSimpleMsgListener` 监听接收文本、自定义消息，相关回调在 `V2TIMSimpleMsgListener` 协议中定义。
* 通过 `addAdvancedMsgListener` 监听接收所有类型消息（文本、自定义、富媒体消息），相关回调在 `V2TIMAdvancedMsgListener` 协议中定义。
  

## 设置消息监听器
SDK 提供了 2 种消息监听器，简单消息监听器 `V2TIMSimpleMsgListener` 和高级消息监听器 `V2TIMAdvancedMsgListener`。
两者的区别在于:
1. 简单消息监听器**只能**接收文本、自定义消息。如果您的业务只需要这两种消息，可以仅使用简单消息监听器。
2. 高级消息监听器可以接收**所有**类型的消息。如果您的业务还需要支持富媒体、合并消息等其他类型，请使用高级消息监听器。

> ! 
> 1. `addSimpleMsgListener` 和 `addAdvancedMsgListener` 请使用其中之一，**切勿混用**，以免产生不可预知的逻辑 bug。
> 2. 如果想要正常接收下面各种类型的消息，**必须**先添加消息监听器，否则无法正常接收。


### 简单消息监听器

#### 添加监听器
接收方调用 `addSimpleMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd96fd1591e41f031421c0655d8e5d6b) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a149cdf7924aa13746692d18d605def88)) 添加简单消息监听器。一般建议在比较靠前的时间点调用，例如聊天消息界面初始化后，确保 App 能及时收到消息。

示例代码如下：
<dx-tabs>
::: Android
```java
V2TIMManager.getInstance().addSimpleMsgListener(simpleMsgListener);
```
:::
::: iOS & Mac
```objectivec
// self 为 id<V2TIMSignalingListener>
[[V2TIMManager sharedInstance] addSimpleMsgListener:self];
```
:::
</dx-tabs>

#### 监听器回调事件
添加成功简单消息监听器后，接收方可以在 `V2TIMSimpleMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSimpleMsgListener.html) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSimpleMsgListener-p.html)) 的回调中接收不同类型消息，说明如下：

<dx-tabs>
::: Android
```java
public abstract class V2TIMSimpleMsgListener {
	// 收到 C2C 文本消息
	public void onRecvC2CTextMessage(String msgID, V2TIMUserInfo sender, String text) {}

	// 收到 C2C 自定义（信令）消息
	public void onRecvC2CCustomMessage(String msgID, V2TIMUserInfo sender, byte[] customData) {}

	// 收到群文本消息
	public void onRecvGroupTextMessage(String msgID, String groupID, V2TIMGroupMemberInfo sender, String text) {}

	// 收到群自定义（信令）消息
	public void onRecvGroupCustomMessage(String msgID, String groupID, V2TIMGroupMemberInfo sender, byte[] customData) {}
}
```
:::
::: iOS & Mac
```objectivec
/// IMSDK 基本消息回调
@protocol V2TIMSimpleMsgListener <NSObject>
@optional

/// 收到 C2C 文本消息
- (void)onRecvC2CTextMessage:(NSString *)msgID  sender:(V2TIMUserInfo *)info text:(NSString *)text;

/// 收到 C2C 自定义（信令）消息
- (void)onRecvC2CCustomMessage:(NSString *)msgID  sender:(V2TIMUserInfo *)info customData:(NSData *)data;

/// 收到群文本消息
- (void)onRecvGroupTextMessage:(NSString *)msgID groupID:(NSString *)groupID sender:(V2TIMGroupMemberInfo *)info text:(NSString *)text;

/// 收到群自定义（信令）消息
- (void)onRecvGroupCustomMessage:(NSString *)msgID groupID:(NSString *)groupID sender:(V2TIMGroupMemberInfo *)info customData:(NSData *)data;
@end
```
:::
</dx-tabs>


#### 移除监听器
如果想停止接收消息，接收方可调用 `removeSimpleMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a86ac462d87f652960d2600a52009849a) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#afa3040f676105f3fb78d4835ee3c898b)) 移除简单消息监听器。

示例代码如下：
<dx-tabs>
::: Android
```java
V2TIMManager.getInstance().removeSimpleMsgListener(simpleMsgListener);
```
:::
::: iOS & Mac
```objectivec
// self 为 id<V2TIMSignalingListener>
[[V2TIMManager sharedInstance] removeSimpleMsgListener:self];
```
:::
</dx-tabs>


### 高级消息监听器

#### 添加监听器
接收方调用 `addAdvancedMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab)) 添加高级消息监听器。一般建议在比较靠前的时间点调用，例如例如聊天消息界面初始化后，确保 App 能及时收到消息。

示例代码如下：
<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().addAdvancedMsgListener(advancedMsgListener);
```
:::
::: iOS & Mac
```objectivec
// self 为 id<V2TIMAdvancedMsgListener>
[[V2TIMManager sharedInstance] addAdvancedMsgListener:self];
```
:::
</dx-tabs>

#### 监听器回调事件
添加成功高级消息监听器后，接收方可以在 `V2TIMAdvancedMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html)) 的回调中接收不同类型消息，说明如下：

<dx-tabs>
::: Android
```java
public abstract class V2TIMAdvancedMsgListener {
	// 收到新消息
	public void onRecvNewMessage(V2TIMMessage msg) {}

	// C2C 对端用户会话已读通知（对端用户调用 markC2CMessageAsRead，自己会收到该通知）
	public void onRecvC2CReadReceipt(List<V2TIMMessageReceipt> receiptList) {}

	// 消息已读回执通知（如果自己发送的消息支持已读回执，消息接收端调用 sendMessageReadReceipts，自己会收到该通知）
	public void onRecvMessageReadReceipts(List<V2TIMMessageReceipt> receiptList) {}

	// 收到消息撤回的通知
	public void onRecvMessageRevoked(String msgID) {}

	// 消息内容被修改
	public void onRecvMessageModified(V2TIMMessage msg) {}
}
```
:::
::: iOS & Mac
```objectivec
/// 高级消息监听器
@protocol V2TIMAdvancedMsgListener <NSObject>
@optional
/// 收到新消息
- (void)onRecvNewMessage:(V2TIMMessage *)msg;

/// 消息已读回执通知（如果自己发的消息支持已读回执，消息接收端调用了 sendMessageReadReceipts 接口，自己会收到该回调）
- (void)onRecvMessageReadReceipts:(NSArray<V2TIMMessageReceipt *> *)receiptList;

/// C2C 对端用户会话已读通知（如果对端用户调用 markC2CMessageAsRead 接口，自己会收到该通知）
- (void)onRecvC2CReadReceipt:(NSArray<V2TIMMessageReceipt *> *)receiptList;

/// 收到消息撤回
- (void)onRecvMessageRevoked:(NSString *)msgID;

/// 消息内容被修改
- (void)onRecvMessageModified:(V2TIMMessage *)msg;
@end
```
:::
</dx-tabs>

#### 移除监听器
如果想停止接收消息，接收方可调用 `removeAdvancedMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a44e1e9126bf5b30234330fe19259cd93) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a28aeebff4a791c9bb8f91a4f61e020e6)) 移除高级消息监听器。

示例代码如下：
<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().removeAdvancedMsgListener(advancedMsgListener);
```
:::
::: iOS & Mac
```objectivec
// self 为 id<V2TIMAdvancedMsgListener>
[[V2TIMManager sharedInstance] removeAdvancedMsgListener:self];
```
:::
</dx-tabs>


## 接收文本消息

### 使用简单消息监听器接收

#### 单聊文本消息
接收方使用简单消息监听器接收单聊文本消息，需要以下几步：
1. 调用 `addSimpleMsgListener` 设置事件监听器。
2. 监听 `onRecvC2CTextMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSimpleMsgListener.html#a59343bacf7c68b560157cdd1417348db) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSimpleMsgListener-p.html#a1b467b330291b233c6c15e7e218762b2)) 回调，在其中接收文本消息。
3. 希望停止接收消息，调用 `removeSimpleMsgListener` 移除监听。该步骤不是必须的，客户可以按照业务需求调用。

代码示例如下：
<dx-tabs>
::: Android
```java
// 设置事件监听器
V2TIMManager.getInstance().addSimpleMsgListener(simpleMsgListener);

// 接收单聊文本消息
/**
 * 收到 C2C 文本消息
 *
 * @param msgID 消息唯一标识
 * @param sender 发送方信息
 * @param text 发送内容
 */
public void onRecvC2CTextMessage(String msgID, V2TIMUserInfo sender, String text) {
	// 可解析消息并展示到 UI
}
```
:::
::: iOS & Mac 
```objectivec
// 设置事件监听器
[[V2TIMManager sharedInstance] addSimpleMsgListener:self];

/// 接收单聊文本消息
/// @param msgID 消息 Id
/// @param info 发送者信息
/// @param text 文本内容
- (void)onRecvC2CTextMessage:(NSString *)msgID sender:(V2TIMUserInfo *)info text:(NSString *)text {
    // 可解析消息并展示到 UI
}
```
:::
</dx-tabs>

#### 群聊文本消息
接收方使用简单消息监听器接收群聊文本消息，需要以下几步：
1. 调用 `addSimpleMsgListener` 设置事件监听器。
2. 监听 `onRecvGroupTextMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSimpleMsgListener.html#a1f9eaa4fdc323a8ec375b7068df7b7d4) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSimpleMsgListener-p.html#abee1960a3674e490ce1291889f366d3c)) 回调，在其中接收文本消息。
3. 希望停止接收消息，调用 `removeSimpleMsgListener` 移除监听。该步骤不是必须的，客户可以按照业务需求调用。
   

代码示例如下：
<dx-tabs>
::: Android
```java
// 设置事件监听器
V2TIMManager.getInstance().addSimpleMsgListener(simpleMsgListener);

// 接收群聊文本消息
/**
 * 收到群文本消息
 *
 * @param msgID 消息唯一标识
 * @param groupID 群 ID
 * @param sender 发送方群成员信息
 * @param text 发送内容
 */
public void onRecvGroupTextMessage(String msgID, String groupID, V2TIMGroupMemberInfo sender, String text) {
	// 可解析消息并展示到 UI
}
```
:::
::: iOS & Mac
```objectivec
// 设置事件监听器
[[V2TIMManager sharedInstance] addSimpleMsgListener:self];

/// 接收群聊文本消息
/// @param msgID 消息 Id
/// @param groupID 群组 ID
/// @param info 发送者信息
/// @param text 文本内容
- (void)onRecvGroupTextMessage:(NSString *)msgID groupID:(NSString *)groupID sender:(V2TIMGroupMemberInfo *)info text:(NSString *)text {
    // 可解析消息并展示到 UI
}
```
:::
</dx-tabs>


### 使用高级消息监听器接收
接收方使用高级消息监听器接收单聊、群聊文本消息，需要以下几步：
1. 调用 `addAdvancedMsgListener` 设置事件监听器。
2. 监听 `onRecvNewMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a6771cfa1a897e24b05c17788aba15ff6) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html#ae36dde0fab51c29f6d1620ab4b13d7a3)) 回调，在其中接收文本消息。
3. 希望停止接收消息，调用 `removeAdvancedMsgListener` 移除监听。该步骤不是必须的，客户可以按照业务需求调用。

代码示例如下：
<dx-tabs>
::: Android
```java
// 设置事件监听器
V2TIMManager.getMessageManager().addAdvancedMsgListener(advancedMsgListener);

/**
 * 收到新消息
 * @param msg 消息
 */
public void onRecvNewMessage(V2TIMMessage msg) {
	// 解析出 groupID 和 userID
	String groupID = msg.getGroupID();
	String userID = msg.getUserID();

	// 判断当前是单聊还是群聊：
	// 如果 groupID 不为空，表示此消息为群聊；如果 userID 不为空，表示此消息为群聊

	// 解析出 msg 中的文本消息
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_TEXT) {
		V2TIMTextElem textElem = msg.getTextElem();
		String text = textElem.getText();
		Log.i("onRecvNewMessage", "text:" + text);
	}
}
```
:::
::: iOS & Mac
```objectivec
// 设置事件监听器
[[V2TIMManager sharedInstance] addAdvancedMsgListener:self];

/// 接收消息
/// @param msg 消息对象
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    // 解析出 groupID 和 userID
    NSString *groupID = msg.groupID;
    NSString *userID = msg.userID;

    // 判断当前是单聊还是群聊：
    // 如果 groupID 不为空，表示此消息为群聊；如果 userID 不为空，表示此消息为群聊

    // 解析出 msg 中的文本消息
    if (msg.elemType == V2TIM_ELEM_TYPE_TEXT) {
        V2TIMTextElem *textElem = msg.textElem;
        NSString *text = textElem.text;
        NSLog(@"onRecvNewMessage, text: %@", text);
    }
}
```
:::
</dx-tabs>


## 接收自定义消息

### 使用简单消息监听器接收

#### 单聊自定义消息

接收方使用简单消息监听器接收单聊自定义消息，需要以下几步：
1. 调用 `addSimpleMsgListener` 设置事件监听器。
2. 监听 `onRecvC2CCustomMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSimpleMsgListener.html#a13d77741c8286b011c1eb7513a9eb2c7) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSimpleMsgListener-p.html#ae6eec84f9664f08591bc743f20f2360b)) 回调，在其中接收单聊自定义消息。
3. 希望停止接收消息，调用 `removeSimpleMsgListener` 移除监听。该步骤不是必须的，客户可以按照业务需求调用。
   

代码示例如下：
<dx-tabs>
::: Android
```java
/**
 * 接收单聊自定义消息
 * @param msgID 消息 ID
 * @param sender 发送方信息
 * @param customData 发送内容
 */
public void onRecvC2CCustomMessage(String msgID, V2TIMUserInfo sender, byte[] customData) {
	Log.i("onRecvC2CCustomMessage", "msgID:" + msgID + ", from:" + sender.getNickName() + ", content:" + new String(customData));
}
```
:::
::: iOS & Mac
```objectivec
/// 接收单聊自定义消息
/// @param msgID 消息 ID
/// @param info 发送者信息
/// @param data 自定义消息二进制内容
- (void)onRecvC2CCustomMessage:(NSString *)msgID sender:(V2TIMUserInfo *)info customData:(NSData *)data {
    NSLog(@"onRecvC2CCustomMessage, msgID: %@, sender: %@, customData: %@", msgID, info, data);
}
```
:::
</dx-tabs>


#### 群聊自定义消息
接收方使用简单消息监听器接收群聊自定义消息，需要以下几步
1. 调用 `addSimpleMsgListener` 设置事件监听器。
2. 监听 `onRecvGroupCustomMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSimpleMsgListener.html#a46b48869e411b41c25a98211d951335c) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMSimpleMsgListener-p.html#abd21785aa5bfcee78ffb1a94383077d1)) 回调，在其中接收群聊自定义消息。
3. 希望停止接收消息，调用 `removeSimpleMsgListener` 移除监听。该步骤不是必须的，客户可以按照业务需求调用。
   

<dx-tabs>
::: Android
```java
/**
 * 接收群聊自定义消息
 * @param msgID 消息 ID
 * @param groupID 群 ID
 * @param sender 发送方群成员信息
 * @param customData 发送内容
 */
public void onRecvGroupCustomMessage(String msgID, String groupID, V2TIMGroupMemberInfo sender, byte[] customData) {
	Log.i("onRecvGroupCustomMessage", "msgID:" + msgID + ", groupID:" + groupID + ", from:" + sender.getNickName() + ", content:" + new String(customData));
}
```
:::
::: iOS & Mac
```objectivec
/// 接收群聊自定义消息
/// @param msgID 消息 ID
/// @param groupID 群组 ID
/// @param info 发送者信息
/// @param text 自定义消息二进制内容
- (void)onRecvGroupCustomMessage:(NSString *)msgID groupID:(NSString *)groupID sender:(V2TIMGroupMemberInfo *)info customData:(NSData *)data {
	NSLog(@"onRecvGroupCustomMessage, msgID: %@, groupID: %@, sender: %@, customData: %@", msgID, groupID, info, data);
}
```
:::
</dx-tabs>


### 使用高级消息监听器接收
接收方使用高级消息监听器接收单聊、群聊自定义消息，需要以下几步：
1. 调用 `addAdvancedMsgListener` 设置事件监听器。
2. 监听 `onRecvNewMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a6771cfa1a897e24b05c17788aba15ff6) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html#ae36dde0fab51c29f6d1620ab4b13d7a3)) 回调，在其中接收自定义消息。
3. 希望停止接收消息，调用 `removeAdvancedMsgListener` 移除监听。该步骤不是必须的，客户可以按照业务需求调用。

代码示例如下：
<dx-tabs>
::: Android
```java
// 设置事件监听器
V2TIMManager.getMessageManager().addAdvancedMsgListener(v2TIMAdvancedMsgListener);

// 接收消息
public void onRecvNewMessage(V2TIMMessage msg) {
	// 解析出 groupID 和 userID
	String groupID = msg.getGroupID();
	String userID = msg.getUserID();

	// 判断当前是单聊还是群聊：
	// 如果 groupID 不为空，表示此消息为群聊；如果 userID 不为空，表示此消息为群聊

	// 解析出 msg 中的自定义消息
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_CUSTOM) {
		V2TIMCustomElem customElem = msg.getCustomElem();
		String data = new String(customElem.getData());
		Log.i("onRecvNewMessage", "customData:" + data);
	}
}
```
:::
::: iOS & Mac
```objectivec
// 设置事件监听器
[[V2TIMManager sharedInstance] addAdvancedMsgListener:self];

/// 接收消息
/// @param msg 消息对象
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    // 解析出 groupID 和 userID
    NSString *groupID = msg.groupID;
    NSString *userID = msg.userID;

    // 判断当前是单聊还是群聊：
    // 如果 groupID 不为空，表示此消息为群聊；如果 userID 不为空，表示此消息为群聊

    // 解析出 msg 中的自定义消息
    if (msg.elemType == V2TIM_ELEM_TYPE_CUSTOM) {
        V2TIMCustomElem *customElem = msg.customElem;
        NSData *customData = customElem.data;
        NSLog(@"onRecvNewMessage, customData: %@", customData);
    }
}
```
:::
</dx-tabs>


## 接收富媒体消息
接收富媒体消息**只能使用**高级消息监听器，需要以下几步：
1. 接收方调用 `addAdvancedMsgListener` 接口设置高级消息监听。
2. 接收方通过监听回调 `onRecvNewMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a6771cfa1a897e24b05c17788aba15ff6) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html#ae36dde0fab51c29f6d1620ab4b13d7a3)) 获取消息 V2TIMMessage。
3. 接收方解析 `V2TIMMessage` 消息中的 `elemType` 属性，并根据其类型进行二次解析，获取消息内部 Elem 中的具体内容。
4. 希望停止接收消息，调用 `removeAdvancedMsgListener` 移除监听。该步骤不是必须的，客户可以按照业务需求调用。


### 图片消息

一个图片消息会包含三种格式大小的图片，分别为原图、大图、微缩图（SDK 会在发送图片消息的时候自动生成微缩图、大图，客户不需要关心）：
* 大图：将原图等比压缩。压缩后宽、高中较小的一个等于 720 像素。
* 缩略图：将原图等比压缩。压缩后宽、高中较小的一个等于 198 像素。

接收端收到图片消息后，我们推荐您调用 SDK 的 `downloadImage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMImageElem_1_1V2TIMImage.html#a9114c16b095bbf608027c71eb40e9025) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMImage.html#a2ef83a4fb5c2a047acaf881ee90df58e)) 将图片下载到本地，再取出图片渲染到 UI 层。

为了避免重复下载，节省资源，我们推荐您将 `V2TIMImage` 对象的 `uuid` 属性值设置到图片的下载路径中，作为图片的标识。

示例代码向您演示如何从 `V2TIMMessage` 中解析出图片消息内容：

<dx-tabs>
::: Android
```java
public void onRecvNewMessage(V2TIMMessage msg) {
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_IMAGE) {
		// 图片消息
		V2TIMImageElem v2TIMImageElem = msg.getImageElem();
		// 一个图片消息会包含三种格式大小的图片，分别为原图、大图、微缩图（SDK 会在发送图片消息的时候自动生成微缩图、大图，客户不需要关心）
		// 大图：是将原图等比压缩，压缩后宽、高中较小的一个等于720像素。
		// 缩略图：是将原图等比压缩，压缩后宽、高中较小的一个等于198像素。
		List<V2TIMImageElem.V2TIMImage> imageList = v2TIMImageElem.getImageList();
		for (V2TIMImageElem.V2TIMImage v2TIMImage : imageList) {
			// 图片 ID，内部标识，可用于外部缓存 key
			String uuid = v2TIMImage.getUUID();
			// 图片类型
			int imageType = v2TIMImage.getType();
			// 图片大小（字节）
			int size = v2TIMImage.getSize();
			// 图片宽度
			int width = v2TIMImage.getWidth();
			// 图片高度
			int height = v2TIMImage.getHeight();
			// 设置图片下载路径 imagePath，这里可以用 uuid 作为标识，避免重复下载
			String imagePath = "/sdcard/im/image/" + "myUserID" + uuid;
			File imageFile = new File(imagePath);
			// 判断 imagePath 下有没有已经下载过的图片文件
			if (!imageFile.exists()) {
				// 下载图片
				v2TIMImage.downloadImage(imagePath, new V2TIMDownloadCallback() {
					@Override
					public void onProgress(V2TIMElem.V2ProgressInfo progressInfo) {
						// 下载进度回调：已下载大小 v2ProgressInfo.getCurrentSize()；总文件大小 v2ProgressInfo.getTotalSize()
					}
					@Override
					public void onError(int code, String desc) {
						// 下载失败
					}
					@Override
					public void onSuccess() {
						// 下载完成
					}
				});
			} else {
				// 图片已存在
			}
		}
	}
}
```
:::
::: iOS & Mac
```objectivec
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    if (msg.elemType == V2TIM_ELEM_TYPE_IMAGE) {
        V2TIMImageElem *imageElem = msg.imageElem;
        // 原图、大图、微缩图列表
        NSArray<V2TIMImage *> *imageList = imageElem.imageList;
        for (V2TIMImage *timImage in imageList) {
            // 图片 ID，内部标识，可用于外部缓存 key
            NSString *uuid = timImage.uuid;
            // 图片类型
            V2TIMImageType type = timImage.type;
            // 图片大小（字节）
            int size = timImage.size;
            // 图片宽度
            int width = timImage.width;
            // 图片高度
            int height = timImage.height;
            // 设置图片下载路径 imagePath，这里可以用 uuid 作为标识，避免重复下载
            NSString *imagePath = [NSTemporaryDirectory() stringByAppendingPathComponent:[NSString stringWithFormat: @"testImage%@", timImage.uuid]];
            // 判断 imagePath 下有没有已经下载过的图片文件
            if (![[NSFileManager defaultManager] fileExistsAtPath:imagePath]) {
                // 下载图片
                [timImage downloadImage:imagePath progress:^(NSInteger curSize, NSInteger totalSize) {
                    // 下载进度
                    NSLog(@"下载图片进度：curSize：%lu,totalSize:%lu",curSize,totalSize);
                } succ:^{
                    // 下载成功
                    NSLog(@"下载图片完成");
                } fail:^(int code, NSString *msg) {
                    // 下载失败
                    NSLog(@"下载图片失败：code：%d,msg:%@",code,msg);
                }];
            } else {
                // 图片已存在
            }
            NSLog(@"图片信息：uuid:%@, type:%ld, size:%d, width:%d, height:%d", uuid, (long)type, size, width, height);
        }
    }
}
```
:::
</dx-tabs>


### 视频消息

接收方收到视频消息后，一般需要在聊天界面显示一个视频预览图，当用户点击消息后，才会触发视频的播放。
所以这里需要两步：
1. 下载视频截图。我们推荐您调用 SDK 的 `downloadSnapshot` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMVideoElem.html#abee852d50627376a147a98a7375dea1a) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMVideoElem.html#a7ae717400d7a9df3f337f0759a6b3163)) 进行下载。
2. 下载视频。我们推荐您调用 SDK 的 `downloadVideo` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMVideoElem.html#a0adbdd0bcaed5093176db51d284976ea) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMVideoElem.html#a6e83b77be6db2005e91b90d2e2ac2f6a))  进行下载。

为了避免重复下载，节省资源，我们推荐您将 `V2TIMVideoElem` 对象的 `videoUUID` 属性值设置到视频的下载路径中，作为视频的标识。

示例代码向您演示如何从 `V2TIMMessage` 中解析出视频消息内容：

<dx-tabs>
::: Android
```java
public void onRecvNewMessage(V2TIMMessage msg) {
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_VIDEO) {
		// 视频消息
		V2TIMVideoElem v2TIMVideoElem = msg.getVideoElem();
		// 视频截图 ID,内部标识，可用于外部缓存 key
		String snapshotUUID = v2TIMVideoElem.getSnapshotUUID();
		// 视频截图文件大小
		int snapshotSize = v2TIMVideoElem.getSnapshotSize();
		// 视频截图宽
		int snapshotWidth = v2TIMVideoElem.getSnapshotWidth();
		// 视频截图高
		int snapshotHeight = v2TIMVideoElem.getSnapshotHeight();
		// 视频 ID,内部标识，可用于外部缓存 key
		String videoUUID = v2TIMVideoElem.getVideoUUID();
		// 视频文件大小
		int videoSize = v2TIMVideoElem.getVideoSize();
		// 视频时长
		int duration = v2TIMVideoElem.getDuration();
		// 设置视频截图文件路径，这里可以用 uuid 作为标识，避免重复下载
		String snapshotPath = "/sdcard/im/snapshot/" + "myUserID" + snapshotUUID;
		File snapshotFile = new File(snapshotPath);
		if (!snapshotFile.exists()) {
			v2TIMVideoElem.downloadSnapshot(snapshotPath, new V2TIMDownloadCallback() {
				@Override
				public void onProgress(V2TIMElem.V2ProgressInfo progressInfo) {
					// 下载进度回调：已下载大小 v2ProgressInfo.getCurrentSize()；总文件大小 v2ProgressInfo.getTotalSize()
				}
				@Override
				public void onError(int code, String desc) {
					// 下载失败
				}
				@Override
				public void onSuccess() {
					// 下载完成
				}
			});
		} else {
			// 文件已存在
		}

		// 设置视频文件路径，这里可以用 uuid 作为标识，避免重复下载
		String videoPath = "/sdcard/im/video/" + "myUserID" + videoUUID;
		File videoFile = new File(videoPath);
		if (!videoFile.exists()) {
			v2TIMVideoElem.downloadVideo(videoPath, new V2TIMDownloadCallback() {
				@Override
				public void onProgress(V2TIMElem.V2ProgressInfo progressInfo) {
				// 下载进度回调：已下载大小 v2ProgressInfo.getCurrentSize()；总文件大小 v2ProgressInfo.getTotalSize()
				}
				@Override
				public void onError(int code, String desc) {
				// 下载失败
				}
				@Override
				public void onSuccess() {
				// 下载完成
				}
			});
		} else {
			// 文件已存在
		}
	}
}
```
:::
::: iOS & Mac
```objectivec
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    if (msg.elemType == V2TIM_ELEM_TYPE_VIDEO) {
        V2TIMVideoElem *videoElem = msg.videoElem;
        // 视频截图 ID,内部标识，可用于外部缓存 key
        NSString *snapshotUUID = videoElem.snapshotUUID;
        // 视频截图文件大小
        int snapshotSize = videoElem.snapshotSize;
        // 视频截图宽
        int snapshotWidth = videoElem.snapshotWidth;
        // 视频截图高
        int snapshotHeight = videoElem.snapshotHeight;
        // 视频 ID,内部标识，可用于外部缓存 key
        NSString *videoUUID = videoElem.videoUUID;
        // 视频文件大小
        int videoSize = videoElem.videoSize;
        // 视频时长
        int duration = videoElem.duration;
        // 设置视频截图文件路径，这里可以用 uuid 作为标识，避免重复下载
        NSString *snapshotPath = [NSTemporaryDirectory() stringByAppendingPathComponent:[NSString stringWithFormat: @"testVideoSnapshot%@",snapshotUUID]];
        if (![[NSFileManager defaultManager] fileExistsAtPath:snapshotPath]) {
            // 下载视频截图
            [videoElem downloadSnapshot:snapshotPath progress:^(NSInteger curSize, NSInteger totalSize) {
                // 下载进度
                NSLog(@"%@", [NSString stringWithFormat:@"下载视频截图进度：curSize：%lu,totalSize:%lu",curSize,totalSize]);
            } succ:^{
                // 下载成功
                NSLog(@"下载视频截图完成");
            } fail:^(int code, NSString *msg) {
                // 下载失败
                NSLog(@"%@", [NSString stringWithFormat:@"下载视频截图失败：code：%d,msg:%@",code,msg]);
            }];
        } else {
            // 视频截图已存在
        }
        NSLog(@"视频截图信息：snapshotUUID:%@, snapshotSize:%d, snapshotWidth:%d, snapshotWidth:%d, snapshotPath:%@", snapshotUUID, snapshotSize, snapshotWidth, snapshotHeight, snapshotPath);
        
        // 设置视频文件路径，这里可以用 uuid 作为标识，避免重复下载
        NSString *videoPath = [NSTemporaryDirectory() stringByAppendingPathComponent:[NSString stringWithFormat: @"testVideo%@",videoUUID]];
        if (![[NSFileManager defaultManager] fileExistsAtPath:videoPath]) {
            // 下载视频
            [videoElem downloadVideo:videoPath progress:^(NSInteger curSize, NSInteger totalSize) {
                // 下载进度
                NSLog(@"%@", [NSString stringWithFormat:@"下载视频进度：curSize：%lu,totalSize:%lu",curSize,totalSize]);
            } succ:^{
                // 下载成功
                NSLog(@"下载视频完成");
            } fail:^(int code, NSString *msg) {
                // 下载失败
                NSLog(@"%@", [NSString stringWithFormat:@"下载视频失败：code：%d,msg:%@",code,msg]);
            }];
        } else {
            // 视频已存在
        }
        NSLog(@"视频信息：videoUUID:%@, videoSize:%d, duration:%d, videoPath:%@", videoUUID, videoSize, duration, videoPath);
    }
}
```
:::
</dx-tabs>

### 语音消息

接收端收到语音消息后，我们推荐您调用 SDK 的 `downloadSound` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMSoundElem.html#a24cb6b4e90687833a6de8fa62e868b3a) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMSoundElem.html#ac06d3cc1193da9e6b10d6256dc95f2b2)) 将语音下载到本地，再获取本地语音文件播放。

为了避免重复下载，节省资源，我们推荐您将 `V2TIMSoundElem` 对象的 `uuid` 属性值设置到语音的下载路径中，作为语音的标识。

示例代码向您演示如何从 `V2TIMMessage` 中解析出语音消息内容：

<dx-tabs>
::: Android
```java
public void onRecvNewMessage(V2TIMMessage msg) {
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_SOUND) {
		// 语音消息
		V2TIMSoundElem v2TIMSoundElem = msg.getSoundElem();
		// 语音 ID,内部标识，可用于外部缓存 key
		String uuid = v2TIMSoundElem.getUUID();
		// 语音文件大小
		int dataSize = v2TIMSoundElem.getDataSize();
		// 语音时长
		int duration = v2TIMSoundElem.getDuration();
		// 设置语音文件路径 soundPath，这里可以用 uuid 作为标识，避免重复下载
		String soundPath = "/sdcard/im/sound/" + "myUserID" + uuid;
		File imageFile = new File(soundPath);
		// 判断 soundPath 下有没有已经下载过的语音文件
		if (!imageFile.exists()) {
			v2TIMSoundElem.downloadSound(soundPath, new V2TIMDownloadCallback() {
				@Override
				public void onProgress(V2TIMElem.V2ProgressInfo progressInfo) {
					// 下载进度回调：已下载大小 v2ProgressInfo.getCurrentSize()；总文件大小 v2ProgressInfo.getTotalSize()
				}
				@Override
				public void onError(int code, String desc) {
					// 下载失败
				}
				@Override
				public void onSuccess() {
					// 下载完成
				}
			});
		} else {
			// 文件已存在
		}
	}
}
```
:::
::: iOS & Mac
```objectivec
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    if (msg.elemType == V2TIM_ELEM_TYPE_SOUND) {
        V2TIMSoundElem *soundElem = msg.soundElem;
        // 语音 ID,内部标识，可用于外部缓存 key
        NSString *uuid = soundElem.uuid;
        // 语音文件大小
        int dataSize = soundElem.dataSize;
        // 语音时长
        int duration = soundElem.duration;
        // 设置语音文件路径 soundPath，这里可以用 uuid 作为标识，避免重复下载
        NSString *soundPath = [NSTemporaryDirectory() stringByAppendingPathComponent:[NSString stringWithFormat: @"testSound%@",uuid]];
        // 判断 soundPath 下有没有已经下载过的语音文件
        if (![[NSFileManager defaultManager] fileExistsAtPath:soundPath]) {
            // 下载语音
            [soundElem downloadSound:soundPath progress:^(NSInteger curSize, NSInteger totalSize) {
                // 下载进度
                NSLog(@"下载语音进度：curSize：%lu,totalSize:%lu",curSize,totalSize);
            } succ:^{
                // 下载成功
                NSLog(@"下载语音完成");
            } fail:^(int code, NSString *msg) {
                // 下载失败
                NSLog(@"下载语音失败：code：%d,msg:%@",code,msg);
            }];
        } else {
            // 语音已存在
        }
        NSLog(@"语音信息：uuid:%@, dataSize:%d, duration:%d, soundPath:%@", uuid, dataSize, duration, soundPath);
    }
}
```
:::
</dx-tabs>

### 文件消息

接收端收到文件消息后，我们推荐您调用 SDK 的 `downloadFile` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFileElem.html#a932e3acc34504d83f0e1e94799057d5a) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMFileElem.html#a6ecb2ec506745c2fce99f78bab616009)) 将文件下载到本地，再获取本地文件展示。

为了避免重复下载，节省资源，我们推荐您将 `V2TIMFileElem` 对象的 `uuid` 属性值设置到文件的下载路径中，作为文件的标识。

示例代码向您演示如何从 `V2TIMMessage` 中解析出文件消息内容：

<dx-tabs>
::: Android
```java
public void onRecvNewMessage(V2TIMMessage msg) {
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_FILE) {
		// 文件消息
		V2TIMFileElem v2TIMFileElem = msg.getFileElem();
		// 文件 ID,内部标识，可用于外部缓存 key
		String uuid = v2TIMFileElem.getUUID();
		// 文件名称
		String fileName = v2TIMFileElem.getFileName();
		// 文件大小
		int fileSize = v2TIMFileElem.getFileSize();
		// 设置文件路径，这里可以用 uuid 作为标识，避免重复下载
		String filePath = "/sdcard/im/file/" + "myUserID" + uuid;
		File file = new File(filePath);
		if (!file.exists()) {
			v2TIMFileElem.downloadFile(filePath, new V2TIMDownloadCallback() {
				@Override
				public void onProgress(V2TIMElem.V2ProgressInfo progressInfo) {
					// 下载进度回调：已下载大小 v2ProgressInfo.getCurrentSize()；总文件大小 v2ProgressInfo.getTotalSize()
				}
				@Override
				public void onError(int code, String desc) {
					// 下载失败
				}
				@Override
				public void onSuccess() {
					// 下载完成
				}
			});
		} else {
			// 文件已存在
		}
	}
}
```
:::
::: iOS & Mac
```objectivec
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    if (msg.elemType == V2TIM_ELEM_TYPE_FILE) {
        V2TIMFileElem *fileElem = msg.fileElem;
        // 文件 ID,内部标识，可用于外部缓存 key
        NSString *uuid = fileElem.uuid;
        // 文件名称
        NSString *filename = fileElem.filename;
        // 文件大小
        int fileSize = fileElem.fileSize;
        // 设置文件路径，这里可以用 uuid 作为标识，避免重复下载
        NSString *filePath = [NSTemporaryDirectory() stringByAppendingPathComponent:[NSString stringWithFormat: @"testFile%@",uuid]];
        if (![[NSFileManager defaultManager] fileExistsAtPath:filePath]) {
            // 下载文件
            [fileElem downloadFile:filePath progress:^(NSInteger curSize, NSInteger totalSize) {
                // 下载进度
                NSLog(@"%@", [NSString stringWithFormat:@"下载文件进度：curSize：%lu,totalSize:%lu",curSize,totalSize]);
            } succ:^{
                // 下载成功
                NSLog(@"下载文件完成");
            } fail:^(int code, NSString *msg) {
                // 下载失败
                NSLog(@"%@", [NSString stringWithFormat:@"下载文件失败：code：%d,msg:%@",code,msg]);
            }];
        } else {
            // 文件已存在
        }
        NSLog(@"文件信息：uuid:%@, filename:%@, fileSize:%d, filePath:%@", uuid, filename, fileSize, filePath);
    }
}
```
:::
</dx-tabs>

### 地理位置消息

接收到地理位置消息后，接收放可直接从 `V2TIMLocationElem` 中解析出经纬度信息。
示例代码向您演示如何从 `V2TIMMessage` 中解析出地理位置消息内容：

<dx-tabs>
::: Android
```java
public void onRecvNewMessage(V2TIMMessage msg) {
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_LOCATION) {
		// 地理位置消息
		V2TIMLocationElem v2TIMLocationElem = msg.getLocationElem();
		// 地理位置信息描述
		String desc = v2TIMLocationElem.getDesc();
		// 经度
		double longitude = v2TIMLocationElem.getLongitude();
		// 纬度
		double latitude = v2TIMLocationElem.getLatitude();
	}
}
```
:::
::: iOS & Mac
```objectivec
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    if (msg.elemType == V2TIM_ELEM_TYPE_LOCATION) {
        V2TIMLocationElem *locationElem = msg.locationElem;
        // 地理位置信息描述
        NSString *desc = locationElem.desc;
        // 经度
        double longitude = locationElem.longitude;
        // 纬度
        double latitude = locationElem.latitude;
        NSLog(@"地理位置信息：desc：%@, longitude:%f, latitude:%f", desc, longitude, latitude);
    }
}
```
:::
</dx-tabs>

### 表情消息

SDK 仅为表情消息提供消息透传的通道，消息内容字段参考 `V2TIMFaceElem` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMFaceElem.html) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMFaceElem.html)) 定义。其中 `index` 和 `data` 的内容由客户自定义。

例如发送方可设置 index = 1, data = "x12345"，表示 “微笑“ 表情。
接收方收到表情消息后解析出 1 和 "x12345"，按照预设的规则将其展示为 “微笑“ 表情。

示例代码向您演示如何从 `V2TIMMessage` 中解析出表情消息内容：
<dx-tabs>
::: Android
```java
public void onRecvNewMessage(V2TIMMessage msg) {
	if (msg.getElemType() == V2TIMMessage.V2TIM_ELEM_TYPE_FACE) {
		// 表情消息
		V2TIMFaceElem v2TIMFaceElem = msg.getFaceElem();
		// 表情所在的位置
		int index = v2TIMFaceElem.getIndex();
		// 表情自定义数据
		byte[] data = v2TIMFaceElem.getData();
	}
}
```
:::
::: iOS & Mac
```objectivec
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    if (msg.elemType == V2TIM_ELEM_TYPE_FACE) {
        V2TIMFaceElem *faceElem = msg.faceElem;
        // 表情所在的位置
        int index = faceElem.index;
        // 表情自定义数据
        NSData *data = faceElem.data;
        NSLog(@"表情信息：index: %d, data: %@", index, data);
    }
}
```
:::
</dx-tabs>

## 接收多个 Elem 的消息

1. 通过 Message 对象正常解析出第一个 Elem 对象。
2. 通过第一个 Elem 对象的 `nextElem` 方法获取下一个 Elem 对象，如果下一个 Elem 对象存在，会返回 Elem 对象实例，如果不存在，会返回 nil/null。

示例代码如下：
<dx-tabs>
::: Android
```java
@Override
public void onRecvNewMessage(V2TIMMessage msg) {
	// 查看第一个 Elem
	int elemType = msg.getElemType();
	if (elemType == V2TIMMessage.V2TIM_ELEM_TYPE_TEXT) {
		// 文本消息
		V2TIMTextElem v2TIMTextElem = msg.getTextElem();
		String text = v2TIMTextElem.getText();
		// 查看 v2TIMTextElem 后面还有没有更多 elem
		V2TIMElem elem = v2TIMTextElem.getNextElem();
		while (elem != null) {
			// 判断 elem 类型，以 V2TIMCustomElem 为例
			if (elem instanceof V2TIMCustomElem) {
			V2TIMCustomElem customElem = (V2TIMCustomElem) elem;
			byte[] data = customElem.getData();
		}
		// 继续查看当前 elem 后面还有没更多 elem
		elem = elem.getNextElem();
		}
		// elem 如果为 null，表示所有 elem 都已经解析完
	}
}
```
:::
::: iOS & Mac
```objectivec
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    // 查看第一个 Elem
    if (msg.elemType == V2TIM_ELEM_TYPE_TEXT) {
        V2TIMTextElem *textElem = msg.textElem;
        NSString *text = textElem.text;
        NSLog(@"文本信息 : %@", text);
        // 查看 textElem 后面还有没更多 Elem
        V2TIMElem *elem = textElem.nextElem;
        while (elem != nil) {
            // 判断 elem 类型
            if ([elem isKindOfClass:[V2TIMCustomElem class]]) {
                V2TIMCustomElem *customElem = (V2TIMCustomElem *)elem;
                NSData *customData = customElem.data;
                NSLog(@"自定义信息 : %@",customData);
            }
            // 继续查看当前 elem 后面还有没更多 elem
            elem = elem.nextElem;
        }
        // elem 如果为 nil，表示所有 elem 都已经解析完
    }
}
```
:::
</dx-tabs>


