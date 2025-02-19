
<dx-alert infotype="explain" title="">
若您的函数于2021年01月29日前创建且尚未进行迁移，如需使用更多日志分析功能，则请参见 [日志投递配置（旧）](https://intl.cloud.tencent.com/document/product/583/34876)，将函数调用日志投递到日志服务 CLS 使用。
</dx-alert>



云函数 SCF 于2021年01月29日起全量接入腾讯云 [日志服务 CLS](https://intl.cloud.tencent.com/document/product/614)，在此之后创建的函数调用日志将投递至 CLS，并支持日志实时输出，在此日期前创建的函数正在按地域逐渐进行迁移，详情可参见 [云函数日志服务变更说明](https://intl.cloud.tencent.com/document/product/583/39328)。

本文介绍云函数 SCF 所提供的 [默认投递](#MRTD) 和 [自定义投递](#ZDYTD) 两种日志服务投递方式及其配置方法。

## 权限说明

为保证日志正常查看，子账号下至少拥有日志服务 CLS 只读权限 `QcloudCLSReadOnlyAccess`。主账号为子账号授权方法请参见 [授权管理](https://intl.cloud.tencent.com/document/product/598/10602)。


## 限制说明

函数调用日志投递至日志服务的限制如下：
- 每个请求5秒内打印的日志量上限为1MB。
- 每个请求5秒内打印的日志条数上限为5000条。
- 每条日志长度上限为8KB，超出将截取前8KB。

请关注日志服务配置是否能够满足业务需求，超限可能会导致日志写入失败。

## 操作步骤
### 默认投递[](id:MRTD)

新建函数时，如不指定日志投递主题，将会使用默认投递日志能力。默认投递日志时，SCF 将会为您开通日志服务并将函数调用日志投递至 SCF 专用日志集下的日志主题中，SCF 专用日志集和日志主题分别以 `SCF_logset` 和 `SCF_logtopic` 为前缀命名，如不存在将自动创建。函数调用日志默认保留7天，您可在 [日志服务控制台](https://console.cloud.tencent.com/cls/logset) 查看及管理。

<dx-alert infotype="notice" title="">
- 日志服务为独立计费产品，SCF 专用日志主题会占用日志服务免费额度，详情可参见 [日志服务计费详情](https://intl.cloud.tencent.com/document/product/614/37509)。
- 为保证 SCF 控制台日志正常展示，SCF 专用日志主题不支持修改索引配置。如需自定义日志索引配置，请参考下文自定义投递配置函数日志主题。
</dx-alert>



#### 配置日志服务

1. 登录云函数控制台，选择左侧导航栏中的 **[函数服务](https://console.cloud.tencent.com/scf/list)**。
2. 在主界面上方选择期望创建函数的地域，并单击**新建**，进入函数创建流程。
3. 选择使用**模板创建**或选择使用**自定义创建**新建函数。本文以**自定义创建**为例。
4. 在“高级配置”中，选择“日志配置”中的“默认投递”。如下图所示： 
![](https://main.qcloudimg.com/raw/3954432a56fdc393ec4d0a72f663854f.png)
5. 单击**完成**即可完成函数日志默认投递。您可在**函数管理** > **函数配置**中查看日志配置。如下图所示： 
![](https://main.qcloudimg.com/raw/4148a9a9e023fb7538a8c311934e43d6.png)

#### 查看和管理日志服务

您可单击函数配置中“日志配置”的日志集 ID，前往 [日志服务控制台](https://console.cloud.tencent.com/cls/logset) 查看和管理日志。SCF 专用日志集在日志服务控制台已用 `SCF` 字样进行标记，如有日志持久化存储、投递或消费、对日志内容进行监控告警等需要，均可在日志服务控制台完成配置。




### 自定义投递[](id:ZDYTD)

新建函数时，如需指定函数调用日志投递主题，可选择使用日志自定义投递能力。在使用日志自定义投递能力之前，需保证账号已经开通 [日志服务](https://intl.cloud.tencent.com/products/cls)。


#### 创建日志集和日志主题

登录 [日志服务控制台](https://console.cloud.tencent.com/cls) 并 [创建日志集和日志主题](https://intl.cloud.tencent.com/document/product/614/42319)。本文以在广州创建 `SCF-test` 日志集和日志主题为例。如下图所示： 
>!日志集地域请选择函数服务所在地域，暂不支持跨地域日志推送。
>
![](https://main.qcloudimg.com/raw/f3ffd10aaaeb6abc2a492e5840339c9f.png)

#### 配置日志服务

1. 登录云函数控制台，选择左侧导航栏中的 **[函数服务](https://console.cloud.tencent.com/scf/list)**。
2. 在主界面上方选择期望创建函数的地域，并单击**新建**，进入函数创建流程。
3. 选择使用**模板创建**或选择使用**自定义创建**新建函数。本文以**自定义创建**为例。
4. 在“高级配置”中，选择“日志配置”中的“自定义投递”，并选择已为该函数创建的日志集和日志主题，本文以 `SCF-test` 为例。如下图所示： 
![](https://main.qcloudimg.com/raw/53a703aee35dd6ed7967d981b139aff0.png)
5. 单击**完成**即可完成函数日志投递自定义配置。






### 索引配置

日志检索依赖日志主题的索引配置，在函数创建时，SCF 会自动为您完成索引配置。如遇索引异常无法正常查看日志，请参考如下步骤配置索引：



1. 登录云函数控制台，选择左侧导航栏中的 **[函数服务](https://console.cloud.tencent.com/scf/list)**。
2. 在“函数服务”列表页面，选择日志索引异常的函数名，进入“函数管理”页面。
3. 在“日志查询”页签中，选择“高级检索”中的“索引配置”。如下图所示： 
![](https://main.qcloudimg.com/raw/8d506d9d22c6c26b3e2396acb33fb499.png)
4. 在“索引配置”页中，开启“索引状态”和“键值索引”并选择**自动配置**。如下图所示： 
![](https://main.qcloudimg.com/raw/861138c664768aab368761d91b441e9e.png)
5. 完成索引配置后单击**确定**保存。



步骤4中的配置方法仅对日志主题中已有函数调用日志的场景有效，日志主题中无函数调用日志，请参照下表手动配置**键值索引**。
<table>
<thead>
<tr>
<th>字段名称</th>
<th>字段类型</th>
<th>字段含义</th>
</tr>
</thead>
<tbody><tr>
<td>SCF_FunctionName</td>
<td>text</td>
<td>函数名称。</td>
</tr>
<tr>
<td>SCF_Namespace</td>
<td>text</td>
<td>函数所在命名空间。</td>
</tr>
<tr>
<td>SCF_StartTime</td>
<td>long</td>
<td>调用开始时间。</td>
</tr>
<tr>
<td>SCF_LogTime</td>
<td>long</td>
<td>日志产生时间。</td>
</tr>
<tr>
<td>SCF_RequestId</td>
<td>text</td>
<td>请求 ID。</td>
</tr>
<tr>
<td>SCF_Duration</td>
<td>long</td>
<td>函数运行时间。</td>
</tr>
<tr>
<td>SCF_Alias</td>
<td>text</td>
<td>别名。</td>
</tr>
<tr>
<td>SCF_Qualifier</td>
<td>text</td>
<td>版本。</td>
</tr>
<tr>
<td>SCF_MemUsage</td>
<td>double</td>
<td>函数运行内存。</td>
</tr>
<tr>
<td>SCF_Level</td>
<td>text</td>
<td>Log4J 日志级别，默认为 INFO。</td>
</tr>
<tr>
<td>SCF_Message</td>
<td>text</td>
<td>日志内容。</td>
</tr>
<tr>
<td>SCF_Type</td>
<td>text</td>
<td>日志类型，Platform 指平台日志，Custom 指用户日志。</td>
</tr>
<tr>
<td>SCF_StatusCode</td>
<td>long</td>
<td>函数运行 <a href="https://intl.cloud.tencent.com/document/product/583/35311">状态码</a>。</td>
</tr>
<tr>
<td>SCF_RetryNum</td>
<td>long</td>
<td>重试次数。</td>
</tr>
</tbody></table>


为保证云函数控制台日志展示效果，请在键值索引配置中为字段打开“开启统计”能力。如下图所示： 
![](https://main.qcloudimg.com/raw/5e34368e42bb03dd6d6be864af695fa3.png)





