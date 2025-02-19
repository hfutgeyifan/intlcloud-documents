### 在接入之前需要做哪些准备?
具体请参见 [接入准备文档](https://intl.cloud.tencent.com/document/product/1158/49607)。

### 应用云渲染云 API 的 Region 参数指的是并发资源地区吗？
不是。Region 是云 API 的公共参数，在应用云渲染的云 API 中是不需要填的。应用云渲染服务会根据 UserIP 选择最优接入区域，不需要业务指定。

### 应用云渲染是否支持用户排队？
应用云渲染的排队页面是需要业务方来开发的，相关功能请参见 [排队功能](https://intl.cloud.tencent.com/document/product/1158/49615#.E6.8E.92.E9.98.9F.E5.8A.9F.E8.83.BD)。

### UserId 和 RequestId 分别指的什么？
UserId 是业务方自定义并传给云渲染服务的用户唯一标示字符串，例如 user123456。云渲染服务接到请求的云 API 之后，会回给业务方一个 RequestId，例如 `01fdc815-c4e7-4642-819e-a011856dfd5a1`。

### 如何查看 RequestId?
1. 在 Chrome 浏览器开发者工具中 NetWork 获取 CreateSession 的 RequestId。
2. 云 API 返回值中包含 RequestId，建议业务后台记录下来。

### 业务可以获取到云渲染资源的公网 IP 来实现访问白名单或者其他功能吗？
不可以，因为云渲染服务提供的外网 IP 是不固定的。需要业务放开对所有来源 IP 使用 UDP 8000 端口限制，如无特殊安全问题，建议放开所有 UDP 端口限制。
