## 简介

**地域（Region）**是腾讯云托管机房的分布地区，对象存储（Cloud Object Storage，COS）的数据存放在这些地域的存储桶中。您可以通过 COS，将数据进行多地域存储。通常情况下，COS 建议您选择在与您业务最近的地域上创建存储桶，以满足低延迟、低成本以及合规性要求。

例如，当您的业务分布在华南地区，那么选择在广州地域创建存储桶可以进一步提高对象的上传、下载速度。

**默认域名**指 COS 的默认存储桶域名，用户在创建存储桶时，由系统根据存储桶名称和地域自动生成。不同地域的存储桶有不同的默认域名。您可以前往 [对象存储控制台](https://console.cloud.tencent.com/cos5)，在存储桶的**概览 > 域名信息**中查看。




### 中国大陆地域

<table>
   <tr>
	 <th colspan=3><center>地域</center></th>
      <th>地域简称</th>
      <th>默认域名（上传/下载/管理 ）</th>
   </tr>
   <tr>
      <td rowspan=10>中国大陆</td>
      <td rowspan=7 nowrap="nowrap">公有云地域</td>
      <td nowrap="nowrap">北京一区（已售罄）</td>
      <td>ap-beijing-1</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-beijing-1.myqcloud.com</td>
   </tr>
   <tr>
      <td>北京</td>
      <td>ap-beijing</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-beijing.myqcloud.com</td>
   </tr>
   <tr>
      <td>南京</td>
      <td>ap-nanjing</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-nanjing.myqcloud.com</td>
   </tr>
   <tr>
      <td>上海</td>
      <td>ap-shanghai</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-shanghai.myqcloud.com</td>
   </tr>
   <tr>
      <td>广州</td>
      <td>ap-guangzhou</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-guangzhou.myqcloud.com</td>
   </tr>
   <tr>
      <td>成都</td>
      <td>ap-chengdu</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-chengdu.myqcloud.com</td>
   </tr>
   <tr>
      <td>重庆</td>
      <td>ap-chongqing</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-chongqing.myqcloud.com</td>
   </tr>
</table>




### 中国香港及海外地域

<table>
   <tr>
	 <th colspan=3><center>地域</center></th>
      <th>地域简称</th>
      <th>默认域名（上传/下载/管理 ）</th>
   </tr>
   <tr>
      <td rowspan=7>亚太</td>
      <td rowspan=13 nowrap="nowrap">公有云地域</td>
      <td>中国香港</td>
      <td>ap-hongkong</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-hongkong.myqcloud.com</td>
   </tr>
   <tr>
      <td>新加坡</td>
      <td>ap-singapore</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-singapore.myqcloud.com</td>
   </tr>
   <tr>
      <td>孟买</td>
      <td>ap-mumbai</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-mumbai.myqcloud.com</td>
   </tr>
   <tr>
      <td  nowrap="nowrap">雅加达</td>
      <td>ap-jakarta</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-jakarta.myqcloud.com</td>
   </tr>
   <tr>
      <td>首尔</td>
      <td>ap-seoul</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-seoul.myqcloud.com</td>
   </tr>
   <tr>
      <td>曼谷</td>
      <td>ap-bangkok</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-bangkok.myqcloud.com</td>
   </tr>
   <tr>
      <td>东京</td>
      <td>ap-tokyo</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-tokyo.myqcloud.com</td>
   </tr>
   <tr>
      <td rowspan=3>北美</td>
      <td nowrap="nowrap">硅谷（美西）</td>
      <td>na-siliconvalley</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-siliconvalley.myqcloud.com</td>
   </tr>
   <tr>
      <td nowrap="nowrap">弗吉尼亚（美东）</td>
      <td>na-ashburn</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-ashburn.myqcloud.com</td>
   </tr>
   <tr>
      <td>多伦多</td>
      <td>na-toronto</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-toronto.myqcloud.com</td>
   </tr>
   <tr>
      <td rowspan=1>南美</td>
      <td>圣保罗</td>
      <td>sa-saopaulo</td>
      <td>&lt;BucketName-APPID&gt;.cos.sa-saopaulo.myqcloud.com</td>
   </tr>
   <tr>
      <td rowspan=2>欧洲</td>
      <td>法兰克福</td>
      <td>eu-frankfurt</td>
      <td>&lt;BucketName-APPID&gt;.cos.eu-frankfurt.myqcloud.com</td>
   </tr>
   <tr>
      <td>莫斯科</td>
      <td>eu-moscow</td>
      <td>&lt;BucketName-APPID&gt;.cos.eu-moscow.myqcloud.com</td>
   </tr>
</table>



### 全球加速域名

全球加速域名的格式为&lt;BucketName-APPID&gt;.cos.accelerate.myqcloud.com，有关全球加速域名的介绍和使用示例，请参见 [全球加速概述](https://intl.cloud.tencent.com/document/product/436/33409)。


### 示例

假设您通过主账号（APPID 为1250000000）登录 COS 控制台创建了一个存储桶，该存储桶的所属地域为**广州**地域，存储桶名称为 **examplebucket**。那么该存储桶默认域名如下：

```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```

>?
>
>- examplebucket-1250000000：表示该存储桶归属于 APPID 为1250000000的用户。APPID 是您在成功申请腾讯云账户后所得到的账号，由系统自动分配，具有固定性和唯一性，可在 [账号信息](https://console.cloud.tencent.com/developer) 中查看。
>- cos：指对象存储（Cloud Object Storage，COS）。
>- ap-guangzhou：指存储桶的地域简称。
>- myqcloud.com：腾讯云域名，固定字符。

创建存储桶完成后，将一个图片文件 picture.jpg 上传到该存储桶，则图片 picture.jpg 的访问地址如下：

```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/picture.jpg
```

>? 假如您将图片的访问权限设置为**公有读私有写**，将图片访问地址粘贴至浏览器打开，则可查看图片详情。
>



## 内网和外网访问

在同地域的云服务器（Cloud Virtual Machine，CVM）上，通过 COS 默认域名访问文件时，默认走内网链路，此时文件的上传和下载均产生内网流量，不会产生流量费用，但仍然有请求次数的收费。

腾讯云 COS 的访问域名使用了智能 DNS 解析，通过互联网在不同的运营商环境下，我们会检测并指向最优链路供您访问 COS。

如果您在腾讯云内部署了服务用于访问 COS，则同地域范围内访问将会自动被指向到内网地址。跨地域暂不支持内网访问，默认将会解析到外网地址。如果您有跨地域内网互通的需求，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系我们处理。

有关内网与外网访问的相关信息，详情请参见 [创建请求概述](https://intl.cloud.tencent.com/document/product/436/30613) 文档。

