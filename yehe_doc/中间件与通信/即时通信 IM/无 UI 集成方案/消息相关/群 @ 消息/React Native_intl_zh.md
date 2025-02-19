## 功能描述

群 @ 消息就是发送方监听输入栏里的输入字符，当用户输入 @ 字符后，弹出群成员选择界面。选择完需要 @ 的成员后以 `“@A @B @C......”` 形式显示在输入框，并可以继续编辑消息内容，完成消息发送。
接收方会在会话界面的群聊天列表，重点显示 `“有人@我”` 或者` “@所有人”` 标识，提醒用户有人在群里 @ 自己了。

> ? 目前仅支持文本 @ 消息。

## 功能演示

| 监听 @ 字符选择群成员                                                            | 编辑群 @ 消息发送                                                                | 收到群 @ 消息                                                                    |
| -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| ![](https://qcloudimg.tencent-cloud.cn/raw/ed60cac72b215f6e7128cf2533bab2f7.jpg) | ![](https://qcloudimg.tencent-cloud.cn/raw/fbabe9cac382a7944676565242b29b59.jpg) | ![](https://qcloudimg.tencent-cloud.cn/raw/b20c30564c78b9fec9ab25260110641f.jpg) |

图一：在聊天界面监听到输入框输入 "@" 字符后，可以跳转到群成员选择界面，选择需要 @ 的群成员。
图二：在群成员选择完成后，重新返回聊天界面，继续编辑群 @ 消息发送。
图三：如果有消息 @ 我，自己会收到会话更新，可以在会话 `Cell` 展示 “有人@我” 信息。

## 发送群 @ 消息

1. 发送方监听聊天界面的文本输入框，启动群成员选择界面。选择完成后回传选择群成员的 ID 和昵称信息，ID 用来构建消息对象 `V2TimMessage`，昵称用来在文本框显示。
2. 发送方调用 `createTextAtMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/createTextAtMessage.html)) 接口创建一条 @ 文本消息，拿到消息对象 `V2TIMMessage`，并在其中指定需要 @ 的成员。
3. 发送方调用 `sendMessage` ([Details](https://comm.qq.com/im/doc/RN/en/Api/V2TIMMessageManager/sendMessage.html)) 接口将刚才创建的 @ 消息对象发送出去。

示例代码如下：

```javascript
const text = "123";
const atUserList = ['user1','user2','all'];

// 创建群@消息
const atMsgRes = await TencentImSDKPlugin.v2TIMManager.getMessageManager().createTextAtMessage(text, atUserList);
// 发送群@消息
TencentImSDKPlugin.v2TIMManager.getMessageManager().sendMessage(
          id: atMsgRes.data.id,
          receiver: "",
          groupID: "",
);
```

## 接收群 @ 消息

1. 在加载和更新会话处，需要调用 `V2TimConversation` 的 `groupAtInfolist` ([Details](https://comm.qq.com/im/doc/RN/en/Interface/Message/V2TimConversation.html#groupatinfolist)) 接口获取会话的 @ 数据列表。
2. 通过列表中 `V2TimGroupAtInfo` 对象的 `atType` ([Details](https://comm.qq.com/im/doc/RN/en/Interface/Group/V2TimGroupAtInfo.html#attype)) 接口获取 @ 数据类型，并更新到当前会话的 @ 信息。

示例代码如下：

```javascript
const nextSeq = "";
const count = 10;
const getConversationList = await TencentImSDKPlugin.v2TIMManager
  .getConversationManager()
  .getConversationList(nextSeq, count);
if (getConversationList.code == 0) {
  getConversationList.data.conversationList.forEach((element) => {
    element.groupAtInfoList.forEach((element) => {
      if (element.atType == 0) {
        // @我
      }
      if (element.atType == 1) {
        // @all
      }
      if (element.atType == 2) {
        // @all&@我
      }
    });
  });
}
```


