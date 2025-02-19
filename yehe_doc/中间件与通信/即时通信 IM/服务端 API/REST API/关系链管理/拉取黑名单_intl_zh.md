## 功能说明

 支持分页拉取所有黑名单。

## 接口调用说明

### 请求 URL 示例

```
https://xxxxxx/v4/sns/black_list_get?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```

### 请求参数说明

下表仅列出调用本接口时涉及修改的参数及其说明，更多参数详情请参考 [REST API 简介](https://intl.cloud.tencent.com/document/product/1047/34620)。

| 参数               | 说明                                 |
| ------------------ | ------------------------------------ |
| https   | 请求协议为 HTTPS，请求方式为 POST       |
| xxxxxx |SDKAppID 所在国家/地区对应的专属域名<li>中国：`console.tim.qq.com`<li>新加坡： `adminapisgp.im.qcloud.com`<li>首尔： `adminapikr.im.qcloud.com`<li>法兰克福：`adminapiger.im.qcloud.com`<li>印度：`adminapiind.im.qcloud.com` |
| v4/sns/black_list_get  | 请求接口                             |
| sdkappid           | 创建应用时即时通信 IM 控制台分配的 SDKAppID |
| identifier         | 必须为 App 管理员帐号，更多详情请参见 [App 管理员](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98)                |
| usersig            | App 管理员帐号生成的签名，具体操作请参见 [生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)    |
| random             | 请输入随机的32位无符号整数，取值范围0 - 4294967295                 |
| contenttype | 请求格式固定值为`json` |

### 最高调用频率

200次/秒。

### 请求包示例

```
{
	"From_Account": "id",
	"StartIndex": 0,
	"MaxLimited": 30,
	"LastSequence": 12
}
```

### 请求包字段说明

| 字段         | 类型    | 属性 | 说明                                                   |
| ------------ | ------- | ---- | ------------------------------------------------------ |
| From_Account | String  | 必填 | 需要拉取该 UserID 的黑名单                         |
| StartIndex   | Integer | 必填 | 拉取的起始位置                                         |
| MaxLimited   | Integer | 必填 | 每页最多拉取的黑名单数                                 |
| LastSequence | Integer | 必填 | 上一次拉黑名单时后台返回给客户端的 Seq，初次拉取时为0；（Rest API 接口拉取填 0 即可） |

### 应答包体示例

```
{
	"BlackListItem": [
		{
			"To_Account": "id1",
			"AddBlackTimeStamp": 1430000001
		},
		{
			"To_Account": "id2",
			"AddBlackTimeStamp": 1430000002
		}
	],
	"StartIndex": 0,
	"CurruentSequence": 13,
	"ActionStatus": "OK",
	"ErrorCode": 0,
	"ErrorInfo": "",
	"ErrorDisplay": ""
}
```

### 应答包字段说明

| 字段              | 类型    | 说明                                                         |
| ----------------- | ------- | ------------------------------------------------------------ |
| BlackListItem     | Array   | 黑名单对象数组，每一个黑名单对象都包括了 To_Account 和 AddBlackTimeStamp |
| To_Account        | String  | 黑名单的 UserID                                          |
| AddBlackTimeStamp | Integer | 添加黑名单的时间                                             |
| StartIndex        | Integer | 下页拉取的起始位置，0表示已拉完                             |
| CurruentSequence  | Integer | 黑名单最新的 Seq                                             |
| ActionStatus      | String  | 请求处理的结果，OK 表示处理成功，FAIL 表示失败           |
| ErrorCode         | Integer | 错误码，0表示成功，非0表示失败，非0取值的详细描述请参见 [错误码说明](#ErrorCode)    |
| ErrorInfo         | String  | 详细错误信息                                                 |
| ErrorDisplay      | String  | 详细的客户端展示信息                                         |
<span id="ErrorCode"></span>

## 错误码说明

除非发生网络错误（例如502错误），否则该接口的 HTTP 返回码均为200。实际的错误码、错误信息是通过应答包体中的 ErrorCode、ErrorInfo 来表示的。
公共错误码（60000 到 79999）请参见 [错误码](https://intl.cloud.tencent.com/document/product/1047/34348) 文档。
本 API 私有错误码如下：

| 错误码 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| 30001  | 请求参数错误，请根据错误描述检查请求参数                     |
| 30003  | 请求的用户帐号不存在                                         |
| 30004  | 请求需要 App 管理员权限                                      |
| 30006  | 服务器内部错误，请重试                                       |
| 30007  | 网络超时，请稍后重试                                         |

## 接口调试工具

通过 [REST API 在线调试工具](https://tcc.tencentcs.com/im-api-tool/#/v4/openim/admin_msgwithdraw?locale=en-US) 调试本接口。

## 参考

- 添加黑名单（<a href="https://intl.cloud.tencent.com/document/product/1047/34911">v4/sns/black_list_add</a>）
- 删除黑名单（<a href="https://intl.cloud.tencent.com/document/product/1047/34912">v4/sns/black_list_delete</a>）
- 校验黑名单（<a href="https://intl.cloud.tencent.com/document/product/1047/34913">v4/sns/black_list_check</a>）
