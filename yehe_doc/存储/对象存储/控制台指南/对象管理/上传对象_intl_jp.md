## 概要

COSコンソールから、バケットのファイルリストページにオブジェクトをアップロードすることができます。詳細については、[オブジェクトの概要](https://intl.cloud.tencent.com/document/product/436/13324)をご参照ください。

>?
> - 現在INTELLIGENT_TIERINGストレージタイプは、北京、南京、上海、広州、成都、重慶、東京、シンガポールリージョンでのみサポートされています。このタイプのアップロードが必要な場合は、まず対応するリージョンのバケットに対して、[INTELLIGENT_TIERINGストレージ設定の有効化](https://intl.cloud.tencent.com/document/product/436/38306)を行ってください。
> - ディープアーカイブストレージタイプは、北京、南京、上海、広州、成都、重慶、東京、シンガポールリージョンでのみサポートされています。このタイプのアップロードが必要な場合は、まず対応するリージョンのバケットを選択してください。
> 

##  前提条件

オブジェクトをアップロードする前に、バケットが作成されていることを確認してください。オブジェクトが作成されていない場合は、まず[バケットの作成](https://intl.cloud.tencent.com/document/product/436/13309)のドキュメントをご参照のうえ、操作を行ってください。

## 操作手順

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側ナビゲーションバーで**バケットリスト**をクリックし、バケットリストページに進みます。
3. ストレージが必要なオブジェクトのバケットをクリックし、バケットのファイルリストページに進みます。
4. ファイルリストで、**ファイルのアップロード**をクリックします。
![](https://main.qcloudimg.com/raw/1f499717168f5559337899f635e19a13.png)
5. ポップアップしたウィンドウで、**ファイルの選択**または**フォルダの選択**をクリックし、実際のニーズに応じて、1つまたは複数のローカルファイル（またはフォルダ）を選択します。
>? 複数のファイルのアップロードをサポートしていないブラウザもありますので、IE10以上、Firefox、Chromeなどの主流ブラウザを使用することをお勧めします。
>
![](https://main.qcloudimg.com/raw/8489d2bae2ba778bac87386093cd51e7.png)
6. （オプション）**パラメータ設定**をクリックし、ファイルのアップロードウィンドウでオブジェクトの属性を設定します。
 ![](https://main.qcloudimg.com/raw/0b7c7b6297a1098fe43074f85a138fbf.png)
設定に関する説明は次のとおりです。
 - **ストレージタイプ**：異なるユースケースに基づき、オブジェクトごとに異なるストレージタイプを設定することができます。デフォルトのストレージタイプは標準ストレージです。ストレージタイプの説明については[ストレージタイプ](https://intl.cloud.tencent.com/document/product/436/6222)をご参照ください。
 - **アクセス権限**：オブジェクトごとに異なるアクセス権限を設定することができます。デフォルトのアクセス権限は継承された権限（継承されたバケット権限）です。アクセス権限の詳細については、[アクセス制御の基本概念](https://intl.cloud.tencent.com/document/product/436/30581)をご参照ください。
 - **サーバー側の暗号化**：オブジェクトをアップロードすると同時に、オブジェクトのサーバー側の暗号化属性を設定します。Tencent Cloud COSは、アップロードされたオブジェクトにデータ暗号化保護ポリシーを追加し、データを書き込む前の自動的な暗号化を支援するだけでなく、そのデータにアクセスすると自動的に復号を行います。現在、SSE-COS、SSE-KMS（北京、上海、広州リージョンでのみサポートされています）をサポートしています。詳細については、[サーバー側の暗号化の概要](https://intl.cloud.tencent.com/document/product/436/18145)をご参照ください。
 - **オブジェクトタグ**：オブジェクトタグはタグのキー(tagKey)とタグの値(tagValue)を「=」でつないだ構成となっています（例：group = IT）。お客様は指定したオブジェクトに対し、タグの設定、照会、削除操作を行うことができます。
 - **メタデータ**：オブジェクトメタデータとは、サーバーがHTTPプロトコルを使ってHTMLデータをブラウザに渡す前に送る文字列で、HTTP Headerとも呼ばれます。HTTP Headerを変更することで、ページの応答形式を変更したり、キャッシュタイムの変更といった設定情報を伝達したりすることができます。オブジェクトのHTTP Headerを変更しても、オブジェクト自体は変更されません。詳細な情報については、[カスタムオブジェクトHeaders](https://intl.cloud.tencent.com/document/product/436/13361)をご参照ください。
7. **アップロード**をクリックします。
ページ右上の「タスク完了」で現在のアップロードの進捗状況を確認することができます。アップロードが完了すると、バケットの「ファイルリスト」ページで先ほどアップロードしたオブジェクトを確認できます。
![](https://main.qcloudimg.com/raw/eab5784b108fc096dbe317fed25f7925.png)
>? 図のタスク進捗状況は、現在の操作で作成されたタスクの数を示しています。例えば、1回の操作で10ファイルをアップロードし、すべてのアップロードに成功した場合、タスク進捗状況は「成功1、失敗0、一時停止0」と表示されます。
>
