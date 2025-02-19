## Overview

You can leverage the alarm policy feature of Cloud Monitor to set threshold-reaching alarms for COS monitoring metrics. An alarm policy must include the policy name, policy type, trigger condition, alarm object, and alarm notification template. You can create an alarm policy for COS as instructed below.

>?Tencent Cloud's Cloud Monitor enables users to monitor cloud resources in real time and provides alarm services. Users can set alarm policies for COS monitoring metrics to query the alarm history and receive alarm notifications. For more information, see [Creating Alarm Policy](https://intl.cloud.tencent.com/document/product/248/38916).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5). On the **Overview** page, click **Configure Alarm Policy** in the **Alarm Configuration** section.
>?**Alarm Configuration** can also be found on the **Overview** page of each bucket.
>
2. Click **Create** and configure a new alarm policy as shown below:
![](https://main.qcloudimg.com/raw/b8340b9590b8204ab082f28c096417e2.png)
<table>
  <tr>
    <th>Configuration Type</th>
    <th width="18%">Configuration Item</th>
    <th>Description</th>
  </tr>
  <tr>
    <td  rowspan="5"> Basic Information</td>
    <td>Policy Name</td>
    <td>Custom policy name.</td>
  </tr>
  <tr>
    <td>Remarks</td>
    <td>Custom policy remarks.</td>
  </tr>
  <tr>
    <td>Monitor Type</td>
    <td>Select **Cloud Product Monitoring**.</td>
  </tr>
  <tr>
    <td>Policy Type</td>
    <td>Select **COS**.</td>
  </tr>
  <tr>
    <td>Project</td>
    <td>Setting the policy project allows you to:<br>   
         <ul>
             <li>Manage alarm policies. Alarm policies of a project can be quickly located in the alarm policy list.</li>
             <li>Manage instances. You can select the project as needed. Instances of the project can be quickly located in **Alarm Object**. You can distribute Tencent Cloud services to the desired project according to your business types. To create a project, see Project Management. After the project is created, you can distribute resources to projects in the console of each Tencent Cloud service. Some Tencent Cloud services cannot be distributed to a project. If you do not have project permission, see <a href="https://intl.cloud.tencent.com/document/product/248/36744">Cloud Access Management (CAM)</a> for authorization.</li></td>   
  </tr>
  <tr>
    <td rowspan="3">Configure Alarm Rule</td>
    <td>Alarm Object</td>
    <td>
      <ul>
			         <li>If you select **Instance ID** from the drop-down list, select the bucket you want to add an alarm to. </li>
               <li>If you select **Instance Group** from the drop-down list, the alarm policy will be bound to the selected instance group. If there is no instance group, you can click **Create Instance Group** on the right to create a group for the bucket first.</li>
		            <li>If you select **All Objects** from the drop-down list, the alarm policy will be bound to all buckets the current account has permission for.</li>
           </ul>
        </td>
  </tr>
	<tr>
    <td>Select template</td>
    <td>Select a configured template from the drop-down list. For more information on the configuration, see <a href="https://intl.cloud.tencent.com/document/product/248/38911">Configuring Trigger Condition Template</a>. If the newly created template is not displayed, click </b>Refresh</b> on the right.</td>
  </tr>
	<tr>
    <td>Manual Configuration<br>(Metric alarm)</td>
    <td>
      <ul>
        <li>**Trigger condition**: Consists of metric, comparison, threshold, statistical period, and the number of consecutive periods.<br>For example, if the metric is set to `STANDARD storage read requests`, comparison to `>`, threshold to `80` times, statistical period to `5` minutes, and the number of consecutive periods to `Last 2 periods`, <br>STANDARD storage read requests are collected every five minutes, and if the number of STANDARD storage read requests in a bucket is greater than 80 in two consecutive periods, the alarm will be triggered.
				<br><li>**Alarm frequency**: You can set a repeated notification policy for each alarm rule. In this way, an alarm notification will be sent repeatedly at a specified frequency when an alarm is triggered.<br>Valid values: Do not repeat; Once every 5 minutes; Once every 10 minutes; At an exponentially increasing interval; Other frequency options.<br><ul><li type="square">An exponentially increasing interval means that a notification is sent when an alarm is triggered the 1st time, 2nd time, 4th time, 8th time, and so on. In other words, the alarm notification will be sent less and less frequently as time goes on to reduce the disturbance caused by repeated notifications.</li>
      <li>**Default logic for repeated alarm notifications**: The alarm notification will be sent to you at the configured frequency within 24 hours after the alarm is triggered. After 24 hours, the alarm notification will be sent once a day by default.</li></ul></li>
      </ul></td>
  </tr>
   <tr>
        <td >Configure Alarm Notification</td>
        <td>Alarm Notification</td>
        <td>Select a preset or custom notification template. Each alarm policy can be bound to three notification templates at most. For more information, see <a href="https://intl.cloud.tencent.com/document/product/248/38906">Cloud Monitor</a>.</td>
    </tr>
		<tr>
      <td>Advanced Settings</td>
      <td >Auto Scaling</td>
      <td>If enabled, the auto scaling policy can be triggered when the alarm condition is met.</td>
     </tr>
</table>
3. After configuring the above information, click **Save**.
