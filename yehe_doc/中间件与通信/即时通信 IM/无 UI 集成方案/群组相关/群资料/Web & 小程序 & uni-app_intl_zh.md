## 功能描述

群资料指的是与群组相关的一些信息，相关属性在核心类 [Group](https://web.sdk.qcloud.com/im/doc/en/Group.html) 中。

## 获取群资料

**接口**

<dx-codeblock>
:::  js

tim.getGroupProfile(options);

:::
</dx-codeblock>

**参数**

参数 options 为 Object 类型，包含的属性值如下：

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID     | String | 		群组 ID |
| groupCustomFieldFilter | Array \| undefined | 群组维度的自定义字段过滤器，指定需要获取的群组维度的自定义字段，详情请参阅 [自定义字段](https://intl.cloud.tencent.com/document/product/1047/33529) |

**返回值**

`Promise` 对象。

**示例**

<dx-codeblock>
:::  js

let promise = tim.getGroupProfile({ groupID: 'group1', groupCustomFieldFilter: ['key1','key2'] });
promise.then(function(imResponse) {
  console.log(imResponse.data.group);
}).catch(function(imError) {
  console.warn('getGroupProfile error:', imError); // 获取群详细资料失败的相关信息
});

:::
</dx-codeblock>

## 修改群资料

**接口**

<dx-codeblock>
:::  js

tim.updateGroupProfile(options);

:::
</dx-codeblock>

参数 options 为 Object 类型，包含的属性值如下：

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupID     | String | 		群组 ID |
| name | String \| undefined | 群名称，最长30字节 |
| avatar | String \| undefined | 群头像 URL，最长100字节 |
| introduction | String \| undefined | 群简介，最长240字节 |
| notification | String \| undefined | 群公告，最长300字节 |
| maxMemberNum | Number \| undefined | 最大群成员数量，最大为6000 |
| muteAllMembers | Boolean \| undefined | 设置全体禁言，true 表示全体禁言，false 表示取消全体禁言，v2.6.2 起支持 |
| joinOption | String | 申请加群处理方式。<br/><li>TIM.TYPES.JOIN_OPTIONS_FREE_ACCESS （自由加入）</li><li>TIM.TYPES.JOIN_OPTIONS_NEED_PERMISSION （需要验证）</li><li>TIM.TYPES.JOIN_OPTIONS_DISABLE_APPLY （禁止加群）</li>注意：TIM.TYPES.GRP_WORK, TIM.TYPES.GRP_MEETING, TIM.TYPES.GRP_AVCHATROOM 类型群组的该属性不允许修改。好友工作群禁止申请加群，临时会议群和直播群自由加入。 |
| groupCustomField | Array \| undefined | 群自定义字段。默认情况是没有的。开通群组维度的自定义字段详情请参见 [自定义字段](https://intl.cloud.tencent.com/document/product/1047/33529) |

**返回值**

`Promise` 对象。

**示例**

<dx-codeblock>
:::  js

let promise = tim.updateGroupProfile({
  groupID: 'group1',
  name: 'new name', // 修改群名称
  introduction: 'this is introduction.', // 修改群简介
  // v2.6.0 起，群成员能收到群自定义字段变更的群提示消息，且能获取到相关的内容，详见 Message.payload.newGroupProfile.groupCustomField
  groupCustomField: [{ key: 'group_level', value: 'high'}] // 修改群组维度自定义字段
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // 修改成功后的群组详细资料
}).catch(function(imError) {
  console.warn('updateGroupProfile error:', imError); // 修改群组资料失败的相关信息
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// v2.6.2 起，提供了全体禁言和取消禁言的功能。目前群全体禁言后，不支持下发群提示消息。
let promise = tim.updateGroupProfile({
  groupID: 'group1',
  muteAllMembers: true, // true 表示全体禁言，false表示取消全体禁言
});
promise.then(function(imResponse) {
  console.log(imResponse.data.group) // 修改成功后的群组详细资料
}).catch(function(imError) {
  console.warn('updateGroupProfile error:', imError); // 修改群组资料失败的相关信息
});

:::
</dx-codeblock>

