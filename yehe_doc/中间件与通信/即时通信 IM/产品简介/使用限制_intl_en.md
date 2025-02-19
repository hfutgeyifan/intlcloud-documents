## Service Feature Limits

<table>
        <tr>
            <th  width="15%">Feature</th>
            <th  width="20%">Limit Item</th>
            <th>Description</th>
        </tr>
        <tr>
            <td  rowspan="5">One-to-one/group message</td>
            <td>Content length</td>
            <td>The maximum length for a single one-to-one/group message is 8,000 bytes. </td>
        </tr>
	<tr>
            <td>Sending frequency</td>
            <td>One-to-one messages: no limit<br>Group messages: 40 messages/second for each group (this limit applies to all group types, and the frequency limits on different groups are independent)</td>
        </tr>
	<tr>
            <td>Receiving frequency</td>
            <td>Android/iOS/Mac/Windows/iPad: no limit for one-to-one messages or group messages<br>Web: no more than 1,000 messages/second (total of one-to-one messages and group messages)</td>
        </tr>	
        <tr>
            <td>Size of a single file</td>
		<td><li>SDKs support a maximum file size of 100 MB for any single file to be sent. </li><li>Mini Program SDK does not support creating and sending file messages. </li><li>WebIM SDK does not support creating and sending audio messages.</li></td>
        </tr>
	<tr>
            <td>Message history storage period</td>
            <td>Historical message storage is available for one-to-one messages and non–audio-video group messages. You can log in to the <a href="https://console.cloud.tencent.com/im">IM console</a> to modify the relevant configuration. The default configurations for different service packages are as follows: <ul style="margin:0;"><li>Free Edition: 7 days, with no extension supported</li><li>Pro Edition: 7 days, with extension supported</li><li>Ultimate Edition: 30 days, with extension supported</li></ul>The extension of the historical message storage period is a value-added service. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/34350">Value-added Service Pricing</a>.</td>
        </tr>
        <tr>
            <td>System message</td>
            <td>Quantity and storage period</td>
            <td>A maximum of 100 system messages can be stored for up to 7 days.</td>
        </tr>
        <tr>
            <td>UserID</td>
            <td>Naming rules</td>
            <td>The maximum length of a user account is limited to 32 bytes. English letters or numbers are supported. Special characters are not allowed.</td>
        </tr>
				<tr>
            <td>User profile</td>
            <td>Custom field</td>
            <td>The keywords of custom fields must consist of English letters with a length no longer than 8 bytes. The length of the values of custom fields cannot exceed 500 bytes.</td>
        </tr>
        <tr>
            <td>UserSig</td>
            <td>Validity period</td>
            <td>User password. The signatures generated by the default API of the IM backend SDK expire after 180 days.</td>
        </tr>
				<tr>
            <td>Conversation management</td>						
            <td>Number of recent contacts</td>
            <td>Up to 100 recent contacts can be saved for an ordinary user.</td>
        </tr>
        <tr>
            <td  rowspan="2">User relationship chain</td>
            <td>Friends and friend lists</td>
            <td><ul style="margin:0;"><li>A single user can have up to 3,000 friends.</li><li>The maximum number of pending friend requests supported is 100.</li><li>The maximum number of friend lists supported is 32.</li><li>The maximum length of a friend list name is 30 characters.</li><li>The maximum length of friend remarks is 96 characters.</li><li>WebIM SDK supports friend relationship chain starting from v2.13.0.</li></ul></td>
        </tr>
        <tr>
            <td>Blocklist</td>
            <td>A single user can add a maximum of 1,000 users to the blocklist.</td>
        </tr>
         <tr>
            <td  rowspan="7">Group</td>
            <td>Number of groups</td>
            <td>This refers to the total number of groups of all group types that simultaneously exist in a single SDKAppID, excluding disbanded groups. If the upper limit has been reached, you can disband unneeded groups and then create new ones. The upper limits for different service packages are as follows:<li>Free Edition: 100</li><li>Pro Edition or Ultimate Edition: no upper limit</li><br>The maximum daily net increase of groups is 10,000, and the free peak group count is 100,000/month. If the peak group count exceeds the free quota, extra fees will be generated. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/34350">Fees for Usage Exceeding the Free Quota</a>.</li></ul></td>
        </tr>
        <tr>
            <td>Number of group members</td>
            <td>Audio-video group (AvChatRoom): no upper limit on the number of group members. <br>For non–audio-video groups, the default configurations for different service packages are as follows: <ul style="margin:0;"><li>Free Edition: 20 members/group </li><li>Pro Edition: 200 members/group, which can be extended to 2,000 members/group</li><li>Ultimate Edition: 2,000 members/group, which can be extended to 6,000 members/group</li>Extending the upper limit on the number of group members is a paid value-added service. For the specific costs, see<a href="https://intl.cloud.tencent.com/document/product/1047/34350">Value-added Service Pricing</a>.</ul></td>
        </tr>
        <tr>
            <td>Number of groups a user can join</td>
            <td>This refers to the total number of groups of all group types that a user can join. The limits for different service packages are as follows: <ul style="margin:0;"><li>Free Edition: 50 groups/user</li><li>Pro Edition: 500 groups/user, which can be extended to 1,000 groups/user</li><li>Ultimate Edition: Can be extended to 3,000 groups/user</li></ul>Extending the upper limit on the number of groups that a user can join is a paid value-added service. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/34350">Value-added Service Pricing</a>.</li></td>
        </tr>
        <tr>
            <td>Group profile</td>
            <td><ul style="margin:0;"><li>The maximum length of the group name is 30 bytes.</li><li>The maximum length of the group introduction is 240 bytes.</li><li>The maximum length of the group announcement is 300 bytes.</li><li>The maximum length of the group profile photo URL is 100 bytes.</li><li>The maximum length of the group name card is 50 bytes.</li></ul></td>
        </tr>
        <tr>
            <td>Custom group ID</td>
            <td>The custom group ID must be printable ASCII characters (0x20-0x7e) with maximum length limited to 48 bytes. It cannot begin with @TGS# so as to avoid confusion with the default group IDs assigned by IM.</td>
        </tr>
        <tr>
            <td>Group custom field</td>
            <td>Groups supports up to 10 custom fields: <ul style="margin:0;"><li>The Key field is String type, with a maximum length of 16 bytes. Its name can contain only uppercase and lowercase letters, numbers, and underscores.</li><li>The Value field is a user-defined buffer and can be binary data. The maximum Value length for groups is 512 bytes.</li></ul></td>
        </tr>
        <tr>
            <td>Group member custom field</td>
            <td>Group member supports up to 5 custom fields: <ul style="margin:0;"><li>The Key field is String type, with a maximum length of 16 bytes. Its name can contain only uppercase and lowercase letters, numbers, and underscores. </li><li>The Value field is a user-defined buffer and can be binary data. The maximum Value length for group member is 64 bytes.</li></ul></td>
        </tr>
</table>

## API-related Limits
>? This document lists only the RESTful APIs that have use limits. For a complete list of APIs, see [RESTful API List](https://intl.cloud.tencent.com/document/product/1047/34621).

### General limits

<table>
        <tr>
            <th  width="30%">Limit Item</th>
            <th>Description</th>
        </tr>
        <tr>
            <td>Call frequency</td>
            <td><ul style="margin:0;"><li>Up to 100 times/second: <a href="https://intl.cloud.tencent.com/document/product/1047/34954">importing multiple accounts</a>, <a href="https://intl.cloud.tencent.com/document/product/1047/34955">deleting accounts</a> and <a href="https://intl.cloud.tencent.com/document/product/1047/34956">querying accounts</a></li><li>Up to 200 times/second: other <a href="https://intl.cloud.tencent.com/document/product/1047/34621">RESTful APIs</a></li></ul></td>
        </tr>
</table>



### Account management

<table>
        <tr>
            <th  width="30%">API</th>
            <th>Description</th>
        </tr>
        <tr>
            <td>Importing multiple accounts</td>
            <td>Up to 100 user names can be imported at a time, and this API does not support directly importing nickname and profile photo information of accounts.</td>
        </tr>
				<tr>
            <td>Querying online status of accounts</td>
            <td>A single request can query the status of up to 500 users.</td>
        </tr>
</table>

### One-to-one message

<table>
        <tr>
            <th  width="30%">API</th>
            <th>Description</th>
        </tr>
        <tr>
            <td>Sending one-to-one messages in batches</td>
            <td>A single request can send one-to-one messages to up to 500 users.</td>
        </tr>
</table>


### Relationship chain management


<table>
        <tr>
            <th  width="30%">API</th>
            <th>Description</th>
        </tr>
        <tr>
            <td>Importing friends</td>
            <td>A single request can import up to 1,000 friends.</td>
        </tr>
</table>


### Group management

<table>
        <tr>
            <th  width="30%">API</th>
            <th>Description</th>
        </tr>
        <tr>
            <td>Adding group members</td>
            <td>A maximum of 100 members can be added at a time.</td>
        </tr>
        <tr>
            <td>Deleting group members</td>
            <td>A single request can delete up to 500 members.</td>
        </tr>
        <tr>
            <td>Querying a user’s identity in the group</td>
            <td>A single request can query up to 500 accounts.</td>
        </tr>
        <tr>
            <td>Batch muting and unmuting</td>
            <td>A single request can mute/unmute up to 500 accounts.</td>
        </tr>
        <tr>
            <td>Sending ordinary messages in a group</td>
            <td>The default sending frequency of a single group is limited to 40 messages/second. <br><b>If two messages sent within 5 minutes from the same sender have the same random value (Random parameter), the later message will be discarded as a duplicate message.</b></td>
        </tr>
        <tr>
            <td>Importing group messages</td>
            <td>A maximum of 20 messages can be imported by a single request. Messages must be imported in ascending order by timestamp. The timestamps of imported messages must be earlier than the current time and later than the group creation time. Otherwise, the import fails.</td>
        </tr>
        <tr>
            <td>Importing group members</td>
            <td>Audio-video groups (AVChatRoom) do not support importing members.<br>Up to 300 members can be imported in one request. However, different group types have different group member limits. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/33515">Group Features</a>.</td>
        </tr>
</table>
