## 功能描述
群定向消息是指向群内部分成员发送消息，而其他群成员无法收到该消息。

> ?
> 1. 该功能需要购买旗舰版。
> 2. 创建定向群消息的原始消息对象不支持群 @ 消息。
> 3. 社群（Community）和直播群（AVChatRoom）不支持发送定向群消息。
> 4. 定向群消息默认不计入群会话的未读计数。

## 发送群定向消息
定向消息是指，向群内部分指定的成员发送消息，而未被指定的群成员无法收到该消息。可以按照下面的方式实现：
调用 `MsgSendMessage` ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgSendMessage.html)) 接口指定消息接收成员列表并发送定向消息。

示例代码如下：


```c#
var message = new Message
{
   message_conv_id = conv_id,
   message_conv_type = TIMConvType.kTIMConv_Group,
   message_elem_array = new List<Elem>{new Elem
   {
     elem_type = TIMElemType.kTIMElem_Text,
     text_elem_content = Input.text
   }},
   message_target_group_member_array = userid_list, //指定群消息接收成员用户 UserID 列表
};
StringBuilder messageId = new StringBuilder(128);
TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_Group, message, messageId, (int code, string desc, string json_param, string user_data)=>{
 // 消息发送异步结果
});
```


## 接收群定向消息
定向群消息默认不计入群会话的未读计数。
接收群定向消息跟接收普通消息是一样的操作步骤，参考[接收消息](https://www.tencentcloud.com/document/product/1047/48573)。




