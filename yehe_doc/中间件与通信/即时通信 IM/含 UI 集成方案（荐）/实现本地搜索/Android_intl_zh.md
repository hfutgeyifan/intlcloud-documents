TUIKit 中的 TUISearch 实现了本地搜索，支持搜索本地存储的聊天记录、联系人、群聊等。搜索可以帮助用户从纷繁的信息中快速找到目标，也可作为运营工具，增加相关内容的引导，简洁高效。

>! “本地搜索”为 IM 旗舰版功能，[购买旗舰版](https://intl.cloud.tencent.com/document/product/1047/34577) 后可使用，详见 [价格说明](https://intl.cloud.tencent.com/document/product/1047/34350)。


## 功能展示
搜索接口的界面分为多个部分，第一部分是搜索好友，第二部分是搜索群组、群成员，第三部分是搜索消息且按照会话分组。
您可通过 [下载安装应用](https://intl.cloud.tencent.com/document/product/1047/34279) 即刻体验，效果如下：
![](https://im.sdk.qcloud.com/tools/resource/search.gif)

## 接入指引
以下步骤将向您演示如何接入 TUISearch 组件。

### 购买套餐包
请单击前往 [购买旗舰版](https://intl.cloud.tencent.com/document/product/1047/34577)。

### 集成 TUISearch
在 `APP` 的 `build.gradle` 文件中添加对 `tuisearch` 的依赖：
```groovy
api project(':tuisearch')
```

### 登录 TUIKit
您需要调用 `TUICore` 的 `TUILogin` 登录 TUIKit。登录接口内部会默认初始化，不需要额外调用初始化。
```
TUILogin.login(this, SDKAPPID, userID, userSig, new TUICallback() {
    @Override
    public void onError(final int code, final String desc) {
        // 登录失败
    }

    @Override
    public void onSuccess() {
        // 登录成功
    }
});
```

### 启动搜索界面
如果您集成了 TUIConversation 和 TUISearch 组件，此时不需要额外处理，searchBar 默认展示在会话列表的上方。
如果您仅集成 TUISearch，此时需要添加自己的搜索视图，然后点击启动 SearchMainActivity 即可。


## 常见问题
1、如何搜索自定义消息
您需要使用接口 [createCustomMessage (byte[] data, String description, byte[] extension)](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a313b1ea616f082f535946c83edd2cc7f) 来创建并发送自定义消息，把需要搜索的文本放到 `description` 参数中。
如果您使用接口 [createCustomMessage (byte[] data)](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a5c2495d4b7ecd66e5636aeb865c17efd) 创建自定义消息，本地保存的是二进制数据流，无法被搜索到。

如果您配置了离线推送功能，参数 `description` 设置后，自定义消息也会有离线推送且通知栏展示该参数内容。
如果不需要离线推送可以用发消息接口 [sendMessage](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a28e01403acd422e53e999f21ec064795) 的参数 [V2TIMOfflinePushInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html) 中的 [disablePush](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a5d0ea30668513f45eda447875528b9c7) 来控制。
如果推送的通知栏内容不想展示为被搜索的文本，可以用参数  [V2TIMOfflinePushInfo](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html) 中的 [setDesc](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMOfflinePushInfo.html#a78c8e202aa4e0859468ce40bde6fd602) 来另外设置推送内容。

2、如何搜索富媒体消息
富媒体消息包含文件、图片、语音、视频消息。
对于文件消息，界面通常显示文件名，因此创建时可以设置 `fileName` 参数，作为被搜索的内容，如果 `fileName` 不设置则会从 `filePath` 提取文件名，并且都会保存到本地和服务器。
而对于图片、语音、视频消息，界面通常显示缩略图或时长，可以指定消息类型做分类搜索，但不能通过关键字搜索。

[](id:feedback)


