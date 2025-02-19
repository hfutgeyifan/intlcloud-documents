多可用区部署可保护数据库，以防数据库实例发生故障或可用区中断，请参见 [地域和可用区](https://intl.cloud.tencent.com/document/product/236/8458)。
云数据库 MySQL 多可用区部署为数据库实例提供高可用性和故障转移支持。多可用区是在单可用区的级别上，将同一地域的多个单可用区组合成的物理区域。

>?
>- 无论数据库集群中的实例是否跨多个可用区，每个云数据库 MySQL 均有实时热备的备机保证数据库的高可用性。
>- 在多可用区部署中，云数据库 MySQL 会自动在不同可用区中预置和维护一个同步备用副本。
>- 主数据库实例将跨可用区同步复制到备用副本，以提供数据冗余、消除 I/O 冻结，并在系统备份期间将延迟峰值降至最小。

### 支持地域
云数据库 MySQL 多可用区部署目前支持广州、上海、北京、成都、弗吉尼亚地区。

### 部署多可用区
1. 登录 [云数据库 MySQL 控制台](https://console.cloud.tencent.com/cdb/)，在实例列表，单击**新建**进入购买页。
2. 在 MySQL 购买页，选择对应支持地域后，在“备可用区”选项，选择对应备可用区。
>?仅部分可用区支持备可用区，具体可选备可用区请在购买页查看。
>
![](https://main.qcloudimg.com/raw/d6b71d73ff799a98ba8eb12077269f96.png)
3. 确认无误后，单击**立即购买**，完成付款后，可返回实例列表查看购买的多可用区实例。

### 故障转移
云数据库 MySQL 会自动处理故障转移，因此您可以快速恢复数据库操作而无需管理干预。如果出现如下任一条件，主数据库实例会自动切换到备可用区的备用副本：
- 可用区中断。
- 主数据库实例故障。
