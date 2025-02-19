## 使用须知

### 内容介绍

本文档向开发者介绍如何拉取网络视频（以 URL 的形式提供）到云点播（VOD）。

### 费用

本文提供的代码是免费开源的，但在使用的过程中可能会产生以下费用：

- 购买腾讯云云服务器（CVM）用于执行 API 请求脚本，详见 [CVM 计费](https://intl.cloud.tencent.com/document/product/213/2180)。

- 消耗 VOD 存储用于存储拉取上传的视频，详见 [存储计费](https://intl.cloud.tencent.com/document/product/266/14666#.E5.AA.92.E8.B5.84.E5.AD.98.E5.82.A8.3Cspan-id.3D.22media_storage.22.3E.3C.2Fspan.3E)。


### 限制

云点播提供的 URL 拉取功能具有如下限制：

- URL 需要直接指向视频文件，不可以是视频网站页面链接。
- 如果 URL 带有时间戳防盗链，请确保防盗链的限制（有效期、访问次数等）足够宽松，否则可能失败。
- 不支持启用了 Referer 防盗链的 URL。
- 不支持 DASH（MPD 文件类型）。
- 如果拉取的对象是 HLS（M3U8 文件类型），那么 Media Segment（一般是 TS 文件类型）的 URI 要求是相对路径，且不能带参数。

## 在控制台拉取上传
<span id="p11"></span>
### 步骤1：开通云点播

请参考 [快速入门 - 步骤1](https://intl.cloud.tencent.com/document/product/266/8757) 开通云点播服务。
<span id="p12"></span>
### 步骤2：创建拉取任务

访问云点播控制台的 [上传页面](https://console.cloud.tencent.com/vod/media/upload)，上传方式选择【视频拉取】，然后单击【添加一行】，填写待拉取视频的 URL（本文以 [测试视频 URL](http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4) 为例，其余项为选填，开发者可以根据需要进行填写），最后单击左下角的【拉取视频】：

![](https://qcloudimg.tencent-cloud.cn/raw/d22654ee0f5d490a09df93d2c8cce778.png)
>?拉取视频所花费的时间和视频文件的大小成正比。建议开发者选择较小的视频（如几十MB以内）进行测试，避免长时间等待。
<span id="p13"></span>
### 步骤3：查看拉取结果

等待一两分钟后（根据视频文件的大小有所差别），在 [媒资管理页面](https://console.cloud.tencent.com/vod/media) 可以看到已经拉取完成的视频：

![](https://qcloudimg.tencent-cloud.cn/raw/8d25e0d8e54b2a59b5aa190c3ced62c8.png)

>?如果拉取过程中浏览器一直停留在媒资管理页面，那么需要刷新页面才能看到拉取完成的视频。

## 调用云 API 拉取上传
<span id="p21"></span>
### 步骤1：准备腾讯云 CVM

云 API 请求脚本需要运行在一台腾讯云 CVM 上，要求如下：

- 地域：任意。
- 机型：官网最低配置（1核1GB）即可。
- 公网：需要拥有公网 IP，带宽1Mbps或以上。
- 操作系统：官网公共镜像`Ubuntu Server 16.04.1 LTS 64位`或`Ubuntu Server 18.04.1 LTS 64位`。

购买 CVM 的方法请参见 [操作指南 - 创建实例](https://intl.cloud.tencent.com/document/product/213/4855)。重装系统的方法请参见 [操作指南 - 重装系统](https://intl.cloud.tencent.com/document/product/213/4933)。

>!如果您没有符合上述条件的腾讯云 CVM，也可以在其它带外网的 Linux（如 CentOS、Debian 等）或 Mac 机器上执行脚本，但需根据操作系统的区别修改脚本中的个别命令，具体修改方式请开发者自行搜索。
<span id="p22"></span>
### 步骤2：获取 API 密钥

请求云 API 需要使用到开发者的 API 密钥（即 SecretId 和 SecretKey）。如果还未创建过密钥，请参见 [创建密钥文档](https://intl.cloud.tencent.com/document/product/598/34228) 生成新的 API 密钥；如果已创建过密钥，请参见 [查看密钥文档](https://intl.cloud.tencent.com/document/product/598/34228) 获取 API 密钥。
<span id="p23"></span>
### 步骤3：开通云点播

请参考 [快速入门 - 步骤1](https://intl.cloud.tencent.com/document/product/266/8757) 开通云点播服务。
<span id="p24"></span>
### 步骤4：发起拉取任务

登录 [步骤1](#p21) 中准备好的 CVM（登录方法详见 [操作指南 - 登录 Linux](https://intl.cloud.tencent.com/document/product/213/5436)），在远程终端输入以下命令并运行：

```
ubuntu@VM-69-2-ubuntu:~$ export SECRET_ID=AKxxxxxxxxxxxxxxxxxxxxxxx; export SECRET_KEY=xxxxxxxxxxxxxxxxxxxxx;git clone https://github.com/tencentyun/vod-server-demo.git ~/vod-server-demo; bash ~/vod-server-demo/installer/pull_upload_api.sh
```

>?请将命令中的 SECRET_ID 和 SECRET_KEY 赋值为 [步骤2](#p22) 中获取到的内容。

该命令将从 Github 下载 Demo 源码并自动执行安装脚本。安装过程需几分钟（具体取决于 CVM 网络状况），期间远程终端会打印如下示例的信息：

```
[2020-07-15 17:40:13]开始安装 pip3。
[2020-07-15 17:40:39]pip3 安装成功。
[2020-07-15 17:40:39]开始安装云 API Python SDK 。
[2020-07-15 17:40:42]云 API Python SDK 安装完成。
[2020-07-15 17:40:42]开始配置 API 参数。
[2020-07-15 17:40:42]API 参数配置完成。
```

执行`pull_upload.py`脚本发起转码：

```
ubuntu@VM-69-2-ubuntu:~$ cd ~/vod-server-demo/pull_upload_api/; python3 pull_upload.py http://1400329073.vod2.myqcloud.com/ff439affvodcq1400329073/e968a7e55285890804162014755/LKk92603oW0A.mp4 API-PullUpload
```

>?请将命令中的 URL 替换为实际需要拉取的视频地址。

该命令将对指定的 URL 发起 [PullUpload](https://intl.cloud.tencent.com/document/product/266/34118) 请求，并打印类似如下的应答内容：

```
{"TaskId": "1400329073-PullUpload-4ea60158fc6f8e611bbfa750eb1fd0a9t0", "RequestId": "4e821b4a-9a29-409f-99cb-b703fa184e50"}
```
<span id="p25"></span>
### 步骤5：查看拉取结果

等待一两分钟后（具体根据视频文件的大小有所差别），在 [媒资管理页面](https://console.cloud.tencent.com/vod/media) 可以看到已经拉取完成的视频：

![](https://main.qcloudimg.com/raw/b5d62be7e0f70654483513a6885ff65b.png)
> ?如果拉取过程中浏览器一直停留在媒资管理页面，那么需要刷新页面才能看到拉取完成的视频。
