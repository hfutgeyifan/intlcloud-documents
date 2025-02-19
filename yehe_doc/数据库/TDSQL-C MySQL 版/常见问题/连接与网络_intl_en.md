### How do I access TDSQL-C for MySQL?
You can connect to TDSQL-C for MySQL in the following ways:
- Private network connection: You can use a CVM instance to connect to the private network address of a TDSQL-C for MySQL instance. This method utilizes the high-speed private network of Tencent Cloud and features low delay. Note that both instances must be under the same account in the same VPC in the same region.
- Public network connection: You can connect to your TDSQL-C for MySQL cluster at its public network address. You need to manually enable the public network address, which you can view on the instance details page in the console and disable if no longer needed.
- DMC connection: You can access TDSQL-C for MySQL through DMC.

For detailed directions, see [Connecting to Cluster](https://intl.cloud.tencent.com/document/product/1098/40627).

### How do I enable the public network addresses of a TDSQL-C for MySQL instance?
TDSQL-C for MySQL public network addresses include public read-write address and public read-only address. You can enable/disable them on the **Cluster Details** page in the console as instructed in [Enabling/Disabling Public Network Address](https://intl.cloud.tencent.com/document/product/1098/44625).

### How do I use Lighthouse to access TDSQL-C for MySQL?
You can use a Lighthouse instance to directly connect to the private network address of a TDSQL-C for MySQL instance over the private network. This method utilizes the high-speed private network of Tencent Cloud and features low delay. Both instances must be under the same account in the same VPC in the same region.

### Can TDSQL-C for MySQL directly interconnect with servers of other cloud vendors over the private network?
No.
You can enable public network access for a TDSQL-C for MySQL instance on the **Cluster Details** page, and then connect to the instance by using a server from another cloud vendor.

### Can I change the public network address of a TDSQL-C for MySQL instance?
No.

### How do I change the network?
TDSQL-C for MySQL allows you to change the VPC in the **Basic Info** section on the **Cluster Details** page in the [console](https://console.cloud.tencent.com/cynosdb).

### How many read-only instances can a TDSQL-C for MySQL cluster contain at most?
A cluster can contain only one read-write instance and up to 15 read-only instances.

### How do I lower the load of a read-write instance?
TDSQL-C for MySQL allows you to create one or more read-only instances in a cluster, which are suitable for read/write separation and one-write-multiple-read application scenarios and capable of lowering the load of the read-write instance. For more information, see [Creating Read-Only Instance](https://intl.cloud.tencent.com/document/product/1098/40631).

### Does TDSQL-C for MySQL support the JDBC protocol?
TDSQL-C for MySQL is fully compatible with MySQL, so it supports the JDBC protocol.
