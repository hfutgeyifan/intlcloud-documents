## Overview

This document provides an overview of APIs and SDK code samples for object deletion.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | Deleting an object | Deletes the specified object from a bucket. |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | Deleting multiple objects | Deletes multiple specified objects from a bucket. |


## Deleting One Object

#### Description

This API (`DELETE Object`) is used to delete the specified object.

#### Method prototype

```
delete_object(Bucket, Key, **kwargs)
```
#### Sample request 1. Deleting an object

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```

#### Sample request 2. Deleting a directory

In COS, a directory is a special object with a path ending in "/". You can directly call the `Delete Object` API to delete a directory. Note that only empty directories can be deleted. If you want to delete non-empty directories, see "Deleting objects with a specified prefix".

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

to_delete_dir='path/to/delete/dir/'
response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key=to_delete_dir,
)
print(response)
```

#### Sample request 3: Deleting objects with a specified prefix

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

# Delete objects with the specified prefix
bucket = 'examplebucket-1250000000'
is_over = False
marker = ''
prefix = 'root/logs'
while not is_over:
    response = client.list_objects(Bucket=bucket, Prefix=prefix, Marker=marker)
    if response['Contents']:
        for content in response['Contents']:
            print("delete object: ", content['Key'])
            client.delete_object(Bucket=bucket, Key=content['Key'])

        if response['IsTruncated'] == 'false':
            is_over = True
            marker = response['Marker']
```

#### Sample request with all parameters

```python
response = client.delete_object(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    VersionId='string',
)
```
#### Parameter description

| Parameter | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes | 
 | Key | Object key, which uniquely identifies an object in a bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
 | VersionId | Version ID of the object if versioning is enabled  | String  | No | 

#### Response description

The response contains the information of the deleted object in dict type:

```python
{
    'x-cos-version-id': 'string',
    'x-cos-delete-marker': 'true'|'false',
}
```

| Parameter | Description | Type | 
| -------------- | -------------- |---------- | 
| x-cos-version-id | Version ID of the deleted object  | String |
| x-cos-delete-marker | Whether the deleted object is a delete marker | String | 

## Deleting Multiple Objects

#### Description

The API (`DELETE Multiple Objects`) is used to delete multiple objects.

#### Method prototype

```
delete_objects(Bucket, Delete={}, **kwargs)
```
#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.delete_objects(
    Bucket='examplebucket-1250000000',
    Delete={
        'Object': [
            {
                'Key': 'exampleobject1'
            },
            {
                'Key': 'exampleobject2'
            }
        ]
    }
)
```
#### Sample request with all parameters

```python
response = client.delete_objects(
    Bucket='examplebucket-1250000000',
    Delete={
        'Object': [
            {
                'Key': 'exampleobject1',
                'VersionId': 'string'
            },
            {
                'Key': 'exampleobject2',
                'VersionId': 'string'
            },
        ],
        'Quiet': 'true'|'false'
    }
)
```

#### Parameter description

| Parameter | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes | 
 | Delete  | Response method and the target objects to be deleted  | Dict | Yes | 
 | Object | Information of each object to be deleted | List | Yes | 
 | key  | Object key, unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`. | String | No |
 | VersionId | Version ID of the target object after versioning is enabled | String  | No |
 | Quiet | Response method. Valid values: `true` (returns only the failed results); `false` (returns all results). Default value: `false`. | String | No |

#### Response description
The response contains the batch deletion result in dict type:
```python
{
    'Deleted': [
        {
            'Key': 'string',
            'VersionId': 'string',
            'DeleteMarker': 'true'|'false',
            'DeleteMarkerVersionId': 'string'
        },
        {
            'Key': 'string',
        },
    ],
    'Error': [
        {
            'Key': 'string',
            'VersionId': 'string',
            'Code': 'string',
            'Message': 'string'
        },
    ]
}
```

| Parameter | Description | Type | 
| -------------- | -------------- |---------- |
 | Deleted | Information of the successfully deleted object       | List   |
 | Key     | Path of the successfully deleted object | String |
 | VersionId | Version ID of the successfully deleted object | String |
 | DeleteMarker | Whether the successfully deleted object is a delete marker | String |
 | DeleteMarkerVersionId | Version ID of the delete marker of the successfully deleted object | String |
 | Error  |  Information of the object that failed to be deleted | List |
 | Key | Path of the object that failed to be deleted | String |
 | VersionId | Version ID of the object that failed to be deleted | String |
 | Code | Error code for the deletion failure | String |
 | Message | Error message for the deletion failure | String |


## Deleting Multiple Objects (Deleting Directory)

#### Description
COS does not have the concept of directories, but you can use slashes (/) as the delimiter to simulate directories.

In COS, deleting a directory and the objects contained actually means deleting objects that have the same specified prefix. Currently, COS Python SDK does not provide a standalone API to perform this operation. However, you can still do so with a combination of basic operations (querying object list + batch deleting objects).

#### Sample request
```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
from qcloud_cos.cos_threadpool import SimpleThreadPool
import os
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as `secret_id`, `secret_key`, and `region`. `Appid` has been removed from CosConfig and thus needs to be specified in `Bucket`, which is in the format of `BucketName-Appid`.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://cloud.tencent.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information on how to generate and use a temporary key, visit https://cloud.tencent.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

bucket = 'examplebucket-1250000000'
folder = 'folder/' # The directory to be deleted (an object name ending with a slash (/) is a directory)

def delete_cos_dir():
    pool = SimpleThreadPool()
    marker = ""
    while True:
        file_infos = []

        # List 100 objects in a response
        response = client.list_objects(Bucket=bucket, Prefix=folder, Marker=marker, MaxKeys=100)

        if "Contents" in response:
            contents = response.get("Contents")
            file_infos.extend(contents)
            pool.add_task(delete_files, file_infos)

        # Quit after listing is completed
        if response['IsTruncated'] == 'false':
            break
        
        # Get the next response
        marker = response["NextMarker"]

    pool.wait_completion()
    return None   

def delete_files(file_infos):

    # Construct the batch deletion request
    delete_list = []
    for file in file_infos:
        delete_list.append({"Key": file['Key']})

    response = client.delete_objects(Bucket=bucket, Delete={"Object": delete_list})
    print(response)

if __name__ == "__main__":
    delete_cos_dir()
```
