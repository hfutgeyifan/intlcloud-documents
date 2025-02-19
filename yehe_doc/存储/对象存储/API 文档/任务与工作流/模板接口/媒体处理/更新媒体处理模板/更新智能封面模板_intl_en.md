## Feature Description

This API is used to update an intelligent thumbnail template.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateTranscodeTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer provides various capabilities such as online call, signature verification, SDK code generation, and quick API search. You can also use it to query the request and response of each API call as well as generate sample code for calls.
            </div>
        </div>
    </div>
</div>



## Request

#### Sample request

```shell
PUT /template/<TemplateId> HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>?
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
>

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>SmartCover</Tag>
    <Name>TemplateName</Name>
    <SmartCover>
        <Format>jpg</Format>
        <Width>1280</Width>
        <Height>960</Height>
        <Count>10</Count>
        <DeleteDuplicates>true</DeleteDuplicates>
    </SmartCover>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :------------- | :-------- | ---- |
| Request            | None     | <a href="https://cloud.tencent.com/document/product/460/80091#Request" target="_blank">Same as `Request` in the intelligent thumbnail template creation API.</a> | Container | Yes   |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <Tag>SmartCover</Tag>
        <Name>TemplateName</Name>
        <TemplateId>t1f43110a08702470b8fa75894629501fa</TemplateId>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <SmartCover>
            <Width>1280</Width>
            <Height>960</Height>
            <Format>jpg</Format>
            <Count>5</Count>
            <DeleteDuplicates>false</DeleteDuplicates>
        </SmartCover>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :-------------------------------------------------- | :-------- |
| Response           | None     | <a href="https://cloud.tencent.com/document/product/460/80091#Response" target="_blank">Same as `Response` in the intelligent thumbnail template creation API.</a> | Container |


#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).

## Samples

#### Request

```shell
PUT /template/t1460606b9752148c4ab182f55163ba7cd HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml

<Request>
    <Tag>SmartCover</Tag>
    <Name>TemplateName</Name>
    <SmartCover>
        <Format>jpg</Format>
        <Width>1280</Width>
        <Height>960</Height>
        <Count>10</Count>
        <DeleteDuplicates>true</DeleteDuplicates>
    </SmartCover>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 14 Jul 2022 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****



<Response>
    <Template>
        <Tag>SmartCover</Tag>
        <Name>TemplateName</Name>
        <TemplateId>t1f43110a08702470b8fa75894629501fa</TemplateId>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <SmartCover>
            <Width>1280</Width>
            <Height>960</Height>
            <Format>jpg</Format>
            <Count>5</Count>
            <DeleteDuplicates>false</DeleteDuplicates>
        </SmartCover>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

