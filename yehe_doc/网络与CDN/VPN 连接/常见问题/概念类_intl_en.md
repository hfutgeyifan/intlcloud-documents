### What is a VPN connection?
A VPN connection is used to connect a customer IDC with a VPC through an encrypted tunnel over the public network. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1037/32679).

### What is a VPN tunnel?
After VPN gateway and customer gateway are created, you can establish a VPN tunnel between the VPC and an external IDC for encrypted communication. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1037/32679).

### What is a VPN gateway?
A VPN gateway is an egress gateway for VPC to establish a VPN connection. It is used with a customer gateway (IPsec VPN gateway on the IDC side) to establish an encrypted communication between a Tencent Cloud VPC and an external IDC. Tencent Cloud VPN gateway uses software virtualization and a dual-server hot backup architecture. When one server fails, automatic switchover helps ensure the normal operation of your businesses.
- A VPN gateway supports eight bandwidth caps: 5 Mbps, 10 Mbps, 20 Mbps, 50 Mbps, 100 Mbps, 200 Mbps, 500 Mbps, and 1,000 Mbps. You can adjust the VPN gateway bandwidth cap, and the adjustment will take effect immediately in a pay-as-you-go VPN gateway.
- You can bind an Anti-DDoS instance to a VPN gateway to defend against DDoS and CC attacks with high-bandwidth protection.


[](id:1)

### What is an IPsec VPN?
 [IPsec VPN](https://intl.cloud.tencent.com/document/product/1037/32680) is used to connect customer IDC with a VPC through an encrypted tunnel over a public network. Tencent Cloud IPsec VPN connection consists of the following components:
- **VPN gateway**: an IPsec VPN gateway in a VPC. It is used with a customer gateway (IPsec VPN gateway on the IDC side) to establish an encrypted communication between the VPC and your IDC.
- **Customer gateway**: an IPsec VPN gateway on the IDC side that is mapped to the VPC. It is used with a VPN gateway. Each VPN gateway can create encrypted VPN tunnels with multiple customer gateways.
- **VPN tunnel**: an encrypted IPsec VPN tunnel over the public network. After the VPN gateway and customer gateway are created, you can establish a VPN tunnel between the VPC and an external IDC for encrypted communication.

### What are the limitations on using a VPN?
 To use a VPN, take notice of the limitations on IP addresses of the VPN connection and the customer gateway. For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/1037/32682).

### How many VPN gateways and VPN tunnels can I create?
The creation limit varies depending on the resources. For more information, see [Quota Limit](https://intl.cloud.tencent.com/document/product/215/38959). To increase the limit, please [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=168&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%20VPC).


[](id:2)

### Can a VPC connect to multiple IDCs through VPN connections?
Yes. You can create VPN gateways in a VPC and create multiple VPN tunnels for each VPN gateway. Each VPN tunnel connects the VPC to one local IDC.

### Can two VPCs communicate with each other through a VPN connection?
Yes. You need to separately purchase VPN gateways and configure VPN tunnels and customer gateways in the two VPCs, but the configuration is complex. So we recommend using [Cloud Connect Network (CCN)](https://intl.cloud.tencent.com/product/ccn) to connect two VPCs over the Tencent Cloud private network and help ensuring the communication quality.

### How do I ensure the network quality between a VPC and a VPN-connected IDC?
- Because a VPC connects to an IDC through a VPN connection on the public network, latency, packet loss, or jitter on the public network may affect the VPN connection. If you require more stable communication, we recommend that you use [Direct Connect](https://intl.cloud.tencent.com/document/product/216).
- Tencent Cloud provides 24-hour monitoring on your VPN gateways and reports alarms for exceptions. OPS personnel are available for emergencies. You can also monitor the traffic of your VPN gateways and tunnels on the console in real time. In case of any exceptions, [contact us](https://intl.cloud.tencent.com/contact-sales) promptly.

[](id:3)

### What are differences between Direct Connect and IPSec VPN connections?
- An IPsec VPN connection establishes an encrypted network connection between your IDC and VPCs based on the public network and IPsec protocol. You can purchase a VPN gateway and make it effective in just a few minutes. However, a VPN connection may be interrupted due to public network jitters or congestion. When your business does not require a high-quality network connection, the VPN connection is a cost-effective choice for rapid deployment.
- Direct Connect provides a network connection solution dedicated to your business. The configuration may take a longer time, but it can provide a highly reliable network connection. When your businesses have a higher requirement for the network quality and security, this option fits in.

The table below lists their specific differences.
<table>
<thead>
<tr>
<th width="16%">Advantage</th>
<th width="40%">Direct Connect</th>
<th width="44%">IPsec VPN Connection</th>
</tr>
</thead>
<tbody><tr>
<td>Stable network latency</td>
<td>Network latency is stable and guaranteed. A Direct Connect instance accesses the network through dedicated links, and supports fixed routes, removing the pain of unstable latency caused by network congestion or failure bypass.</td>
<td>Network latency is unstable. An IPsec VPN connection accesses the network over the Internet, which may be exposed to bypass due to network congestion.</td>
</tr>
<tr>
<td>Highly reliable disaster recovery access</td>
<td>Access devices and network forwarding devices are deployed in distributed clusters to ensure high reliability of all links. It also supports dual-line access with protection to provide more than 99.95% of uptime.</td>
<td>Features a dual-server hot backup architecture with high availability at the gateway layer. However, it cannot provide the same network availability as dedicated lines due to the unreliable Internet links.</td>
</tr>
<tr>
<td>High bandwidth</td>
<td>It provides a bandwidth of up to 10 Gbps for each link. You can have multiple 10 Gbps links for network load balancing, so it can theoretically support unlimited bandwidth.</td>
<td>A single IPsec VPN gateway supports a bandwidth of up to 1 Gbps and a VPC can have multiple VPN gateways, which can meet the need for a VPN connection larger than 1 Gbps.</td>
</tr>
<tr>
<td>High security</td>
<td>Dedicated network links offer strong security without data leakage risks, satisfying the demanding network connection requirements of the finance and government sectors.</td>
<td>Network transmission is encrypted using IKE pre-shared key, which can satisfy the security requirements for most network transmission.</td>
</tr>
<tr>
<td>Network address translation</td>
<td>It supports configuring the network address translation service on gateways, as well as IP mapping on the two sides of Direct Connect and IP port mapping on the VPC side, to avoid address conflict in case of interconnection among multiple networks.</td>
<td>Not supported.</td>
</tr>
</tbody></table>


### Can I access the Internet through a VPN connection?
No. VPN gateways only provide access to VPCs but not to the Internet.


### Can I use VPN Connections without a public IP?  
If you use an IPsec VPN connection, you must have a public IP.
If you don't have a public IP, you can try using an SSL VPN connection to connect your LAN and the cloud environment. To check whether an SSL VPN connection can meet your requirements, see [Directions](https://intl.cloud.tencent.com/document/product/1037/43900).
>?
>- Using an IPSec VPN connection requires the customer gateway to have a fixed IP address.
>- An SSL VPN gateway doesn't require that the customer gateway have a fixed public IP address. It is an egress gateway through which the VPC establishes an SSL VPN connection and is used together with the SSL VPN client (mobile client). For more information, see [Directions](https://intl.cloud.tencent.com/document/product/1037/43900).
