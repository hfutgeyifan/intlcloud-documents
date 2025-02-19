## 功能描述
发送方可以撤回一条已经发送成功的消息。

默认情况下，发送者只能撤回 2 分钟以内的消息，您可以按需更改消息撤回时间限制，具体操作请参见 [消息撤回设置](https://intl.cloud.tencent.com/document/product/1047/34419)。

消息的撤回同时需要接收方 UI 代码的配合：当发送方撤回一条消息后，接收方会收到消息撤回通知 `onRecvMessageRevoked`。通知中包含了撤回消息的 msgID，您可以根据这个 msgID 判断 UI 层是哪一条消息撤回了，然后把对应的消息气泡切换成 "消息已被撤回" 状态。

## 发送方撤回消息
发送方可调用 `revokeMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#ad0dfce6be749165cd90a9ff67a1308b1) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a972ac3fb7744458eb0d6abd96ce35126)) 撤回一条消息。

示例代码如下：
<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().revokeMessage(v2TIMMessage, new V2TIMCallback() {
	@Override
	public void onError(int code, String desc) {
		// 撤回消息失败
	}
	@Override
	public void onSuccess() {
		// 撤回消息成功
	}
});
```
:::
::: iOS & Mac
```objectivec
// selectedMessage 为待撤回消息
[[V2TIMManager sharedInstance] revokeMessage:selectedMessage
										succ:^{
	// 撤回消息成功
} fail:^(int code, NSString *msg) {
	// 撤回消息失败
}];
```
:::
</dx-tabs>

## 接收方感知消息被撤回
1. 接收方调用 `addAdvancedMsgListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aaccdec10b9fbee5e43eaf908e359c823) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#acf794752cc6bfa786aea5cd7fabadfab)) 设置高级消息监听。
2. 接收方在 `onRecvMessageRevoked` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMAdvancedMsgListener.html#a13d8197eaba83bfadc7a2f695d671272) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/protocolV2TIMAdvancedMsgListener-p.html)) 中接收消息撤回通知。

示例代码如下：
<dx-tabs>
::: Android
```java
V2TIMManager.getMessageManager().addAdvancedMsgListener(new V2TIMAdvancedMsgListener() {
	@Override
	public void onRecvMessageRevoked(String msgID) {
		// msgList 为当前聊天界面的消息列表
		for (V2TIMMessage msg : msgList) {
			if (msg.getMsgID().equals(msgID)) {
				// msg 即为被撤回的消息，您需要修改 UI 上相应的消息气泡的状态
			}
		}
	}
}
```
:::
::: iOS & Mac
```objectivec
// V2TIMAdvancedMsgListener
- (void)onRecvMessageRevoked:(NSString *)msgID {
	// 收到消息撤回通知，您需要修改 UI 上相应的消息气泡的状态
}
```
:::
</dx-tabs>

