開発者がGME製品APIのデバッグ・アクセスを行いやすいように、ここで、Unity開発に適用されるクイックアクセス技術ドキュメントを説明します。

GMEクイックスタート文書は、ユーザーがアクセスDemoを参照してアクセスするのを支援するための最も主要なアクセスインターフェースのみを提供しています。


## GME利用上の重要事項

GMEは2つの部分に分かれます。リアルタイム音声サービス、音声メッセージおよびテキスト変換サービスを提供しており、これらのサービスの利用はInitやPollなどのコアインターフェースに依存しています。

<dx-alert infotype="notice" title="关于 Init 接口">
例えば、リアルタイムの音声サービスを使用する同時に音声メッセージ・サービスも使用する場合、**Init初期化インターフェースを1回だけ呼び出す必要があります**。
</dx-alert>

###　インターフェース呼び出しのフローチャート

![image](https://qcloudimg.tencent-cloud.cn/raw/20564e5a251c6a53a06fa2b660a93061.png)

### 統合の手順

####　コアインターフェース


<dx-tag-link link="#Init" tag="接口：Init">GMEの初期化</dx-tag-link>
<dx-tag-link link="#Poll" tag="接口：Poll">定期的なPoll呼び出しによるコールバックのトリガー</dx-tag-link>

#### リアルタイム音声

<dx-steps>
-<dx-tag-link link="#EnterRoom" tag="接口：EnterRoom">リアルタイム音声ルームへの参加</dx-tag-link>
-<dx-tag-link link="#EnableMic" tag="接口：EnableMic">マイクのオン/オフ</dx-tag-link>
-<dx-tag-link link="#EnableSpeaker" tag="接口：EnableSpeaker">スピーカーのオン/オフ</dx-tag-link>
-<dx-tag-link link="#ExitRoom" tag="接口：ExitRoom">音声ルーム退出</dx-tag-link>
</dx-steps>

#### 音声メッセージ

<dx-steps>
-<dx-tag-link link="#ApplyPtt" tag="接口：ApplyPTTAuthbuffer">認証の初期化</dx-tag-link>
-<dx-tag-link link="#StartRWSR" tag="接口：StartRecordingWithStreamingRecognition">ストリーミング音声認識の起動</dx-tag-link>
-<dx-tag-link link="#Stop" tag="接口：StopRecording">レコーディング停止</dx-tag-link>
</dx-steps>

<dx-tag-link link="#Init" tag="接口：UnInit">GMEの録画を停止</dx-tag-link>

## コアインターフェースのアクセス

### 1. Demoのダウンロード 

ダウンロード案内ページにアクセスして、必要なクライアント<dx-tag-link link="https://cloud.tencent.com/document/product/607/18521" tag="DownLoad">Demoエンジニアリングコードをダウンロードします</dx-tag-link>。


### 2. ヘッダーファイルを取り込む

<dx-codeblock>
::: Java Java
import com.tencent.TMG.ITMGContext;
import com.tencent.av.sig.AuthBuffer;
import com.tencent.bugly.crashreport.CrashReport;
:::
::: Object-C objetctive-c
#import "GMESDK/TMGEngine.h"
#import "GMESDK/QAVAuthBuffer.h"
:::
::: C++ C++
#include "auth_buffer.h"
#include "tmg_sdk.h"
#include "AdvanceHeaders/tmg_sdk_adv.h"
#include <vector>
:::
</dx-codeblock>


### 3. シングルトンの取得

音声機能を使用する場合、先にITMGContextオブジェクトを取得してください。

####  関数のプロトタイプ 

<dx-codeblock>
::: Java Java
public static ITMGContext GetInstance(Context context)
:::
::: Object-C objetctive-c

+ (ITMGContext*) GetInstance;
  :::
  ::: C++ C++
  __UNUSED static ITMGContext* ITMGContextGetInstance(){
  return ITMGContextGetInstanceInner(TMG_SDK_VERSION);
  }
  :::
  </dx-codeblock>

####  サンプルコード  


<dx-codeblock>
::: Java Java
//MainActivity.java
import com.tencent.TMG.ITMGContext; 
ITMGContext tmgContext = ITMGContext.GetInstance(this);
:::
::: Object-C objetctive-c
//TMGSampleViewController.m
ITMGContext* _context = [ITMGContext GetInstance];
:::
::: C++ C++
ITMGContext* context = ITMGContextGetInstance();
:::
</dx-codeblock>

### 4. コールバックの設定

インターフェースクラスは、Delegateメソッドを使用して、アプリケーションにコールバック通知を送信します。コールバック関数をSDKに登録して、コールバック情報を受信します。ルームに参加する前に設定してください。

####　関数のプロトタイプとサンプルコード

コールバックの情報を受信するためのコールバックを設定します。ルームに入る前に設定してください。

<dx-codeblock>
::: Java Java
//ITMGContext
public abstract int SetTMGDelegate(ITMGDelegate delegate);

//MainActivity.java
tmgContext.SetTMGDelegate(TMGCallbackDispatcher.getInstance());
:::
::: Object-C objetctive-c
ITMGDelegate < NSObject >

//TMGSampleViewController.m
ITMGContext* _context = [ITMGContext GetInstance];
_context.TMGDelegate = [DispatchCenter getInstance];
:::
::: C++ C++
//SDKの初期化時
m_pTmgContext = ITMGContextGetInstance();
m_pTmgContext->SetTMGDelegate(this);
//デストラクタ内
CTMGSDK_For_AudioDlg::~CTMGSDK_For_AudioDlg()
{
    ITMGContextGetInstance()->SetTMGDelegate(NULL);
}
:::
</dx-codeblock>

#### コールバックの例  

コンストラクタでこのコールバック関数をオーバーライドして、コールバックパラメータを処理させます。


<dx-codeblock>
::: Java Java
//MainActivity.java
tmgContext.SetTMGDelegate(TMGCallbackDispatcher.getInstance());

//RealTimeVoiceActivity.java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
        if (type == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
		{
			//コールバック処理
		}
}

//TMGCallbackDispatcher.java、TMGCallbackHelper.javaおよびTMGDispatcherBase.javaを参考にしてください
:::
::: Object-C Object-C
//TMGRealTimeViewController.m
TMGRealTimeViewController ()< ITMGDelegate >


- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data {
  NSString *log = [NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
  [self showLog:log];
  NSLog(@"====%@====", log);
  switch (eventType) {
      // Step 6/11 : Perform the enter room event
      case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM: {
          int result = ((NSNumber*)[data objectForKey:@"result"]).intValue;
          NSString* error_info = [data objectForKey:@"error_info"];

          [self showLog:[NSString stringWithFormat:@"OnEnterRoomComplete:%d msg:(%@)", result, error_info]];
      
          if (result == 0) {
              [self updateStatusEnterRoom:YES];
          }
      }
      break;

  }
  }

//DispatchCenter.h、DispatchCenter.mを参考にしてください
:::
::: C++ C++
//ヘッダファイルにおける宣言
virtual void OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data);
//サンプルコード
void CTMGSDK_For_AudioDlg::OnEvent(ITMG_MAIN_EVENT_TYPE eventType, const char* data)
{
    switch(eventType)
    {
    case ITMG_MAIN_EVENT_TYPE_XXXX_XXXX:
        {
            //コールバックの処理
        }
        break;
    }
}
:::
</dx-codeblock>


| パラメータ |               タイプ               | 意味                     |
| ---- | :------------------------------: | ------------------------ |
| type | ITMGContext.ITMG_MAIN_EVENT_TYPE | コールバックのイベントタイプ           |
| data |         Intent メッセージタイプ          | コールバックの関連情報、イベントデータ |

### [5. SDKを初期化する](id:Init)

- このインターフェースはGMEサービスの初期化に使用され、アプリケーションの初期化時にアプリケーション側で呼び出すことをお勧めします。
- **パラメータsdkAppIdの取得については[音声サービス有効化ガイド](https://intl.cloud.tencent.com/document/product/607/39698)**をご参照ください。
- **OpenIdはユーザーを一意に識別するために使用されます。現在はINT64のみがサポートされています。ルールはApp開発者が独自に設定し、App内で重複しないようにしてください**。

#### 関数のプロトタイプ

<dx-codeblock>
::: Java Java
public abstract int Init(String sdkAppId, String openId);
:::
::: Object-C objetctive-c
-(int)InitEngine:(NSString*)sdkAppID openID:(NSString*)openID;
:::
::: C++ C++
ITMGContext virtual int Init(const char* sdkAppId, const char* openId)
:::
</dx-codeblock>


| パラメータ     |  タイプ  | 意味                                                         |
| -------- | :----: | ------------------------------------------------------------ |
| sdkAppId | String | [Tencent Cloudコンソール](https://console.cloud.tencent.com/gamegme)のGMEサービスが提供するAppId。 |
| OpenId   | String | openIdはInt64型のみをサポートします（stringに変換されて渡されます）。               |

#### サンプルコード 

<dx-codeblock>
::: Java Java
//MainActivity.java
int nRet = tmgContext.Init(appId, openId);
if (nRet == AV_OK )
{
    GMEAuthBufferHelper.getInstance().setGEMParams(appId, key, openId);
    // Step 4/11: Poll to trigger callback
    //https://cloud.tencent.com/document/product/607/15210#.E8.A7.A6.E5.8F.91.E4.BA.8B.E4.BB.B6.E5.9B.9E.E8.B0.83
    EnginePollHelper.createEnginePollHelper();
    showToast("Init success");
}else if (nRet == AV_ERR_HAS_IN_THE_STATE) // 初期化されました。この操作は成功したと考えられます。
{
    showToast("Init success");
}else
{
    showToast("Init error errorCode:" + nRet);
}
:::
::: Object-C objetctive-c
//TMGSampleViewController.m
QAVResult result = [_context InitEngine:self.appIDTF.text openID:self.openIDTF.text];
if (result == QAV_OK) {
    self.isSDKInit = YES;
}
:::
::: C++ C++
#define SDKAPPID3RD "14000xxxxx"
cosnt char* openId="10001";
ITMGContext* context = ITMGContextGetInstance();
context->Init(SDKAPPID3RD, openId);
:::
</dx-codeblock>


### [6. イベントコールバックのトリガー](id:Poll)

updateで周期的にPollを呼び出すことで、イベントのコールバックをトリガできます。GMEは定期的にPoll APIを呼び出してイベントコールバックをトリガする必要があります。Pollが呼び出されないと、SDKサービス全体が異常に動作します。

DemoのEnginePollHelper.javaファイルをご参照ください。

#### サンプルコード

<dx-codeblock>
::: Java Java
//MainActivity.java
[EnginePollHelper createEnginePollHelper];

//EnginePollHelper.java
private Handler mhandler = new Handler();
    private Runnable mRunnable = new Runnable() {
        @Override
        public void run() {
            if (s_pollEnabled) {
                if (ITMGContext.GetInstance(null) != null)
                    ITMGContext.GetInstance(null).Poll();
            }
            mhandler.postDelayed(mRunnable, 33);
        }
    };
//Pollの周期的な呼び出しについてはEnginePollHelper.javaの書き方をご参照ください
:::
::: Object-C objetctive-c
//TMGSampleViewController.m
[EnginePollHelper createEnginePollHelper];
//EnginePollHelper.mとEnginePollHelper.hを参考にしてください
:::
::: C++ C++
void TMGTestScene::update(float delta)
{
  ITMGContextGetInstance()->Poll();
}
:::
</dx-codeblock>

### 7.認証情報

関連する機能の暗号化と認証のためのAuthBufferを生成します。    
音声メッセージやテキスト変換の認証を取得する場合、ルーム番号のパラメータをnullに設定してください。

####  関数のプロトタイプ

<dx-codeblock>
::: Java Java
AuthBuffer public native byte[] genAuthBuffer(int sdkAppId, String roomId, String openId, String key)
:::
::: Object-C objetctive-c
//TMGSampleViewController.m
[EnginePollHelper createEnginePollHelper];
//EnginePollHelper.mとEnginePollHelper.hを参考にしてください
:::
::: C++ C++
void TMGTestScene::update(float delta)
{
  ITMGContextGetInstance()->Poll();
}
:::
</dx-codeblock>

| パラメータ   |  タイプ  | 意味                                                         |
| ------ | :----: | ------------------------------------------------------------ |
| appId  |  int   | Tencent CloudコンソールからのAppId番号。                              |
| roomId | string | ルーム番号であり、最大127文字まで対応しています（オフライン音声ルーム番号のパラメータをnullに設定しなければならない）。   |
| openId | string | ユーザーID。Initの場合のopenIdと同じです。                        |
| key    | string | Tencent Cloud[コンソール](https://console.cloud.tencent.com/gamegme)からの権限キー。 |


####  サンプルコード  

<dx-codeblock>
::: Java Java
//GMEAuthBufferHelper.java
import com.tencent.av.sig.AuthBuffer;//ヘッダーファイル
public byte[] createAuthBuffer(String roomId)
    {
        byte[] authBuffer;
        // Generate AuthBuffer for encryption and authentication of relevant features. For release in the production environment,
        // please use the backend deployment key as detailed in https://intl.cloud.tencent.com/document/product/607/12218
        if (TextUtils.isEmpty(roomId))
        {
            authBuffer =  AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(mAppId), "0", mOpenId, mKey);
        }else
        {
            authBuffer =  AuthBuffer.getInstance().genAuthBuffer(Integer.parseInt(mAppId), roomId, mOpenId, mKey);
        }
        return authBuffer;
    }
:::
::: Object-C objetctive-c
//リアルタイム音声認証 
NSData* authBuffer = [QAVAuthBuffer GenAuthBuffer:SDKAPPID3RD.intValue roomID:self.roomIdTF.text openID:_openId key:_key];
//音声メッセージ認証
NSData* authBuffer =  [QAVAuthBuffer GenAuthBuffer:(unsigned int)SDKAPPID3RD.integerValue roomID:nil openID:self.openId key:AUTHKEY];
:::
::: C++ C++
unsigned int bufferLen = 512;
unsigned char retAuthBuff[512] = {0};
QAVSDK_AuthBuffer_GenAuthBuffer(atoi(SDKAPPID3RD), roomId, "10001", AUTHKEY,retAuthBuff,bufferLen);
:::
</dx-codeblock>


## リアルタイム音声アクセス

###  [1. ルームに参加](id:EnterRoom)

生成された認証情報を使って入室する場合、メッセージがITMG_MAIN_EVENT_TYPE_ENTER_ROOMのコールバックを受信します。入室する際に、マイクとスピーカーはデフォルトでオフになっています。戻り値がAV_OKの場合、成功したことを示します。

ルームのオーディオタイプについては、「音質選択」(https://intl.cloud.tencent.com/document/product/607/18522)をご参照ください。

####  関数のプロトタイプ

<dx-codeblock>
::: Java Java
public abstract int EnterRoom(String roomID, int roomType, byte[] authBuffer);
:::
::: Object-C objetctive-c
-(int)EnterRoom:(NSString*) roomId roomType:(int)roomType authBuffer:(NSData*)authBuffer;
:::
::: C++ C++
ITMGContext virtual int EnterRoom(const char*  roomID, ITMG_ROOM_TYPE roomType, const char* authBuff, int buffLen);
:::
</dx-codeblock>

| パラメータ       | タイプ     | 意味                    |
| ---------- | :----: | ----------------------- |
| roomId     |String |ルーム番号、127文字まで入力可能 |
| roomType   |  int   | ルームオーディオタイプ            |
| authBuffer | byte[] | 認証コード                  |

#### サンプルコード  

<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
byte[] authBuffer =  GMEAuthBufferHelper.getInstance().createAuthBuffer(roomId);
ITMGContext.GetInstance(this).EnterRoom(roomId, roomType, authBuffer);
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m
[[ITMGContext GetInstance] EnterRoom:self.roomIdTF.text roomType:(int)self.roomTypeControl.selectedSegmentIndex + 1 authBuffer:authBuffer];
:::
::: C++ C++
ITMGContext* context = ITMGContextGetInstance();
context->EnterRoom(roomID, ITMG_ROOM_TYPE_STANDARD, (char*)retAuthBuff,bufferLen);
:::
</dx-codeblock>

#### 入室イベントのコールバック

入室後とメッセージITMG_MAIN_EVENT_TYPE_ENTER_ROOMを送信し、OnEvent関数でコールバックを判定した後に処理します。コールバックが成功した場合、その時点で正常に入室したと判定し、**課金**が開始されます。

<dx-fold-block title="计费问题参考">
[購入ガイド。](https://intl.cloud.tencent.com/document/product/607/36276)
[課金に関するよくあるご質問。](https://intl.cloud.tencent.com/document/product/607/30255)
[リアルタイム音声を使用した後、クライアントの接続が切れた場合課金は継続されますか？](https://intl.cloud.tencent.com/document/product/607/30255)
</dx-fold-block>

- **サンプルコード**  
ルーム参加イベントや接続切断イベントなど、コールバック処理の関連コードです。
<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
    if (type == ITMG_MAIN_EVENT_TYPE_ENTER_ROOM)
    {
        // Step 6/11 : Perform the enter room event
        int nErrCode = TMGCallbackHelper.ParseIntentParams2(data).nErrCode;
        String strMsg = TMGCallbackHelper.ParseIntentParams2(data).strErrMsg;
        if (nErrCode == AV_OK)
        {
            appendLog2MonitorView("EnterRomm success");
        }else
        {
            appendLog2MonitorView(String.format(Locale.getDefault(), "EnterRomm errCode:%d errMsg:%s", nErrCode, strMsg));
        }
    }
}		
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m

- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data {
  NSString *log = [NSString stringWithFormat:@"OnEvent:%d,data:%@", (int)eventType, data];
  [self showLog:log];
  NSLog(@"====%@====", log);
  switch (eventType) {
      // Step 6/11 : Perform the enter room event
      case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM: {
          int result = ((NSNumber*)[data objectForKey:@"result"]).intValue;
          NSString* error_info = [data objectForKey:@"error_info"];

          [self showLog:[NSString stringWithFormat:@"OnEnterRoomComplete:%d msg:(%@)", result, error_info]];
      
          if (result == 0) {
              [self updateStatusEnterRoom:YES];
          }
      }
      break;

  }
  :::
  ::: C++ C++
  void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
  switch (eventType) {
      case ITMG_MAIN_EVENT_TYPE_ENTER_ROOM:
      {
          ListMicDevices();
          ListSpeakerDevices();
              std::string strText = "EnterRoom complete: ret=";
          strText += data;
          m_EditMonitor.SetWindowText(MByteToWChar(strText).c_str());
          }
  }
  }
  :::
  </dx-codeblock>
- **エラーコード**
<table>
<thead>
<tr>
<th>エラーコードの値</th>
<th>原因と解決策</th>
</tr>
</thead>
<tbody><tr>
<td>7006</td>
<td>次の理由で認証に失敗しました：<ul><li>AppIDが存在しないか、エラーです</li><li>authbuff認証エラーです</li><li>認証期限切れです</li><li>openIdが仕様に準拠していません</li></ul></td>
</tr>
<tr>
<td>7007</td>
<td>他のルームにいます</td>
</tr>
<tr>
<td>1001</td>
<td>ルーム参加中でこの操作を繰り返しています。コールバックが戻るまで、ルーム参加インターフェースを呼び出さないことをお勧めします</td>
</tr>
<tr>
<td>1003</td>
<td>ルームに参加してルームにいますが、もう1回ルーム参加インターフェースを呼び出しました</td>
</tr>
<tr>
<td>1101</td>
<td>SDKが初期化されていること、openIdが規則に準拠していること、またはインターフェースが同じスレッドで呼び出されていること、およびPollインタフェースが正常に呼び出されていることを確認してください</td>
</tr>
</tbody></table>





### [2. マイクのオン/オフ](id:EnableMic)

このインターフェースは、マイクのオン/オフに使用されます。入室する際、マイクとスピーカーはデフォルトでオフになっています。

#### サンプルコード  

<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
ITMGContext.GetInstance(this).GetAudioCtrl().EnableMic(true);
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m
[[[ITMGContext GetInstance] GetAudioCtrl] EnableMic:YES];
:::
::: C++ C++
ITMGContextGetInstance()->GetAudioCtrl()->EnableMic(true);
:::
</dx-codeblock>

### [3. スピーカーのオン/オフ](id:EnableSpeaker)

このインターフェースは、スピーカーのオン/オフに使用されます。

####  サンプルコード  

<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
ITMGContext.GetInstance(this).GetAudioCtrl().EnableSpeaker(true);
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m
[[[ITMGContext GetInstance] GetAudioCtrl] EnableSpeaker:YES];
:::
::: C++ C++
ITMGContextGetInstance()->GetAudioCtrl()->EnableSpeaker(true);
:::
</dx-codeblock>


### [4. 退室](id:ExitRoom)

このインターフェースを呼び出すことで、ルームから退出できます。このインターフェースは非同期であり、戻り値がAV_OKの場合は、非同期送信が成功したことを示します。

#### サンプルコード  

<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
ITMGContext.GetInstance().ExitRoom();
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m
[[ITMGContext GetInstance] ExitRoom];
:::
::: C++ C++
ITMGContext* context = ITMGContextGetInstance();
context->ExitRoom();
:::
</dx-codeblock>


#### 退室コールバック

退室してからはコールバックが発生します、メッセージはITMG_MAIN_EVENT_TYPE_EXIT_ROOMです。サンプルコードは次の通りです：
<dx-codeblock>
::: Java Java
//RealTimeVoiceActivity.java
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVENT_TYPE_EXIT_ROOM == type)
        {
            //退室成功イベントの受信
        }
}
:::
::: Object-C objetctive-c
//TMGRealTimeViewController.m
-(void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary *)data{
NSLog(@"OnEvent:%lu,data:%@",(unsigned long)eventType,data);
switch (eventType) {
    case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM：
    {
        //退室成功イベントの受信
    }
        break;
	}
}
:::
::: C++ C++
void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
switch (eventType) {
    case ITMG_MAIN_EVENT_TYPE_EXIT_ROOM:
    {
        //処理します
        break;
        }
    }
}
:::
</dx-codeblock>



## 音声メッセージの導入


### [1. 認証初期化](id:ApplyPtt)

SDKを初期化してから認証の初期化を呼び出します。authBufferの取得については、前記のリアルタイム音声の認証情報インターフェースgenAuthBufferをご参照ください。

#### 関数のプロトタイプ  

<dx-codeblock>
::: Java Java
public abstract int ApplyPTTAuthbuffer(byte[] authBuffer);
:::
::: Object-C objetctive-c
-(QAVResult)ApplyPTTAuthbuffer:(NSData *)authBuffer;
:::
::: C++ C++
ITMGPTT virtual int ApplyPTTAuthbuffer(const char* authBuffer, int authBufferLen)
:::
</dx-codeblock>

| パラメータ       |  タイプ  | 意味 |
| ---------- | :----: | ---- |
| authBuffer | String | 認証 |

#### サンプルコード  

<dx-codeblock>
::: Java Java
//VoiceMessageRecognitionActivity.java
byte[] authBuffer = GMEAuthBufferHelper.getInstance().createAuthBuffer("");
ITMGContext.GetInstance(this).GetPTT().ApplyPTTAuthbuffer(authBuffer);
:::
::: Object-C objetctive-c
//TMGPTTViewController.m
NSData* authBuffer =  [QAVAuthBuffer GenAuthBuffer:(unsigned int)SDKAPPID3RD.integerValue roomID:nil openID:self.openId key:AUTHKEY];
[[[ITMGContext GetInstance] GetPTT] ApplyPTTAuthbuffer:authBuffer];
:::
::: C++ C++
ITMGContextGetInstance()->GetPTT()->ApplyPTTAuthbuffer(authBuffer,authBufferLen);
:::
</dx-codeblock>

### [2. ストリーミング音声認識を起動](id:StartRWSR)

このインターフェースは、ストリーミング音声識別の開始に使われています。コールバックにおいて、音声はリアルタイムでテキストに変換されて返されます。言語を指定し識別することができるし、音声から識別した情報を指定した言語に翻訳してから返すこともできます。**録音の停止にはStopRecording**を呼び出します。停止後にコールバックが発生します。

#### インターフェースのプロトタイプ  

<dx-codeblock>
::: Java Java
public abstract int StartRecordingWithStreamingRecognition (String filePath);
public abstract int StartRecordingWithStreamingRecognition (String filePath,String language,String translatelanguage);
public abstract int StopRecording();
:::
::: Object-C objetctive-c
-(int)StartRecordingWithStreamingRecognition:(NSString *)filePath;
-(int)StartRecordingWithStreamingRecognition:(NSString *)filePath language:(NSString*)speechLanguage translatelanguage:(NSString*)translatelanguage;
-(QAVResult)StopRecording;
:::
::: C++ C++
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath) 
ITMGPTT virtual int StartRecordingWithStreamingRecognition(const char* filePath,const char* translateLanguage,const char* translateLanguage)
ITMGPTT virtual int StopRecording()
:::
</dx-codeblock>


| パラメータ              |  タイプ  | 意味                                                         |
| ----------------- | :----: | ------------------------------------------------------------ |
| filePath          | String | ボイスの保存パス                                               |
| speechLanguage    | String | 指定した言語のテキストに識別するパラメータです。パラメータについては、[音声のテキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください |
| translateLanguage | String | 指定した言語のテキストに翻訳するパラメータです。パラメータについては、[音声のテキスト変換の言語パラメータ参照リスト](https://intl.cloud.tencent.com/document/product/607/30260)をご参照ください。（このパラメータは一時的に無効です。speechLanguageと同じのパラメータを入力してください） |

#### サンプルコード  

<dx-codeblock>
::: Java Java
//VoiceMessageRecognitionActivity.java
ITMGContext.GetInstance(this).GetPTT().StartRecordingWithStreamingRecognition(recordfilePath,"cmn-Hans-CN");
:::
::: Object-C objetctive-c
//TMGPTTViewController.m
QAVResult ret = [[[ITMGContext GetInstance] GetPTT] StartRecordingWithStreamingRecognition:[self pttTestPath] language:@"cmn-Hans-CN"];
if (ret == 0) {
    self.currentStatus = @"ストリーミング録音を開始します";
} else {
    self.currentStatus = @"ストリーミング録音の開始に失敗しました";
}
:::
::: C++ C++
ITMGContextGetInstance()->GetPTT()->StartRecordingWithStreamingRecognition(filePath,"cmn-Hans-CN","cmn-Hans-CN");
:::
</dx-codeblock>

#### ストリーミング音声識別コールバック

ストリーミング音声認識を開始した後、コールバック関数OnEventでコールバックメッセージを受信する必要があります。イベントメッセージは`ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE`があり、録音を停止して認識を完了した後にテキストを返します。これは、話が終わってから認識されたテキストを返すことに相当します。

OnEvent関数で、必要に応じて適切なイベントメッセージを判断します。渡されるパラメータには次の4つの情報が含まれます。

| メッセージ名称  |                    意味                     |
| --------- | :-----------------------------------------: |
| result    |    ストリーミングボイス認識が完了したかどうかを判断するための戻りコード     |
| text      |            ボイステキスト変換で認識されたテキスト             |
| file_path |             録音を保存するローカルアドレス              |
| file_id   | 録音はバックグラウンドのURLアドレスにあり、録音はサーバーで90日間保存します |

- **サンプルコード**  
<dx-codeblock>
::: Java Java
//VoiceMessageRecognitionActivity.java
import static com.tencent.TMG.ITMGContext.ITMG_MAIN_EVENT_TYPE.ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE;
public void OnEvent(ITMGContext.ITMG_MAIN_EVENT_TYPE type, Intent data) {
	if (type == ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE)
        {
            // Step 1.3/3 handle ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE event
            mIsRecording = false;
            if (nErrCode ==0)
            {
                String recordfilePath = data.getStringExtra("file_path");
                mRecFilePathView.setText(recordfilePath);

                String recordFileUrl = data.getStringExtra("file_id");
                mRecFileUrlView.setText(recordFileUrl);
            }
            else
            {
                appendLog2MonitorView("Record and recognition fail errCode:" + nErrCode);
            }
        }

}
:::
::: Object-C objetctive-c
//TMGPTTViewController.m

- (void)OnEvent:(ITMG_MAIN_EVENT_TYPE)eventType data:(NSDictionary*)data
  {
  NSNumber *number = [data objectForKey:@"result"];
  switch(eventType)
  {
  	case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE:
  	{
            if (data != NULL &&[[data objectForKey:@"result"] intValue]== 0)
            {
                self.translateTF.text = [data objectForKey:@"text"] ;
                 self.currentStatus = @"ストリーム変換が完了しました";
            }
        }
  	break;
  }
  :::
  ::: C++ C++
  void TMGTestScene::OnEvent(ITMG_MAIN_EVENT_TYPE eventType,const char* data){
    switch (eventType) {
        case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_COMPLETE:
        {
            HandleSTREAM2TEXTComplete(data,true);
            break;
        }
        ...
        case ITMG_MAIN_EVNET_TYPE_PTT_STREAMINGRECOGNITION_IS_RUNNING:
        {
            HandleSTREAM2TEXTComplete(data, false);
            break;
        }
    }
  }
  void CTMGSDK_For_AudioDlg::HandleSTREAM2TEXTComplete(const char* data, bool isComplete)
  {
    std::string strText = "STREAM2TEXT: ret=";
    strText += data;
    m_EditMonitor.SetWindowText(MByteToWChar(strText).c_str());
    Json::Reader reader;
    Json::Value root;
    bool parseRet = reader.parse(data, root);
    if (!parseRet) {
        ::SetWindowText(m_EditInfo.GetSafeHwnd(),MByteToWChar(std::string("parse result Json error")).c_str());
    }
        else
        {
            if (isComplete) {
                                ::SetWindowText(m_EditUpload.GetSafeHwnd(), MByteToWChar(root["file_id"].asString()).c_str());
                            }
                            else {
                                    std::string isruning = "STREAMINGRECOGNITION_IS_RUNNING";
                                    ::SetWindowText(m_EditUpload.GetSafeHwnd(), MByteToWChar(isruning).c_str());
                                 }
    }
  }
  :::
  </dx-codeblock>
- **エラーコード**
<table>
<thead>
<tr>
<th>エラーコード</th>
<th align="center">意味</th>
<th align="center">処理方式</th>
</tr>
</thead>
<tbody><tr>
<td>32775</td>
<td align="center">ストリーミング音声をテキストに変更できませんが、録音は成功しました</td>
<td align="center">UploadRecordedFileインターフェースを呼び出して録音をアップロードし、SpeechToTextインターフェースを呼び出して音声を文字に変換します</td>
</tr>
<tr>
<td>32777</td>
<td align="center">ストリーミング音声をテキストに変更できませんが、録音とアップロードは成功しました</td>
<td align="center">返されたメッセージには正常にアップロードしたバックグラウンドURLがあり、SpeechToTextインターフェースを呼び出して音声から文字への変換操作を行います</td>
</tr>
<tr>
<td>32786</td>
<td align="center">ストリーミング音声をテキストに変更できませんでした</td>
<td align="center">ストリーミングレコーディングステータスでは、ストリーミングレコーディングインターフェースの実行結果が返されるまで待ってください</td>
</tr>
</tbody></table>



### [3. 録音を停止](id:Stop)

このインターフェースは、録音の停止に使われています。このインターフェースが非同期インターフェースであるため、録音を停止した後には録音完了のコールバックがあります。コールバックが成功してから、録音ファイルが利用できるようになります。

#### インターフェースのプロトタイプ  

<dx-codeblock>
::: Java Java
public abstract int StopRecording();
:::
::: Object-C objetctive-c
-(QAVResult)StopRecording;
:::
::: C++ C++
ITMGPTT virtual int StopRecording();
:::
</dx-codeblock>


#### サンプルコード  

<dx-codeblock>
::: Java Java
//VoiceMessageRecognitionActivity.java
ITMGContext.GetInstance(this).GetPTT().StopRecording();
:::
::: Object-C objetctive-c
//TMGPTTViewController.m

- (void)stopRecClick {
  // Step 3/12 stop recording,  need handle ITMG_MAIN_EVNET_TYPE_PTT_RECORD_COMPLETE event
  // https://cloud.tencent.com/document/product/607/15221#.E5.81.9C.E6.AD.A2.E5.BD.95.E9.9F.B3
  QAVResult ret =  [[[ITMGContext GetInstance] GetPTT] StopRecording];
   if (ret == 0) {
       self.currentStatus = @"録音を停止します";
   } else {
        self.currentStatus = @"録音の停止に失敗しました";
   }
  }
  :::
  ::: C++ C++
  ITMGContextGetInstance()->GetPTT()->StopRecording();
  :::
  </dx-codeblock>
