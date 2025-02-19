## 功能描述
删除消息分为两种：删除本地消息和删除云端消息。
删除云端消息会在删除本地消息的基础上，同步删除云端存储的消息，且**无法恢复**。

如果删除的是最后一条消息，会话的 `lastMessage` 会变为前一条消息。
* 如果您的 SDK 版本是 5.5.892 之前，使用了 `lastMesasge` 进行排序，此时会影响您的会话列表顺序。
* 如果你的 SDK 版本是 5.5.892 及以后，并且采用了 `orderKey` 进行排序，此时不影响您的会话列表顺序。
详情请参考 [会话列表](https://intl.cloud.tencent.com/document/product/1047/48326)。

### 删除本地消息

您可以调用 `deleteMessageFromLocalStorage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#aa31e3b48fb666b970120fc0bc6343534) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a2bb42528f4d166ac826914094655841c)) 删除本地消息。

> ?
> 1. 该接口只能删除本地历史。消息删除后，SDK 会在本地把这条消息标记为已删除状态，调用 `getHistoryMessage` 不能拉取到。
> 2. 如果程序卸载重装，本地会失去对这条消息的删除标记，调用 `getHistoryMessage` 能拉取到该条消息。

示例代码如下：
<dx-tabs>
::: Android
```java
// selectedMsg 为用户选中待删除的消息
V2TIMManager.getMessageManager().deleteMessageFromLocalStorage(selectedMsg, new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// 删除本地消息成功
  }

  @Override
  public void onError(int code, String desc) {
  	// 删除本地消息失败
  }
});
```
:::
::: iOS & Mac 
```objectivec
// selectedMsg 为用户选中待删除的消息
[[V2TIMManager sharedInstance] deleteMessageFromLocalStorage:selectedMessage
                                                        succ:^{
    NSLog(@"删除本地消息成功");
} fail:^(int code, NSString *msg) {
    NSLog(@"删除本地消息失败, code: %d, desc: %@", code, msg);
}];
```
:::
</dx-tabs>


### 删除云端存储的消息

您可以调用 `deleteMessages` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#adb346fede13d493e415f6574df911e9a) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a9e394ea720ecdc10d497b63b6f2b22c4)) 删除云端存储的消息。

该接口会在删除本地消息的基础上，同步删除云端存储的消息，且无法恢复。

> ?
> 1. 每次调用，最多只能删除 30 条消息。
> 2. 每次调用，待删除的消息**必须**属于同一会话。
> 3. 接口限频：1 秒钟最多只能调用 1 次该接口。
> 4. 如果一个账号在某设备上拉取过这些消息，那么调用该接口删除云端消息后，这些消息仍然会保存在该设备上，即删除消息不支持多端同步。

示例代码如下：
<dx-tabs>
::: Android
```java
// selectedMessageList 为用户选中待删除的消息列表
V2TIMManager.getMessageManager().deleteMessages(selectedMessageList, new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// 删除云端消息成功
  }

  @Override
  public void onError(int code, String desc) {
  	// 删除云端消息失败
  }
});
```
:::
::: iOS & Mac
```objectivec
// selectedMessageList 为用户选中待删除的消息列表
NSArray *selectedMessageList = @[selectedMessage1, selectedMessage2];
[[V2TIMManager sharedInstance] deleteMessages:selectedMessageList
                                        succ:^{
    NSLog(@"删除云端消息成功");
} fail:^(int code, NSString *desc) {
    NSLog(@"删除云端消息失败, code: %d, desc: %@", code, desc);
}];
```
:::
</dx-tabs>

