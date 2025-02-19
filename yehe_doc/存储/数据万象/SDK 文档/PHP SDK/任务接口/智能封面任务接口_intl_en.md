## Overview

This document provides an overview of APIs and SDK code samples for submitting an intelligent thumbnail job.

| API | Description |
| ------------- |  ---------------------- |
| Submitting intelligent thumbnail job | Submits intelligent thumbnail job |


## Submitting Intelligent Thumbnail Job

#### Feature description

This API is used to submit an intelligent thumbnail job.

#### Method prototype

```php
public Guzzle\Service\Resource\Model createMediaSmartCoverJobs(array $args = array());
```

#### Sample request

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; // Replace it with your real `secretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; // Replace it with your real `secretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; // Replace it with your real region information, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    // Submit an intelligent thumbnail job: https://cloud.tencent.com/document/product/436/54017
    $result = $cosClient->createMediaSmartCoverJobs(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'SmartCover',
        'QueueId' => 'p81e648afxxxxxxxxxxxxxxxxx',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-Appid`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'SmartCover-${Number}.jpg',
            ),
        ),
    ));
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :----------------------------------------------------------- | :-------- | :------- |
| Tag                | Request | Job type. Valid values: Transcode (transcoding), Animation (animated image), SmartCover (intelligent thumbnail), Snapshot (screenshot), Concat (splicing)                                 | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule. Up to six operation rules are supported.                                                | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBack           | Request | Callback address                                                | String    | No   |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :--------- | :----- | :------- |
| Object             | Request.Input | Media filename | String | Yes   |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :---------------- | :------------------------------------ | :-------- | :------- |
| SmartCover                   | Request.Operation | This node is valid only when `Tag` is `SmartCover`. Currently, it is null.        | Container | No   |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------- | :----------------------------------------------------------- | :----- | :------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Result filename. **If the job type is `SmartCover`, ${Number} must be included in the filename.** For example, if `Object` is `my-new-cover-${Number}.jpg`, and there are three result files, the output result filenames are as follows: my-new-cover-0.jpg, my-new-cover-1.jpg, my-new-cover-2.jpg | String | Yes   |

#### Sample response

```php
GuzzleHttp\Command\Result Object
(
    [Body] => GuzzleHttp\Psr7\Stream Object
        (
            [stream:GuzzleHttp\Psr7\Stream:private] => Resource id #88
            [size:GuzzleHttp\Psr7\Stream:private] => 
            [seekable:GuzzleHttp\Psr7\Stream:private] => 1
            [readable:GuzzleHttp\Psr7\Stream:private] => 1
            [writable:GuzzleHttp\Psr7\Stream:private] => 1
            [uri:GuzzleHttp\Psr7\Stream:private] => php://temp
            [customMetadata:GuzzleHttp\Psr7\Stream:private] => Array
                (
                )

        )

    [RequestId] => NjI2MASOIDUAOIDUJIAOJDIOADJyMjNjZDE=
    [ContentType] => application/xml
    [ContentLength] => 832
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.ci.ap-beijing.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-22T11:12:33+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-1250000000
                            [Object] => video01.mp4
                            [Region] => ap-beijing
                        )

                    [JobId] => j0d9bc17z890zx8c9s877z97187147
                    [Message] => 
                    [Operation] => Array
                        (
                            [Output] => Array
                                (
                                    [Bucket] => examplebucket-1250000000
                                    [Object] => SmartCover-${Number}.jpg
                                    [Region] => ap-beijing
                                )

                            [SmartCover] => Array
                                (
                                    [Count] => 
                                    [DeleteDuplicates] => false
                                    [Format] => 
                                    [Height] => 
                                    [Width] => 
                                )

                        )

                    [QueueId] => p81e648afzx8c09z8xc09zx8c097be086
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => SmartCover
                )

        )

)
```

