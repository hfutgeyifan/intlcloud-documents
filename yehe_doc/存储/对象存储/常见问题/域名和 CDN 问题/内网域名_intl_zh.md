### COS 是否有内网域名？

对象存储（Cloud Object Storage，COS）的默认源站域名格式为：&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com，默认已支持公网访问和同地域的内网访问。您在内网环境下通过该域名访问 COS 时，COS 会智能解析到内网 IP 上，此时产生的流量均为内网流量，不需收取流量费用。
例如，examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com，更多域名相关介绍，请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224)。



