### 短信默认的频率限制是什么？
为了保障业务和通道安全，减少业务被刷后的经济损失，短信默认的频率限制策略为：
- 同一号码同一内容30秒内最多发送1条。
- 同一手机号一个自然日最多发送10条。

企业认证用户可以登录 [短信控制台](https://console.cloud.tencent.com/smsv2) 设置或修改相应的频率限制策略，具体操作请参见 [设置发送频率限制](https://intl.cloud.tencent.com/document/product/382/35469)。
个人认证用户不提供修改频率限制的权限。如需使用该功能，请将 “个人认证” 修改为 “企业认证”，更多企业认证用户权益信息请参见 [权益区别](https://intl.cloud.tencent.com/document/product/382/40653)。

### 如何添加告警联系人？
详细操作请参见 [配置告警联系人](https://intl.cloud.tencent.com/document/product/382/35470)。

### 如何预防短信轰炸（盗刷）？[](id:Q4)
短信轰炸（盗刷）是指通过恶意程序或者工具，利用网站客户端或服务端漏洞，在短时间内（例如一天以内）给很多无关的手机号码发送大量的验证码短信，导致手机用户被骚扰。
出现短信轰炸（盗刷）后，既会对无辜用户造成骚扰，引起大量投诉导致短信通道不可用，也会给业务方造成大量的经济损失，所以需要提前做好预防措施。
下图是客户遇到的一个实际案例（正常情况下每天几十条短信下发量，被轰炸期间每天几万条短信下发量）
![](https://main.qcloudimg.com/raw/071fbb50d64aa2dcc1f44e0e12ced9eb.png)
鉴于短信轰炸（盗刷）的发起一般都是服务器行为，还可采用以下综合手段进行防御：

- 单 IP 请求次数限制。
- 限制单个号码发送次数，可 [设置发送频率限制](https://intl.cloud.tencent.com/document/product/382/35469) ，并 [配置告警联系人](https://intl.cloud.tencent.com/document/product/382/35470)。
- [设置发送超量提醒](https://intl.cloud.tencent.com/document/product/382/35469)。
- 定期（例如每天）登录 [短信控制台](https://console.cloud.tencent.com/smsv2) 查看具体统计数据，关注短信下发情况。如发现异常及时处理，紧急情况下可在短信控制台停用短信服务。

### 中国大陆地区、国际/港澳台短信发送的区别？
因运营商要求，发送中国大陆地区短信必须携带短信签名；发送国际/港澳台短信无短信签名要求，您可根据情况选择是否需要携带签名。
- 发送中国大陆地区短信前，您必须先 [创建签名](https://intl.cloud.tencent.com/document/product/382/35456) 和 [创建正文模板](https://intl.cloud.tencent.com/document/product/382/35457)，并审核通过。
- 发送国际/港澳台短信前，您必须先 [创建正文模板](https://intl.cloud.tencent.com/document/product/382/35461) 并审核通过。如需携带签名则还应 [创建签名](https://intl.cloud.tencent.com/document/product/382/35460) 并审核通过，否则无需创建签名。

### 如何查询单个手机发送记录？
您可以登录 [短信控制台](https://console.cloud.tencent.com/smsv2) ，单击目标应用名称进入应用详情页，根据实际需求选择以下方式进行查询：
- 中国大陆地区短信：选择【统计分析】>【中国大陆地区短信】>【短信记录】页面输入手机号可查询，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/a727c37158e9b9d3688ebfeabc13d512.png)
- 国际/港澳台短信：选择【统计分析】>【国际/港澳台短信】>【短信记录】页面查询。

### 如何创建和查看应用（SDK AppID）？
SDK AppID 用于标识应用，每个短信应用拥有唯一的 SDK AppID，添加应用后由系统自动生成。具体添加操作请参见 [创建应用](https://intl.cloud.tencent.com/document/product/382/35468)。
您可以登录 [短信控制台](https://console.cloud.tencent.com/smsv2) ，选择【应用管理】>【应用列表】，单击目标应用名称进入应用详情页查看已有应用的 SDK AppID。

### 测试、告警手机号如何开通频率限制白名单？
如需开通测试手机号无频率限制，请联系 [腾讯云短信小助手](https://tccc.qcloud.com/web/im/index.html#/chat?webAppId=8fa15978f85cb41f7e2ea36920cb3ae1&title=Sms)。

### 需要知道具体哪个手机号是否收到短信怎么查？
您可以登录 [短信控制台](https://console.cloud.tencent.com/smsv2) ，单击目标应用名称进入应用详情页，根据实际需求选择以下方式进行查询或导出记录：
- 中国大陆地区短信：选择【统计分析】>【中国大陆地区短信】>【短信记录】页面查询或导出指定时间段内的记录。
- 国际/港澳台短信：选择【统计分析】>【国际/港澳台短信】>【短信记录】页面查询或导出指定时间段内的记录。

### 发送国际/港澳台短信是否有数量限制？
单个腾讯云账户的国际/港澳台短信每日发送量限额为1000条，如需调整，请联系 [腾讯云短信小助手](https://tccc.qcloud.com/web/im/index.html#/chat?webAppId=8fa15978f85cb41f7e2ea36920cb3ae1&title=Sms)。
