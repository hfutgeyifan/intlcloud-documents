>! 对于云产品产生的告警、审计等运维事件，将全部投递至云服务事件集，该投递为默认投递，不支持更改或编辑。您可以在事件总线控制台，为云服务事件集绑定相应的规则和目标，完成云服务事件的分发处理。

## 官方云服务事件简介
官方云服务事件分为 [**监控事件**](https://intl.cloud.tencent.com/document/product/1108/46252)（如云服务器的内核故障、内存 oom 等）与**审计事件**（Coming Soon），由官方云服务主动产生。对于不同的事件，投递的事件内容也有一定区别：
- **监控事件**
```json
{
    "specversion":"1.0",
    "id":"13a3f42d-7258-4ada-da6d-023a333b4662",
    "source":"${ProductName}.cloud.tencent",
    "type":"cvm:ErrorEvent:ping_unreachable",
    "subject":"${资源 ID}",
    "time": 1615430559146,
    "region":"ap-guangzhou",
    "resource":[
        "qcs::eb:ap-guangzhou:uid1250000000:eventbusid/eventruleid"
    ],
    "datacontenttype":"application/json;charset=utf-8",
    "tags":{
        "key1":"value1",
        "key2":"value2"
     },
    "status":"1",
    "data":{
        "appId":"1250000011",
        "instanceId":"ins-sjdksjk",
        "projectId":"11",
        "dimensions":{
            "ip":"127.0.0.1"
            },
        "additionalMsg":{
            "IP":"something unnormal"
            }
    }
}
```

- **审计事件**
```json
{
    "specversion":"1.0",
    "id":"13a3f42d-7258-4ada-da6d-023a333b4662",
    "source":"${ProductName}.cloud.tencent",
    "type":"cvm:CloudEvent:ApiCall",
    "subject":"${资源 ID}",
    "time": 1615430559146,
    "region":"ap-guangzhou",
    "resource":[
        "qcs::eb:ap-guangzhou:uid1250000000:eventbusid/eventruleid"
    ],
    "datacontenttype":"application/json;charset=utf-8",
    "tags":{
        "key1":"value1",
        "key2":"value2"
     },
    "data":{
        ${原始 API 操作日志}
    }
}
```

## 支持事件列表
- [云监控告警事件](https://intl.cloud.tencent.com/document/product/1108/46252)
- [云审计服务事件](https://intl.cloud.tencent.com/document/product/1021/37598)


## 最佳实践
- [Oceanus 告警信息实时推送](https://intl.cloud.tencent.com/document/product/1108/45208)
- [云服务器异常自动备份与重启](https://intl.cloud.tencent.com/document/product/1108/45207)
