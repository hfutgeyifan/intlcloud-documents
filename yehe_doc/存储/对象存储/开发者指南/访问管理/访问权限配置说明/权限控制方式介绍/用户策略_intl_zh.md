腾讯云主账户可以在 [访问管理（Cloud Access Management，CAM）](https://console.cloud.tencent.com/cam/overview) 控制台创建 CAM 用户，并关联策略，授予 CAM 用户使用腾讯云资源的权限。

## 概述

用户可以在 [CAM](https://intl.cloud.tencent.com/document/product/598/10583) 中，对于主账号名下的不同类型用户，授予不同的权限。这些权限通过访问策略语言描述，并以用户为出发点进行授权，因此被称为**用户策略**。

#### 用户策略与存储桶策略的区别

用户策略与存储桶策略的最大差别是：用户策略只描述效力（Effect）、操作（Action）、资源（Resource）和条件（Condition，可选），不描述身份（Principal）。因此，用户策略的使用方式为：
- 用户策略需要撰写完成后，再对子用户、用户组或角色执行关联操作。
- 用户策略**不支持将操作和资源权限授予匿名用户**。

#### 预设策略和自定义策略

用户策略包括两类，[预设策略和自定义策略](https://intl.cloud.tencent.com/document/product/598/10601)，您可以使用 [预设策略进行关联授权](https://intl.cloud.tencent.com/document/product/598/10602)，也可以 [自行撰写用户策略](https://intl.cloud.tencent.com/document/product/598/35596) 再进行关联授权，详见访问管理的 [授权指南](https://intl.cloud.tencent.com/document/product/598/32668)。

## 适用场景
当您关心用户能做什么，推荐用户策略时，可通过查找 CAM 用户，并检查其所属用户组的权限来了解用户能做什么。推荐场景有：
- 要配置对象存储（Cloud Object Storage，COS）服务级权限时，例如创建桶（PutBucket）、列举桶（GetService）。
- 需要使用主账号下所有 COS 桶和对象。
- 要对主账号下的大量 CAM 用户授予相同权限。

## 用户策略语法

### 策略语法

和存储桶策略一样，用户策略使用 JSON 语言描述，遵循 [访问策略语言](https://intl.cloud.tencent.com/document/product/436/18023) 的统一规范（委托人、效力、操作、资源、条件等）。但由于用户策略是直接关联到用户/用户组上的，因此用户策略不需要填写委托人（Principal）。

下表是用户策略和存储桶策略的区别对比：

| 元素|用户策略 |存储桶策略 |
|---|---|---|
|委托人 |**不填**|必填|
|效力 |必填 |必填 |
|操作 |必填 |必填 |
|资源 |必填 |**该存储桶内资源**|
|条件 |选填 |选填 |

### 策略示例

以下是一个典型的用户策略示例，策略含义为：授权位于广州的存储桶examplebucket-1250000000所有 COS 操作的策略。您需要将策略保存后再关联到 [CAM](https://intl.cloud.tencent.com/document/product/598/10583) 子用户、用户组或角色方可生效：

```
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["cos:*"],
      "Resource": [
          "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*",
          "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/"
      ]
    }
  ],
  "Version": "2.0"
}
```

## 通过用户策略授权子账号访问 COS

### 前提条件

已创建 CAM 子账号，创建方法可参考 [创建子账号](https://intl.cloud.tencent.com/document/product/436/11714)。

<span id="自定义策略"></span>
### 配置步骤

CAM 提供了 [预设策略和自定义策略](https://intl.cloud.tencent.com/document/product/598/10601)。预设策略为 CAM 提供的系统预设策略，COS 相关策略见 [预设策略](https://intl.cloud.tencent.com/document/product/436/45236?lang=en&pg=#preset-policy)；自定义策略支持用户自定义资源、操作等元素，更加灵活。下面说明如何新建一个自定义策略，为子账户授权：

1. 登录 [CAM 控制台](https://console.cloud.tencent.com/cam)。
2. 选择**策略 > 新建自定义策略 > 按策略语法创建**，进入策略创建页面。
3. 您可按照实际需求选择**空白模板** 自定义授权策略，或选择与 COS 相关联的**系统模板**。这里以选择**空白模板**为例。

4. 选择**空白模板**，输入您的策略语法。

需要包括以下基本元素：
 - **resource：授权资源**。
     - 所有资源（`"*"`）
     - 指定存储桶(`"qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"`)
     - 存储桶内指定目录或对象(`"qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/test/*"`)
 - **action：授权操作**。
 - **effect：效力**。选择`"allow"`(允许)或`"deny"`（拒绝）。
 - **condition：生效条件**。可选项。

 COS 提供了用户策略示例，您也可以参考以下文档，直接将策略内容复制粘贴到**策略内容**编辑框内，确认输入无误后单击**完成**即可。
 - [授权子账号访问 COS](https://intl.cloud.tencent.com/document/product/436/11714)
 - [COS API 授权策略使用指引](https://intl.cloud.tencent.com/document/product/436/30580)
5. 创建完成后，您可在 [CAM 控制台](https://console.cloud.tencent.com/cam) 的**策略 > 自定义策略**中查看已创建的自定义策略，并将策略关联到子账号。

6. 勾选子账号并单击**确定**授权后，即可使用子账号访问所限定的 COS 资源。


<span id="预设策略"></span>
## 预设策略
CAM 提供了一些预设策略，您可以在 [CAM 控制台](https://console.cloud.tencent.com/cam) 的**策略 > 预设策略**中查看，搜索“COS”筛选。


单击策略名，进入**策略语法 > JSON** 查看具体的策略内容。预设策略的资源（`resource`）被设置为 COS 所有资源(`"*"`)，且不支持修改。若您需要对部分 COS 存储桶、对象授权，可以复制 JSON 的预设策略，创建 [自定义策略](https://intl.cloud.tencent.com/document/product/436/45236?lang=en&pg=#directions)。



表1和表2列出了 CAM 提供的 COS 相关的预设策略及说明。

**表1：COS 预设策略**

<table>
<tr>
	<th>预设策略</th>
	<th>说明</th>
	<th>JSON策略</th>
</tr>
<tr>
	<td>QcloudCOS<br>Bucket<br>ConfigRead</td>
	<td>拥有该权限的用户可以读取 COS 存储桶配置</td>
	<td>
	<pre>
	<code>
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:GetBucket*",
                "cos:HeadBucket"
            ],
            "resource": "*"
        }
    ]
}
	</code>
	</pre>
	</td>
</tr>
<tr>
	<td>QcloudCOS<br>Bucket<br>ConfigWrite</td>
	<td>拥有该权限的用户可以修改 COS 存储桶配置</td>
	<td>
	<pre>
	<code>
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:PutBucket*"
            ],
            "resource": "*"
        }
    ]
}
	</code>
	</pre>
	</td>
</tr>
<tr>
	<td>QcloudCOS<br>Data<br>FullControl</td>
	<td>包含 COS 存储桶内数据读、写、删除、列出的访问权限</td>
	<td>
	<pre>
	<code>
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:GetService",
                "cos:GetBucket",
                "cos:ListMultipartUploads",
                "cos:GetObject*",
                "cos:HeadObject",
                "cos:GetBucketObjectVersions",
                "cos:OptionsObject",
                "cos:ListParts",
                "cos:DeleteObject",
                "cos:PostObject",
                "cos:PostObjectRestore",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload",
                "cos:DeleteMultipleObjects",
                "cos:AppendObject"
            ],
            "resource": "*"
        }
    ]
}
	</code>
	</pre>
	</td>
</tr>

</table>

**表2：COS 操作与预设策略的关系**

|说明 |操作 |QcloudCOS<br>Bucket<br>ConfigRead |QcloudCOS<br>Bucket<br>ConfigWrite |QcloudCOS<br>Data<br>FullControl |QcloudCOS<br>Data<br>ReadOnly |QcloudCOS<br>Data<br>WriteOnly |QcloudCOS<br>Full<br>Access |QcloudCOS<br>GetService<br>Access |QcloudCOS<br>ListOnly |QcloudCOS<br>Read<br>OnlyAccess |
|---|---|---|---|---|---|---|---|---|---|---|
|列举桶 |GetService |❌ |❌ |✅ |❌ |❌ |✅ |✅ |✅ |✅ |
|创建桶 |PutBucket |❌ |✅ |❌ |❌ |❌ |✅ |❌ |❌ |❌ |
|删除桶 |DeleteBucket |❌ |❌ |❌ |❌ |❌ |✅ |❌ |❌ |❌ |
|获取桶基本信息 |HeadBucket |✅ |❌ |❌ |❌ |❌ |✅ |❌ |✅ |✅ |
|获取桶的配置项 |GetBucket* |✅ |❌ |❌ |❌ |❌ |✅ |❌ |❌ |✅ |
|修改桶的配置项 |GetBucket* |❌ |✅ |❌ |❌ |❌ |✅ |❌ |❌ |❌ |
|获取桶的访问权限 |GetBucketAcl |✅ |❌ |❌ |❌ |❌ |✅ |❌ |❌ |✅ |
|修改桶的访问权限 |PutBucketAcl |❌ |✅ |❌ |❌ |❌ |✅ |❌ |❌ |❌ |
|列举桶内对象 |GetBucket |✅ |❌ |✅ |❌ |❌ |✅ |❌ |✅ |✅ |
|列举桶内对象的所有版本 |GetBucketObjectVersions |✅ |❌ |✅ |❌ |❌ |✅ |❌ |✅ |✅ |
|上传对象 |PutObject |❌ |❌ |✅ |❌ |✅ |✅ |❌ |❌ |❌ |
|分块上传 |ListParts<br>InitiateMultipartUpload<br>UploadPart<br>UploadPartCopy<br>CompleteMultipartUpload<br>AbortMultipartUpload<br>ListMultipartUploads |❌ |❌ |✅ |❌ |✅ |✅ |❌ |❌ |❌ |
|追加对象 |AppendObject |❌ |❌ |✅ |❌ |❌ |✅ |❌ |❌ |❌ |
|下载对象 |GetObject |❌ |❌ |✅ |✅ |❌ |✅ |❌ |❌ |❌ |
|查看对象元数据 |HeadObject |❌ |❌ |✅ |✅ |❌ |✅ |❌ |❌ |✅ |
|跨域（CORS）预检 |OptionsObject |❌ |❌ |✅ |✅ |❌ |✅ |❌ |❌ |✅ |


## 更多用户策略示例

- [授权子账号访问 COS](https://intl.cloud.tencent.com/document/product/436/11714)
- [COS API 授权策略使用指引](https://intl.cloud.tencent.com/document/product/436/30580)

