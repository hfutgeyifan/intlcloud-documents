[](id:1)
### VPN 网关是如何实现的，可用性如何？
- VPN 网关是通过网络功能虚拟化（NFV）实现的，采用双机热备的策略，单台故障时自动切换，不会影响业务正常运行。
- VPN 通道在公网中运行，公网网络出现阻塞、抖动、延迟等问题都会对 VPN 网络质量产生影响。如果业务对网络传输的延迟、抖动容忍度较低，建议使用 [专线接入](https://intl.cloud.tencent.com/document/product/216)。

[](id:2)

### 为什么 VPN 网关与 VPN 通道显示的监控数据有时不一致？
目前 VPN 网关与 VPN 通道的数据采集位置与上报间隔存在区别，其中 VPN 网关的统计粒度为1分钟，VPN 通道的统计粒度为10秒，统计粒度不一致。因此在监控页进行数据聚合的时候，会造成 VPN 网关与 VPN 通道的展示数据不一致的情况。


### 如何配置 VPN？
IPsec VPN 可以在控制台实现全自助配置，详情请参见 [快速入门](https://intl.cloud.tencent.com/document/product/1037/32689)。

### 如何创建 VPN 网关？
用户可以进入 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 创建 VPN 网关，详情请参见 [创建 VPN 网关](https://intl.cloud.tencent.com/document/product/1037/32690)。

### 如何创建 VPN 通道？
用户可以进入 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 创建 VPN 通道，详情请参见 [创建 VPN 通道](https://intl.cloud.tencent.com/document/product/1037/32692)。

### 如何查看 VPN 连接监控数据？
用户可以进入 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 查看 VPN 连接监控数据，详情请参见[ 查看监控数据](https://intl.cloud.tencent.com/document/product/1037/32698)。

### 如何设置 VPN 连接告警？
用户可以进入 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 设置 VPN 连接告警，详情请参见 [设置告警](https://intl.cloud.tencent.com/document/product/1037/32699)。

### 如何查看 VPN 网关详细信息？
用户可以进入[私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 查看 VPN 网关详细信息，详情请参见 [查看 VPN 网关详细信息](https://intl.cloud.tencent.com/document/product/1037/32700)。

### 如何修改 VPN 通道配置？
用户可以进入 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 修改 VPN 通道配置，详情请参见 [修改 VPN 通道配置](https://intl.cloud.tencent.com/document/product/1037/32701)。

### 如何开启网关流控明细？
用户可以进入 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 开启网关流控明细，详情请参见 [开启网关流控明细](https://intl.cloud.tencent.com/document/product/1037/32702)。

### 如何设置网关流控明细？
用户可以进入 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 设置网关流控明细，详情请参见 [设置网关流控明细](https://intl.cloud.tencent.com/document/product/1037/32703)。

### 如何查看网关流控明细？
用户可以进入 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 查看网关流控明细，详情请参见 [查看网关流控明细](https://intl.cloud.tencent.com/document/product/1037/32704)。

### 如何绑定高防包？
用户可以进入 [DDoS 防护（大禹）管理控制台](https://console.cloud.tencent.com/ddos/overview) 绑定高防包，详情请参见 [绑定高防包](https://intl.cloud.tencent.com/document/product/1037/32705)。

### 为什么创建不了100MB以上的VPN连接？
- 部分地域还未开放，请在控制台进行查看。
- A5路由未配置。
- 您的账户还未开通该功能，请提交 [工单申请](https://console.cloud.tencent.com/workorder/category)。

### 健康检查怎么配置？
1. 首先确保与 VPN 相连的对端是否为路由型网关，需要进行路由型做对接。
2. 在腾讯云控制台侧配置健康检查。
>?
>- 在进行健康检查配置前，请做好隧道主备，以防业务受到影响。
>- 需要确保两端 IP 不冲突，如果两端 IP 在同一网段，则不需要单独配置路由来指定对端。
>
3. 配置 VPN 网关路由并设置优先级。

### 通道健康状态为“不健康”，是什么原因？
您配置的健康检查 IP Ping 失败，请检查健康检查配置。


### 通道未联通/已删除，为什么还在自动扣费？
腾讯云 VPN 收取的是出 VPN 网关的流量的费用，不使用时请及时删除。


### 是否支持升降配&计费转换？
- 计费方面，当前仅支持包年包月方式转换按量计费。
- 配额方面，当前仅支持**5-100**和**200-1000**升降配。包年仅支持升配，不支持降配。




