## Overview
TencentDB for MySQL comes with the transparent data encryption (TDE) feature. Transparent encryption means that the data encryption and decryption are transparent to users. TDE supports real-time I/O encryption and decryption of data files. It encrypts data before it is written to disk, and decrypts data when it is read into memory from disk, which meets the compliance requirements of static data encryption.

## Limits
- The database version must be MySQL 5.7 or 8.0.
- Key Management Service (KMS) must be activated. To do so, you can follow the instructions provided during the TDE activation process.
- KMS key permissions must be granted. To do so, you can follow the instructions provided during the TDE activation process.
- Your account needs the `QcloudAccessForMySQLRole` permission. To do so, you can follow the instructions provided during the TDE activation process.
>?
>-The keys used for encryption are generated and managed by [KMS](https://intl.cloud.tencent.com/document/product/1030/32774). TencentDB for MySQL does not provide keys or certificates required for encryption.
>- TDE does not incur fees, but KMS may. For more information, see [KMS Billing Overview](https://intl.cloud.tencent.com/document/product/1030/31966).
- If your account has overdue payment, you cannot get keys from KMS, which may cause instance migration and upgrade tasks to fail. For more information, see [Notes on Arrears](https://intl.cloud.tencent.com/document/product/1030/31968).

## Notes
- Once the authorization is revoked, MySQL databases will be inaccessible upon restart.
- TDE can't be disabled once enabled.
- Once TDE is enabled, you need to decrypt data before you can restore it to a local database.
- TDE enhances the security of static data while compromising the read-write performance of encrypted databases. Therefore, use it based on your actual needs.
- If the source instance is associated with a read-only or disaster recovery instance, you only need to enable TDE for the source instance, which will then be automatically enabled for its associated instances.
- After TDE is enabled, if your account has overdue payment, you cannot get keys from KMS, which may cause migration, upgrade, and other tasks to fail.
- After TDE is enabled, more CPU resources will be consumed, and about 5% of the performance will be compromised.


## Directions
### Enabling TDE
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the **Data Encryption** tab, toggle on **Encryption Status**.
>!
>- An instance with TDE enabled cannot be restored from a physical backup to a self-created database on another server.
>- Once you enable TDE, you cannot disable it.
>
![](https://main.qcloudimg.com/raw/bc032cee3e68506b77c044622e8c029f.png)
3. In the pop-up dialog box, activate the KMS, grant the KMS key permissions, select a key, and click **Encrypt**.
   - If you select **Use key auto-generated by Tencent Cloud**, the key will be auto-generated by Tencent Cloud.
    ![](https://main.qcloudimg.com/raw/d54abe36c8e392c09b39045f0b7a5b95.png)
   - If you select **Use existing custom key**, you can select a key created by yourself.
>?If there are no custom keys, click **go to create** to create keys in the KMS console. For more information, see [Creating a Key](https://intl.cloud.tencent.com/document/product/1030/31971).
>
![](https://main.qcloudimg.com/raw/39d442d9620f36c1d57b55a409e6f9e2.png)


### Encrypting a table
Once you enable TDE, you can encrypt a table of a MySQL instance by running the example DDL statements on the table.
- To encrypt a table upon creation, run the following statement:
```
CREATE TABLE t1 (c1 INT) ENCRYPTION='Y';
```
- To encrypt an existing table, run the following statement:
```
ALTER TABLE t1 ENCRYPTION='Y';
```

### Decrypting a table
Once you enable TDE, you can decrypt a table of a MySQL instance by running the example DDL statement on the table.
To decrypt an encrypted table, run the following statement:
```
ALTER TABLE t1 ENCRYPTION='N';
```

