123
? 12367

## Overview
Tencent Kubernetes Engine (TKE) allows you to use Cloud Object Storage (COS) by creating PersistentVolumes (PVs) or PersistentVolumeClaims (PVCs) and mounting volumes to workloads. This document describes how to mount COS to a workload.

## Preparations
444
### Installing the COS add-on
>? If your cluster has been installed with the COS-CSI add-on, skip this step.

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Click **Cluster** in the left sidebar to go to the **Cluster Management** page.
3. Select the ID of the cluster for which you want to create an add-on and click **Add-On Management** in the left sidebar on the cluster details page.
4. On the **Add-On Management** page, click **Create** to go to the **Create Add-On** page.
5. Select **COS** and click **Done**.
<span id="CreatAccessKey"></span>
### Creating an access key
>!
>- To avoid cloud asset loss due to the leakage of the root account key, we recommend that you stop using your root account to log in to the console, or use the root account key to access cloud APIs and use a sub-account or collaborator with the relevant management permissions to manage related resources. For more information, see [Security Setting Policy](https://intl.cloud.tencent.com/document/product/598/10592).
>- This document describes how to create or view an access key as a sub-user with relevant access management permissions. For more information on how to create a sub-user and grant access management permissions to the sub-user, see [Creating a Custom Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).

1. Use a sub-account to log in to the [Cloud Access Management console](https://console.cloud.tencent.com/cam/overview) and choose **Access Key** > **API Keys** in the left sidebar to go to the **API Key Management** page.
2. Click **Create Key** and wait until the key is created.
>?
>- One sub-user can have at most two API keys.
>- An API key is an important credential for creating Tencent Cloud API requests. To secure your assets and services, store your keys properly and update them regularly. Delete old keys when new ones are created.

<span id="CreatBucket"></span>
### Creating a bucket
>! According to relevant laws and policies, you need to complete [Identity Verification](https://console.cloud.tencent.com/developer/auth) before using Tencent Cloud COS.

1. Log in to the [Cloud Object Storage console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to go to the **Bucket List** page.
2. Click **Create Bucket**. In the **Create Bucket** page that appears, configure the parameters as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/eb8c2ca6089302bd1f3b78bcd9daf6f8.png)
   - **Name**: enter a custom bucket name, whose format is [custom name]-[developer’s APPID] and cannot be modified once configured. For naming instructions, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312).
   - **Region**: select the region where the target cluster described in this document resides, which cannot be modified once configured. For more information, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).
   - **Multi-AZ feature**: after this feature is enabled, disaster recovery for multiple IDCs in the same region is provided. For more information, see [Overview of the Multi-AZ Feature](https://intl.cloud.tencent.com/document/product/436/35208).
   - **Access Permissions**: a bucket provides the **Private Read/Write**, **Public Read/Private Write**, and **Public Read/Write** permissions by default, which can be modified once configured.
      - **Private Read/Write**: only the creator of this bucket and authorized accounts have the permission to read or write objects in this bucket. This is the default access permission for a bucket and is recommended.
      - **Public Read/Private Write**: everyone (including anonymous visitors) has the permission to read objects in this bucket, but only the creator of this bucket and authorized accounts have the permission to write objects in this bucket.
      - **Public Read/Write**: everyone (including anonymous visitors) has the permissions to read or write objects in this bucket. This permission is not recommended.
   -**Bucket Tag**: the bucket tag is used as a key pair (key = value) and an identifier to manage buckets in groups. For more information, see [Setting Bucket Tags](https://intl.cloud.tencent.com/document/product/436/30928).
   - **Server-Side Encryption**: valid values are **None** and **SSE-COS**, where the latter indicates server-side encryption that uses COS to manage keys.
      - **SSE-COS**: server-side encryption that uses COS to manage keys. COS is used to host the primary key and manage data. You can use COS to directly manage and encrypt data. For more information, see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).
3. Verify the information and click **OK**. After the bucket is created, you can find it in the bucket list.

<span id="getPath"></span>
### Obtaining the subdirectory of a bucket

1. On the **Bucket List** page, select a created bucket to go to the bucket details page.
2. On the bucket details page, click the sub-folder to mount to go to the sub-folder details page. Obtain the subdirectory path (for example, `/costest`) in the upper-right corner of the page, as shown in the following figure.
![](https://main.qcloudimg.com/raw/abcc4a290bee8163889b2593836d9683.png)





## Directions

### Using COS through the console
<span id="StepOne"></span>
#### Creating a secret that can access COS

1. Click **Cluster** in the left sidebar to go to the **Cluster Management** page.
2. Select the ID of the target cluster to go to the cluster details page.
3. On the cluster details page, choose **Configuration Management** > **Secret** in the left sidebar to go to the **Secret** page, as shown in the following figure.
![](https://main.qcloudimg.com/raw/92d8c864b36bf486b7e034973396da65.png)
4. Click **Create** to go to the **Create Secret** page, where you can configure the parameters as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/1066fb90d03545ed7ee358a90e0d3ef7.png)
	- **Name**: specify a custom name. This document uses `cos-secret` as an example.
	- **Secret Type**: select **Opaque**. This type is applicable to storing key certificates and configuration files. The value is Base64-coded.
	- **Validity Range**: select **Specify namespace**. The `kube-system` namespace is required.
	- **Content**: configure the access key of the secret that is required to access a bucket. The value must include the variable names `SecretId` and `SecretKey`, as well as the corresponding variable values.
	For more information, see [Creating an access key](#CreatAccessKey). Then, go to the [API Key Management](https://console.cloud.tencent.com/cam/capi) page to obtain an access key.
5. Click **Create Secret** to complete the process.

<span id="StepTwo"></span>
#### Creating a PV that supports COS-CSI dynamic configuration 
>! This step requires a bucket. If no bucket is available in the current region, create one. For more information, see [Creating a bucket](#CreatBucket).
>
1. On the details page of the target cluster, choose **Storage** > **PersistentVolume** in the left sidebar to go to the **PersistentVolume** page.
2. Click Create to go to the **Create PersistentVolume** page, where you can configure PV parameters as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/e2dc010057dbf2351f993fb7a79c719b.png)
Main parameters are described as follows:
	- **Creation Method**: select **Manual**.
	- **Name**: specify a custom name. This document uses `cos-pv` as an example.
	- **Provisioner**: select **COS**.
	- **R/W permission**: COS only supports multi-host read and write.
	- **Secret**: select the secret that you created in [step 1](#StepOne). In this case, `cos-secret`is used as an example.
	- **Bucket List**: indicates the list of buckets for storing COS objects. You can select an available bucket as required.
	- **Bucket Sub-directory**: enter the subdirectory obtained in [Obtaining the subdirectory of a bucket](#getPath). This document uses `/costest` as an example.
	- **Domain**: the default domain name is used and displayed. You can use this domain name to access the bucket.
	- **Mount Option**: the COSFS tool can locally mount a bucket. After the bucket is mounted, you can directly manage the COS objects in it. This option is used to configure related restrictions. The mount option `-oensure_diskfree=20480` in this example indicates that when the free capacity of the disk where cache files are stored is less than 20,480 MB, running the COSFS tool minimizes disk space consumption.
>? Different mount options must be separated by spaces. For more mount options, see [COSFS](https://intl.cloud.tencent.com/document/product/436/6883).
3. Click **Create a PersistentVolume** to complete the process.

<span id="StepThree"></span>
#### Creating a PVC that is bound to a PV
>! Do not bind a PV that is already bound.

1. On the details page of the target cluster, choose **Storage** > **PersistentVolumeClaim** in the left sidebar to go to the **PersistentVolumeClaim** page.
2. Click **Create** to go to the **Create a PersistentVolumeClaim** page, where you can configure the parameters as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/5863b8983019a9a40531b750062010c6.png)
	- **Name**: specify a custom name. This document uses `cos-pvc` as an example.
	- **Namespace**: select **kube-system**.
	- **Provisioner**: select **COS**.
	- **R/W permission**: COS only supports multi-host read and write.
	- **PersistentVolume**: select the PV that you created in [step 2](#StepTwo). This document uses `cos-pv` as an example.
3. Click **Create a PersistentVolumeClaim**.

#### Creating a PVC used by a pod
>? This step creates a Deployment workload as an example.

1. On the details page of the target cluster, choose **Workload** > **Deployment** to go to the **Deployment** page.
2. Click **Create** to go to the **Create Workload** page. For more information, see [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662). Then, mount a volume as required, as shown in the following figure.
![](https://main.qcloudimg.com/raw/c295374ca83c63c1dc5346e2346ba72a.png)
	- **Volume (optional)**:
      - **Mount Method**: select **Using existing PVC**.
      - **Volume name**: specify a custom name. This document uses `cos-vol` as an example.
      - **Select PVC**: select the PVC that you created in [step 3](#StepThree). This document uses `cos-pvc` as an example.
	- **Containers in the instance**: click **Add Mount Point** to configure a mount point.
      - **Volume**: select the `cos-vol` volume that you added in this step.
      - **Destination Path**: enter a destination path. This document uses `/cache` as an example.
      - **Sub-path**: mount only a sub-path or a single file in the selected volume, such as `./data` or `data`.
3. Click **Create Workload**.

### Using COS through a YAML file
<span id="StepOne"></span>
#### Creating a secret that can access COS

You can create a secret that can access COS by using a YAML file. The YAML file template is as follows:
```yaml
apiVersion: v1
kind: Secret
type: Opaque
metadata:
  name: cos-secret
  # Replaced by your secret namespace.
  namespace: kube-system
data:
  # Replaced by your temporary secret file content. You can generate a temporary secret key with these docs:
  # Note: the value must be encoded by base64.
  SecretId: VWVEJxRk5Fb0JGbDA4M...(base64 encode)
  SecretKey: Qa3p4ZTVCMFlQek...(base64 encode)
```
<span id="StepTwo"></span>
#### Creating a PV that supports COS-CSI dynamic configuration
You can create a PV to support COS-CSI dynamic configuration by using a YAML file. The YAML file template is as follows:
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: "cos-pv"
spec:
  accessModes:
  - ReadWriteMany
  capacity:
    storage: 1Gi
  csi:
    driver: com.tencent.cloud.csi.cosfs
    # Specify a unique volumeHandle like bucket name. (this value must different from other pv's volumeHandle)
    volumeHandle: xxx
    volumeAttributes:
      # Replaced by the url of your region.
      url: "http://cos.ap-guangzhou.myqcloud.com"
      # Replaced by the bucket name you want to use.
      bucket: "testbucket-1010101010"
      # You can specify the sub-directory of the bucket in the cosfs command here.
      path: /costest
      # You can specify any other options used by the cosfs command in here.
      #additional_args: "-oallow_other"
    nodePublishSecretRef:
      # Replaced by the name and namespace of your secret.
      name: cos-secret
      namespace: kube-system
```

#### Creating a PVC that is bound to a PV

You can create a PVC that is bound to the preceding PV by using a YAML file. The YAML file template is as follows:
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
    name: cos-pvc
spec:
  accessModes:
  - ReadWriteMany
  resources:
    requests:
      storage: 1Gi
  # You can specify the pv name manually or just let Kubernetes bind the pv and pvc.
  # volumeName: cos-pv
  # Currently cos only supports static provisioning, the StorageClass name should be empty.
  storageClassName: ""
```

#### Creating a pod that uses a PVC
You can create a pod by using a YAML file. The YAML file template is as follows:
```yaml
apiVersion: v1
kind: Pod
metadata:
    name: pod-cos
spec:
  containers:
  - name: pod-cos
    command: ["tail", "-f", "/etc/hosts"]
    image: "centos:latest"
    volumeMounts:
    - mountPath: /data
      name: cos
    resources:
      requests:
        memory: "128Mi"
        cpu: "0.1"
  volumes:
  - name: cos
    persistentVolumeClaim:
      # Replaced by your pvc name.
      claimName: cos-pvc
```




