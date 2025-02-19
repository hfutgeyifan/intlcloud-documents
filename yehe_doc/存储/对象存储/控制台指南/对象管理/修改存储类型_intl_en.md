## Overview

You can modify the storage class of your object uploaded to COS through the console at any time to meet your business needs in different scenarios. COS offers a range of storage classes, including INTELLIGENT TIERING, STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE. For more information, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). The following section will guide you through how to modify the storage class of an object.

> ?
> - To modify the storage class of an object stored in **ARCHIVE** or **DEEP ARCHIVE**, you need to restore it first into STANDARD. For more information, see [Restoring Archived Objects](https://intl.cloud.tencent.com/document/product/436/30961).
> - COS does not allow modifying the storage class of an object larger than 5 GB.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left sidebar.
5. Find the target object and click **More Actions > Modify Storage Class** in the **Operation** column on the right.
![](https://main.qcloudimg.com/raw/da4233ef18fa8d9820c97450341092d3.png)
To batch modify the storage class of multiple objects, select multiple objects and click **More Actions** > **Modify Storage Class** at the top.

6. Select the target storage class and click **OK** in the pop-up window.

