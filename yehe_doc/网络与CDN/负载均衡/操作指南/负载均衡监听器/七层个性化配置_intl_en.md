CLB supports custom configurations, allowing you to set the configuration parameters for a single CLB instance, such as `client_max_body_size` and `ssl_protocols`, so as to meet your unique needs.
>?
>- Each region can have up to 200 entries of custom configurations.
>- Custom configurations are limited to 64K bytes.
>- Each instance can be bound to only one entry of custom configuration.
>- Custom configurations are valid only for layer-7 HTTP/HTTPS CLB (former Application CLB) listeners.

## CLB Custom Configuration Parameters
CLB custom configuration supports the following configuraitons:

| Configuration |   Default Value/Recommended Value  |    Parameter Range  | Description  |
| :-------- | :-------- | :------ |:------ |
|ssl_protocols |TLSv1 TLSv1.1 TLSv1.2 TLSv1.3 |TLSv1 TLSv1.1 TLSv1.2 TLSv1.3 | Version of TLS protocol used |
|  ssl_ciphers  | See further below. | See further below. | Encryption suite |
|  client_header_timeout  | 60s |  [30-120]s | Timeout period of obtaining a client request header; in case of timeout, a 408 error will be returned.|
|  client_header_buffer_size | 4k |[1-256]k | Size of default buffer where a client request header is stored. |
|  client_body_timeout | 60s |  [30-120]s | Timeout period of obtaining a client request body, which is not the time for obtaining the entire body but refers to the idle period without data transmission; in case of timeout, a 408 error will be returned. |
|  client_max_body_size | 60M |[1-10240]M| <ul><li>Default: 1 - 256.</li><li>Maximum size: 10,240 MB (10 GB); if `client_max_body_size` is more than 256 MB, the value of <a href="#buffer">proxy_request_buffering</a> must be `off`.</li></ul> |
|  keepalive_timeout | 75s | [0-900]s| `Client-server` persistent connection hold time; if it is set to 0, persistent connection is prohibited. If you want to set it to over 900, please submit an application(https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=163&source=0&data_title=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB&step=1). The maximum value you can set is 3600. |
|  add_header |Custom| - | Specific header field returned to the client in the format of `add_header xxx yyy`. |
|  more_set_headers |Custom| - | Specific header field returned to the client in the format of `more_set_headers "A:B"`. |
|  proxy_connect_timeout | 4s | [4-120]s |Timeout period of upstream backend connection.|
|  proxy_read_timeout |60s |[30-3600]s|Timeout period of reading upstream backend response.|
|  proxy_send_timeout |60s |[30-3600]s|Timeout period of sending a request to the upstream backend.|
|  server_tokens | on | on, off | <ul><li>`on`: displays version information;</li><li>`off`: hides version information.</li></ul>|
|  keepalive_requests | 100 | [1-10000] |Maximum number of requests that can be sent over the `client-server` persistent connection.|
|  proxy_buffer_size | 4k |[1-32]k| Size of server response header, which is the size of a single buffer set in `proxy_buffer` by default; to use `proxy_buffer_size`, `proxy_buffers` must be set at the same time.|
|  proxy_buffers | 8 4k |[3-8] [4-16]k|Buffer quantity and size.|
|  <span id="buffer">proxy_request_buffering</span> | on |on, off|<ul><li>`on`: caches the client request body; the CLB instance caches the request and forwards it to the backend CVM instance in multiple parts after the request is completely received.</li><li>`off`: does not cache the client request body; after receiving a request, the CLB instance directly forwards it to the backend CVM instance, which increases pressure on the backend CVM performance.</li></ul>|
|  proxy_set_header   |X-Real-Port $remote_port|<ul><li>X-Real-Port $remote_port</li><li>X-clb-stgw-vip $server_addr</li><li>Stgw-request-id $stgw_request_id</li><li>X-Forwarded-Port $vport</li><li>X-Method $request_method</li><li>X-Uri $uri</li></ul>|<ul><li>`X-Real-Port $remote_port`: client port.</li><li>`X-clb-stgw-vip $server_addr`: CLB VIP.</li><li>`Stgw-request-id $stgw_request_id`: request ID (used in CLB only).</li><li>`X-Forwarded-Port`: CLB listener port.</li><li>`X-Method`: client request method.</li><li>`X-Uri`: client request URI.</li></ul> |
|  send_timeout | 60s |[1-3600]s|Timeout period of data transfer from the server to the client, which is the time interval between two consecutive data transfer actions, not the entire request transfer period.|
|  ssl_verify_depth |  1 |[1, 10]|Verification depth of the client certificate chain.|
|proxy_redirect | http:// https:// | http:// https://  | If the upstream server returns a redirect or refresh request (code 301 or 302), `proxy_redirect` will reset `http` to `https` in the `Location` or `Refresh` field in the HTTP header for safe redirection.  |
| ssl_early_data  |  off |on, off| Enables or disables TLS 1.3 0-RTT. Only when the field value of `ssl_protocols` contains `TLSv1.3`, `ssl_early_data` can take effect. **You shall consider the risk of replay attacks before enabling `ssl_early_data`.**|
|http2_max_field_size|4k|[1-256]k|Restricts the maximum size of the request header compressed in HPACK.|
|error_page|-|error_page code [ = [ response]] uri|A predefined URL will be shown for the specific error code. The default response code defaults to 302. The URI must start with `/`.|
| proxy_ignore_client_abort | off | on, off | Connects or disconnects the CLB instance with the real server if the client disconnect with the CLB instance without waiting for a response.|


>?Requirements on the value of `proxy_buffer_size` and `proxy_buffers`: 2 * max (proxy_buffer_size, proxy_buffers.size) ≤ (proxy_buffers.num - 1)\* proxy_buffers.size; For example, if `proxy_buffer_size` is "24k", `proxy_buffers` is "8 8k"; then 2 * 24k = 48k, (8 - 1)\* 8k = 56k; and 48k ≤ 56k, so there will be no configuration error.
>
## ssl_ciphers Configuration Instructions
The ssl_ciphers encryption suite being configured must be in the same format as that used by OpenSSL. The algorithm list is one or more `<cipher strings>`; multiple algorithms should be separated with ":"; ALL represents all algorithms, "!" indicates not to enable an algorithm, and "+" indicates to move an algorithm to the last place.
The encryption algorithm for default forced disabling is: `!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE`.

**Default value:**
```plaintext
ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-CHACHA20-POLY1305:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128:AES256:AES:HIGH:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE:3DES;
```

**Parameter range:**
```plaintext
ECDH-ECDSA-AES128-SHA256:ECDH-RSA-AES256-SHA:ECDH-ECDSA-AES256-SHA:SRP-DSS-AES-256-CBC-SHA:SRP-AES-128-CBC-SHA:ECDH-RSA-AES128-SHA256:DH-RSA-AES128-SHA256:DH-RSA-CAMELLIA128-SHA:DH-DSS-AES256-GCM-SHA384:DH-RSA-AES256-SHA256:AES256-SHA256:SEED-SHA:CAMELLIA256-SHA:ECDH-RSA-AES256-SHA384:ECDH-ECDSA-AES128-GCM-SHA256:DH-RSA-AES128-SHA:DH-RSA-AES128-GCM-SHA256:DH-DSS-AES128-SHA:ECDH-RSA-AES128-SHA:DH-DSS-CAMELLIA256-SHA:SRP-AES-256-CBC-SHA:DH-DSS-AES128-SHA256:SRP-RSA-AES-256-CBC-SHA:ECDH-ECDSA-AES256-GCM-SHA384:ECDH-RSA-AES256-GCM-SHA384:DH-DSS-AES256-SHA256:ECDH-ECDSA-AES256-SHA384:AES128-SHA:DH-DSS-AES128-GCM-SHA256:AES128-SHA256:DH-RSA-SEED-SHA:ECDH-ECDSA-AES128-SHA:IDEA-CBC-SHA:AES128-GCM-SHA256:DH-RSA-CAMELLIA256-SHA:CAMELLIA128-SHA:DH-RSA-AES256-GCM-SHA384:SRP-RSA-AES-128-CBC-SHA:SRP-DSS-AES-128-CBC-SHA:ECDH-RSA-AES128-GCM-SHA256:DH-DSS-CAMELLIA128-SHA:DH-DSS-SEED-SHA:AES256-SHA:DH-RSA-AES256-SHA:kEDH+AESGCM:AES256-GCM-SHA384:DH-DSS-AES256-SHA:HIGH:AES128:AES256:AES:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!DHE
```

## CLB Custom Configuration Examples
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance/index?rid=8) and click **Custom Configuration** on the left sidebar.
2. Select a region at the top of the **Custom Configuration** page, and click **Create**.
3. On the **Create custom configuration** page, enter the configuration name and code configuration items, each item ending with a semicolon (;). After filling in all the information, click **Completed**.
![](https://main.qcloudimg.com/raw/7ef70a06f9509ba8759e5a923515a471.png) 
4. Return to the **Custom Configuration** page. Click **Bind to Instance** on the right.
5. On the pop-up **Bind to Instance** page, select a CLB instance to bind, and click **Submit**.
![](https://main.qcloudimg.com/raw/ad8fb7874b9ce1fe7bf5c9366c7e64e7.png)
6. On the **Custom Configuration** page, click the configured ID to enter its details page. You can check the bound instance on the **Bind Instance** tab.
7. (Optional) You can now view the corresponding custom configuration information on the instance list page.
>?If **Bind Custom Configurations** is not displayed on the instance list, click ![](https://main.qcloudimg.com/raw/8cc99da2a299fc570d3d9b314c9dcae6.svg) in the top-right corner. In the pop-up **Customize List Field** dialog, select **Bind Custom Configurations**, and click **OK**. You should see the column displayed.
>
![](https://main.qcloudimg.com/raw/d07bdbc134480fa89f732c93c3861243.png)
Default configuration sample code:
```plaintext
ssl_protocols   TLSv1 TLSv1.1 TLSv1.2;
client_header_timeout   60s;
client_header_buffer_size   4k;
client_body_timeout    60s;
client_max_body_size   60M;
keepalive_timeout    75s;
add_header     xxx yyy;
more_set_headers      "A:B";
proxy_connect_timeout    4s;
proxy_read_timeout    60s;
proxy_send_timeout    60s;
```

