
管理功能费用指用户开启并使用了管理功能（如清单或检索功能）后所产生的费用。

>?关于存储类型的更多介绍，请参见 [存储类型概述](https://intl.cloud.tencent.com/document/product/436/30925)。
> 

<table>
<thead>
<tr>
<th>计费项</th>
<th>适用的存储类型</th>
<th>计费项说明</th>
<th>计费方式</th>
</tr>
</thead>
<tbody><tr>
<td>清单功能费用</td>
<td nowrap="nowrap">与存储类型不相关</td>
<td>当用户开启了清单功能后，列出存储桶对象列表时产生的费用</td>
<td>按量计费</li></td>
</tr>
<tr>
<td >检索功能费用</td>
<td>标准存储<br>低频存储</td>
<td>当用户开启了检索功能后，扫描对象时产生的费用</td>
<td>按量计费</td>
</tr>
<tr>
<td>批量处理费用</td>
<td nowrap="nowrap">与存储类型不相关</td>
<td>当用户开启了批量处理功能后，COS 会按创建的任务数和对象处理量进行收费</td>
<td>按量计费</td>
</tr>
<tr>
<td>对象标签费用</td>
<td nowrap="nowrap">与存储类型不相关</td>
<td>当用户开启了对象标签功能后，COS 会按对象标签数量进行收费</td>
<td>按量计费</td>
</tr>
</tbody></table>



## 管理功能费用的计费方式和计算方法

<table>
   <tr>
      <th>计费方式</th>
      <th>计费项</th>
      <th>计费方法</th>
   </tr>
   <tr>
      <td rowspan=4>按量计费</td>
      <td>清单功能费用</td>
      <td nowrap="nowrap"><ul  style="margin: 0;"><li>按日结算</li><li>清单功能费用 = 列出的对象数/百万 x 单价</li></ul></td>
   </tr>
   <tr>
      <td>检索功能费用</td>
      <td nowrap="nowrap"><ul  style="margin: 0;"><li>按日结算</li><li>检索功能费用 = 每 GB 单价 x 日累计数据检索量</li></ul></td>
   </tr>
   <tr>
      <td>批量处理费用</td>
			<td nowrap="nowrap">批量处理费用包括任务费用和对象处理费用。<ul  style="margin: 0;"><li>按日结算<br><li>任务费用 = 创建的任务数 x 单价</li><li>对象处理费用 = 每处理万个对象 x 单价</li></ul></td>
   </tr>
   <tr>
      <td>对象标签费用</td>
			<td nowrap="nowrap"><ul  style="margin: 0;"><li>按日结算</li><li>对象标签费用 = 每万个标签数 x 单价</li></ul></td>
   </tr>
</table>


## 管理功能定价

关于管理功能单价，请查看 [产品定价](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)。

>!2021年09月30日起，对象标签进行刊例价降价调整。
>1. 公有云中国大陆地域降至0.00025817美元/万个标签/日，中国香港和海外地域降至0.0003098美元/万个标签/日。
>2. 此价格将在2021年10月01日的账单生效（即2021年09月30日账单）。
>




## 计费案例

>? 以下案例中出现的费用价格仅供参考，实际价格请参见 COS [产品定价](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)。
>


### 案例：标准存储容量费用 + 对象标签费用 + 请求费用

假设用户 A 于2020年11月1日上传了10GB标准存储类型的数据至广州地域的 COS 存储桶，当天给10万个对象批量添加标签，并且产生了10万次请求次数，其余时间无其他操作，按照每日对上一日产生的费用进行结算。那么：

- 标准存储容量费用：在2020年11月2日结算。
- 标准存储请求费用：在2020年11月2日结算。
- 对象标签费用：在2020年11月2日结算。

费用分析如下：


- 标准存储容量费用 = 0.024美元/GB/月 /30 x 10GB x 30天 = 0.24美元。
- 标准存储请求费用 = 0.002美元/万次 x 10万次 = 0.02美元
- 对象标签费用 = 0.00025817美元/每万个标签/日 x 30 x 10万个对象 = 0.077451美元

综合上面分析得出，整个11月用户 A 总花费为0.24 + 0.02 + 0.077451 = 0.337451美元。

