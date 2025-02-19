## 简介

本文档提供关于列出对象操作相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名                   | 操作描述                                       |
| ------------------------------------------------------------ | ------------------------ | ---------------------------------------------- |
| [GET Bucket（List Objects）](https://intl.cloud.tencent.com/document/product/436/30614) | 查询对象列表             | 查询存储桶下的部分或者全部对象                 |
| [GET Bucket Object Versions](https://intl.cloud.tencent.com/document/product/436/31551) | 查询对象及其历史版本列表 | 查询存储桶下的部分或者全部对象及其历史版本信息 |

## 查询对象列表

#### 功能说明

查询存储桶下的部分或者全部对象。

#### 方法原型

```go
func (s *BucketService) Get(ctx context.Context, opt *BucketGetOptions) (*BucketGetResult, *Response, error)
```

#### 请求示例1：列出对象列表

[//]: # ".cssg-snippet-get-bucket"
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main() {
    // 存储桶名称，由bucketname-appid 组成，appid必须填入，可以在COS控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
    // 替换为用户的 region，存储桶region可以在COS控制台“存储桶概览”查看 https://console.cloud.tencent.com/ ，关于地域的详情见 https://intl.cloud.tencent.com/document/product/436/6224 。
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // 通过环境变量获取密钥
            // 环境变量 SECRETID 表示用户的 SecretId，登录访问管理控制台查看密钥，https://console.cloud.tencent.com/cam/capi
            SecretID: os.Getenv("SECRETID"),
            // 环境变量 SECRETKEY 表示用户的 SecretKey，登录访问管理控制台查看密钥，https://console.cloud.tencent.com/cam/capi
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })
    opt := &cos.BucketGetOptions{
        Prefix:  "test",
        MaxKeys: 100,
    }
    _, _, err := client.Bucket.Get(context.Background(), opt)
    if err != nil {
        panic(err)
    }
}
```

#### 请求示例2：列出目录下对象
对象存储中本身是没有文件夹和目录的概念的，为了满足用户使用习惯，用户可通过分隔符/来模拟“文件夹”。

[//]: # ".cssg-snippet-get-bucket2"
```go
package main

import (
    "context"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
    "fmt"
)

func main() {
    // 存储桶名称，由bucketname-appid 组成，appid必须填入，可以在COS控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
    // 替换为用户的 region，存储桶region可以在COS控制台“存储桶概览”查看 https://console.cloud.tencent.com/ ，关于地域的详情见 https://intl.cloud.tencent.com/document/product/436/6224 。
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // 通过环境变量获取密钥
            // 环境变量 SECRETID 表示用户的 SecretId，登录访问管理控制台查看密钥，https://console.cloud.tencent.com/cam/capi
            SecretID: os.Getenv("SECRETID"),
            // 环境变量 SECRETKEY 表示用户的 SecretKey，登录访问管理控制台查看密钥，https://console.cloud.tencent.com/cam/capi
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })
    var marker string
    opt := &cos.BucketGetOptions{
        Prefix:    "folder/", // prefix表示要查询的文件夹
        Delimiter: "/",       // deliter表示分隔符, 设置为/表示列出当前目录下的object, 设置为空表示列出所有的object
        MaxKeys:   1000,      // 设置最大遍历出多少个对象, 一次listobject最大支持1000
    }
    isTruncated := true
    for isTruncated {
        opt.Marker = marker
        v, _, err := client.Bucket.Get(context.Background(), opt)
        if err != nil {
            fmt.Println(err)
            break
        }
        for _, content := range v.Contents {
            fmt.Printf("Object: %v\n", content.Key)
        }
        // common prefix表示表示被delimiter截断的路径, 如delimter设置为/, common prefix则表示所有子目录的路径
        for _, commonPrefix := range v.CommonPrefixes {
            fmt.Printf("CommonPrefixes: %v\n", commonPrefix)
        }
        isTruncated = v.IsTruncated // 是否还有数据
        marker = v.NextMarker       // 设置下次请求的起始 key
    }
}
```

#### 参数说明

```go
type BucketGetOptions struct {
    Prefix       string 
    Delimiter    string 
    EncodingType string 
    Marker       string 
    MaxKeys      int    
}
```

| 参数名称     | 参数描述                                                     | 类型   | 是否必填 |
| ------------ | ------------------------------------------------------------ | ------ | ---- |
| Prefix       | 默认为空，对对象键进行筛选，匹配前缀 prefix 为相同值的 objects | string | 否   |
| Delimiter    | 默认为空，如需模拟文件夹，可设置分隔符`/`                    | string | 否   |
| EncodingType | 默认不编码，规定返回值的编码方式，可选值：url                | string | 否   |
| Marker       | 默认以 UTF-8 二进制顺序列出条目，标记返回 objects 的 list 的起点位置 | string | 否   |
| MaxKeys      | 最多返回的 objects 数量，默认为最大的1000                    | int    | 否   |

#### 返回结果说明

```go
type BucketGetResult struct {
    Name           string
    Prefix         string 
    Marker         string 
    NextMarker     string 
    Delimiter      string 
    MaxKeys        int
    IsTruncated    bool
    Contents       []Object 
    CommonPrefixes []string 
    EncodingType   string   
}
```

| 参数名称       | 参数描述                                                     | 类型     |
| -------------- | ------------------------------------------------------------ | -------- |
| Name           | 存储桶名称，格式：BucketName-APPID，例如 examplebucket-1250000000 | string   |
| Prefix         | 默认为空，对对象键进行筛选，匹配前缀 prefix 为相同值的 objects | string   |
| Marker         | 默认以 UTF-8 二进制顺序列出条目，标记返回 objects 的 list 的起点位置 | string   |
| NextMarker     | 当 IsTruncated 为 true 时，标记下一次返回 objects 的 list 的起点位置 | string   |
| Delimiter      | 默认为空，如需模拟文件夹，可设置分隔符`/`                   | string   |
| MaxKeys        | 最多返回的 objects 数量，默认为最大的1000                    | int      |
| IsTruncated    | 表示返回的 objects 是否被截断                                | bool     |
| Contents       | 包含所有 object 元信息的 list，每个 Object 类型包括 ETag，StorageClass，Key，Owner，LastModified，Size 等信息 | []Object |
| CommonPrefixes | 所有以 Prefix 开头，以 Delimiter 结尾的 Key 被归到同一类     | []string |
| EncodingType   | 默认不编码，规定返回值的编码方式，可选值：url                | string   |

## 查询对象历史版本列表

#### 功能说明

查询开启版本控制的存储桶下的部分或者全部对象。

#### 方法原型
```go
func (s *BucketService) GetObjectVersions(ctx context.Context, opt *BucketGetObjectVersionsOptions) (*BucketGetObjectVersionsResult, *Response, error)
```

#### 示例代码：获取所有对象历史版本列表

[//]: #	".cssg-snippet-list-objects-versioning"

```go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "os"
)

func main() {
    // 存储桶名称，由bucketname-appid 组成，appid必须填入，可以在COS控制台查看存储桶名称。 https://console.cloud.tencent.com/cos5/bucket
    // 替换为用户的 region，存储桶region可以在COS控制台“存储桶概览”查看 https://console.cloud.tencent.com/ ，关于地域的详情见 https://intl.cloud.tencent.com/document/product/436/6224 。
    u, _ := url.Parse("https://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            // 通过环境变量获取密钥
            // 环境变量 SECRETID 表示用户的 SecretId，登录访问管理控制台查看密钥，https://console.cloud.tencent.com/cam/capi
            SecretID: os.Getenv("SECRETID"),
            // 环境变量 SECRETKEY 表示用户的 SecretKey，登录访问管理控制台查看密钥，https://console.cloud.tencent.com/cam/capi
            SecretKey: os.Getenv("SECRETKEY"),
        },
    })
    keyMarker := ""
    versionIdMarker := ""
    isTruncated := true
    opt := &cos.BucketGetObjectVersionsOptions{}
    for isTruncated {
        opt.KeyMarker = keyMarker
        opt.VersionIdMarker = versionIdMarker
        v, _, err := client.Bucket.GetObjectVersions(context.Background(), opt)
        if err != nil {
            // ERROR
            break
        }
        for _, vc := range v.Version {
            fmt.Printf("Version: %v, %v, %v, %v\n", vc.Key, vc.Size, vc.VersionId, vc.IsLatest)
        }
        for _, dc := range v.DeleteMarker {
            fmt.Printf("DeleteMarker: %v, %v, %v\n", dc.Key, dc.VersionId, dc.IsLatest)
        }
        keyMarker = v.NextKeyMarker
        versionIdMarker = v.NextVersionIdMarker
        isTruncated = v.IsTruncated
    }
}
```

#### 参数说明
```go
type BucketGetObjectVersionsOptions struct {
    Prefix          string
    Delimiter       string
    EncodingType    string
    KeyMarker       string
    VersionIdMarker string
    MaxKeys         int
}
```

| 名称              | 描述                                                         | 类型   | 是否必选 |
| :---------------- | :----------------------------------------------------------- | :----- | :------- |
| prefix            | 对象键匹配前缀，限定响应中只包含指定前缀的对象键             | string | 否       |
| delimiter         | 一个字符的分隔符，用于对对象键进行分组。所有对象键中从 prefix 或从头（如未指定 prefix）到首个 delimiter 之间相同的部分将作为 CommonPrefixes 下的一个 Prefix 节点。被分组的对象键不再出现在后续对象列表中，具体场景和用法可参考下面的实际案例 | string | 否       |
| encoding-type     | 规定返回值的编码方式，可选值：url，代表返回的对象键为 URL 编码（百分号编码）后的值，例如“腾讯云”将被编码为`%E8%85%BE%E8%AE%AF%E4%BA%91` | string | 否       |
| key-marker        | 起始对象键标记，从该标记之后（不含）按照 UTF-8 字典序返回对象版本条目 | string | 否       |
| version-id-marker | 起始版本 ID 标记，从该标记之后（不含）返回对象版本条目，如果上一次 List 结果的 NextVersionIdMarker 为空，则该参数也指定为空 | string | 否       |
| max-keys          | 单次返回最大的条目数量，默认值为1000，最大为1000 **注意：**该参数会限制每一次 List 操作返回的最大条目数，COS 在每次 List 操作中将返回不超过 max-keys 所设定数值的条目（CommonPrefixes、Version 和 DeleteMarker 合计），如果单次响应中未列出所有对象，COS 会返回 NextKeyMarker 和 NextVersionIdMarker 节点，其值分别为您下次 List 请求的 key-marker 和 version-id-marker 参数，以便您列出后续版本 | int    | 否       |

#### 返回结果说明

```go
type BucketGetObjectVersionsResult struct {
    Name                string
    EncodingType        string
    Prefix              string
    KeyMarker           string
    VersionIdMarker     string
    MaxKeys             int
    Delimiter           string
    IsTruncated         bool
    NextKeyMarker       string
    NextVersionIdMarker string
    CommonPrefixes      []string
    Version             []ListVersionsResultVersion
    DeleteMarker        []ListVersionsResultDeleteMarker
}
type ListVersionsResultVersion struct {
    Key          string
    VersionId    string
    IsLatest     bool
    LastModified string
    ETag         string
    Size         int
    StorageClass string
    Owner        *Owner
}
type ListVersionsResultDeleteMarker struct {
    Key          string
    VersionId    string
    IsLatest     bool
    LastModified string
    Owner        *Owner
}
```

具体的节点描述如下：

| 节点名称（关键字） | 父节点 | 描述                                           | 类型      |
| :----------------- | :----- | :--------------------------------------------- | :-------- |
| ListVersionsResult | 无     | 保存 GET Bucket Object versions 结果的所有信息 | Container |

**Container 节点 ListVersionsResult 的内容：**

| 节点名称（关键字）  | 父节点             | 描述                                                         | 类型      |
| :------------------ | :----------------- | :----------------------------------------------------------- | :-------- |
| EncodingType        | ListVersionsResult | 编码格式，对应请求中的 encoding-type 参数，且仅当请求中指定了 encoding-type 参数才会返回该节点 | string    |
| Name                | ListVersionsResult | 存储桶的名称，格式为`<BucektName-APPID>`，例如`examplebucket-1250000000`       | string    |
| Prefix              | ListVersionsResult | 对象键匹配前缀，对应请求中的 prefix 参数                     | string    |
| KeyMarker           | ListVersionsResult | 起始对象键标记，从该标记之后（不含）按照 UTF-8 字典序返回对象版本条目，对应请求中的 key-marker 参数 | string    |
| VersionIdMarker     | ListVersionsResult | 起始版本 ID 标记，从该标记之后（不含）返回对象版本条目，对应请求中的 version-id-marker 参数 | string    |
| MaxKeys             | ListVersionsResult | 单次响应返回结果的最大条目数量，对应请求中的 max-keys 参数   | integer   |
| IsTruncated         | ListVersionsResult | 响应条目是否被截断，布尔值，例如 true 或 false               | boolean   |
| NextKeyMarker       | ListVersionsResult | 仅当响应条目有截断（IsTruncated 为 true）才会返回该节点，该节点的值为当前响应条目中的最后一个对象键，当需要继续请求后续条目时，将该节点的值作为下一次请求的 key-marker 参数传入 | string    |
| NextVersionIdMarker | ListVersionsResult | 仅当响应条目有截断（IsTruncated 为 true）才会返回该节点，该节点的值为当前响应条目中的最后一个对象的版本 ID，当需要继续请求后续条目时，将该节点的值作为下一次请求的 version-id-marker 参数传入。该节点的值可能为空，此时下一次请求的 version-id-marker 参数也需要指定为空。 | string    |
| Delimiter           | ListVersionsResult | 分隔符，对应请求中的 delimiter 参数，且仅当请求中指定了 delimiter 参数才会返回该节点 | string    |
| CommonPrefixes      | ListVersionsResult | 从 prefix 或从头（如未指定 prefix）到首个 delimiter 之间相同的部分，定义为 Common Prefix。仅当请求中指定了 delimiter 参数才有可能返回该节点 | Container |
| Version             | ListVersionsResult | 对象版本条目                                                 | Container |
| DeleteMarker        | ListVersionsResult | 对象删除标记条目                                             | Container |

**Container 节点 CommonPrefixes 的内容：**

| 节点名称（关键字） | 父节点                            | 描述                      | 类型   |
| :----------------- | :-------------------------------- | :------------------------ | :----- |
| Prefix             | ListVersionsResult.CommonPrefixes | 单条 Common Prefix 的前缀 | string |

**Container 节点 Version 的内容：**

| 节点名称（关键字） | 父节点                     | 描述                                                         | 类型      |
| :----------------- | :------------------------- | :----------------------------------------------------------- | :-------- |
| Key                | ListVersionsResult.Version | 对象键                                                       | string    |
| VersionId          | ListVersionsResult.Version | 对象的版本 ID 当未启用版本控制时，该节点的值为空字符串当启用版本控制时，启用版本控制之前的对象，其版本 ID 为 null当暂停版本控制时，新上传的对象其版本 ID 为 null，且同一个对象最多只存在一个版本 ID 为 null 的对象版本 | string    |
| IsLatest           | ListVersionsResult.Version | 当前版本是否为该对象的最新版本                               | boolean   |
| LastModified       | ListVersionsResult.Version | 当前版本的最后修改时间，为 ISO8601 格式，例如2019-05-24T10:56:40Z | date      |
| ETag               | ListVersionsResult.Version | 对象的实体标签（Entity Tag），是对象被创建时标识对象内容的信息标签，可用于检查对象的内容是否发生变化 例如"8e0b617ca298a564c3331da28dcb50df"。此头部并不一定返回对象的 MD5 值，而是根据对象上传和加密方式而有所不同 | string    |
| Size               | ListVersionsResult.Version | 对象大小，单位为 Byte                                        | integer   |
| StorageClass       | ListVersionsResult.Version | 对象存储类型。枚举值请参见 [存储类型](https://intl.cloud.tencent.com/document/product/436/30925) 文档，例如 STANDARD_IA，ARCHIVE | Enum      |
| StorageTier        | ListVersionsResult.Version | 当对象存储类型为智能分层存储时，指示对象当前所处的存储层，枚举值：FREQUENT（标准层），INFREQUENT（低频层）。仅当 StorageClass 为 INTELLIGENT_TIERING（智能分层）时才会返回该节点 | Enum      |
| Owner              | ListVersionsResult.Version | 对象持有者信息                                               | Container |

**Container 节点 Version.Owner 的内容：**

| 节点名称（关键字） | 父节点                           | 描述               | 类型   |
| :----------------- | :------------------------------- | :----------------- | :----- |
| ID                 | ListVersionsResult.Version.Owner | 对象持有者的 APPID | string |
| DisplayName        | ListVersionsResult.Version.Owner | 对象持有者的名称   | string |

**Container 节点 DeleteMarker 的内容：**

| 节点名称（关键字） | 父节点                          | 描述                                                         | 类型      |
| :----------------- | :------------------------------ | :----------------------------------------------------------- | :-------- |
| Key                | ListVersionsResult.DeleteMarker | 对象键                                                       | string    |
| VersionId          | ListVersionsResult.DeleteMarker | 对象的删除标记的版本 ID                                      | string    |
| IsLatest           | ListVersionsResult.DeleteMarker | 当前删除标记是否为该对象的最新版本                           | boolean   |
| LastModified       | ListVersionsResult.DeleteMarker | 当前删除标记的删除时间，为 ISO8601 格式，例如2019-05-24T10:56:40Z | date      |
| Owner              | ListVersionsResult.DeleteMarker | 对象持有者信息                                               | Container |

**Container 节点 DeleteMarker.Owner 的内容：**

| 节点名称（关键字） | 父节点                                | 描述               | 类型   |
| :----------------- | :------------------------------------ | :----------------- | :----- |
| ID                 | ListVersionsResult.DeleteMarker.Owner | 对象持有者的 APPID | string |
| DisplayName        | ListVersionsResult.DeleteMarker.Owner | 对象持有者的名称   | string |
