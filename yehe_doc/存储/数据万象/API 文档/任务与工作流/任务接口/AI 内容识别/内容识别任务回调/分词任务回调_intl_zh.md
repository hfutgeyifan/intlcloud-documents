## 功能说明

数据万象支持自定义设置回调 URL，在任务完成后，系统向该 URL 发送 HTTP POST 请求，请求体中包含通知内容。您可通过配置的回调地址及时了解任务处理的进展和状态，以便进行其他业务操作。

## 回调内容

任务完成后，系统会向您设置的回调地址发送回调内容，该响应体返回为 **application/xml** 数据，包含完整节点数据的内容展示如下：

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Tag>WordsGeneralize</Tag>
        <Code>Success</Code>
        <CreationTime>2022-07-25T16:35:39+0800</CreationTime>
        <EndTime>2022-07-25T16:35:43+0800</EndTime>
        <Input>
            <Object>text.txt</Object>
            <BucketId>test-123456789</BucketId>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>ac34be3aa0bf411ed9ce39d7cc972e427</JobId>
        <Message>Success</Message>
        <Operation>
            <UserData>This is my WordsGeneralize job.</UserData>
            <JobLevel>0</JobLevel>
            <WordsGeneralize>
                <NerMethod>DL</NerMethod>
                <SegMethod>MIX</SegMethod>
            </WordsGeneralize>
            <WordsGeneralizeResult>
                <WordsGeneralizeLable>
                    <Category>交通</Category>
                    <Word>打车</Word>
                </WordsGeneralizeLable>
                <WordsGeneralizeToken>
                    <Length>2</Length>
                    <Offset>0</Offset>
                    <Pos>t</Pos>
                    <Word>今天</Word>
                </WordsGeneralizeToken>
                <WordsGeneralizeToken>
                    <Length>2</Length>
                    <Offset>2</Offset>
                    <Pos>v</Pos>
                    <Word>打车</Word>
                </WordsGeneralizeToken>
                <WordsGeneralizeToken>
                    <Length>1</Length>
                    <Offset>4</Offset>
                    <Pos>v</Pos>
                    <Word>花</Word>
                </WordsGeneralizeToken>
                <WordsGeneralizeToken>
                    <Length>2</Length>
                    <Offset>5</Offset>
                    <Pos>nx</Pos>
                    <Word>60</Word>
                </WordsGeneralizeToken>
                <WordsGeneralizeToken>
                    <Length>1</Length>
                    <Offset>7</Offset>
                    <Pos>q</Pos>
                    <Word>元</Word>
                </WordsGeneralizeToken>
            </WordsGeneralizeResult>
        </Operation>
    </JobsDetail>
</Response>
```

具体的数据内容如下：

| 节点名称（关键字） | 父节点 | 描述           | 类型      |
| :----------------- | :----- | :------------- | :-------- |
| Response           | 无     | 保存结果的容器 | Container |

Container 节点 Response 的内容：

| 节点名称（关键字） | 父节点   | 描述           | 类型      |
| :----------------- | :------- | :------------- | :-------- |
| EventName          | Response | 固定值，为 TaskFinish    | String |
| JobsDetail         | Response | 任务的详细信息           | Container |

Container 节点 JobsDetail 的内容：
<a href="https://intl.cloud.tencent.com/document/product/1045/49790" target="_blank">同提交分词任务接口中的 Response.JobsDetail</a>

**如果任务是通过工作流触发的，Response.JobsDetail.Input 还会包含 CosHeaders 节点，类型为 Container 数组。**

Container 节点 CosHeaders 的内容：

| 节点名称（关键字） | 父节点                               | 描述                | 类型   |
| :----------------- | :----------------------------------- | :------------------ | :----- |
| Key                | Response.JobsDetail.Input.CosHeaders | 自定义 Header 的名称  | String |
| Value              | Response.JobsDetail.Input.CosHeaders | 自定义 Header 的值 | String |

**如果任务是通过工作流触发的，Response.JobsDetail 还会包含 Workflow 节点，类型为 Container。**

Container 节点 Workflow 的内容：

| 节点名称（关键字） | 父节点                                    | 描述                                   | 类型   |
| ------------------ | ----------------------------------------- | -------------------------------------- | ------ |
| RunId              | Response.Workflow | 工作流实例 ID                    | String |
| WorkflowId         | Response.Workflow | 工作流 ID                       | String |
| WorkflowName       | Response.Workflow | 工作流名称                      | String |
| Name               | Response.Workflow | 工作流节点名称                   | String |

## 实际案例

### 案例 1：通过任务接口触发的任务回调

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Tag>WordsGeneralize</Tag>
        <Code>Success</Code>
        <CreationTime>2022-07-25T16:35:39+0800</CreationTime>
        <EndTime>2022-07-25T16:35:43+0800</EndTime>
        <Input>
            <Object>text.txt</Object>
            <BucketId>test-123456789</BucketId>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>ac34be3aa0bf411ed9ce39d7cc972e427</JobId>
        <Message>Success</Message>
        <Operation>
            <UserData>This is my WordsGeneralize job.</UserData>
            <JobLevel>0</JobLevel>
            <WordsGeneralize>
                <NerMethod>DL</NerMethod>
                <SegMethod>MIX</SegMethod>
            </WordsGeneralize>
            <WordsGeneralizeResult>
                <WordsGeneralizeLable>
                    <Category>交通</Category>
                    <Word>打车</Word>
                </WordsGeneralizeLable>
                <WordsGeneralizeToken>
                    <Length>2</Length>
                    <Offset>0</Offset>
                    <Pos>t</Pos>
                    <Word>今天</Word>
                </WordsGeneralizeToken>
                <WordsGeneralizeToken>
                    <Length>2</Length>
                    <Offset>2</Offset>
                    <Pos>v</Pos>
                    <Word>打车</Word>
                </WordsGeneralizeToken>
                <WordsGeneralizeToken>
                    <Length>1</Length>
                    <Offset>4</Offset>
                    <Pos>v</Pos>
                    <Word>花</Word>
                </WordsGeneralizeToken>
                <WordsGeneralizeToken>
                    <Length>2</Length>
                    <Offset>5</Offset>
                    <Pos>nx</Pos>
                    <Word>60</Word>
                </WordsGeneralizeToken>
                <WordsGeneralizeToken>
                    <Length>1</Length>
                    <Offset>7</Offset>
                    <Pos>q</Pos>
                    <Word>元</Word>
                </WordsGeneralizeToken>
            </WordsGeneralizeResult>
        </Operation>
    </JobsDetail>
</Response>
```

### 案例 2：通过任务触发的任务回调, 格式为 JSON

```plaintext
{
    "Response": {
        "EventName": "TaskFinish",
        "JobsDetail": {
            "Code": "Success",
            "CreationTime": "2022-07-25T16:35:39+0800",
            "EndTime": "2022-07-25T16:35:43+0800",
            "Input": {
                "Object": "text.txt",
                "BucketId": "test-123456789",
                "Region": "ap-chongqing"
            },
            "JobId": "ac34be3aa0bf411ed9ce39d7cc972e427",
            "Message": "Success",
            "Operation": {
                "JobLevel": "0",
                "WordsGeneralize": {
                    "NerMethod": "DL",
                    "SegMethod": "MIX"
                },
                "WordsGeneralizeResult": {
                    "WordsGeneralizeLable": {
                        "Category": "交通",
                        "Word": "打车"
                    },
                    "WordsGeneralizeToken": [{
                            "Length": "2",
                            "Offset": "0",
                            "Pos": "t",
                            "Word": "今天"
                        },
                        {
                            "Length": "2",
                            "Offset": "2",
                            "Pos": "v",
                            "Word": "打车"
                        },
                        {
                            "Length": "1",
                            "Offset": "4",
                            "Pos": "v",
                            "Word": "花"
                        },
                        {
                            "Length": "2",
                            "Offset": "5",
                            "Pos": "nx",
                            "Word": "60"
                        },
                        {
                            "Length": "1",
                            "Offset": "7",
                            "Pos": "q",
                            "Word": "元"
                        }
                    ]
                }
            }
        }
    }
}
```
