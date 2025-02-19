### 如何设置访问对象时直接显示，而不需要下载?

绑定用户自有域名（如需购买域名，可通过腾讯云 [注册域名](https://www.tencentcloud.com/document/product/242)）并开启静态网站功能即可。详情参考 [设置静态网站](https://intl.cloud.tencent.com/document/product/436/14984)。

### 在 COS 控制台设置自定义域名失败，如何处理？

1. 确认域名已备案。
2. 确认域名的 DNS 解析正确（在关闭 CDN 加速情况下，需要预先在 DNS 解析控制台将域名 CNAME 到存储桶的 [默认域名](https://intl.cloud.tencent.com/document/product/436/18424)）。

### 开启了静态网站功能，但是仍无法显示图片？

1. 实现访问 COS 时直接显示对象（图片），需要开启静态网站功能，不能通过设置对象头部的 Content-Disposition:inline 来实现。 
2. 检查是否有浏览器、CDN 缓存。可以通过 curl、wget 命令来避免浏览器缓存，CDN 地址可以在 [CDN 控制台](https://console.cloud.tencent.com/cdn) 进行清缓存操作。

### 用户绑定自有域名时，开启 CDN 加速和关闭 CDN 加速的区别？

- **开启 CDN 加速：**域名由 CDN 管理，在 COS 控制台开启 CDN 加速与在 [CDN 控制台](https://console.cloud.tencent.com/cdn) 添加域名（源站选择 COS），是一样的效果。用户在解析域名时，需要使用 CDN 分配的 CNAME 记录。配置时，先添加域名，再解析域名即可，解析域名可参见快速添加域名解析。
- **关闭 CDN 加速：**域名由 COS 管理，域名配置会下发到对应存储桶所属地域的所有下载接入机器上。用户在解析域名时，需要使用存储桶的默认域名作为 CNAME 记录。配置时，需要先解析域名，再添加自定义域名。

### 为什么设置了对象的自定义头部 Content-Disposition 后仍然不生效？

自定义头部中的其他自定义头部，设置后即可生效，而 Content-Disposition 头部比较特殊，只有在开启静态网站功能，且使用自定义域名访问时，该头部才生效。


### 开启了静态网站功能，但是仍无法显示图片？

请检查是否有浏览器、CDN 缓存。可以通过 curl、wget 命令来避免浏览器缓存。若使用 CDN 域名访问，可以在 [CDN 控制台](https://console.cloud.tencent.com/cdn) 进行缓存刷新操作。

### 使用 CDN 域名无法访问配置好的静态网站怎么办？

请根据以下步骤进行排查确认 CDN 加速域名配置。

1. 源站类型请注意源站选择静态网站源站。
2. 回源鉴权、CDN 服务授权需根据存储桶的权限进行对应设置：
 - 当存储桶权限为私有读时，需要对 CDN 服务授权并开启回源鉴权。
 - 当存储桶权限为公有读时，无需对 CDN 服务授权并开启回源鉴权。
3. CDN 鉴权需要根据存储桶的权限进行对应设置：
 1. 当存储桶权限为私有读时：
 <table>
	<tr><th>CDN 鉴权配置</th><th>CDN 加速域名访问</th><th>COS 域名访问</th><th>常见场景</th></tr>
	<tr><td>关闭（默认）</td><td>不可访问</td><td>需使用 COS 鉴权</td><td>可直接访问 CDN 域名，保护源站数据</td></tr>
	<tr><td>开启</td><td>需使用 URL 鉴权</td><td>需使用 COS 鉴权</td><td>全链路保护访问，支持 CDN 鉴权防盗链</td></tr>
</table>
 2. 当存储桶权限为公有读时：
<table>
	<tr><th>CDN 鉴权配置</th><th>CDN 加速域名访问</th><th>COS 域名访问</th><th>常见场景</th></tr>
	<tr><td>关闭（默认）</td><td>可访问</td><td>可访问</td><td>全站许可公共访问，通过 CDN 或源站均可访问</td></tr>
	<tr><td>开启</td><td>需使用 URL 鉴权</td><td>可访问</td><td>对 CDN 访问开启防盗链，但不保护源站访问，不推荐</td></tr>
</table>
4. 确认以上配置无误后，请确认您访问 CDN 加速域名使用的协议和静态网站的 **强制 HTTPS** 配置：
 - 当您访问 CDN 加速域名使用的是 HTTP 协议，**请勿开启强制 HTTPS** 选项。
 - 当您访问 CDN 加速域名使用的是 HTTPS 协议，建议对 CDN 加速域名配置 **开启回源跟随301/302**。详情请参见 [回源跟随301/302配置](https://intl.cloud.tencent.com/document/product/228/7183)。
5. 如果按照以上步骤排查后，仍无法解决问题，您可以 [联系我们](https://intl.cloud.tencent.com/contact-sales)，进行进一步的问题排查。

### 静态网站功能配合前端 Vue 框架一起使用，当路由设置为 History 模式，刷新页面遇到404问题怎么办？

请在存储桶的静态网站配置页面，将错误文档配置为 Web 应用的入口（一般为 index.html），并将错误文档响应码设置为200。关于静态网站的配置指引，请参见 [设置静态网站](https://intl.cloud.tencent.com/document/product/436/14984)。
![](https://qcloudimg.tencent-cloud.cn/raw/079dbe1519636756de506789cb9a990c.png)

>! 按上述方法配置完成之后，如果还需要实现正常响应404的功能，用户可自行在 Vue 的前端路由配置最底层设置（一般为通配符匹配到自定义的404组件）。
>


