## 概要

Cloud Object Storage(COS)コンソールは、ストレージデータの概要ページを提供しており、そのページでは、バケット数、オブジェクト数、ストレージ使用量、リクエスト数、トラフィックなどのデータを確認することができます。

>!
> - サブアカウントでデータを確認するには、**バケットリストアクセス**権限が必要です。詳細については、[サブアカウントのアクセスバケットリスト](https://intl.cloud.tencent.com/document/product/436/17061)ドキュメントのプリセットポリシーの箇所をご参照ください。
> - このデータの概要は、**バケット数**を除いたリアルタイムデータですが、他のデータはリアルタイムデータではなく、約2時間の遅延があります。このデータは、モニタリングデータの参照のみを目的としており、正確な課金計測データを確認する必要がある場合は、[料金センター](https://console.cloud.tencent.com/account)で確認することができます。
> 

## データ折れ線グラフの確認

### 操作手順

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインし、左側メニューの**使用統計**>**基本使用統計**をクリックし、データモニタリングページに進みます。
2. **データの概要**ページでは、以下の情報を確認することができます。
   ![](https://main.qcloudimg.com/raw/036d7c5f1e31fa9f69507733c2a4d8d9.png)
   - **バケット数**：現在作成されているバケット総数です。                                     
    - **オブジェクト数**：現在作成されているすべてのバケット内のオブジェクト総数で、さまざまなストレージタイプのオブジェクト数の表示もサポートしています。                      
    - **当月の1日あたり平均ストレージ使用量**：当月の1日あたりの平均ストレージ使用量で、具体的な計算式は、現在のストレージ量/当月の日数です。標準ストレージ、低頻度ストレージ、Cloud Archive Strage(CAS)といったタイプごとに、1日あたり平均ストレージ使用量があります。
   - **ストレージ使用量折れ線グラフ**：標準ストレージ、低頻度ストレージ、CASのストレージ使用量を選択して表示できます。過去1年間のデータ内訳の照会をサポートしています。
   - **トラフィック折れ線グラフ**：現在、標準ストレージと低頻度ストレージのパブリックネットワークダウンリンクトラフィック、プライベートネットワークトラフィック、CDN back-to-originトラフィックを選択して表示できます。過去1年間のデータ内訳の照会をサポートしています。
   - **リクエスト数折れ線グラフ**：標準ストレージ、低頻度ストレージタイプの読み取り/書き込みリクエストを選択して表示できます。過去1年間のデータ内訳の照会をサポートしています。 
   - **ユーザー有効リクエスト比率折れ線グラフ**：標準ストレージのユーザーの有効な読み取り/書き込みリクエスト比率を選択して表示できます。過去1年間のデータ内訳の照会をサポートしています。 
   - **データ取得量折れ線グラフ**：低頻度ストレージ、CASタイプのデータ取得量の表示をサポートします。そのうちCASタイプには、高速取得量、標準取得量、一括取得量があります。過去1年間のデータ内訳の照会をサポートしています。
   - **バケットデータの概要**：バケットごとに昨日または当月のバケットの主要データを表示します。主要データのカテゴリーは、選択したストレージの種類によって、標準ストレージ、低頻度ストレージ、CASの使用量、低頻度データ取得量、アーカイブデータ取得量、標準・低頻度の読み取り/書き込みリクエスト数、パブリックネットワークダウンリンクトラフィック、プライベートネットワークダウンリンクトラフィックおよびCDN back-to-originトラフィックがあります。
3. グラフ右上のダウンロードボタンで、主要データをワンクリックでエクスポートできます。 

## バケットディメンションごとにデータを表示

### 操作手順

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインし、左側メニューの**バケットリスト**をクリックし、インターフェースで**統計データ**を選択します。
2. 統計データインターフェースでは、各バケットのストレージ使用量、データ取得量、トラフィックおよびリクエスト数など、ストレージタイプや時間帯ごとの統計データを確認することができます。
