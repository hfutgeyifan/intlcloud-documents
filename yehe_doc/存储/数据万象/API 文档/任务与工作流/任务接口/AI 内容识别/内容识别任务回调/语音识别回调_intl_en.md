## Feature Overview

CI supports user-defined callback URLs. After a task is completed, the system sends an HTTP POST request whose body contains notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the task so that you can perform other operations as needed.

## Callback Content

After the task is completed, the system sends the callback content to the callback URL that you configure. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <State>Success</State>
        <Tag>SpeechRecognition</Tag>
        <Code>Success</Code>
        <CreationTime>2022-09-02T10:25:38+0800</CreationTime>
        <StartTime>2022-09-02T10:25:39+0800</StartTime>
        <EndTime>2022-09-02T10:25:46+0800</EndTime>
        <Input>
            <BucketId>test-1234567890</BucketId>
            <Object>minnong.mp3</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>s886c0a7c2a6611ed847a618901112dcf</JobId>
        <QueueId>pe91d0af11fc14337987ff0c34f8b0886</QueueId>
        <Message/>
        <Operation>
            <UserData>This is my SpeechRecognition job.</UserData>
            <JobLevel>0</JobLevel>
            <Output>
                <Bucket>test-1234567890</Bucket>
                <Object>/example.txt</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <SpeechRecognitionResult>
                <AudioTime>19.7124</AudioTime>
                <DetailObjectName>/example.txt.detail</DetailObjectName>
                <ObjectName>/example.txt</ObjectName>
                <Result>[0:3.320,0:19.712]  minnong, lishen, chuheridangwu, handihexiatu. shuizhipanzhongcan, lilijiexinku.</Result>
                <ResultDetail>
                    <EndMs>19712</EndMs>
                    <FinalSentence>minnong, lishen, chuheridangwu, handihexiatu. shuizhipanzhongcan, lilijiexinku.</FinalSentence>
                    <SliceSentence>min nong , li shen , chuhe ri dangwu , handi he xia tu . shuizhi panzhongcan , lili jie xinku .</SliceSentence>
                    <SpeakerId>0</SpeakerId>
                    <SpeechSpeed>2.4</SpeechSpeed>
                    <StartMs>3320</StartMs>
                    <Words>
                        <OffsetEndMs>2190</OffsetEndMs>
                        <OffsetStartMs>0</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>min</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>2625</OffsetEndMs>
                        <OffsetStartMs>2190</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>nong</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>2625</OffsetEndMs>
                        <OffsetStartMs>2190</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>,</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>3060</OffsetEndMs>
                        <OffsetStartMs>2625</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>li</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>3825</OffsetEndMs>
                        <OffsetStartMs>3060</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>shen</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>3825</OffsetEndMs>
                        <OffsetStartMs>3060</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>,</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>5040</OffsetEndMs>
                        <OffsetStartMs>3825</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>chuhe</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>5475</OffsetEndMs>
                        <OffsetStartMs>5040</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>ri</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>6390</OffsetEndMs>
                        <OffsetStartMs>5475</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>dangwu</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>6390</OffsetEndMs>
                        <OffsetStartMs>5475</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>,</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>7365</OffsetEndMs>
                        <OffsetStartMs>6390</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>handi</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>7755</OffsetEndMs>
                        <OffsetStartMs>7365</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>he</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>8130</OffsetEndMs>
                        <OffsetStartMs>7755</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>xia</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>8850</OffsetEndMs>
                        <OffsetStartMs>8130</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>tu</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>8850</OffsetEndMs>
                        <OffsetStartMs>8130</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>.</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>9915</OffsetEndMs>
                        <OffsetStartMs>8850</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>shuizhi</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>11130</OffsetEndMs>
                        <OffsetStartMs>9915</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>panzhongcan</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>11130</OffsetEndMs>
                        <OffsetStartMs>9915</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>,</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>12045</OffsetEndMs>
                        <OffsetStartMs>11130</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>lili</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>12540</OffsetEndMs>
                        <OffsetStartMs>12045</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>jie</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>14745</OffsetEndMs>
                        <OffsetStartMs>12540</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>xinku</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>14745</OffsetEndMs>
                        <OffsetStartMs>12540</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>.</Word>
                    </Words>
                    <WordsNum>22</WordsNum>
                </ResultDetail>
            </SpeechRecognitionResult>
            <TemplateId>t14aea553bb55c468b963fafa472afc538</TemplateId>
            <TemplateName>test</TemplateName>
        </Operation>
    </JobsDetail>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------- | :-------- |
| EventName          | Response | Fixed value: `TaskFinish`.    | String |
| JobsDetail | Response | Job details |  Container |

`JobsDetail` has the following sub-nodes:
Same as the `Response.JobsDetail` in the speech recognition job submitting API.

**If the job is triggered by a workflow, `Response.JobsDetail.Input` will also contain a `CosHeaders` node of the container array type.**

`CosHeaders` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------------- | :------------------ | :----- |
| Key                | Response.JobsDetail.Input.CosHeaders | Name of the custom header  | String |
| Value              | Response.JobsDetail.Input.CosHeaders | Value of the custom header | String |

**If the job is triggered by a workflow, `Response.JobsDetail` will also contain a `Workflow` node of the container type.**

`Workflow` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ----------------------------------------- | -------------------------------------- | ------ |
| RunId              | Response.Workflow | Workflow instance ID                    | String |
| WorkflowId         | Response.Workflow | Workflow ID                       | String |
| WorkflowName       | Response.Workflow | Workflow name                      | String |
| Name               | Response.Workflow | Workflow node name                   | String |

## Examples

### Sample 1: Job callback triggered by a job API

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <State>Success</State>
        <Tag>SpeechRecognition</Tag>
        <Code>Success</Code>
        <CreationTime>2022-09-02T10:25:38+0800</CreationTime>
        <StartTime>2022-09-02T10:25:39+0800</StartTime>
        <EndTime>2022-09-02T10:25:46+0800</EndTime>
        <Input>
            <BucketId>test-1234567890</BucketId>
            <Object>minnong.mp3</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>s886c0a7c2a6611ed847a618901112dcf</JobId>
        <QueueId>pe91d0af11fc14337987ff0c34f8b0886</QueueId>
        <Message/>
        <Operation>
            <UserData>This is my SpeechRecognition job.</UserData>
            <JobLevel>0</JobLevel>
            <Output>
                <Bucket>test-1234567890</Bucket>
                <Object>/example.txt</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <SpeechRecognitionResult>
                <AudioTime>19.7124</AudioTime>
                <DetailObjectName>/example.txt.detail</DetailObjectName>
                <ObjectName>/example.txt</ObjectName>
                <Result>[0:3.320,0:19.712]  minnong, lishen, chuheridangwu, handihexiatu. shuizhipanzhongcan, lilijiexinku.</Result>
                <ResultDetail>
                    <EndMs>19712</EndMs>
                    <FinalSentence>minnong, lishen, chuheridangwu, handihexiatu. shuizhipanzhongcan, lilijiexinku.</FinalSentence>
                    <SliceSentence>min nong , li shen , chuhe ri dangwu , handi he xia tu . shuizhi panzhongcan , lili jie xinku .</SliceSentence>
                    <SpeakerId>0</SpeakerId>
                    <SpeechSpeed>2.4</SpeechSpeed>
                    <StartMs>3320</StartMs>
                    <Words>
                        <OffsetEndMs>2190</OffsetEndMs>
                        <OffsetStartMs>0</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>min</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>2625</OffsetEndMs>
                        <OffsetStartMs>2190</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>nong</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>2625</OffsetEndMs>
                        <OffsetStartMs>2190</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>,</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>3060</OffsetEndMs>
                        <OffsetStartMs>2625</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>li</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>3825</OffsetEndMs>
                        <OffsetStartMs>3060</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>shen</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>3825</OffsetEndMs>
                        <OffsetStartMs>3060</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>,</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>5040</OffsetEndMs>
                        <OffsetStartMs>3825</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>chuhe</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>5475</OffsetEndMs>
                        <OffsetStartMs>5040</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>ri</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>6390</OffsetEndMs>
                        <OffsetStartMs>5475</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>dangwu</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>6390</OffsetEndMs>
                        <OffsetStartMs>5475</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>,</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>7365</OffsetEndMs>
                        <OffsetStartMs>6390</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>handi</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>7755</OffsetEndMs>
                        <OffsetStartMs>7365</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>he</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>8130</OffsetEndMs>
                        <OffsetStartMs>7755</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>xia</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>8850</OffsetEndMs>
                        <OffsetStartMs>8130</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>tu</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>8850</OffsetEndMs>
                        <OffsetStartMs>8130</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>.</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>9915</OffsetEndMs>
                        <OffsetStartMs>8850</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>shuizhi</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>11130</OffsetEndMs>
                        <OffsetStartMs>9915</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>panzhongcan</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>11130</OffsetEndMs>
                        <OffsetStartMs>9915</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>,</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>12045</OffsetEndMs>
                        <OffsetStartMs>11130</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>lili</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>12540</OffsetEndMs>
                        <OffsetStartMs>12045</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>jie</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>14745</OffsetEndMs>
                        <OffsetStartMs>12540</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>xinku</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>14745</OffsetEndMs>
                        <OffsetStartMs>12540</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>.</Word>
                    </Words>
                    <WordsNum>22</WordsNum>
                </ResultDetail>
            </SpeechRecognitionResult>
            <TemplateId>t14aea553bb55c468b963fafa472afc538</TemplateId>
            <TemplateName>test</TemplateName>
        </Operation>
    </JobsDetail>
</Response>
```

### Sample 2: Job callback triggered by a workflow

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-09-02T10:25:38+0800</CreationTime>
        <EndTime>2022-09-02T10:25:46+0800</EndTime>
        <Input>
            <BucketId>test-1234567890</BucketId>
            <Object>minnong.mp3</Object>
            <Region>ap-chongqing</Region>
            <CosHeaders>
                <Key>Content-Type</Key>
                <Value>Audio/mp3</Value>
            </CosHeaders>
            <CosHeaders>
                <Key>x-cos-request-id</Key>
                <Value>NjJiZDYwYTFfNjUzYTYyNjRfZjEwZl8xMmZhYzY5</Value>
            </CosHeaders>
            <CosHeaders>
                <Key>EventName</Key>
                <Value>cos:ObjectCreated:Put</Value>
            </CosHeaders>
            <CosHeaders>
                <Key>Size</Key>
                <Value>1424687</Value>
            </CosHeaders>
        </Input>
        <JobId>s886c0a7c2a6611ed847a618901112dcf</JobId>
        <Message/>
        <Operation>
            <UserData>This is my SpeechRecognition job.</UserData>
            <JobLevel>0</JobLevel>
            <Output>
                <Bucket>test-1234567890</Bucket>
                <Object>/example.txt</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <SpeechRecognitionResult>
                <AudioTime>19.7124</AudioTime>
                <DetailObjectName>/example.txt.detail</DetailObjectName>
                <ObjectName>/example.txt</ObjectName>
                <Result>[0:3.320,0:19.712]  minnong, lishen, chuheridangwu, handihexiatu. shuizhipanzhongcan, lilijiexinku.</Result>
                <ResultDetail>
                    <EndMs>19712</EndMs>
                    <FinalSentence>minnong, lishen, chuheridangwu, handihexiatu. shuizhipanzhongcan, lilijiexinku.</FinalSentence>
                    <SliceSentence>min nong , li shen , chuhe ri dangwu , handi he xia tu . shuizhi panzhongcan , lili jie xinku .</SliceSentence>
                    <SpeakerId>0</SpeakerId>
                    <SpeechSpeed>2.4</SpeechSpeed>
                    <StartMs>3320</StartMs>
                    <Words>
                        <OffsetEndMs>2190</OffsetEndMs>
                        <OffsetStartMs>0</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>min</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>2625</OffsetEndMs>
                        <OffsetStartMs>2190</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>nong</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>2625</OffsetEndMs>
                        <OffsetStartMs>2190</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>,</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>3060</OffsetEndMs>
                        <OffsetStartMs>2625</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>li</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>3825</OffsetEndMs>
                        <OffsetStartMs>3060</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>shen</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>3825</OffsetEndMs>
                        <OffsetStartMs>3060</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>,</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>5040</OffsetEndMs>
                        <OffsetStartMs>3825</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>chuhe</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>5475</OffsetEndMs>
                        <OffsetStartMs>5040</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>ri</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>6390</OffsetEndMs>
                        <OffsetStartMs>5475</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>dangwu</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>6390</OffsetEndMs>
                        <OffsetStartMs>5475</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>,</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>7365</OffsetEndMs>
                        <OffsetStartMs>6390</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>handi</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>7755</OffsetEndMs>
                        <OffsetStartMs>7365</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>he</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>8130</OffsetEndMs>
                        <OffsetStartMs>7755</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>xia</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>8850</OffsetEndMs>
                        <OffsetStartMs>8130</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>tu</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>8850</OffsetEndMs>
                        <OffsetStartMs>8130</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>.</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>9915</OffsetEndMs>
                        <OffsetStartMs>8850</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>shuizhi</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>11130</OffsetEndMs>
                        <OffsetStartMs>9915</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>panzhongcan</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>11130</OffsetEndMs>
                        <OffsetStartMs>9915</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>,</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>12045</OffsetEndMs>
                        <OffsetStartMs>11130</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>lili</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>12540</OffsetEndMs>
                        <OffsetStartMs>12045</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>jie</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>14745</OffsetEndMs>
                        <OffsetStartMs>12540</OffsetStartMs>
                        <VoiceType>0</VoiceType>
                        <Word>xinku</Word>
                    </Words>
                    <Words>
                        <OffsetEndMs>14745</OffsetEndMs>
                        <OffsetStartMs>12540</OffsetStartMs>
                        <VoiceType>1</VoiceType>
                        <Word>.</Word>
                    </Words>
                    <WordsNum>22</WordsNum>
                </ResultDetail>
            </SpeechRecognitionResult>
            <TemplateId>t14aea553bb55c468b963fafa472afc538</TemplateId>
            <TemplateName>test</TemplateName>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-09-02T10:25:39+0800</StartTime>
        <State>Success</State>
        <Tag>SpeechRecognition</Tag>
        <Workflow>
            <Name>SpeechRecognition_1581665960537</Name>
            <RunId>ic90edd59f84f11ec9d4f525400a3c59f</RunId>
            <WorkflowId>web6ac56c1ef54dbfa44d7f4103203be9</WorkflowId>
            <WorkflowName>workflow-test</WorkflowName>
        </Workflow>
    </JobsDetail>
</Response>
```

### Sample 3: Job callback in JSON format triggered by a workflow

```plaintext
{
	"EventName": "TaskFinish",
	"JobsDetail": {
		"Code": "Success",
		"CreationTime": "2022-09-02T10:25:38+0800",
		"EndTime": "2022-09-02T10:25:46+0800",
		"Input":{
			"BucketId": "test-1234567890",
			"Object": "minnong.mp3",
			"Region": "ap-chongqing",
			"CosHeaders": [{
					"Key": "Content-Type",
					"Value": "Audio/mp3"
				},
				{
					"Key": "x-cos-request-id",
					"Value": "NjJiZDYwYTFfNjUzYTYyNjRfZjEwZl8xMmZhYzY5"
				},
				{
					"Key": "EventName",
					"Value": "cos:ObjectCreated:Put"
				},
				{
					"Key": "Size",
					"Value": "1424687"
				}
			]
		},
		"JobId": "s886c0a7c2a6611ed847a618901112dcf",
		"Operation": {
			"UserData": "This is my SpeechRecognition job.",
			"JobLevel": "0",
			"Output":{
				"Bucket": "test-1234567890",
				"Object": "/example.txt",
				"Region": "ap-chongqing"
			},
			"SpeechRecognitionResult": {
				"AudioTime": "19.7124",
				"DetailObjectName": "/example.txt.detail",
				"ObjectName": "/example.txt",
				"Result": "[0:3.320,0:19.712]  minnong, lishen, chuheridangwu, handihexiatu. shuizhipanzhongcan, lilijiexinku.",
				"ResultDetail": {
					"EndMs": "19712",
					"FinalSentence": "minnong, lishen, chuheridangwu, handihexiatu. shuizhipanzhongcan, lilijiexinku.",
					"SliceSentence": "min nong , li shen , chuhe ri dangwu , handi he xia tu . shuizhi panzhongcan , lili jie xinku .",
					"SpeakerId": "0",
					"SpeechSpeed": "2.4",
					"StartMs": "3320",
					"Words": [{
							"OffsetEndMs": "2190",
							"OffsetStartMs": "0",
							"VoiceType": "0",
							"Word": "min"
						},
						{
							"OffsetEndMs": "2625",
							"OffsetStartMs": "2190",
							"VoiceType": "0",
							"Word": "nong"
						},
						{
							"OffsetEndMs": "2625",
							"OffsetStartMs": "2190",
							"VoiceType": "1",
							"Word": ","
						},
						{
							"OffsetEndMs": "3060",
							"OffsetStartMs": "2625",
							"VoiceType": "0",
							"Word": "li"
						},
						{
							"OffsetEndMs": "3825",
							"OffsetStartMs": "3060",
							"VoiceType": "0",
							"Word": "shen"
						},
						{
							"OffsetEndMs": "3825",
							"OffsetStartMs": "3060",
							"VoiceType": "1",
							"Word": ","
						},
						{
							"OffsetEndMs": "5040",
							"OffsetStartMs": "3825",
							"VoiceType": "0",
							"Word": "chuhe"
						},
						{
							"OffsetEndMs": "5475",
							"OffsetStartMs": "5040",
							"VoiceType": "0",
							"Word": "ri"
						},
						{
							"OffsetEndMs": "6390",
							"OffsetStartMs": "5475",
							"VoiceType": "0",
							"Word": "dangwu"
						},
						{
							"OffsetEndMs": "6390",
							"OffsetStartMs": "5475",
							"VoiceType": "1",
							"Word": ","
						},
						{
							"OffsetEndMs": "7365",
							"OffsetStartMs": "6390",
							"VoiceType": "0",
							"Word": "handi"
						},
						{
							"OffsetEndMs": "7755",
							"OffsetStartMs": "7365",
							"VoiceType": "0",
							"Word": "he"
						},
						{
							"OffsetEndMs": "8130",
							"OffsetStartMs": "7755",
							"VoiceType": "0",
							"Word": "xia"
						},
						{
							"OffsetEndMs": "8850",
							"OffsetStartMs": "8130",
							"VoiceType": "0",
							"Word": "tu"
						},
						{
							"OffsetEndMs": "8850",
							"OffsetStartMs": "8130",
							"VoiceType": "1",
							"Word": "."
						},
						{
							"OffsetEndMs": "9915",
							"OffsetStartMs": "8850",
							"VoiceType": "0",
							"Word": "shuizhi"
						},
						{
							"OffsetEndMs": "11130",
							"OffsetStartMs": "9915",
							"VoiceType": "0",
							"Word": "panzhongcan"
						},
						{
							"OffsetEndMs": "11130",
							"OffsetStartMs": "9915",
							"VoiceType": "1",
							"Word": ","
						},
						{
							"OffsetEndMs": "12045",
							"OffsetStartMs": "11130",
							"VoiceType": "0",
							"Word": "lili"
						},
						{
							"OffsetEndMs": "12540",
							"OffsetStartMs": "12045",
							"VoiceType": "0",
							"Word": "jie"
						},
						{
							"OffsetEndMs": "14745",
							"OffsetStartMs": "12540",
							"VoiceType": "0",
							"Word": "xinku"
						},
						{
							"OffsetEndMs": "14745",
							"OffsetStartMs": "12540",
							"VoiceType": "1",
							"Word": "."
						}
					],
					"WordsNum": "22"
				}
			},
			"TemplateId": "t14aea553bb55c468b963fafa472afc538",
			"TemplateName": "test"
		},
		"QueueId": "p2242ab62c7c94486915508540933a2c6",
		"StartTime": "2022-09-02T10:25:39+0800",
		"State": "Success",
		"Tag": "SpeechRecognition",
		"Workflow": {
			"Name": "SpeechRecognition_1581665960537",
			"RunId": "ic90edd59f84f11ec9d4f525400a3c59f",
			"WorkflowId": "web6ac56c1ef54dbfa44d7f4103203be9",
			"WorkflowName": "workflow-test"
		}
	}
}
```
