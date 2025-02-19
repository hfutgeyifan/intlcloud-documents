## Overview

The JavaScript SDK provides APIs for getting object URLs and pre-signed request URLs.

>?
> - We recommend you use a temporary key to generate a pre-signed URL for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [principle of least privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, we recommend you limit the permission of the permanent key to uploads and downloads only to avoid risks.
> 



## Signature Calculation

In all COS XML API requests, the authentication credential `Authorization` is required for all operations on private resources for COS to determine whether a request is valid.

There are two ways to use the authentication credential:

1. Put it in the header parameter with the field name `authorization`.
2. Put it in the URL parameter with the field name `sign`.

The `COS.getAuthorization` method is used to calculate the authentication credential (Authorization), which is the signing information used to verify the validity of the request.

>! We recommend you use this method only for frontend debugging but not in actual projects, as it may disclose keys.
>

#### Sample code

Get the authentication credential for object download:

[//]: # (.cssg-snippet-get-authorization)
```js
// Log in at https://console.cloud.tencent.com/cam/capi to view and manage the `SECRETID` and `SECRETKEY`.
var Authorization = COS.getAuthorization({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY',
    Method: 'get',
    Key: 'exampleobject',
    Expires: 60,
    Query: {},
    Headers: {}
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ------ | ---- |
| SecretId | Your `SecretId`. | String | Yes |
| SecretKey | Your `SecretKey`. | String | Yes |
| Method | HTTP request method, such as `GET`, `POST`, `DELETE`, or `HEAD`. | String | Yes |
| Key | Object key (object name), which is the unique identifier of an object in a bucket. **If the request operation is to be performed on a file, this parameter will be required and should be a filename.** If the operation is on a bucket, this parameter should be left empty. | String | No |
| Query     | Request parameters to be included in the signature in the format of `{key: 'val'}`                                         | Object | No   |
| Headers   | Request headers to be included in the signature in the format of `{key: 'val'}`                                         | Object | No   |
| Expires | Signature expiration time in seconds. Default value: `900`. | Number | No |

#### Returned value description

The returned value is the calculated authentication credential string `authorization`.

## Getting Pre-signed Request URL

### Sample download requests

Sample 1: Getting an object URL without a signature

[//]: # (.cssg-snippet-get-presign-download-url)
```js
var url = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
    Sign: false
});
```

Sample 2: Getting a signed object URL

[//]: # (.cssg-snippet-get-presign-download-url-signed)
```js
var url = cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
});
```

Sample 3: Getting a signed URL through callback

> ?If the signing process is async, you need to get the signed URL through callback.

[//]: # (.cssg-snippet-get-presign-download-url-callback)
```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
    Sign: false
}, function (err, data) {
    console.log(err || data.Url);
});
```

Sample 4: Specifying the validity period of a link

[//]: # (.cssg-snippet-get-presign-download-url-expiration)
```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
    Sign: true,
    Expires: 3600, // Unit: Second
}, function (err, data) {
    console.log(err || data.Url);
});
```

Sample 5: Getting an object URL and downloading the object

[//]: # (.cssg-snippet-get-presign-download-url-then-fetch)
```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
    Sign: true
}, function (err, data) {
    if (err) return console.log(err);
    var downloadUrl = data.Url + (data.Url.indexOf('?') > -1 ? '&' : '?') + 'response-content-disposition=attachment'; // Add the parameter for a forced download
    /* The filename can be concatenated to rename the object during download */
    /* downloadUrl += ';filename=myname'; */
    // (The `window.open()` method is recommended) This opens the URL in a new window. If you need to open the URL in the current window, you can use the hidden iframe for download, or use the <a> tag download attribute.
    window.open(downloadUrl);
});
```

Sample 6: Generating a pre-signed URL with the signature containing `Query` and `Header`

[//]: # (.cssg-snippet-get-obejct-url-with-params)
```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
    Sign: true,
    /* The HTTP request parameters passed in should be the same as those of the actual request. This can prevent users from tampering with the HTTP request parameters. */
    Query: {
      'imageMogr2/thumbnail/200x/': '' 
    },
    /* The HTTP request headers passed in should be included in the actual request. This can prevent users from tampering with the HTTP request headers that are signed here. */
    Headers: {
      host: 'xxx' /* Specify the host for access. Error code 403 will be reported for access by a non-specified host. */
    },
}, function (err, data) {
    console.log(err || data.Url);
});
```

### Sample upload requests

Sample 1: Getting a pre-signed URL for `Put Object`

[//]: # (.cssg-snippet-get-presign-upload-url)
```js
cos.getObjectUrl({
    Bucket: 'examplebucket-1250000000', /* Your bucket (required) */
    Region: 'COS_REGION',  /* Bucket region (required), such as ap-beijing */
    Key: '1.jpg',  /* Object key stored in the bucket (required), such as `1.jpg` and `a/b/test.txt`. */
    Method: 'PUT',
    Sign: true
}, function (err, data) {
    if (err) return console.log(err);
    console.log(data.Url);
    
    /* After the URL is obtained, the object can be uploaded in the frontend by using AJAX. */
    var xhr = new XMLHttpRequest();
    xhr.open('PUT', data.Url, true); /* `PUT` corresponds to the `Method` entered in `getObjectUrl`. */
    xhr.onload = function (e) {
        console.log('Uploaded successfully', xhr.status, xhr.statusText);
    };
    xhr.onerror = function (e) {
        console.log('Upload failed', xhr.status, xhr.statusText);
    };
    xhr.send(file); /* `file` is the object to be uploaded. */
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID`. The bucket name entered here must be in this format. | String | Yes |
| Region  | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), which is the unique identifier of an object in a bucket. **If the request operation is to be performed on a file, this parameter will be required and should be a filename.** If the operation is on a bucket, this parameter should be left empty. | String | Yes |
| Sign | Whether to return a signed URL. Default value: `true`. | Boolean | No |
| Protocol    | Valid values: `http:` (default value), `https:`. | String | No |
| Domain    | Bucket access domain name. Default value: `{BucketName-APPID}.cos.{Region}.myqcloud.com`. | String | No |
| Method | HTTP request method, such as `GET`, `POST`, `DELETE`, or `HEAD`. Default value: `GET`. | String | No |
| Query     | Request parameters to be included in the signature in the format of `{key: 'val'}`                                         | Object | No   |
| Headers   | Request headers to be included in the signature in the format of `{key: 'val'}`                                         | Object | No   |
| Expires | Signature expiration time in seconds. Default value: `900`. | Number | No |

#### Returned value description

The returned value is a string. There are two possible cases:

1. If the signature can be calculated synchronously (for example, `SecretId` and `SecretKey` have been passed in during instantiation), the signed URL will be returned by default.
2. Otherwise, an unsigned URL will be returned.

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------ | ------------------------------------------------------------ | ------ |
| err    | The object returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| data         | The object returned when the request is successful. If an error occurs with the request, this parameter is empty.               | Object |
| - Url | Calculated URL | String |

