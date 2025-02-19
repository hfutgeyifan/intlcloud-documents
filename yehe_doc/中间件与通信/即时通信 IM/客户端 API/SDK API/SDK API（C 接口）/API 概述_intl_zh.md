腾讯即时通信 IM 的跨平台 C 接口（API）。

**各个平台的下载链接：**

- Windows 平台 [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/Windows)，Windows 快速开始 [集成 IM SDK](https://intl.cloud.tencent.com/document/product/1047/34310) 和 [一分钟跑通 Demo](https://intl.cloud.tencent.com/document/product/1047/34553)。支持32位/64位系统。
- iOS 平台 [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/iOS/IMSDK)。
- Mac 平台 [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/Mac/IMSDK)。
- Android 平台 [IM SDK](https://github.com/tencentyun/TIMSDK/tree/master/Android/IMSDK)。

回调分两种，一种是指调用接口的异步返回，另外一种指后台推送的通知。回调在 IM SDK 内部的逻辑线程触发，跟调用接口的线程可能不是同一线程。
在 Windows 平台，如果调用 [TIMInit](https://intl.cloud.tencent.com/document/product/1047/34388) 接口进行初始化 IM SDK 之前，已创建了 UI 的消息循环，且调用 [TIMInit](https://intl.cloud.tencent.com/document/product/1047/34388) 接口的线程为主 UI 线程，则 IM SDK 内部会将回调抛到主 UI 线程调用。

>!如果接口的参数字符串包含中文，请使用 UTF-8 编码。



### 事件回调接口

| API | 描述 |
|-----|-----|
| [TIMAddRecvNewMsgCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | 增加接收新消息回调 |
| [TIMRemoveRecvNewMsgCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | 删除接收新消息回调 |
| [TIMSetMsgReadedReceiptCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | 设置消息已读回执回调 |
| [TIMSetMsgRevokeCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | 设置接收的消息被撤回回调 |
| [TIMSetMsgElemUploadProgressCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | 设置消息内元素相关文件上传进度回调 |
| [TIMSetGroupTipsEventCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | 设置群组系统消息回调 |
| [TIMSetConvEventCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | 设置会话事件回调 |
| [TIMSetNetworkStatusListenerCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | 设置网络连接状态监听回调 |
| [TIMSetKickedOfflineCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | 设置被踢下线通知回调 |
| [TIMSetUserSigExpiredCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | 设置票据过期回调 |
| [TIMSetOnAddFriendCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | 设置添加好友的回调 |
| [TIMSetOnDeleteFriendCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | 设置删除好友的回调 |
| [TIMSetUpdateFriendProfileCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | 设置更新好友资料的回调 |
| [TIMSetFriendAddRequestCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | 设置好友添加请求的回调 |
| [TIMSetLogCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | 设置日志回调 |
| [TIMSetMsgUpdateCallback](https://intl.cloud.tencent.com/document/product/1047/34389) | 设置消息在云端被修改后回传回来的消息更新通知回调 |


### IM SDK 初始化相关接口

| API | 描述 |
|-----|-----|
| [TIMInit](https://intl.cloud.tencent.com/document/product/1047/34388) | IM SDK 初始化 |
| [TIMUninit](https://intl.cloud.tencent.com/document/product/1047/34388) | IM SDK 卸载 |
| [TIMGetSDKVersion](https://intl.cloud.tencent.com/document/product/1047/34388) | 获取 IM SDK 版本号 |
| [TIMSetConfig](https://intl.cloud.tencent.com/document/product/1047/34388) | 设置额外的用户配置 |


### 登录登出相关接口

| API | 描述 |
|-----|-----|
| [TIMLogin](https://intl.cloud.tencent.com/document/product/1047/34390) | 登录 |
| [TIMLogout](https://intl.cloud.tencent.com/document/product/1047/34390) | 登出 |


### 会话相关接口

| API | 描述 |
|-----|-----|
| [TIMConvCreate](https://intl.cloud.tencent.com/document/product/1047/34557) | 创建会话 |
| [TIMConvDelete](https://intl.cloud.tencent.com/document/product/1047/34557) | 删除会话 |
| [TIMConvGetConvList](https://intl.cloud.tencent.com/document/product/1047/34557) | 获取最近联系人的会话列表 |
| [TIMConvSetDraft](https://intl.cloud.tencent.com/document/product/1047/34557) | 设置指定会话的草稿 |
| [TIMConvCancelDraft](https://intl.cloud.tencent.com/document/product/1047/34557) | 删除指定会话的草稿 |


### 消息相关接口

| API | 描述 |
|-----|-----|
| [TIMMsgSendNewMsg](https://intl.cloud.tencent.com/document/product/1047/34391) | 发送新消息 |
| [TIMMsgReportReaded](https://intl.cloud.tencent.com/document/product/1047/34391) | 消息上报已读 |
| [TIMMsgRevoke](https://intl.cloud.tencent.com/document/product/1047/34391) | 消息撤回 |
| [TIMMsgFindByMsgLocatorList](https://intl.cloud.tencent.com/document/product/1047/34391) | 根据消息定位精准查找指定会话的消息 |
| [TIMMsgImportMsgList](https://intl.cloud.tencent.com/document/product/1047/34391) | 导入消息列表到指定会话 |
| [TIMMsgSaveMsg](https://intl.cloud.tencent.com/document/product/1047/34391) | 保存自定义消息 |
| [TIMMsgGetMsgList](https://intl.cloud.tencent.com/document/product/1047/34391) | 获取指定会话的消息列表 |
| [TIMMsgDelete](https://intl.cloud.tencent.com/document/product/1047/34391) | 删除指定会话的消息 |
| [TIMMsgDownloadElemToPath](https://intl.cloud.tencent.com/document/product/1047/34391) | 下载消息内元素到指定文件路径（图片、视频、音频、文件） |
| [TIMMsgBatchSend](https://intl.cloud.tencent.com/document/product/1047/34391) | 群发消息，该接口不支持向群组发送消息。 |


### 群组相关接口

| API | 描述 |
|-----|-----|
| [TIMGroupCreate](https://intl.cloud.tencent.com/document/product/1047/34393) | 创建群组 |
| [TIMGroupDelete](https://intl.cloud.tencent.com/document/product/1047/34393) | 删除（解散）群组 |
| [TIMGroupJoin](https://intl.cloud.tencent.com/document/product/1047/34393) | 申请加入群组 |
| [TIMGroupQuit](https://intl.cloud.tencent.com/document/product/1047/34393) | 退出群组 |
| [TIMGroupInviteMember](https://intl.cloud.tencent.com/document/product/1047/34393) | 邀请加入群组 |
| [TIMGroupDeleteMember](https://intl.cloud.tencent.com/document/product/1047/34393member) | 删除群组成员 |
| [TIMGroupGetJoinedGroupList](https://intl.cloud.tencent.com/document/product/1047/34393) | 获取已加入群组列表 |
| [TIMGroupGetGroupInfoList](https://intl.cloud.tencent.com/document/product/1047/34393) | 获取群组信息列表 |
| [TIMGroupModifyGroupInfo](https://intl.cloud.tencent.com/document/product/1047/34393) | 修改群信息 |
| [TIMGroupGetMemberInfoList](https://intl.cloud.tencent.com/document/product/1047/34393) | 获取群成员信息列表 |
| [TIMGroupModifyMemberInfo](https://intl.cloud.tencent.com/document/product/1047/34393) | 修改群成员信息 |
| [TIMGroupGetPendencyList](https://intl.cloud.tencent.com/document/product/1047/34393) | 获取群未决信息列表。<br/>群未决信息是指还没有处理的操作，例如，邀请加群或者请求加群操作还没有被处理，称之为群未决信息 |
| [TIMGroupReportPendencyReaded](https://intl.cloud.tencent.com/document/product/1047/34393) | 上报群未决信息已读 |
| [TIMGroupHandlePendency](https://intl.cloud.tencent.com/document/product/1047/34393) | 处理群未决信息 |


### 用户资料相关接口

| API | 描述 |
|-----|-----|
| [TIMProfileGetUserProfileList](https://intl.cloud.tencent.com/document/product/1047/34558) | 获取指定用户列表的个人资料 |
| [TIMProfileModifySelfUserProfile](https://intl.cloud.tencent.com/document/product/1047/34558) | 修改自己的个人资料 |


### 关系链相关接口

| API | 描述 |
|-----|-----|
| [TIMFriendshipGetFriendProfileList](https://intl.cloud.tencent.com/document/product/1047/34559) | 获取好友列表 |
| [TIMFriendshipAddFriend](https://intl.cloud.tencent.com/document/product/1047/34559) | 添加好友 |
| [TIMFriendshipHandleFriendAddRequest](https://intl.cloud.tencent.com/document/product/1047/34559) | 处理好友请求 |
| [TIMFriendshipModifyFriendProfile](https://intl.cloud.tencent.com/document/product/1047/34559) | 更新好友资料（备注等） |
| [TIMFriendshipDeleteFriend](https://intl.cloud.tencent.com/document/product/1047/34559) | 删除好友 |
| [TIMFriendshipCheckFriendType](https://intl.cloud.tencent.com/document/product/1047/34559) | 检测好友类型（单向或双向） |
| [TIMFriendshipCreateFriendGroup](https://intl.cloud.tencent.com/document/product/1047/34559) | 创建好友分组 |
| [TIMFriendshipGetFriendGroupList](https://intl.cloud.tencent.com/document/product/1047/34559) | 获取指定好友分组的分组信息 |
| [TIMFriendshipModifyFriendGroup](https://intl.cloud.tencent.com/document/product/1047/34559) | 修改好友分组 |
| [TIMFriendshipDeleteFriendGroup](https://intl.cloud.tencent.com/document/product/1047/34559group) | 删除好友分组 |
| [TIMFriendshipAddToBlackList](https://intl.cloud.tencent.com/document/product/1047/34559) | 添加指定用户到黑名单 |
| [TIMFriendshipGetBlackList](https://intl.cloud.tencent.com/document/product/1047/34559) | 获取黑名单列表 |
| [TIMFriendshipDeleteFromBlackList](https://intl.cloud.tencent.com/document/product/1047/34559) | 从黑名单中删除指定用户列表 |
| [TIMFriendshipGetPendencyList](https://intl.cloud.tencent.com/document/product/1047/34559) | 获取好友添加请求未决信息列表 |
| [TIMFriendshipDeletePendency](https://intl.cloud.tencent.com/document/product/1047/34559) | 删除指定好友添加请求未决信息 |
| [TIMFriendshipReportPendencyReaded](https://intl.cloud.tencent.com/document/product/1047/34559) | 上报好友添加请求未决信息已读 |



