>! The **Workflow Management** section of the MPS console has been replaced with **Scheme Management**, which offers easier and more flexible settings. To configure a scheme, go to **Scheme Management**.


## Overview
After you set up a workflow, media files uploaded to the specified bucket and directory will be processed automatically, and the results will be uploaded to the specified bucket and directory. Workflows can include tasks such as transcoding, screenshot taking, animated screenshot generating, moderation, content recognition, content analysis, and watermarking.

## Creating a Workflow[](id:create)
1. Log in to the [MPS console](https://console.cloud.tencent.com/mps) and select **Workflow Management** on the left sidebar.
2. Click **Create Workflow** to enter the workflow creation page and set the workflow name, trigger bucket, trigger directory, output bucket, output directory, event notifications and tasks. For detailed instructions, please see [workflow configuration](#workflow).
![](https://qcloudimg.tencent-cloud.cn/raw/e46b738c267c5b34715abd01cc577b2d.png)

The table below lists the information needed to configure a workflow.
<table>
<tr><th width=15%>Item<a id="workflow"></a></th><th>Required</th><th>Description</th></tr>
<tr>
<td>Workflow name</td>
<td>Yes</td>
<td>Max 128 characters; supports Chinese characters, letters, digits, underscores, and hyphens. Example: "MPS"</td>
</tr><tr>
<td>Trigger bucket</td>
<td>Yes</td>
<td>Select a bucket created under the current `APPID`. After the workflow is enabled, videos uploaded to this bucket will be processed automatically.</td>
</tr><tr>
<td>Trigger directory</td>
<td>No</td>
<td>A string that ends with <code>(/)</code>. If it is left empty, the workflow will be applied to all directories under the selected trigger bucket.</td>
</tr><tr>
<td>Output bucket</td>
<td>Yes</td>
<td>By default, the output bucket is the same as the trigger bucket. You can also select a bucket in the same region under the same `APPID`. After a workflow is executed, the processed videos will be stored in this bucket.</td>
</tr><tr>
<td>Output directory</td>
<td>No</td>
<td>A string that ends with <code>(/)</code>. If it is left empty, the output directory will be the same as the trigger directory.</td>
</tr><tr>
<td>Event notifications</td>
<td>No</td>
<td>
<ul style="margin:0"><li>Disabled by default. For detailed instructions on how to configure event notifications, please see <a href="#recall">callback configuration</a> below. </li><li>To enable TDMQ-CMQ event notifications, you need to activate <a href="https://console.cloud.tencent.com/tdmq/cmq-queue?rid=1">Tencent Distributed Message Queue</a> and create a model. After TDMQ-CMQ event notifications are enabled, the specified message queue will receive notifications about video processing events.</li></ul></td>
</tr><tr>
<td>Configuration items</td>
<td>Yes</td>
<td>From transcoding, screenshot taking, animated image generation, moderation, content recognition, and content analysis, select at least one task for configuration. For details, see <a href="#p1">task configuration</a> below.</td>
</tr></table>
<table>
<tr><th>Callback Method<a id="recall"></a></th><th>Configuration</th></tr>
<tr>
<td>TDMQ-CMQ callbacks</td>
<td>
<ul style="margin:0">
<li>TDMQ-CMQ model: Select “Queue model”. or “Topic model”.</li>
<li>TDMQ-CMQ region: Select Guangzhou, Shanghai, Beijing, Shanghai Finance, Shenzhen Finance, Hong Kong (China), Chengdu, North America, or west US.</li>
<li>Queue name/Topic name: Enter a custom name.</li>
</ul>
</td>
</tr>
<tr>
<td>HTTP callbacks</td>
<td>When calling the notification configuration API <a href="https://intl.cloud.tencent.com/document/product/1041/33690#TaskNotifyConfig">TaskNotifyConfig</a>, set `NotifyType` to `URL` and `NotifyUrl` to the HTTP callback address.
</td>
</tr>
<tr>
<td>SCF callbacks</td>
<td>You can click <a href="https://console.cloud.tencent.com/scf/list-create?rid=1&ns=default&keyword=mps">Go to SCF console</a> to configure a function in the SCF console. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/1041/40337">MPS Task Callback Notification</a>. <br>SCF callback configuration applies to all workflows and is not saved specifically for the current workflow.</td>
</tr>
</table>


## Event Notifications[](id:event)
### Receiving event notifications via CMQ
- Event notifications are disabled by default. To receive notifications via CMQ, click the toggle next to **Enable Event Notifications**, select queue or topic model for **CMQ Model**, and set the model name and region. MPS event notifications will be sent to the specified queue or topic.
- You can receive event notifications via CMQ only after you activate the CMQ service and create a queue or topic model. For more information, please see [CMQ > Getting Started](https://intl.cloud.tencent.com/document/product/406/8435).

### Receiving event notifications via SCF
SCF allows quick handling of the event notifications generated by MPS. The figure below shows the data flow.
<img src="https://main.qcloudimg.com/raw/02656fefa8e2f61f71252727747b7a02.png" style="zoom: 67%;" />
Events are pushed to SCF by the MPS trigger and are handled by serverless functions.

#### Use cases
CLS can deliver the data in log topics to SCF via an MPS log trigger to enable operations such as notification sending, status monitoring, and alarm handling.

| Function Processing Scenario | Description |
| -------------------- | ------------------------------------------------------- |
| Video task backup to COS | Backing up the called back tasks of MPS to COS via SCF in a timely manner |
| Video task callback notifications | Receiving MPS data messages in real time and sending the messages to users via WeCom or email. |

>! Sending data to SCF will incur fees. For details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/583/17299).

## Managing Workflows[](id:manage)
1. Log in to the [MPS console](https://console.cloud.tencent.com/mps) and select **Workflow Management** on the left sidebar.
2. The workflow list displays information including workflow name, trigger bucket, region, trigger directory, creation time, and status. You can sort workflows by creation time, search for a workflow by name, and view, edit, or delete a workflow.
	-  **Enable a workflow**
		- Workflows are disabled by default. To enable a workflow, click the toggle in the **Enable** column.
		- After a workflow is enabled, it will be automatically executed for videos uploaded to the trigger bucket.
	- **Disable a workflow**
		- To disable a workflow, click the toggle in the **Enable** column.
		- After a workflow is disabled, it will no longer be automatically executed on videos uploaded to the trigger bucket.
	- **Edit a workflow**
		- Click **Edit** in the **Operation** column of the target workflow to modify its name, trigger bucket, trigger directory, output bucket, output directory, event notification settings, and tasks.
		- You cannot edit or delete an enabled workflow.
	- **Delete a workflow**
		- Click **Delete** in the **Operation** column of the target workflow to delete it.
		- After a workflow is deleted, it will no longer be automatically executed on videos uploaded to the trigger bucket.
		- You cannot edit or delete an enabled workflow.
