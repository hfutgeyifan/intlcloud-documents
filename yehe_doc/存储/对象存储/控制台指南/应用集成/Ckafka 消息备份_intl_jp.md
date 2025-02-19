## 概要

Ckafkaメッセージのバックアップは、Tencent CloudのCloud Object Storage(COS)が提供する[Serverless Cloud Function（SCF）](https://intl.cloud.tencent.com/document/product/583)をベースとしたCkafkaメッセージをCOSにダンプする機能です。ユーザーがCkafkaメッセージをダンプすることを支援し、データの分析やダウンロードなどの操作を行いやすくします。

Ckafkaは、オープンソースのApache Kafkaメッセージキューエンジンをベースとして、高いスループット性能と拡張性を備えたメッセージキューサービスを提供します。詳細については、[Ckafka製品概要](https://intl.cloud.tencent.com/document/product/597/10066)をご参照ください。

ユーザーが指定したバケットにバックアップ関数ルールを設定すると、CKafkaインスタンスがメッセージを生成する際に、SCFは所定の時間粒度に従ってメッセージを取得し、COSバケットにダンプします。

## 注意事項

- 以前にCOSコンソールでバケットにCKafkaメッセージのバックアップルールを追加したことがある場合は、[SCFコンソール](https://console.cloud.tencent.com/scf/list?rid=1&ns=default)で、作成したCKafkaメッセージバックアップ関数を確認できます。この関数を削除すると、ルールが有効にならない場合がありますので削除**しないで**ください。
- COSへのCKafkaメッセージバックアップは、広州、上海、中国香港、北京、成都、シンガポール、ムンバイ、トロント、シリコンバレーなどでサポートされています。その他のサポートリージョンについては、[SCF製品ドキュメント](https://intl.cloud.tencent.com/document/product/583)をご参照ください。

## 操作手順

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側ナビゲーションで**アプリケーション統合**をクリックし、**Ckafkaメッセージバックアップ**を見つけます。
3. **バックアップルールの設定**をクリックし、ルール設定ページに進みます。
4. **関数の追加**をクリックします。
>! SCFサービスをアクティブ化していない場合は、[SCFコンソール](https://console.cloud.tencent.com/scf)に移動してSCFサービスをアクティブ化し、プロンプトに従ってサービス権限承認を行えば完了です。
>
5. ポップアップトウィンドウで、以下の情報を設定します。

 - **関数名**：関数の一意の識別名として、作成後に変更することはできません。[SCFコンソール](https://console.cloud.tencent.com/scf/list?rid=1&ns=default)でこの関数を確認できます。
 - **関連バケット**：Ckafkaメッセージを格納するCOSバケットです。
 - **時間粒度**：メッセージを収集する時間間隔は、メッセージ量のサイズに応じて5～15分の範囲で選択されます。ダンプ性能を確保するため、集約されるファイル数はPartition数、partition_maxの設定値に関連します。Partitionの説明については、[パーティション](https://intl.cloud.tencent.com/document/product/597/32275)をご参照ください。
 - **SCF権限承認**：CKafkaメッセージのバックアップには、お客様のCKafkaサービスから関連するインスタンスメッセージを読み取り、お客様が指定したバケットにダンプするための権限承認が必要です。そのため、この権限承認を追加する必要があります。
6. **次のステップ**をクリックし、Ckafkaを設定します。設定項目の説明は次のとおりです。

 - **インスタンス選択**：メッセージソースのCkafkaインスタンスを選択します。同じリージョンのCkafkaインスタンスのみをサポートしています。
 - **トピックの選択**：メッセージソースのトピックを選択します。
 - **開始位置**：メッセージダンプをバックアップする際のメッセージ履歴の処理方法とtopic offsetの設定です。
 - **アクセスアドレス**：VPCプライベートネットワークへアクセスするアドレスである必要があります。基幹ネットワークのCKafkaインスタンスにルーティングポリシーを追加してください。詳細については、[ルーティングポリシーの追加](https://intl.cloud.tencent.com/document/product/597/32555)をご参照ください。
>! 対応するVPCサブネットに使用できるIPが必要で、DHCPがサポートされている必要があります。
>
7. **次のステップ**をクリックし、配信の設定を行います。設定項目の説明は次のとおりです。

**配布パス**：バックアップファイルの配布パスのプレフィックスは、入力しないとデフォルトでバケットルートパスに保存されます。指定するプレフィックスは、スラッシュ/で終わる必要があります。
8. 設定を追加して**確定**をクリックすると、関数が追加されたことを確認できます。

新規作成した関数に対しては、次のような操作が可能です。
 - **ログの確認**をクリックして、Ckafkaメッセージのバックアップ履歴を確認します。バックアップでエラーが発生した場合は、**ログの確認**をクリックしてSCFコンソールにすばやくジャンプし、ログエラーの詳細を確認することもできます。
 - **編集**をクリックして、Ckafkaメッセージのバックアップルールを変更します。
 - **削除**をクリックして、使用しないCkafkaメッセージのバックアップルールを削除します。

