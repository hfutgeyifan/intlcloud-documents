云数据库 MySQL 支持设置密码复杂度，提升数据库访问密码的强度，保障数据库的安全性。

## 前提条件
数据库版本为：
- MySQL 5.6，小版本20201231及以上。
- MySQL 5.7，小版本20201231及以上。
- MySQL 8.0，小版本20201230及以上。

## 注意事项
通过 MySQL 控制台创建帐号设置密码或重置帐号密码时，密码复杂度设置策略无法突破以下初始帐号密码限制：
- 长度在8 - 64个字符以内。
- 由大写或小写字母、数字、特殊字符中的任意三种组成。
- 特殊字符为`_+-&=!@#$%^*()`。

## 开启密码复杂度
>?开启密码复杂度功能后，新创建帐号设置密码或重置帐号密码时按照新密码复杂度策略执行密码设置。

### 在购买页创建实例时开启
1. 登录 [MySQL 购买页](https://buy.intl.cloud.tencent.com/cdb)。
2. 根据需要配置各项参数，在**密码复杂度**参数项后，选择**开启**。
![](https://qcloudimg.tencent-cloud.cn/raw/d8954b4267f8b9c75b3f33834c8a8ad5.png)
3. 选择开启后，完成以下设置。
<table>
<thead><tr><th>参数</th><th>说明</th></tr></thead>
<tbody><tr>
<td>小写和大写的最小字符数</td>
<td>设置范围为1 - 16个字符，默认值为1</td></tr>
<tr>
<td>数字字符的最小字符数</td>
<td>设置范围为1 - 16个字符，默认值为1</td></tr>
<tr>
<td>特殊字符的最小字符数</td>
<td>设置范围为1 - 16个字符，默认值为1</td></tr>
<tr>
<td>密码最小字符数</td>
<td>设置范围为8 - 64个字符，默认值为8，且最小值须大于以上三个参数的最小字符数之和</td></tr>
</tbody></table>

### 在控制台对存量实例开启
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。
2. 在实例管理页面，选择**数据库管理** > **帐号管理**页，单击**密码复杂度**（默认关闭）。
![](https://qcloudimg.tencent-cloud.cn/raw/ae8c348798736f38a4ea1069e29c7b5f.png)
3. 在密码复杂度弹窗下选择开启，完成以下参数设置，单击**确定**。
![](https://qcloudimg.tencent-cloud.cn/raw/f4407c8d310de235c596f541f087d747.png)
<table>
<thead><tr><th>参数</th><th>说明</th></tr></thead>
<tbody><tr>
<td>小写和大写的最小字符数</td>
<td>设置范围为1 - 16个字符，默认值为1</td></tr>
<tr>
<td>数字字符的最小字符数</td>
<td>设置范围为1 - 16个字符，默认值为1</td></tr>
<tr>
<td>特殊字符的最小字符数</td>
<td>设置范围为1 - 16个字符，默认值为1</td></tr>
<tr>
<td>密码最小字符数</td>
<td>设置范围为8 - 64个字符，默认值为8，且最小值须大于以上三个参数的最小字符数之和</td></tr>
</tbody></table>

## 关闭密码复杂度
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。
2. 在实例管理页面，选择**数据库管理** > **帐号管理**页，单击**密码复杂度**。
![](https://qcloudimg.tencent-cloud.cn/raw/ae613393746da572d25e4bc90e940895.png)
3. 在密码复杂度弹窗下选择**关闭**，单击**确定**。
![](https://qcloudimg.tencent-cloud.cn/raw/06c7f71ceaacb063768ac6c83ab78b76.png)

## 相关文档
- [创建账号](https://intl.cloud.tencent.com/document/product/236/31900)
- [重置密码](https://intl.cloud.tencent.com/document/product/236/31901)
