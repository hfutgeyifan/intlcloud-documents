## Feature Description
The app admin can pull operational data for last 30 days through this API. The operation fields that can be pulled are described as follows.

## API Invocation Description
### Request URL example
```
https://xxxxxx/v4/openconfigsvr/getappinfo?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```


### Request parameters

The following table lists and describes only the parameters to be modified when this API is invoked. For details on other parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com`<li>India: `adminapiind.im.qcloud.com` |
| v4/openconfigsvr/getappinfo | Request API |
| sdkappid | SDKAppID assigned by the IM console when an app is created |
| identifier | This must be the app admin account. For details, see [App Admins](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | The signature generated by the app admin account. For details, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | Enter a random 32-bit unsigned integer ranging from 0 to 4294967295. |
| contenttype | Request format. The value is always `json`. |


### Maximum invocation frequency
The maximum invocation frequency is 200 times per second.
### Request packet example
Query operational data for last 30 days for SDKAppID.

- **Basic format**
Pull all fields by default.
```
{}
```
- **Specifying a field to be pulled**
Specify a field to be pulled in RequestField.
```
{
    "RequestField":[
        "ChainIncrease",
        "ChainDecrease"
    ]
}
```

### Request packet fields

| Field | Type | Attribute | Description |
|---------|---------|---------|---------|
| RequestField | Array | Optional | This field is used to specify operational data to be pulled. If this field is not specified, all fields will be pulled by default. For details, see the operation fields that can be pulled below. |

### Response packet examples
- **Basic format**
```
{
	"ErrorCode": 0,
	"ErrorInfo": "OK",
	"Result": [{
		"APNSMsgNum": "84",
		"ActiveUserNum": "2014",
		"AppId": "1104620500",
		"AppName": "Real-Time Communication Scenario Trial Edition",
		"C2CAPNSMsgNum": "84",
		"C2CDownMsgNum": "11040",
		"C2CSendMsgUserNum": "9",
		"C2CUpMsgNum": "52209",
		"CallBackReq": "73069",
		"CallBackRsp": "72902",
		"ChainDecrease": "16",
		"ChainIncrease": "18",
		"Company": "LinYe",
		"Date": "20160607",
		"DownMsgNum": "11869",
		"GroupAPNSMsgNum": "0",
		"GroupAllGroupNum": "41913",
		"GroupDestroyGroupNum": "35019",
		"GroupDownMsgNum": "829",
		"GroupJoinGroupTimes": "121438",
		"GroupNewGroupNum": "35904",
		"GroupQuitGroupTimes": "108292",
		"GroupSendMsgGroupNum": "5189",
		"GroupSendMsgUserNum": "12",
		"GroupUpMsgNum": "8433",
		"LoginTimes": "13708",
		"LoginUserNum": "2094",
		"MaxOnlineNum": "62",
		"RegistUserNumOneDay": "1052",
		"RegistUserNumTotal": "53091",
		"SendMsgUserNum": "19",
		"UpMsgNum": "60642",
	}]
}
```
- **Specifying a field to be pulled**
```
{
    "ErrorCode":0,
    "ErrorInfo":"OK",
    "Result":[{
            "ChainDecrease":"8",
            "ChainIncrease":"8",
            "Date":"20160605"
        },
        {
            "ChainDecrease":"17",
            "ChainIncrease":"17",
            "Date":"20160604"
        }
    ]
}
```

### Response packet fields

| Field | Type | Description |
|---------|---------|---------|
| Result | Array | The requested operational data from last 30 days. |
| ErrorCode | Integer | The error code. 0: succeeded. Others: failed. |
| ErrorInfo | String | The error information |

## Error Codes
Unless a network error (such as error 502) occurs, the HTTP return code for this API is always 200. ErrorCode and ErrorInfo in the response packet represent the actual error code and error information, respectively.
For common error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API.

| Error Code | Description |
|---------|---------|
| 130001 | JSON parsing error of the request packet |
| 130009 | SQL opening error |
| 130010 | SQL pinging error |
| 130011 | SQL query error |
| 130012 | SQL result parsing error |

## Operation Fields That Can Be Pulled

| Field | Description |
|---------|---------|
| AppName | App name |
| AppId | SDKAppID of the app |
| Company | Customer name |
| ActiveUserNum | Number of active users |
| RegistUserNumOneDay | Number of newly registered users |
| RegistUserNumTotal | Total number of registered users |
| LoginTimes | Number of logins |
| LoginUserNum | Number of logged-in users |
| UpMsgNum | Number of upstream messages |
| SendMsgUserNum | Number of sending users |
| APNSMsgNum | Number of pushed APN messages |
| C2CUpMsgNum | Number of upstream messages (C2C) |
| C2CDownMsgNum|Number of downstream messages (C2C)|
| C2CSendMsgUserNum | Number of sending users (C2C) |
| C2CAPNSMsgNum | Number of pushed APN messages (C2C) |
| MaxOnlineNum | Maximum number of online users |
| DownMsgNum| Total number of downstream messages (C2C and group)|
| ChainIncrease | Increase in relationship chain pairs |
| ChainDecrease | Decrease in relationship chain pairs |
| GroupUpMsgNum | Number of upstream messages (group) |
| GroupDownMsgNum| Number of downstream messages (group) |
| GroupSendMsgUserNum | Number of sending users (group) |
| GroupAPNSMsgNum | Number of pushed APN messages (group) |
| GroupSendMsgGroupNum | Number of sending groups |
| GroupJoinGroupTimes | Total number of joined groups |
| GroupQuitGroupTimes | Total number of quit groups |
| GroupNewGroupNum | Number of newly added groups |
| GroupAllGroupNum | Total number of groups |
| GroupDestroyGroupNum | Number of dismissed groups |
| CallBackReq | Number of callback requests |
| CallBackRsp | Number of callback responses |
| Date | Date |

## API Commissioning Tool

Use the [RESTful online commissioning tool for APIs](https://tcc.tencentcs.com/im-api-tool/#/v4/openim/admin_msgwithdraw?locale=en-US) to commission this API.
