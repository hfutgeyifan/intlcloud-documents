## 功能描述
如果您想实现合并转发功能，需要进行以下步骤：
1. 根据原始消息列表创建一条合并消息。
2. 把合并消息发送到对端。
3. 对端收到合并消息后解析出原始消息列表。

合并消息的展示还需要标题和摘要信息，如下图所示：

| 合并转发                                                                                                | 合并消息展示                                                                                            | 点击合并消息下载合并消息列表展示                                                                       |
| ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| <img src="https://qcloudimg.tencent-cloud.cn/raw/cb970fdd471cdd668b5ce31d188970fd.png" width = "300" /> | <img src="https://qcloudimg.tencent-cloud.cn/raw/2304c7ea1e29de702f99d96e52a9739c.png" width = "300" /> | <img src="https://qcloudimg.tencent-cloud.cn/raw/f2c81dc8df0064cf8202d06a79f7af16.png" width = "300"/> |


## 合并转发消息
### 创建并发送合并转发消息

我们在创建一条合并消息的时候不仅要设置合并消息列表，还要设置标题和摘要信息，实现流程如下：
1. 创建一条合并消息，创建合并消息的时候需要设置原始消息列表，合并消息标题、合并消息摘要等信息。

<img src="https://qcloudimg.tencent-cloud.cn/raw/dbc9a0f199effcf6d865b6497ec185f3.pngg" width = "450" />

| 属性                       | 含义         | 说明                                                                                                           |
| -------------------------- | ------------ | -------------------------------------------------------------------------------------------------------------- |
| merge_elem_message_array   | 原始消息列表 | 合并转发的原始消息列表                                                                                         |
| merge_elem_title           | 标题         | 合并消息的标题，如上图所示 “xixiyah 和 Hello 的聊天记录”                                                       |
| merge_elem_abstract_array  | 摘要列表     | 合并消息的摘要信息，如上图所示，合并消息需要预先展示原始消息的摘要信息，当用户点击 Cell 后才去展示完整消息内容 |
| merge_elem_compatible_text | 兼容文本信息 | 低版本 SDK 如果不支持合并消息，默认会收到一条文本消息，文本消息的内容为 merge_elem_compatible_text             |

创建并发送合并消息示例代码如下：


```c#
// 需要被转发的消息列表，消息列表里可以包含合并消息，不能包含群 Tips 消息
var message = new Message
{
   message_conv_id = conv_id,
   message_conv_type = TIMConvType.kTIMConv_Group,
   message_elem_array = new List<Elem>{
    new Elem
   {
     elem_type = TIMElemType.kTIMElem_Merge,
     merge_elem_title = "user1与user2的聊天", // 合并消息标题
     merge_elem_message_array = new List<Message>
     {
      message1,
      message2
     },
     merge_elem_abstract_array = new List<string>
     {
      "user1:hello", "user2:你好" // 合并消息摘要列表
     },
     merge_elem_compatible_text = "当前版本不支持该消息" // 合并消息兼容文本，低版本 SDK 如果不支持合并消息，默认会收到一条文本消息，文本消息的内容为 compatibleText
   }},
};
StringBuilder messageId = new StringBuilder(128);
TIMResult res = TencentIMSDK.MsgSendMessage(conv_id, TIMConvType.kTIMConv_Group, message, messageId, (int code, string desc, string json_param, string user_data)=>{
 // 消息发送异步结果
});
```



### 接收合并转发消息

#### 添加监听器
接收方调用 `AddRecvNewMsgCallback` ([Details](https://comm.qq.com/im/doc/unity/en/api/SDKRegisteringCallback/AddRecvNewMsgCallback.html)) 添加消息监听器。
一般建议在比较靠前的时间点调用，例如例如聊天消息界面初始化后，确保 App 能及时收到消息。

示例代码如下：


```c#
TencentIMSDK.AddRecvNewMsgCallback((List<Message> messages, string user_data)=>{
  foreach(Message message in messages)
  {
    foreach (Elem elem in message.message_elem_array)
    {
      // 有下一个消息
      if (elem.elem_type == TIMElemType.kTIMElem_Merge)
      {
      }
    }
  }
})
```


#### 解析消息
添加监听器后，接收方会在 `RecvNewMsgCallback` 中收到合并消息 `Message`。
可以先通过合并消息元素获取 `merge_elem_title` 和  `merge_elem_abstract_array`  UI 展示。
当用户点击合并消息的时候再调用 `MsgDownloadMergerMessage`([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgDownloadMergerMessage.html)) 接口下载合并消息列表 UI 展示。

示例代码如下：


```c#
if(elem.TIMElemType == TIMElemType.kTIMElem_Merge){
   elem.merge_elem_abstract_array;
   elem.merge_elem_layer_over_limit;
   elem.merge_elem_title;
   TIMResult res = TencentIMSDK.MsgDownloadMergerMessage(message, (int code, string desc, List<Message> messages, string user_data)=>{
    // 处理异步逻辑
   });
}
```



## 逐条转发消息
如果您需要转发单条消息，可以先创建一条和原消息内容完全一样的转发消息，再调用 `MsgSendMessage` ([Details](https://comm.qq.com/im/doc/unity/en/api/MessageApi/MsgSendMessage.html)) 接口把转发消息发送出去。






