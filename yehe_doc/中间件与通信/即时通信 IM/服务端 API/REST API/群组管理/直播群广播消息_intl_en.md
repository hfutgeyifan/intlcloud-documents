## Feature Description
 This API is used to deliver broadcast messages to all the audio-video groups.
>! This feature is supported by the SDK of the Enhanced edition on v6.5.2803 or later and the SDK for web on v2.21.0 or later. To use it, you need to [purchase the Ultimate edition](https://intl.cloud.tencent.com/document/product/1047/34577), go to the [**console**](https://console.cloud.tencent.com/im/qun-setting), select **Group configuration** > **Group feature configuration**, and enable **Broadcast messaging of audio-video group**.

## API Call Description
### Applicable group types

| Group Type ID | Support for This RESTful API |
|-----------|------------|
| Private | No. Same as work groups (Work) in the new version. |
| Public | No |
| ChatRoom | No. Same as meeting group (Meeting) in the new version. |
|AVChatRoom| Yes. Messages are sent to all the audio-video groups. |
|Community | No |

These are the preset group types in IM. For more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

### Sample request URL
```
https://xxxxxx/v4/group_open_http_svc/send_broadcast_msg?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Request parameters

The following table describes the modified parameters when this API is called. For other parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https | The request protocol is HTTPS, and the request method is POST. |
| xxxxxx | Domain name corresponding to the country/region where your SDKAppID is located.<li>Chinese mainland: `console.tim.qq.com`<li>Singapore: `adminapisgp.im.qcloud.com`<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com`<li>India: `adminapiind.im.qcloud.com` |
| v4/group_open_http_svc/send_broadcast_msg | Request API                             |
| sdkappid | SDKAppID assigned by the IM console when an app is created |
| identifier | App admin account. For more information, see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated by the app admin account. For details, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4,294,967,295 |
| contenttype   |Request format, which should always be `json`.|

### Maximum call frequency
1 calls per second

### Sample request

- **Basic format**

It is used to deliver broadcast messages to all the audio-video groups.

```
{
    "From_Account": "test",  // Specify the message sender (optional)
    "Random":8912345,  // A random number. If two messages sent within five minutes have the same value, they are considered to be the same message.
    "MsgBody":[ 
        {
            "MsgType": "TIMCustomElem",  // Custom message
            "MsgContent":{
                "Data": "{ \"type\":1, \"content\":\"hello world\"}"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}
```

>! `MsgBody` supports multiple message elements. If you need to call it more than once every second, the business can merge messages into one of up to 8,000 bytes.

### Request fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| From_Account | String | No | Message source account. If this field is not specified, the message sender is the app admin account used to call the API. Alternatively, apps can specify the message sender in this field to implement some special features. Note that if this field is specified, you must ensure that the account in this field exists. |
| Random | Integer | Yes | It is a 32-bit unsigned integer. If two messages sent within five minutes have the same content and `Random` value, the latter message will be discarded as a repeat. |
| MsgBody | Array | Yes | Message body. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |
| CloudCustomData | String | No | Custom message data  |

### Sample response

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "MsgSeq": 1283
}
```

### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. Valid values: `OK`: succeeded; `FAIL`: failed. |
| ErrorCode |	Integer	| Error code. Valid values: `0`: succeeded; other values: failed. |
| ErrorInfo | String | Error message |
| MsgSeq | Integer | Message sequence number, the unique identifier of a message |

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 10002 | Internal server error. Try again. |
| 10003 | Invalid command word. |
| 10004 | Invalid parameter. Check the error description and troubleshoot the issue. |
| 10007  | Insufficient operation permissions. For example, the switch is not enabled in the console, or the operating account is not the root account.    |
| 10023  | The message sending frequency limit is exceeded. Try again later. |

## API Debugging Tool
Use the [RESTful API online debugging tool](https://tcc.tencentcs.com/im-api-tool/#/v4/openim/admin_msgwithdraw?locale=en-US) to debug this API.

## References

- Sending Ordinary Messages in a Group ([v4/group_open_http_svc/send_group_msg](https://intl.cloud.tencent.com/document/product/1047/34959))
- [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527)
