## 2020年12月

<table>
<thead>
<tr>
<th  width=20%>动态名称</th>
<th  width=44%>动态描述</th>
<th  width=16%>发布时间</th>
<th  width=20%>相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>新增推送排查功能</td>
<td>当某个设备未收到推送时，可以通过该设备 Token 与推送的 PushID 查询未收到原因，快速排查问题</td>
<td>2020-12-02</td>
<td>可前往【控制台】>【工具箱】>【<a href="https://console.cloud.tencent.com/tpns/user-tools/">排查工具</a>】>【推送查询】体验</td>
</tr>
<tr>
<td>新增预估设备数功能</td>
<td>确认推送前可查看所选推送目标预估设备数，快速预估当前推送覆盖范围</td>
<td>2020-12-02</td>
<td>-</td>
</tr>
<tr>
<td>控制台标签选择优化</td>
<td>标签选择控制台重构，提升标签选择体验</td>
<td>2020-12-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/35392">标签功能</a></td>
</tr>
</tbody></table>

## 2020年11月

<table>
<thead>
<tr>
<th width=20%>动态名称</th>
<th width=44%>动态描述</th>
<th width=16%>发布时间</th>
<th width=20%>相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>推送文案支持快捷插入 emoji</td>
<td>控制台创建推送时，文案输入框右侧支持快捷插入 emoji，有效提升点击率</td>
<td>2020-11-20</td>
<td>-</td>
</tr>
<tr>
<td>IP 白名单</td>
<td>在控制台配置后，可对 Rest API 的请求做权限管控，仅在白名单内的 IP 可请求 Rest API，提升推送安全性</td>
<td>2020-11-20</td>
<td>-</td>
</tr>
<tr>
<td>测试预览</td>
<td>在控制台保存常用的测试设备 Token，正式推送前可直接选取测试设备发送推送预览，快速验证推送配置</td>
<td>2020-11-20</td>
<td>-</td>
</tr>
<tr>
<td>号码包推送详情中可显示号码包文件名</td>
<td>号码包推送的推送详情中可显示推送时的号码包文件名，快速定位到推送目标</td>
<td>2020-11-20</td>
<td>-</td>
</tr>
<tr>
<td>华为 V2 协议升级通知</td>
<td>华为官方通知：「<b>2021年9月30日起停用 V2 协议</b>」。TPNS 已将华为推送协议升级到 V5，V5 协议不支持通过【附加参数】字段携带自定义参数。如果您集成了华为厂商通道，建议您改用 <a href="https://intl.cloud.tencent.com/document/product/1024/32624"> Intent 方式</a> 携带自定义参数，否则将导致自定义参数不能成功通过华为推送通道下发</td>
<td>2020-11-09</td>
<td>-</td>
</tr>
<tr>
<td>【NEW】个性化推送</td>
<td>将昵称等用户属性与 Token 绑定后，通过一次配置即可向不同用户发送带有用户属性的个性化推送，平均点击率提升40%</td>
<td>2020-11-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/38542">个性化通知</a></td>
</tr>
<tr>
<td>号码包文件支持直接上传 <code>.txt</code> 或 <code>.csv</code> 格式文件</td>
<td>如果号码包文件（<code>.txt</code> 或 <code>.csv</code> 格式）本身小于100M，可直接上传并使用，无需压缩</td>
<td>2020-11-09</td>
<td>-</td>
</tr>
<tr>
<td>iOS 推送支持通道策略</td>
<td>APNs 静默消息对单设备每小时限额3条，iOS 通知栏消息与静默消息均支持 TPNS 通道与 APNs 通道互补下发，可自定义下发策略</td>
<td>2020-11-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/36151">通道策略</a></td>
</tr>
</tbody></table>

## 2020年10月

<table>
<thead>
<tr>
<th  width=20%>动态名称</th>
<th  width=44%>动态描述</th>
<th  width=16%>发布时间</th>
<th  width=20%>相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>控制台数据统计优化</td>
<td>拆分推送统计与设备统计</td>
<td>2020-10-22</td>
<td>详见控制台 <a href="https://console.cloud.tencent.com/tpns/overview">数据统计</a> 模块</td>
</tr>
<tr>
<td>iOS 快速集成升级</td>
<td>使用快速集成工具进行 iOS SDK 接入，3分钟快速集成完整推送能力</td>
<td>2020-10-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/35770">iOS 快速接入</a></td>
</tr>
<tr>
<td>iOS 针对通知栏关闭的设备不下发通知</td>
<td>若 iOS 设备通知栏已关闭，则下发推送时该设备不会被计算进<b>计划发送</b>指标内</td>
<td>2020-10-22</td>
<td>-</td>
</tr>
</tbody></table>

## 2020年09月

<table>
<thead>
    <tr>
        <th width=20%>动态名称</th>
        <th width=44%>动态描述</th>
        <th width=16%>发布时间</th>
        <th width=20%>相关文档</th>
    </tr>
</thead>
<tbody>
<tr>
<td>排查工具支持按账号查询 Token</td>
<td>支持通过账号搜索设备 Token，定位问题将更方便、更快捷</td>
<td>2020-09-28</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/38389">排查工具</a></td>
</tr>
<tr>
<td>用户标签支持新增、活跃、沉默标签</td>
<td>支持新增、活跃、沉默用户标签，可快速进行精准用户促活、流失召回，轻轻松松提升用户活跃度</td>
<td>2020-09-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/35392">标签功能</a></td>
</tr>

</tbody></table>

## 2020年08月

<table>
<thead>
    <tr>
        <th width=20%>动态名称</th>
        <th width=44%>动态描述</th>
        <th width=16%>发布时间</th>
        <th width=20%>相关文档</th>
    </tr>
</thead>
<tbody>
<tr>
<td>新增“<B>分组折叠</B>”功能</td>
<td>增加“<B>分组折叠</B>”功能，可决定推送在通知中心中是否折叠，以及自定义折叠策略</td>
<td>2020-08-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/37807">消息折叠功能</a></td>
</tr>
<tr>
<td>Android 通道策略优化</td>
<td>Android 通道策略-自定义策略优化，可自由选择设备在线是否优先通过 TPNS 通道下发</td>
<td>2020-08-11</td>
<td>-</td>
</tr>

<tr>
<td>数据概览页新增数据指标</td>
<td>控制台数据概览页新增按天查看通知栏开启数、卸载/失效设备数</td>
<td>2020-08-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/36384">数据概览</td>
</tr>
</tbody></table>

## 2020年07月

<table>
<thead>
    <tr>
        <th width=20%>动态名称</th>
        <th width=44%>动态描述</th>
        <th width=16%>发布时间</th>
        <th width=20%>相关文档</th>
    </tr>
</thead>
<tbody>
<tr>
<td>新增“<B>设备统计</B>”页面</td>
<td>控制台新增“<B>设备统计</B>”页面，随时掌握应用所有注册设备各个维度的分布情况，辅助运营决策</td>
<td>2020-07-30</td>
<td>-</td>
</tr>
<tr>
<td>富媒体通知升级</td>
<td>富媒体通知能力升级，通知带图片，点击率 Up Up ！ （适配华为、小米通道富媒体通知） </td>
<td>2020-07-30</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/1024/37858 ">富媒体通知</a></td>
</tr>

<tr>
<td>新增按量计费（后付费）计费模式</td>
<td>支持按量计费购买，按日结算，适用于日活跃用户数（DAU）波动较大的应用</td>
<td>2020-07-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/36877">按量计费</a></td>
</tr>
</tbody></table>

## 2020年06月

<table>
<thead>
    <tr>
        <th width=20%>动态名称</th>
        <th width=44%>动态描述</th>
        <th width=16%>发布时间</th>
        <th width=20%>相关文档</th>
    </tr>
</thead>
<tbody><tr>
<td>公告栏</td>
<td>控制台【产品管理】页面顶部增加公告栏模块，承载产品动态通知以及业务通知</td>
<td>2020-06-10</td>
<td>-</td>
</tr>
<tr>
<td>通知文案超长提醒</td>
<td>在控制台输入通知标题/内容时，若文案在部分机型不能完全展示，控制台会展示相应提醒，但不影响推送正常下发</td>
<td>2020-06-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1024/35286">文案长度限制说明</a></td>
</tr>
<tr>
<td>工具箱功能更新</td>
<td>在工具箱可通过 Token 查询该设备的一些基本属性</td>
<td>2020-06-10</td>
<td>-</td>
</tr>
</tbody></table>

## 2020年05月

<table>
    <tr>
        <th width=20%>动态名称</th>
        <th width=44%>动态描述</th>
        <th width=16%>发布时间</th>
        <th width=20%>相关文档</th>
    </tr>
<tr>
        <td>应用级别推送漏斗数据</td>
        <td>支持应用级别的每日及实时的消息发送、抵达（PV/UV）、点击、清除趋势数据并支持分通道查看</td>
        <td>2020-05-25</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/36384">数据概览</a></td>
    </tr> 
    <tr>
        <td>任务级通道选择</td>
        <td>支持对单条推送指定推送通道，以节省厂商通道额度</td>
        <td>2020-05-07</td>
        <td>-</td>
    </tr>
</table>

## 2020年04月

<table>
    <tr>
        <th width=20%>动态名称</th>
        <th width=44%>动态描述</th>
        <th width=16%>发布时间</th>
        <th width=20%>相关文档</th>
    </tr>
    <tr>
        <td>小米通道超额提醒</td>
        <td>小米通道超额后，自动走 TPNS 通道推送，且控制台提示</td>
        <td>2020-04-23</td>
        <td>-</td>
    </tr>
    <tr>
        <td>控制台推送记录支持搜索</td>
        <td>支持根据 pushid 搜索推送</td>
        <td>2020-04-23</td>
        <td>-</td>
    </tr>
    <tr>
        <td>推送进度</td>
				<td><a href="https://console.cloud.tencent.com/tpns">控制台</a>-推送详情页面增加推送进度，可查看推送下发情况</td>
        <td>2020-04-23</td>
        <td>-</td>
    </tr>
    <tr>
        <td>推送时效</td>
        <td>推送详情页面增加推送时效分析，实时查看推送抵达和点击时效</td>
        <td>2020-04-23</td>
        <td>-</td>
    </tr>
    <tr>
        <td>工具箱更新</td>
        <td>工具箱新增「通知栏状态」，可根据token查询当前设备通知栏是否开启</td>
        <td>2020-04-23</td>
        <td>-</td>
    </tr>
    <tr>
        <td>标签组合逻辑优化</td>
        <td>支持标签与或非三层嵌套运算，人群更加细分</td>
        <td>2020-04-09</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/35392">标签功能使用</a></td>
    </tr>
    <tr>
        <td>数据概览增加指标</td>
        <td>丰富数据概览页面指标，多维查看推送数据</td>
        <td>2020-04-09</td>
        <td>-</td>
    </tr>
</table>

## 2020年03月

<table>
    <tr>
        <th width=20%>动态名称</th>
        <th width=44%>动态描述</th>
        <th width=16%>发布时间</th>
        <th width=20%>相关文档</th>
    </tr>
    <tr>
        <td>Android全面支持多包名推送</td>
        <td>TPNS通道和各主流厂商通道均支持多包名推送</td>
        <td>2020-03-12</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/35393">多包名推送功能</a></td>
    </tr>
</table>

## 2020年02月


<table>
    <tr>
        <th width=20%>动态名称</th>
        <th width=44%>动态描述</th>
        <th width=16%>发布时间</th>
        <th width=20%>相关文档</th>
    </tr>
    <tr>
        <td>控制台交互升级</td>
        <td>整合控制台功能结构</td>
        <td>2020-02-24 </td>
        <td>-</td>
    </tr>
      <tr>
        <td>SDK快速接入</td>
        <td>Android支持配置文件快速接入；<br>iOS可通过本地化工具实现无代码集成</td>
        <td>2020-02-24 </td>
        <td><li><a href="https://intl.cloud.tencent.com/document/product/1024/35769">Android快速接入</a><li><a href="https://intl.cloud.tencent.com/document/product/1024/35770">iOS快速接入</a></li></td>
    </tr>
      <tr>
        <td>资源级权限控制</td>
        <td>可为子账号分配某个应用的操作权限</td>
        <td>2020-02-24 </td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/35288">TPNS 可授权的资源</a></td>
    </tr>
</table>


## 2020年01月

<table>
    <tr>
        <th width=20%>动态名称</th>
        <th width=44%>动态描述</th>
        <th width=16%>发布时间</th>
        <th width=20%>相关文档</th>
    </tr>
    <tr>
        <td>厂商通道超额策略</td>
        <td>厂商通道超额后自动通过TPNS通道下发，最大程度保证消息可达</td>
        <td>2020-02-24</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/35829">厂商通道限额说明</a></td>
    </tr>
</table>

## 2019年12月

<table>
    <tr>
        <th width=20%>动态名称</th>
        <th width=44%>动态描述</th>
        <th width=16%>发布时间</th>
        <th width=20%>相关文档</th>
    </tr>
    <tr>
        <td>推送详情优化</td>
        <td>推送详情分通道展示，可通过通道维度分析推送效果</td>
        <td>2019-12-25</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/32606">查询推送记录</a></td>
    </tr>
    <tr>
        <td>增加试用机制</td>
        <td>日活跃用户数（DAU）1000以下的应用免费试用30天</td>
        <td>2019-12-25</td>
        <td>-</td>
    </tr>
    <tr>
        <td>工具箱上线</td>
        <td>上线问题排查工具，根据 token 自助查询设备信息、账号绑定以及标签绑定等状态，以便快速定位推送问题</td>
        <td>2019-12-19</td>
        <td>-</td>
    </tr>
    <tr>
        <td>聚合统计</td>
        <td>可通过`groupld`字段聚合统计多条推送的推送漏斗数据</td>
        <td>2019-12-19</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1024/33775">多条任务统计数据聚合查询</a></td>
    </tr>
</table>
