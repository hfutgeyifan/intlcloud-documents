## 简介

本文档提供关于超分辨率任务接口的 API 概览和 SDK 示例代码。

| API                                                          | 操作描述         |
| ------------------------------------------------------------ | ---------------- |
| [提交超分辨率任务](https://intl.cloud.tencent.com/document/product/436/47105)| 提交超分辨率任务 |


## 提交超分辨率任务

#### 功能说明

提交超分辨率任务。

#### 方法原型

```php
public Guzzle\Service\Resource\Model createMediaSuperResolutionJobs(array $args = array());
```

#### 请求示例

#### 示例一： 使用模板

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    $result = $cosClient->createMediaSuperResolutionJobs(array(
        'Bucket' => 'examplebucket-125000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'SuperResolution',
        'QueueId' => 'p81e648af2aee49688570xxxxxxxxxxx',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'TemplateId' =>'t19ea5e0c0b7054d7b904axxxxxxxxxxx',
            'TranscodeTemplateId' =>'t0b612860a293f41078xxxxxxxxxxx',
            'WatermarkTemplateId' =>'t185e2e24551b24259a02xxxxxxxxxxx',
            'DigitalWatermark' => array(
                'Message' => 'xxx',
                'Type' => 'Text',
                'Version' => 'V1',
                'IgnoreError' => 'true',
            ),
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-125000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'SuperResolution.flv',
            ),
        ),
        'CallBack' => '',
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 示例二： 自定义参数

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
try {
    $result = $cosClient->createMediaSuperResolutionJobs(array(
        'Bucket' => 'examplebucket-125000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Tag' => 'SuperResolution',
        'QueueId' => 'p81e648af2aee49688570xxxxxxxxxxx',
        'Input' => array(
            'Object' => 'video01.mp4'
        ),
        'Operation' => array(
            'SuperResolution' => array(
                'Resolution' => '',
                'EnableScaleUp' => '',
            ),
            'Transcode' => array(
                'Tag' => '',
                'Name' => '',
                'Container' => array(
                    'Format' => '',
                ),
                'Video' => array(
                    'Codec' => '',
                    'Width' => '',
                    'Height' => '',
                    'Fps' => '',
                    'Remove' => '',
                    'Profile' => '',
                    'Bitrate' => '',
                    'Crf' => '',
                    'Gop' => '',
                    'Preset' => '',
                    'Bufsize' => '',
                    'Maxrate' => '',
                    'HlsTsTime' => '',
                    'Pixfmt' => '',
                    'LongShortMode' => '',
                ),
                'TimeInterval' => array(
                    'Start' => '',
                    'Duration' => '',
                ),
                'Audio' => array(
                    'Codec' => '',
                    'Samplerate' => '',
                    'Bitrate' => '',
                    'Channels' => '',
                    'Remove' => '',
                    'KeepTwoTracks' => '',
                    'SwitchTrack' => '',
                    'SampleFormat' => '',
                ),
                'TransConfig' => array(
                    'AdjDarMethod' => '',
                    'IsCheckReso' => '',
                    'ResoAdjMethod' => '',
                    'IsCheckVideoBitrate' => '',
                    'VideoBitrateAdjMethod' => '',
                    'IsCheckAudioBitrate' => '',
                    'AudioBitrateAdjMethod' => '',
                    'DeleteMetadata' => '',
                    'IsHdr2Sdr' => '',
                    'HlsEncrypt' => array(
                        'IsHlsEncrypt' => '',
                        'UriKey' => '',
                    ),
                ),
            ),
            'Watermark' => array(
                'Type' => '',
                'Pos' => '',
                'LocMode' => '',
                'Dx' => '',
                'Dy' => '',
                'StartTime' => '',
                'EndTime' => '',
                'Image' => array(
                    'Url' => '',
                    'Mode' => '',
                    'Width' => '',
                    'Height' => '',
                    'Transparency' => '',
                    'Background' => '',
                ),
                'Text' => array(
                    'FontSize' => '',
                    'FontType' => '',
                    'FontColor' => '',
                    'Transparency' => '',
                    'Text' => '',
                ),
            ),
            'DigitalWatermark' => array(
                'Message' => '',
                'Type' => '',
                'Version' => '',
                'IgnoreError' => '',
            ),
            'Output' => array(
                'Region' => $region,
                'Bucket' => 'examplebucket-125000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
                'Object' => 'SuperResolution.flv',
            ),
        ),
        'CallBack' => '',
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

Request 中的具体数据描述如下：

| 节点名称（关键字） | 父节点  | 描述                            | 类型      | 是否必选 |
| :----------------- | :------ | :------------------------------ | :-------- | :------- |
| Tag                | Request | 创建任务的 Tag：SuperResolution | String    | 是       |
| Input              | Request | 待操作的媒体信息                | Container | 是       |
| Operation          | Request | 操作规则                        | Container | 是       |
| QueueId            | Request | 任务所在的队列 ID               | String    | 是       |
| CallBack           | Request | 回调地址                        | String    | 否       |

Container 类型 Input 的具体数据描述如下：

| 节点名称（关键字） | 父节点        | 描述       | 类型   | 是否必选 |
| :----------------- | :------------ | :--------- | :----- | :------- |
| Object             | Request.Input | 媒体文件名 | String | 是       |

Container 类型 Operation 的具体数据描述如下：

| 节点名称（关键字）  | 父节点            | 描述                                                         | 类型      | 是否必选 |
| :------------------ | :---------------- | :----------------------------------------------------------- | :-------- | :------- |
| SuperResolution     | Request.Operation | 指定超分辨率模板参数                                         | Container | 否       |
| TemplateId          | Request.Operation | 指定的模板 ID                                                | String    | 否       |
| Transcode           | Request.Operation | 指定转码模板参数，不能与 TranscodeTemplateId 同时为空        | Container | 否       |
| TranscodeTemplateId | Request.Operation | 指定的转码模板 ID,优先使用模板 ID，不能与 Transcode 同时为空 | String    | 否       |
| Watermark           | Request.Operation | 指定水印模板参数，同创建水印模板 CreateMediaTemplate 接口的 Request.Watermark，最多传3个 | Container | 否       |
| WatermarkTemplateId | Request.Operation | 指定的水印模板 ID，可以传多个水印模板 ID，最多传3个，优先使用模板 ID | String    | 否       |
| DigitalWatermark    | Request.Operation | 指定数字水印参数                                             | Container | 否       |
| Output              | Request.Operation | 结果输出地址                                                 | Container | 是       |

>!
>
> 优先使用 TemplateId，无 TemplateId 时使用对应任务类型的参数。

Container 类型 SuperResolution 的具体数据描述如下：

| 节点名称（关键字） | 父节点                            | 描述                                                         |
| :----------------- | :-------------------------------- | :----------------------------------------------------------- |
| Resolution         | Request.Operation.SuperResolution | 同创建超分辨率模板 CreateMediaTemplate 接口中的 Request.Resolution |
| EnableScaleUp      | Request.Operation.SuperResolution | 同创建超分辨率模板 CreateMediaTemplate 接口中的 Request.EnableScaleUp |

Container 类型 DigitalWatermark 的具体数据描述如下：

| 节点名称（关键字） | 父节点                             | 描述                                                         | 类型   | 必选 |
| :----------------- | :--------------------------------- | :----------------------------------------------------------- | :----- | :--- |
| Message            | Request.Operation.DigitalWatermark | 数字水印嵌入的字符串信息，长度不超过64个字符，仅支持中文、英文、数字、_、-和* | string | 是   |
| Type               | Request.Operation.DigitalWatermark | 水印类型，当前仅可设置为 Text                                | String | 是   |
| Version            | Request.Operation.DigitalWatermark | 水印版本，当前仅可设置为 V1                                  | String | 是   |
| IgnoreError        | Request.Operation.DigitalWatermark | 当添加水印失败是否忽略错误继续执行任务，限制为 true/false，默认 false | string | 否   |

Container 类型 Output 的具体数据描述如下：

| 节点名称（关键字） | 父节点                   | 描述             | 类型   | 是否必选 |
| :----------------- | :----------------------- | :--------------- | :----- | :------- |
| Region             | Request.Operation.Output | 存储桶的地域     | String | 是       |
| Bucket             | Request.Operation.Output | 存储结果的存储桶 | String | 是       |
| Object             | Request.Operation.Output | 输出结果的文件名 | String | 是       |

#### 返回结果示例

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

    [RequestId] => NjI2OGY4ZDdfZmNjYTNiMGAJODIJAOIDJAOMmVmNDU=
    [ContentType] => application/xml
    [ContentLength] => 1170
    [Bucket] => examplebucket-125000000
    [Location] => examplebucket-125000000.ci.ap-guangzhou.myqcloud.com/jobs
    [Response] => Array
        (
            [JobsDetail] => Array
                (
                    [Code] => Success
                    [CreationTime] => 2022-04-27T16:03:35+0800
                    [EndTime] => -
                    [Input] => Array
                        (
                            [BucketId] => examplebucket-125000000
                            [Object] => video01.mp4
                            [Region] => ap-guangzhou
                        )

                    [JobId] => j89be22b8c60011ec9070fasd8a09d80a9b8
                    [Message] => 
                    [Operation] => Array
                        (
                            [DigitalWatermark] => Array
                                (
                                    [IgnoreError] => true
                                    [Message] => xxx
                                    [State] => Running
                                    [Type] => Text
                                    [Version] => V1
                                )

                            [Output] => Array
                                (
                                    [Bucket] => examplebucket-125000000
                                    [Object] => SuperResolution.flv
                                    [Region] => ap-guangzhou
                                )

                            [TemplateId] => t19ea5e0c0b7b904a8sd09a8sd09a80sd10
                            [TemplateName] => SuperResolution-1
                            [TranscodeTemplateId] => t19ea5e0c0b7b904a8sd09a8sd09a80sd10
                            [WatermarkTemplateId] => t19ea5e0c0b7b904a8sd09a8asdasddsd10
                        )

                    [QueueId] => p81e648af2aee49688570asd8a90sd6
                    [StartTime] => -
                    [State] => Submitted
                    [Tag] => SuperResolution
                )

        )

)
```



