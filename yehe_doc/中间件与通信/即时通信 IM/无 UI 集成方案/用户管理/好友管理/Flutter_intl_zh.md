## 功能描述
IM SDK 支持好友的管理，用户可以主动添加、删除好友，也可以设置仅针对好友才能发送消息。

### 获取好友列表
IM SDK 支持好友关系链逻辑，您可以调用 `getFriendList` ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/getFriendList.html)) 接口获取好友列表。

示例代码如下：


```dart
// 获取好友列表
V2TimValueCallback<List<V2TimFriendInfo>> friendsList = await friendshipManager.getFriendList();
```



### 添加好友
您可以调用 `addFriend` ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/addFriend.html)) 接口添加好友。

示例代码如下：


```dart
// 添加双向好友
V2TimValueCallback<V2TimFriendOperationResult> addFriend = await friendshipManager.addFriend(userID: "userID",remark:"加好友的备注",addWording:"附言",addType:FriendTypeEnum.V2TIM_FRIEND_TYPE_BOTH);
```


根据对方用户资料中的加好友需要验证与否，可以分为两种处理流程：

#### 第一种：加好友不需要对方验证
1. 用户 A 和 B 调用 `setFriendListener` 设置关系链监听器。

2. 用户 B 通过 `setSelfInfo` 函数里的 `allowType` ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/models_v2_tim_user_full_info/V2TimUserFullInfo/allowType.html)) 字段设置为加好友不需要验证（`V2TIM_FRIEND_ALLOW_ANY`）。

3. 用户 A 调用 `addFriend` 申请添加 B 为好友即可添加成功。添加成功后，按照申请参数 `V2TIMFriendAddApplication` 中 `addType` 的设置有两种情况：
   * 如果设置为双向好友 (`V2TIM_FRIEND_TYPE_BOTH`) ，则用户 A 和 B 都会收到 `onFriendListAdded` ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimFriendshipListener/V2TimFriendshipListener/onFriendListAdded.html)) 回调；
   * 如果设置为单向好友（`V2TIM_FRIEND_TYPE_SINGLE`），则只有用户 A 收到 `onFriendListAdded` 回调。


#### 第二种：加好友需要通过对方验证
1. 用户 A 和 B 调用 `setFriendListener` 设置关系链监听。

2. 用户 B 通过 `setSelfInfo` 函数里的 `allowType` 字段设置为加好友需要验证（`V2TIM_FRIEND_NEED_CONFIRM`）。 
   
3. 用户 A 调用  `addFriend` 申请添加 B 为好友，接口的成功回调参数中 `resultCode` 返回 30539，表示需要等待用户 B 的验证。同时 A 和 B 都会收到 `onFriendApplicationListAdded` ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimFriendshipListener/V2TimFriendshipListener/onFriendApplicationListAdded.html)) 的回调。
   
4. 用户 B 会收到 `onFriendApplicationListAdded` 的回调，当参数 `V2TIMFriendApplication` 中的 `type` 为 `V2TIM_FRIEND_APPLICATION_COME_IN` 时，可以选择接受或者拒绝：
    - B 调用 `acceptFriendApplication` ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/acceptFriendApplication.html)) 接受好友请求。如果参数接受类型为仅同意加单向好友（`V2TIM_FRIEND_ACCEPT_AGREE`）时:
      - A 会收到 `onFriendListAdded` 回调，说明单向加好友成功。
      - B 会收到 `onFriendApplicationListDeleted` ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/enum_V2TimFriendshipListener/V2TimFriendshipListener/onFriendApplicationListDeleted.html)) 回调，此时 B 成为 A 的好友，但 A 仍不是 B 的好友。
    - B 调用 `acceptFriendApplication` 接受好友请求，如果参数接受类型为同意加双向好友时（`V2TIM_FRIEND_ACCEPT_AGREE_AND_ADD`），A 和 B 都会收到 `onFriendListAdded` 回调，说明互相加好友成功。
    - B 调用 `refuseFriendApplication` ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/refuseFriendApplication.html)) 拒绝好友请求，双方都会收到 `onFriendApplicationListDeleted` 回调。


### 删除好友
您可以调用 `deleteFromFriendList` ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/deleteFromFriendList.html)) 接口删除好友关系。

示例代码如下：


```dart
// 删除双向好友
V2TimValueCallback<List<V2TimFriendOperationResult>> deleteres = await friendshipManager.deleteFromFriendList(deleteType: FriendTypeEnum.V2TIM_FRIEND_TYPE_BOTH,userIDList:['user1']);
```



### 检查好友关系
您可以调用 `checkFriend` ([Details](https://pub.dev/documentation/tencent_im_sdk_plugin_platform_interface/latest/im_flutter_plugin_platform_interface/ImFlutterPlatform/checkFriend.html)) 接口检查好友关系。

示例代码如下：


```dart
// 检测好友是否有双向（单向）好友关系。
V2TimValueCallback<List<V2TimFriendCheckResult>> checkres = await friendshipManager.checkFriend(checkType:FriendTypeEnum.V2TIM_FRIEND_TYPE_BOTH,userIDList: [] );
```


### 设置只能给好友发消息
IM SDK 在发送单聊消息的时候，默认不检查好友关系。在客服场景中，如果用户需要先加客服为好友才能进行沟通非常不方便，因此该默认设置常用于在线客服等场景。
如需实现“先加好友，再发消息”的交互体验，您可以在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) >【功能配置】>【登录与消息】>【好友关系检查】中开启"发送单聊消息检查关系链"。开启后，用户只能给好友发送消息，当用户给非好友发消息时，SDK 会报 20009 错误码。



