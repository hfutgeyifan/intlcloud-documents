
## 功能描述
在某些场景下，您可能需要对会话进行分组，例如分为 "产品体验"、"需求研发" 等，您可以调用以下接口实现。
> ?
- 该功能仅对旗舰版客户开放，购买 [旗舰版](https://www.tencentcloud.com/document/product/1047/34577) 后可使用。
- 该功能仅v2.22.0及以上版本支持。

## 会话分组

### 新建会话分组
您可以调用 [createConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#createConversationGroup) 接口新建会话分组。调用接口成功后 SDK 会派发事件 [TIM.EVENT.CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) 和 [TIM.EVENT.CONVERSATION_GROUP_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_GROUP_LIST_UPDATED)。
>? 会话分组最大支持 20 个，超过后创建新的分组会报 `51010` 错误，不再使用的分组请及时删除。


**接口**

<dx-codeblock>
:::  js

tim.createConversationGroup(options);

:::
</dx-codeblock>

**参数**

参数 options 为 Object 类型，包含的属性值如下：

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| conversationIDList  | String | 会话 ID 列表 |
| groupName   | String | 分组名，长度最大支持32字节 |

**返回值**

`Promise` 对象。

**示例**

<dx-codeblock>
:::  js

let promise = tim.createConversationGroup({
  conversationIDList: ['GROUPtest', 'C2Cexample'],
  groupName: 'Suppliers',
});
promise.then(function(imResponse) {
  // 创建会话分组成功
  const { successConversationIDList, failureConversationIDList } = imResponse.data;
  // successConversationIDList - 成功的会话 ID 列表
  // 获取会话列表
  const conversationList = tim.getConversationList(successConversationIDList);

  // failureConversationIDList - 失败的会话 ID 列表
  failureConversationIDList.forEach((item) => {
    const { conversationID, code, message } = item;
  });
}).catch(function(imError) {
  console.warn('createConversationGroup error:', imError);
});
:::
</dx-codeblock>

### 删除会话分组
您可以调用 [deleteConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversationGroup) 接口删除会话分组。调用接口成功后 SDK 会派发事件 [TIM.EVENT.CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) 和 [TIM.EVENT.CONVERSATION_GROUP_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_GROUP_LIST_UPDATED)。
>? 如果会话分组不存在，删除对应分组会报 `51009` 错误。

**接口**

<dx-codeblock>
:::  js

tim.deleteConversationGroup(groupName);

:::
</dx-codeblock>

**参数**

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| groupName   | String | 分组名，长度最大支持32字节 |

**返回值**

`Promise` 对象。

**示例**

<dx-codeblock>
:::  js

let promise = tim.deleteConversationGroup('Suppliers');
promise.then(function() {
  // 删除成功
}).catch(function(imError) {
  console.warn('deleteConversationGroup error:', imError);
});

:::
</dx-codeblock>

### 重命名会话分组
您可以调用 [renameConversationGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#renameConversationGroup) 接口重命名会话分组。调用接口成功后 SDK 会派发事件 [TIM.EVENT.CONVERSATION_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_LIST_UPDATED) 和 [TIM.EVENT.CONVERSATION_GROUP_LIST_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_GROUP_LIST_UPDATED)。

**接口**

<dx-codeblock>
:::  js

tim.renameConversationGroup(options);

:::
</dx-codeblock>

**参数**

参数 options 为 Object 类型，包含的属性值如下：

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| oldName  | String | 旧的分组名 |
| newName   | String | 新的分组名，长度最大支持32字节 |

**返回值**

`Promise` 对象。

**示例**

<dx-codeblock>
:::  js

let promise = tim.renameConversationGroup({
  oldName: 'Suppliers_old',
  newName: 'Suppliers_new'
});
promise.then(function(imResponse) {
  // 重命名成功
}).catch(function(imError) {
  console.warn('renameConversationGroup error:', imError);
});

:::
</dx-codeblock>

### 获取会话分组列表
您可以调用 [getConversationGroupList](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationGroupList) 接口获取会话分组列表。

**接口**

<dx-codeblock>
:::  js

tim.getConversationGroupList();

:::
</dx-codeblock>

**返回值**

`Promise` 对象。

**示例**

<dx-codeblock>
:::  js

let promise = tim.getConversationGroupList();
promise.then(function(imResponse) {
  const groupNameList = imResponse.data; // 会话分组名列表
});

:::
</dx-codeblock>

<dx-codeblock>
:::  js

// 获取指定会话分组下的所有会话
let promise = tim.getConversationList({ groupName: 'Suppliers' });
promise.then(function(imResponse) {
  const conversationList = imResponse.data.conversationList; // 会话列表
});

:::
</dx-codeblock>

### 添加会话到一个分组
当分组创建成功后，您可以调用 [addConversationsToGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#addConversationsToGroup)  接口添加一个新会话到分组。调用接口成功后 SDK 会派发事件 [TIM.EVENT.CONVERSATION_IN_GROUP_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_GROUP_LIST_UPDATED)。

**接口**

<dx-codeblock>
:::  js

tim.addConversationsToGroup(options);

:::
</dx-codeblock>

**参数**

参数 options 为 Object 类型，包含的属性值如下：

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| conversationIDList  | String | 会话 ID 列表 |
| groupName   | String | 分组名，长度最大支持32字节 |

**返回值**

`Promise` 对象。

**示例**

<dx-codeblock>
:::  js

let promise = tim.addConversationsToGroup({
  conversationIDList: ['GROUPtest', 'C2Cexample'],,
  groupName: 'Suppliers_new',
});
promise.then(function(imResponse) {
  // 添加会话到分组成功
  const { successConversationIDList, failureConversationIDList } = imResponse.data;
  // successConversationIDList - 成功的会话 ID 列表
  // 获取会话列表
  const conversationList = tim.getConversationList(successConversationIDList);

  // failureConversationIDList - 失败的会话 ID 列表
  failureConversationIDList.forEach((item) => {
    const { conversationID, code, message } = item;
  });
}).catch(function(imError) {
  console.warn('addConversationsToGroup error:', imError);
});

:::
</dx-codeblock>

### 从分组中删除某会话
您可以调用 [deleteConversationsFromGroup](https://web.sdk.qcloud.com/im/doc/en/SDK.html#deleteConversationsFromGroup) 从分组中删除某会话。调用接口成功后 SDK 会派发事件 [TIM.EVENT.CONVERSATION_IN_GROUP_UPDATED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.CONVERSATION_GROUP_LIST_UPDATED)。

**接口**

<dx-codeblock>
:::  js

tim.deleteConversationsFromGroup(options);

:::
</dx-codeblock>

**参数**

参数 options 为 Object 类型，包含的属性值如下：

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| conversationIDList  | String | 会话 ID 列表 |
| groupName   | String | 分组名，长度最大支持32字节 |

**返回值**

`Promise` 对象。

**示例**

<dx-codeblock>
:::  js

let promise = tim.deleteConversationsFromGroup({
  conversationIDList: ['GROUPtest', 'C2Cexample'],,
  groupName: 'Suppliers_new',
});
promise.then(function(imResponse) {
  // 从分组删除会话成功
  const { successConversationIDList, failureConversationIDList } = imResponse.data;
  // successConversationIDList - 成功的会话 ID 列表
  // 获取会话列表
  const conversationList = tim.getConversationList(successConversationIDList);

  // failureConversationIDList - 失败的会话 ID 列表
  failureConversationIDList.forEach((item) => {
    const { conversationID, code, message } = item;
  });
}).catch(function(imError) {
  console.warn('deleteConversationsFromGroup error:', imError);
});

:::
</dx-codeblock>

### 监听会话分组变更通知

会话分组更新时触发（如创建会话分组、删除会话分组、重命名会话分组）。

**示例**

<dx-codeblock>
:::  js

let onConversationGroupListUpdated = function(event) {
  console.log(event.data); // 全量的会话分组名列表
}
tim.on(TIM.EVENT.CONVERSATION_GROUP_LIST_UPDATED, onConversationGroupListUpdated);

:::
</dx-codeblock>

### 监听分组内的会话变更通知

会话分组内的会话更新时触发（如添加会话到分组，或者从分组内删除会话）。

**示例**

<dx-codeblock>
:::  js

let onConversationInGroupUpdated = function(event) {
  const { groupName, conversationList }  = event.data;
  // groupName - 会话分组名
  // conversationList - 分组内的会话列表
}
tim.on(TIM.EVENT.CONVERSATION_IN_GROUP_UPDATED, onConversationInGroupUpdated);

:::
</dx-codeblock>
