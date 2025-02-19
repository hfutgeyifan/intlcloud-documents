## 会话介绍
当用户创建了一个单聊或群聊，对应的会话就随之创建。
在腾讯云 IM SDK 中，会话类为 `ConvInfo`。您可以使用会话管理类中的 API 实现会话列表展示/更新、会话未读数更新、置顶会话、会话草稿、会话免打扰等功能。

## 会话类介绍
会话类为 `ConvInfo` ([Details](https://comm.qq.com/im/doc/unity/en/types/ConvAttributes/ConvInfo.html))。`ConvInfo` 定义了以下内容：

| 属性                     | 含义                   | 说明                                                                                                                                   |
| ------------------------ | ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| conv_type                | 会话类型               | 参考 `TIMConvType` 定义。分为 C2C（单聊）和 Group（群聊）。                                                                            |
| conv_id                  | 会话唯一 ID            | 如果是单聊，组成方式为 c2c_userID；如果是群聊，组成方式为 group_groupID。                                                              |
| conv_active_time         | 会话的激活时间         |                                                                                                                                        |
| conv_is_has_lastmsg      | 会话是否有最后一条消息 |                                                                                                                                        |
| conv_show_name           | 会话展示名称           | 群聊会话名称优先级：群名称 > 群 ID；<br>单聊会话名称优先级：对方好友备注 > 对方昵称 > 对方的 userID。                                  |
| conv_unread_num          | 会话未读消息数         | 直播群（AVChatRoom）不支持未读计数，默认为 0。                                                                                         |
| conv_recv_opt            | 消息接收选项           | 参考 `TIMReceiveMessageOpt` 定义。                                                                                                     |
| conv_last_msg            | 会话最后一条消息       | 具体使用请参考 [会话列表](https://comm.qq.com/im/doc/unity/en/api/ConvApi/ConvGetConvInfo.html)。                                      |
| conv_group_at_info_array | 群会话 @ 信息列表      | 通常用于展示 “有人@我” 或 “@所有人” 这两种提醒状态。                                                                                   |
| conv_draft               | 草稿信息               | 设置草稿信息请调用 `ConvSetDraft` 接口，具体实现请参考 [会话草稿](https://comm.qq.com/im/doc/unity/en/api/ConvApi/ConvSetDraft.html)。 |
| conv_is_has_draft        | 会话是否有草稿         |                                                                                                                                        |
| conv_is_pinned           | 会话是否置顶           | 具体使用请参考 [置顶会话](https://comm.qq.com/im/doc/unity/en/api/ConvApi/ConvPinConversation.html)。                                  |

## 会话存储策略
本地存储的会话列表没有数量上限。
云端存储的会话列表最大数量为 100。如果您希望扩展此数量，可以升级旗舰版。旗舰版用户可以在控制台配置最高数量为 500。

云端存储的会话列表最大数量为 100。如果您希望扩展此数量，可以升级旗舰版。旗舰版用户可以在控制台配置最高数量为 500，配置页面如下图所示：

![](https://qcloudimg.tencent-cloud.cn/raw/ba00871ad091df6fbe7cbf0ceb0e7607.png)

如果一个会话长时间没有信息变更，该会话在云端最多保存 7 天。如需放宽限制，请 [联系我们](https://console.cloud.tencent.com/workorder/category)。

本地存储的会话和云端存储的会话并不总是一致的，如果用户不主动调用 `ConvDelete` 接口删除本地的会话，该会话就会一直存在。而云端存储的会话最大只会保存 100 条，且对于长时间没有信息变更的会话，云端最多保存 7 天，所以不同的终端本地显示的会话可能会不一样。

