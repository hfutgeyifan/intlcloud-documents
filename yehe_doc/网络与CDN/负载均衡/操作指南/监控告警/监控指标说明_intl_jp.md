Cloud Monitor（CM）は実行中のCLBインスタンスからオリジナルデータを収集し、わかりやすいチャート形式でデータを表示します。統計データはデフォルトで1か月間保存されます。インスタンスの1か月間の実行状況を観察することで、アプリケーションサービスの実行状況をより適切に把握することができます。

CLBの監視データは[CMコンソール](https://console.cloud.tencent.com/monitor/overview)で確認することをお勧めします。**クラウド製品監視** > [**Cloud Load Balancer-CLB**](https://console.cloud.tencent.com/monitor/clb)を選択し、CLBインスタンスIDをクリックして監視詳細ページに進み、そのCLBインスタンスの監視データを確認します。インスタンスを表示すると、リスナー、バックエンドサーバーなどの監視情報を確認できます。

## CLBインスタンスディメンション

| 指標の英語名          | 指標の日本語名                 | 指標の説明                                                     | 単位    | 統計粒度    |
| ------------------- | -------------------------- | ------------------------------------------------------------ | ------- | ----------- |
| ClientConnum        | クライアントからLBへのアクティブ接続数   | 統計粒度内のある時刻における、クライアントからCLBまたはリスナーへのアクティブ接続数です。 | 個      | 10、60、300 |
| ClientInactiveConn  | クライアントからLBへの非アクティブ接続数 | 統計粒度内のある時刻における、クライアントからCLBまたはリスナーへの非アクティブ接続数です。 | 個      | 10、60、300 |
| ClientConcurConn    | クライアントからLBへの同時接続数   | 統計粒度内のある時刻における、クライアントからCLBまたはリスナーへの同時接続数です。 | 個      | 10、60、300 |
| ClientNewConn       | クライアントからLBへの新規接続数   | 統計粒度内における、クライアントからCLBまたはリスナーへの新規接続数です。     | 個/秒   | 10、60、300 |
| ClientInpkg         | クライアントからLBへのインバウンドパケット       | 統計粒度内における、クライアントからCLBへの1秒あたりの送信データパケット数です。        | 個/秒   | 10、60、300 |
| ClientOutpkg        | クライアントからLBへのアウトバウンドパケット       | 統計粒度内における、CLBからクライアントへの1秒あたりの送信データパケット数です。     | 個/秒   | 10、60、300 |
| ClientAccIntraffic  | クライアントからLBへのインバウンドトラフィック       | 統計粒度内における、クライアントからCLBに流入したトラフィックです。                | MB      | 10、60、300 |
| ClientAccOuttraffic | クライアントからLBへのアウトバウンドトラフィック       |統計粒度内における、CLBからクライアントに流出したトラフィックです。                    | MB      | 10、60、300 |
| ClientOuttraffic    | クライアントからLBへのアウトバウンド帯域幅       |統計粒度内における、CLBからクライアントへの流出に使用された帯域幅です。                 | Mbps    | 10、60、300 |
| ClientIntraffic     | クライアントからLBへのインバウンド帯域幅       | 統計粒度内における、クライアントからCLBへの流入に使用された帯域幅です。             | Mbps    | 10、60、300 |
| OutTraffic          | LBからバックエンドへのアウトバウンド帯域幅          | 統計粒度内における、バックエンドRSからCLBへの流出に使用された帯域幅です。          | Mbps    | 60、300     |
| InTraffic           | LBからバックエンドへのインバウンド帯域幅          | 統計粒度内における、CLBからバックエンドRSへの流入に使用された帯域幅です。               | Mbps    | 60、300     |
| AccOuttraffic       | LBからバックエンドへのアウトバウンドトラフィック          | 統計粒度内における、CLBからバックエンドRSに流入したトラフィックです。<br/>この指標はパブリックネットワークCLBインスタンスのみサポートしており、プライベートネットワークCLBではサポートしていません。                 | MB      | 10、60、300、3600 |
| DropTotalConns      | 破棄された接続数                 | 統計粒度内における、CLBまたはリスナー上で破棄された接続数です。<br/>この指標は標準アカウントタイプのみサポートしており、従来型アカウントタイプではサポートしていません。アカウントタイプの判断方法については、[アカウントタイプの判断](https://intl.cloud.tencent.com/document/product/684/15246)をご参照ください。 | 個      | 10、60、300 |
| InDropBits          | 破棄されたインバウンド帯域幅                 | 統計粒度内における、クライアントがパブリックネットワークを経由してCLBにアクセスした際に破棄された帯域幅です。<br/>この指標は標準アカウントタイプのみサポートしており、従来型アカウントタイプではサポートしていません。アカウントタイプの判断方法については、[アカウントタイプの判断](https://intl.cloud.tencent.com/document/product/684/15246)をご参照ください。 | バイト      | 10、60、300 |
| OutDropBits         | 破棄されたアウトバウンド帯域幅                 | 統計粒度内における、CLBがパブリックネットワークにアクセスした際に破棄された帯域幅です。<br/>この指標は標準アカウントタイプのみサポートしており、従来型アカウントタイプではサポートしていません。アカウントタイプの判断方法については、[アカウントタイプの判断](https://intl.cloud.tencent.com/document/product/684/15246)をご参照ください。 | バイト      | 10、60、300 |
| InDropPkts          | 破棄されたインバウンドパケット                 | 統計粒度内における、クライアントがパブリックネットワークを経由してCLBにアクセスした際に破棄されたデータパケットです。<br/>この指標は標準アカウントタイプのみサポートしており、従来型アカウントタイプではサポートしていません。アカウントタイプの判断方法については、[アカウントタイプの判断](https://intl.cloud.tencent.com/document/product/684/15246)をご参照ください。 | 個/秒      | 10、60、300 |
| OutDropPkts         | 破棄されたアウトバウンドパケット             | 統計粒度内における、CLBがパブリックネットワークにアクセスした際に破棄されたデータパケットです。<br/>この指標は標準アカウントタイプのみサポートしており、従来型アカウントタイプではサポートしていません。アカウントタイプの判断方法については、[アカウントタイプの判断](https://intl.cloud.tencent.com/document/product/684/15246)をご参照ください。 | 個/秒      | 10、60、300 |
| DropQps      | 破棄されたQPS               | 統計粒度内における、CLBまたはリスナー上で破棄されたリクエスト数です。<br/>この指標はレイヤー7リスナー独自の指標です。標準アカウントタイプのみサポートしており、従来型アカウントタイプではサポートしていません。アカウントタイプの判断方法については、[アカウントタイプの判断](https://intl.cloud.tencent.com/document/product/684/15246)をご参照ください。 | 個      | 60、300 |
| ReqAvg              | 平均リクエスト時間               | 統計粒度内における、CLBの平均リクエスト時間です。<br/>この指標はレイヤー7リスナー独自の指標です。 | ミリ秒    | 60、300     |
| ReqMax              | 最大リクエスト時間               | 統計粒度内における、CLBの最大リクエスト時間です。 <br/>この指標はレイヤー7リスナー独自の指標です。 | ミリ秒    | 60、300     |
| RspAvg              | 平均応答時間               | 統計粒度内における、CLBの平均応答時間です。 <br/>この指標はレイヤー7リスナー独自の指標です。 | ミリ秒    | 60、300     |
| RspMax              | 最大応答時間               | 統計粒度内における、CLBの最大応答時間です。 <br/>この指標はレイヤー7リスナー独自の指標です。 | ミリ秒    | 60、300     |
| RspTimeout          | 応答タイムアウト数               | 統計粒度内における、CLBの応答タイムアウト数です。 <br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分    | 60、300     |
| SuccReq             | 1分あたりの成功リクエスト数           | 統計粒度内における、CLBの1分あたりの成功リクエスト数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分    | 60、300     |
| TotalReq            | 1秒あたりのリクエスト数                 | 統計粒度内における、CLBの1秒あたりのリクエスト数です。  <br/>この指標はレイヤー7リスナー独自の指標です。 | 個      | 60、300     |
| ClbHttp3xx          | CLBが返した3xxステータスコード      | 統計粒度内における、CLBが返した3xxステータスコードの数（CLBとバックエンドサーバーの戻りコードの和）です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| ClbHttp4xx          | CLBが返した4xxステータスコード      | 統計粒度内における、CLBが返した4xxステータスコードの数（CLBとバックエンドサーバーの戻りコードの和）です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| ClbHttp5xx          | CLBが返した5xxステータスコード      | 統計粒度内における、CLBが返した5xxステータスコードの数（CLBとバックエンドサーバーの戻りコードの和）です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| ClbHttp404          | CLBが返した404ステータスコード      | 統計粒度内における、CLBが返した404ステータスコードの数（CLBとバックエンドサーバーの戻りコードの和）です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| ClbHttp499          | CLBが返した499ステータスコード      | 統計粒度内における、CLBが返した499ステータスコードの数（CLBとバックエンドサーバーの戻りコードの和）です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| ClbHttp502          | CLBが返した502ステータスコード      | 統計粒度内における、CLBが返した502ステータスコードの数（CLBとバックエンドサーバーの戻りコードの和）です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| ClbHttp503          | CLBが返した503ステータスコード      | 統計粒度内における、CLBが返した503ステータスコードの数（CLBとバックエンドサーバーの戻りコードの和）です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| ClbHttp504          | CLBが返した504ステータスコード      | 統計粒度内における、CLBが返した504ステータスコードの数（CLBとバックエンドサーバーの戻りコードの和）です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http2xx             | 2xxステータスコード                 | 統計粒度内における、バックエンドサーバーが返した2xxステータスコードの数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http3xx             | 3xxステータスコード                 | 統計粒度内における、バックエンドサーバーが返した3xxステータスコードの数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http4xx             | 4xxステータスコード                 | 統計粒度内における、バックエンドサーバーが返した4xxステータスコードの数です。 <br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http5xx             | 5xxステータスコード                 | 統計粒度内における、バックエンドサーバーが返した5xxステータスコードの数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http404             | 404ステータスコード                 | 統計粒度内における、バックエンドサーバーが返した404ステータスコードの数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http499             | 499ステータスコード                 | 統計粒度内における、バックエンドサーバーが返した499ステータスコードの数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http502             | 502ステータスコード                 | 統計粒度内における、バックエンドサーバーが返した502ステータスコードの数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http503             | 503ステータスコード                 | 統計粒度内における、バックエンドサーバーが返した503ステータスコードの数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http504             | 504ステータスコード                 | 統計粒度内における、バックエンドサーバーが返した504ステータスコードの数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
|UnhealthRsCount|	ヘルスチェック異常数	|統計周期内の、CLBのヘルスチェック異常数です。|	個	|60、300|



## レイヤー4リスナー（TCP/UDP）ディメンション
レイヤー4リスナーは以下の3つのディメンションで、下表の各監視指標の確認をサポートします。
- リスナーディメンションです。
- バックエンドCVMディメンションです。
- バックエンドCVMポートディメンションです。

| 指標の英語名          | 指標の日本語名                 | 指標の説明                                                     | 単位    | 統計粒度    |
| ------------------- | -------------------------- | ------------------------------------------------------------ | ------- | ----------- |
| ClientConnum        | クライアントからLBへのアクティブ接続数   | 統計粒度内のある時刻における、クライアントからCLBまたはリスナーへのアクティブ接続数です。 | 個      | 10、60、300 |
| ClientNewConn       | クライアントからLBへの新規接続数   | 統計粒度内における、クライアントからCLBまたはリスナーへの新規接続数です。     | 個/秒   | 10、60、300 |
| ClientInpkg         | クライアントからLBへのインバウンドパケット       | 統計粒度内における、クライアントからCLBへの1秒あたりの送信データパケット数です。        | 個/秒   | 10、60、300 |
| ClientOutpkg        | クライアントからLBへのアウトバウンドパケット       | 統計粒度内における、CLBからクライアントへの1秒あたりの送信データパケット数です。     | 個/秒   | 10、60、300 |
| ClientAccIntraffic  | クライアントからLBへのインバウンドトラフィック       | 統計粒度内における、クライアントからCLBに流入したトラフィックです。                | MB      | 10、60、300 |
| ClientAccOuttraffic | クライアントからLBへのアウトバウンドトラフィック       |統計粒度内における、CLBからクライアントに流出したトラフィックです。                    | MB      | 10、60、300 |
| ClientOuttraffic    | クライアントからLBへのアウトバウンド帯域幅       |統計粒度内における、CLBからクライアントへの流出に使用された帯域幅です。                 | Mbps    | 10、60、300 |
| ClientIntraffic     | クライアントからLBへのインバウンド帯域幅       | 統計粒度内における、クライアントからCLBに流入したトラフィックです。             | Mbps    | 10、60、300 |
| OutTraffic          | LBからバックエンドへのアウトバウンド帯域幅          | 統計粒度内における、バックエンドRSからCLBへの流出に使用された帯域幅です。          | Mbps    | 60、300     |
| InTraffic           | LBからバックエンドへのインバウンド帯域幅          | 統計粒度内における、CLBからバックエンドRSへの流入に使用された帯域幅です。               | Mbps    | 60、300     |
| OutPkg              | LBからバックエンドへのアウトバウンドパケット          | 統計粒度内における、バックエンドRSからCLBへの1秒あたりの送信データパケット数です。      | 個/秒   | 60、300     |
| InPkg               | LBからバックエンドへのインバウンドパケット          |統計粒度内における、CLBからバックエンドRSへの1秒あたりの送信データパケット数です。   | 個/秒   | 60、300     |
| AccOuttraffic       | LBからバックエンドへのアウトバウンドトラフィック          | 統計粒度内における、CLBからバックエンドRSに流入したトラフィックです。<br/>この指標はパブリックネットワークCLBインスタンスのみサポートしており、プライベートネットワークCLBではサポートしていません。                 | MB      | 10、60、300、3600 |
| ConNum              | LBからバックエンドへの接続数          | 統計粒度内における、CLBからバックエンドRSへの接続数です。                 | 個      | 60、300     |
| NewConn             | LBからバックエンドへの新規接続数      | 統計粒度内における、CLBからバックエンドRSへの新規接続数です。             | 個/分 | 60、300     |
|UnhealthRsCount|	ヘルスチェック異常数	|統計周期内の、CLBのヘルスチェック異常数です。|	個	|60、300|



## レイヤー7リスナー（HTTP/HTTPS）ディメンション
レイヤー7リスナーは以下の5つのディメンションで、下表の各監視指標の確認をサポートします。
- リスナーディメンションです。
- バックエンドCVMディメンションです。
- バックエンドCVMポートディメンションです。

| 指標の英語名          | 指標の日本語名                 | 指標の説明                                                     | 単位    | 統計粒度    |
| ------------------- | -------------------------- | ------------------------------------------------------------ | ------- | ----------- |
| ClientConnum        | クライアントからLBへのアクティブ接続数   | 統計粒度内のある時刻における、クライアントからCLBまたはリスナーへのアクティブ接続数です。 | 個      | 10、60、300 |
| ClientNewConn       | クライアントからLBへの新規接続数   | 統計粒度内における、クライアントからCLBまたはリスナーへの新規接続数です。     | 個/秒   | 10、60、300 |
| ClientInpkg         | クライアントからLBへのインバウンドパケット       | 統計粒度内における、クライアントからCLBへの1秒あたりの送信データパケット数です。        | 個/秒   | 10、60、300 |
| ClientOutpkg        | クライアントからLBへのアウトバウンドパケット       | 統計粒度内における、CLBからクライアントへの1秒あたりの送信データパケット数です。     | 個/秒   | 10、60、300 |
| ClientAccIntraffic  | クライアントからLBへのインバウンドトラフィック       | 統計粒度内における、クライアントからCLBに流入したトラフィックです。                | MB      | 10、60、300 |
| ClientAccOuttraffic | クライアントからLBへのアウトバウンドトラフィック       |統計粒度内における、CLBからクライアントに流出したトラフィックです。                    | MB      | 10、60、300 |
| ClientOuttraffic    | クライアントからLBへのアウトバウンド帯域幅       |統計粒度内における、CLBからクライアントへの流出に使用された帯域幅です。                 | Mbps    | 10、60、300 |
| ClientIntraffic     | クライアントからLBへのインバウンド帯域幅       | 統計粒度内における、クライアントからCLBに流入したトラフィックです。             | Mbps    | 10、60、300 |
| OutTraffic          | LBからバックエンドへのアウトバウンド帯域幅          | 統計粒度内における、バックエンドRSからCLBへの流出に使用された帯域幅です。          | Mbps    | 60、300     |
| InTraffic           | LBからバックエンドへのインバウンド帯域幅          | 統計粒度内における、CLBからバックエンドRSへの流入に使用された帯域幅です。               | Mbps    | 60、300     |
| OutPkg              | LBからバックエンドへのアウトバウンドパケット          | 統計粒度内における、バックエンドRSからCLBへの1秒あたりの送信データパケット数です。      | 個/秒   | 60、300     |
| InPkg               | LBからバックエンドへのインバウンドパケット          |統計粒度内における、CLBからバックエンドRSへの1秒あたりの送信データパケット数です。   | 個/秒   | 60、300     |
| AccOuttraffic       | LBからバックエンドへのアウトバウンドトラフィック          | 統計粒度内における、CLBからバックエンドRSに流入したトラフィックです。<br/>この指標はパブリックネットワークCLBインスタンスのみサポートしており、プライベートネットワークCLBではサポートしていません。                 | MB      | 10、60、300、3600 |
| ConNum              | LBからバックエンドへの接続数          | 統計粒度内における、CLBからバックエンドRSへの接続数です。                 | 個      | 60、300     |
| NewConn             | LBからバックエンドへの新規接続数      | 統計粒度内における、CLBからバックエンドRSへの新規接続数です。             | 個/分 | 60、300     |
| ReqAvg              | 平均リクエスト時間               | 統計粒度内における、CLBの平均リクエスト時間です。<br/>この指標はレイヤー7リスナー独自の指標です。 | ミリ秒    | 60、300     |
| ReqMax              | 最大リクエスト時間               | 統計粒度内における、CLBの最大リクエスト時間です。 <br/>この指標はレイヤー7リスナー独自の指標です。 | ミリ秒    | 60、300     |
| RspAvg              | 平均応答時間               | 統計粒度内における、CLBの平均応答時間です。 <br/>この指標はレイヤー7リスナー独自の指標です。 | ミリ秒    | 60、300     |
| RspMax              | 最大応答時間               | 統計粒度内における、CLBの最大応答時間です。 <br/>この指標はレイヤー7リスナー独自の指標です。 | ミリ秒    | 60、300     |
| RspTimeout          | 応答タイムアウト数               | 統計粒度内における、CLBの応答タイムアウト数です。 <br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分    | 60、300     |
| SuccReq             | 1分あたりの成功リクエスト数           | 統計粒度内における、CLBの1分あたりの成功リクエスト数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分    | 60、300     |
| TotalReq            | 1秒あたりのリクエスト数                 | 統計粒度内における、CLBの1秒あたりのリクエスト数です。  <br/>この指標はレイヤー7リスナー独自の指標です。 | 個      | 60、300     |
| ClbHttp3xx          | CLBが返した3xxステータスコード      | 統計粒度内における、CLBが返した3xxステータスコードの数（CLBとバックエンドサーバーの戻りコードの和）です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| ClbHttp4xx          | CLBが返した4xxステータスコード      | 統計粒度内における、CLBが返した4xxステータスコードの数（CLBとバックエンドサーバーの戻りコードの和）です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| ClbHttp5xx          | CLBが返した5xxステータスコード      | 統計粒度内における、CLBが返した5xxステータスコードの数（CLBとバックエンドサーバーの戻りコードの和）です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| ClbHttp404          | CLBが返した404ステータスコード      | 統計粒度内における、CLBが返した404ステータスコードの数（CLBとバックエンドサーバーの戻りコードの和）です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| ClbHttp499          | CLBが返した499ステータスコード      | 統計粒度内における、CLBが返した499ステータスコードの数（CLBとバックエンドサーバーの戻りコードの和）です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| ClbHttp502          | CLBが返した502ステータスコード      | 統計粒度内における、CLBが返した502ステータスコードの数（CLBとバックエンドサーバーの戻りコードの和）です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| ClbHttp503          | CLBが返した503ステータスコード      | 統計粒度内における、CLBが返した503ステータスコードの数（CLBとバックエンドサーバーの戻りコードの和）です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| ClbHttp504          | CLBが返した504ステータスコード      | 統計粒度内における、CLBが返した504ステータスコードの数（CLBとバックエンドサーバーの戻りコードの和）です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http2xx             | 2xxステータスコード                 | 統計粒度内における、バックエンドサーバーが返した2xxステータスコードの数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http3xx             | 3xxステータスコード                 | 統計粒度内における、バックエンドサーバーが返した3xxステータスコードの数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http4xx             | 4xxステータスコード                 | 統計粒度内における、バックエンドサーバーが返した4xxステータスコードの数です。 <br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http5xx             | 5xxステータスコード                 | 統計粒度内における、バックエンドサーバーが返した5xxステータスコードの数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http404             | 404ステータスコード                 | 統計粒度内における、バックエンドサーバーが返した404ステータスコードの数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http499             | 499ステータスコード                 | 統計粒度内における、バックエンドサーバーが返した499ステータスコードの数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http502             | 502ステータスコード                 | 統計粒度内における、バックエンドサーバーが返した502ステータスコードの数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http503             | 503ステータスコード                 | 統計粒度内における、バックエンドサーバーが返した503ステータスコードの数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
| Http504             | 504ステータスコード                 | 統計粒度内における、バックエンドサーバーが返した504ステータスコードの数です。<br/>この指標はレイヤー7リスナー独自の指標です。 | 個/分 | 60、300     |
|UnhealthRsCount|	ヘルスチェック異常数	|統計周期内の、CLBのヘルスチェック異常数です。|	個	|60、300|


>?あるリスナー下のあるCVMの監視データを確認したい場合は、[CLBコンソール](https://console.cloud.tencent.com/clb)にログインし、CLBインスタンスIDの横の監視アイコンをクリックすると、監視フローティングウィンドウから各インスタンスのパフォーマンスデータをすぐに閲覧することができます。



## 関連ドキュメント
[パブリックネットワークCLBの監視指標](https://intl.cloud.tencent.com/document/product/248/10997)
