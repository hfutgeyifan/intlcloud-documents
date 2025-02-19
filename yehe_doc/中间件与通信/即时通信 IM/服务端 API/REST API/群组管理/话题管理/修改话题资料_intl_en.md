## Feature Description
This API is used to modify the topic profile.

## API Call Description
### Applicable group types

| Group Type ID       | Whether This RESTful API Is Supported           |
| ----------------- | ----------------------------- |
| Private           | No                        |
| Public            | No                        |
| ChatRoom          | No                        |
| AVChatRoom        | No                        |
| Community | This API applies only to topic-enabled communities. |


These are the preset group types in IM. For more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

### Sample request URL

```https
https://xxxxxx/v4/million_group_open_http_svc/modify_topic?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```

### Request parameters

The following table describes the modified parameters when this API is called. For other parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter                                        | Description                                                         |
| ------------------------------------------- | ------------------------------------------------------------ |
| https | The request protocol is HTTPS, and the request method is POST. |
| xxxxxx | Domain name corresponding to the country/region where your SDKAppID is located.<li>Chinese mainland: `console.tim.qq.com`<li>Singapore: `adminapisgp.im.qcloud.com`<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com`<li>India: `adminapiind.im.qcloud.com` |
| v4/million_group_open_http_svc/modify_topic | Request API                                                     |
| sdkappid                                    | The `SDKAppID` assigned by the IM console when the application is created                  |
| identifier                                   | It must be the application admin account. For more information, see [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig                                  | Signature generated by the application admin account. For detailed directions, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random                                   | Enter a random 32-bit unsigned integer in the range of 0 to 4294967295.           |
| contenttype                                  | Request format. Fixed value: `json`.                                       |

### Maximum call frequency

200 calls per second

### Sample request

- **Modify the basic topic information**
Modify the basic topic information, such as topic name and topic notice.
```json
{
    "GroupId":"@TGS#_@TGS#cQVLVHIM62CJ",	// Group of the topic to be modified, which is required
    "TopicId":"@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_@TOPIC#cRTE3HIM62C5",	// ID of the topic to be modified, which is required
    "From_Account":"1400187352",	// Member modifying the topic profile
    "TopicName":"TestTopicName",	// Topic name, which is optional
    "FaceUrl":"http://this.is.new.face.url", // Topic profile photo, which is optional
    "Notification":"Notification",	// Topic notice, which is optional
    "Introduction":"Introduction",	// Topic introduction,	 which is optional
    "MuteAllMember":"On", // Set to mute all. This setting is optional. Valid values: `On`, `Off`.
    "CustomString":"This is a customs string." // Custom string, which is optional
}
```


- **Set only the custom topic information**
Set the custom topic field. `TopicDefinedData` and the custom shared group field can be configured in the [IM console](https://console.cloud.tencent.com/im) as instructed in [Group System](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5).
```json
{
    "GroupId":"@TGS#_@TGS#cQVLVHIM62CJ", // Group of the topic to be modified, which is required
    "TopicId":"@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_@TOPIC#cRTE3HIM62C5", // ID of the topic to be modified, which is required
    "TopicDefinedData": [ // Custom field, which is optional
        {
            "Key": "TopicTestData", // Key of the custom field to be modified
            "Value": "NewData"  // New value of the custom field
        }
    ]
}
```

- **Delete the custom topic information**
Delete the configured custom topic field.
```json
{
    "GroupId":"@TGS#_@TGS#cQVLVHIM62CJ", // Group of the topic to be modified, which is required
    "TopicId":"@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_@TOPIC#cRTE3HIM62C5", // ID of the topic to be modified, which is required
    "TopicDefinedData": [ // Custom field, which is optional
        {
            "Key": "TopicTestData", // Key of the custom field to be modified
            "Value": ""  // An empty value indicates to delete the custom field.
        }
    ]
}
```

- **ALL IN ONE**
```json
{
    "GroupId":"@TGS#_@TGS#cQVLVHIM62CJ",	// Group of the topic to be modified, which is required
    "TopicId":"@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_@TOPIC#cRTE3HIM62C5",	// ID of the topic to be modified, which is required
    "From_Account":"1400187352",	// Member modifying the topic
    "TopicName":"TestTopicName",	// Topic name, which is optional
    "FaceUrl":"http://this.is.new.face.url", // Topic profile photo, which is optional
    "Notification":"Notification",	// Topic notice, which is optional
    "Introduction":"Introduction",	// Topic introduction,	 which is optional
    "MuteAllMember":"On", // Set to mute all. This setting is optional. Valid values: `On`, `Off`. 
    "CustomString":"This is a customs string.", // Custom string, which is optional
    "TopicDefinedData": [ // Custom field, which is optional
        {
            "Key": "TopicTestData", // Key of the custom field to be modified
            "Value": "NewData"  // New value of the custom field
        }
    ]
}
```

[](id:Parameters)

### Request fields

| Field             | Type   | Attribute | Description                                                         |
| ---------------- | ------ | ---- | ------------------------------------------------------------ |
| GroupId          | String | Required | Group ID of the topic to be modified                                   |
| TopicId          | String | Required | ID of the topic to be modified                                             |
| TopicName        | String | Optional | Topic name, which can contain up to 30 bytes, encoded in UTF-8.      |
| From_Account     | uint64 | Optional | User account that wants to modify the topic                                   |
| CustomString     | String | Optional | A custom string, which can contain up to 3,000 bytes. encoded in UTF-8. |
| FaceUrl | String | Optional |Profile photo URL of the topic, which can contain up to 100 bytes. |
| Notification     | String | Optional | Topic notice, which can contain up to 300 bytes, encoded in UTF-8.     |
| Introduction | String | Optional |Topic introduction, which can contain up to 240 bytes, encoded in UTF-8. |
| MuteAllMember    | String | Optional | Mutes members in the topic. Only the group admin, group owner, and system admin can mute members.     |
| TopicDefinedData | Array | Optional |Custom topic information. `TopicDefinedData` and the custom shared group field can be configured in the [IM console](https://console.cloud.tencent.com/im) as instructed in [Group System](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5).|


### Sample response
```json
{
    "ActionStatus": "OK",
    "ErrorInfo": "ok",
    "ErrorCode": 0
}
```

### Response fields

| Field         | Type    | Description                                           |
| ------------ | ------- | ---------------------------------------------- |
| ActionStatus | String | Request result. Valid values: `OK`: succeeded; `FAIL`: failed. |
| ErrorCode | Integer | Error code. Valid values: `0`: succeeded; other values: failed.                 |
| ErrorInfo    | String  | Error message                                       |

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 10002 | Internal server error. Try again. |
| 10003 | Invalid command word. |
| 10004 | Invalid parameter. Check the error description and troubleshoot the issue. |
| 10006  | The operation frequency exceeds the limit. Reduce the call frequency. It is usually reported when too many groups are added in a day or the operation to get all the groups in the application is too frequent.  |
| 10007 | Insufficient operation permissions. Check the request parameters based on the error message. |
| 10008  | Invalid request. It may be that the signature information in the request is not verified successfully. Try again or [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=29&level2_id=40&source=0&data_title=%E4%BA%91%E9%80%9A%E4%BF%A1%20%20IM&step=1) for assistance. |
| 10010  | Invalid request. The topic has been deleted.                                     |
| 10015 | The requested group ID is invalid. Check the request parameter based on the error message. |
| 10016 | The application backend rejected this operation through a third-party callback. Check the returned value of the callback after topic profile modification. |
|11000|The current group does not support the community topic feature. To use this feature, you need to purchase the [Ultimate edition](https://www.tencentcloud.com/document/product/1047/34577) and apply for enablement as instructed in [Configuration Change Ticket](https://intl.cloud.tencent.com/document/product/1047/44322).|
| 80001  | Failed to pass the security check. Check the request parameters based on the error message.                   |

## API Debugging Tool

Use the [RESTful API online debugging tool](https://tcc.tencentcs.com/im-api-tool/index.html#/v4/group_open_http_svc/create_group) to debug this API.

## Possible Callbacks

- [Callback after topic profile modification](https://intl.cloud.tencent.com/document/product/1047/49466)

