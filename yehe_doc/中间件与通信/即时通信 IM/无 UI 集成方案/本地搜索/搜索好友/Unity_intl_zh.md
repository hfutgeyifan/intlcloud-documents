## 功能描述
用户搜索只能搜索本地存储过的用户，比如拉取过的好友列表，拉取过的用户资料等。


## 搜索本地用户资料
调用接口 `FriendshipSearchFriends` ([Details](https://comm.qq.com/im/doc/unity/en/api/FriendshipApi/FriendshipSearchFriends.html)) 可以搜索本地用户资料。
您可以设置搜索关键字 `friendship_search_param_keyword_list`，并指定搜索的范围，即是否搜索用户的 `userID`、`nickName`、`remark` 字段。

示例代码如下：



```c#
// 通过关键词搜索好友
FriendSearchParam param = new FriendSearchParam
{
  friendship_search_param_keyword_list = new List<string>
  {
    "关键词1"
  },
  friendship_search_param_search_field_list = new List<TIMFriendshipSearchFieldKey>
  {
    TIMFriendshipSearchFieldKey.kTIMFriendshipSearchFieldKey_Identifier,
    TIMFriendshipSearchFieldKey.kTIMFriendshipSearchFieldKey_NikeName,
    TIMFriendshipSearchFieldKey.kTIMFriendshipSearchFieldKey_Remark
  }
};
TIMResult res = TencentIMSDK.MsgSearchLocalMessages(param, (int code, string desc, List<FriendInfoGetResult> result, string user_data)=>{
 // 处理异步逻辑
});
```




