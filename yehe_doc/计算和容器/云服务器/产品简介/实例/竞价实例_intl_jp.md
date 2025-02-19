## スポットインスタンスとは
スポットインスタンスは、大幅割引価格とシステム中断メカニズムを特徴とする CVM インスタンスの新しいモードです。スポット インスタンスを割引価格で購入できますが、システムによって自動的に回収される可能性があります。スポットインスタンスの使用方法（コンソールでの操作、リモートログイン、サービスのデプロイ、VPC との関連付けなど）は従量課金CVMインスタンスと基本的に同じです。

- 関連リンク：[FAQ > インスタンスについて > スポットインスタンス](https://intl.cloud.tencent.com/document/product/213/17817)
- 関連リンク：[スポットインスタンスの購入方法](https://intl.cloud.tencent.com/document/product/213/17926)

## 現段階の特殊ポリシー
- **固定の割引比例**：すべての仕様のスポットインスタンスは固定した割引で販売されます（同じ仕様の従量課金インスタンスの20%の価格で販売される）。一部のタイプのインスタンスは価格を若干調整することがあります。
- **在庫不足によるシステムの中断**：現段階では、システムは市場価格により中断しませんが、スポットインスタンスリソースプールの在庫不足により中断することがあります。在庫不足の場合は、システムは割り当てたスポットインスタンスからランダムに回収します。この場合、インスタンスデータが保持されません。
- **すべてのリージョンで利用可能**：スポットインスタンスは、ほぼ全てのTencent Cloudリージョンで登場し、スポットインスタンスでサポートされるインスタンス タイプは、従量課金インスタンスでサポートされるインスタンス タイプと同じです。サポートされている最新のリージョンとインスタンス タイプについては、[スポットインスタンス](https://intl.cloud.tencent.com/document/product/213/17817#.E5.BD.93.E5.89.8D.E7.AB.9E.E4.BB.B7.E5.AE.9E.E4.BE.8B.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E5.9C.B0.E5.9F.9F.E5.92.8C.E5.AE.9E.E4.BE.8B.E7.B1.BB.E5.9E.8B.E5.8F.8A.E8.A7.84.E6.A0.BC.EF.BC.9F)をご参照ください。

## 製品の特徴
### I. 高いコストパフォーマンス
![](https://main.qcloudimg.com/raw/8179ef6629ac0a0b4b9c3c9cd6f80ffa.png)
スポットインスタンスは、オンデマンド料金に比べ最大 90% の割引料金でご利用いただけます。

- **割引の幅**：スポットインスタンスは、同じ仕様の従量課金インスタンスに比べ最大 90% 低い価格で購入できます。
- **割引対象**：CVM CPUとメモリのみが割引対象になります。システム ディスク、データ ディスク、帯域幅、有料イメージなど、その他の CVM 関連の課金項目は割引対象外です。
- **価格変動**：一定期間内にこの割引は変動しません。ただし、アベイラビリティゾーンで大量購入がある場合、価格が変動する可能性があります（現段階では、割引は80%オフに固定されています）。

### II. システム中断メカニズム
![](https://main.qcloudimg.com/raw/a4db964d52400b9a00d3c7e96c0b833d.png)
ユーザーのみがリリースできる従量課金制インスタンスとは異なり、スポットインスタンスは、システムによって中断される場合があります。システムは現在の価格とリソースプール等の総合的な状況に基づいて、 割り当てられたスポット インスタンスを中断するかどうかを決定します。 
![](https://main.qcloudimg.com/raw/824a585f8dfeb1914f4d72ea1eafdb6c.png)

- **価格原因による中断**：市場価格が顧客の最高指値以上になった場合は、インスタンスが回収されます（現段階では、市場価格が固定されている）。
- **在庫原因による中断**：スポットインスタンスの在庫が不足している場合、システムは在庫不足の状況によりスポットインスタンスを回収します。在庫が回復したら、スポットインスタンスを再度申請できます。

## 適用しないシナリオ
スポットインスタンスは中断される可能性があるため、ユーザーはスポットインスタンスのライフサイクルを完全に把握できません。そのため、スポットインスタンスで高い安定性が要求されるサービスを実行しないことをお勧めします。例えば：
- データベースサービス
- ロードバランサーを使用しないオンライン サービスとWebサイトサービス
- 分散式アーキテクチャの中核であるマスターコントロールノード
- 長時間（10+時間）のビッグデータコンピューティング作業

## 適用シナリオと業界
### ユースケース
- ビッグデータコンピューティング
- ロードバランサーを使用したオンライン サービスと Web サイト サービス
- ネットワーククローラーサービス
- 細かい粒度コンピューティングシナリオ、またはチェックポイントからの再起動をサポートするコンピューティングシナリオ

### 適用業界
- 遺伝子配列解析および分析
- 薬物結晶分析
- ビデオのトランスコーディング、ビデオレンダリング
- 金融、取引データの分析
- 画像およびマルチメディアの処理
- 科学技術コンピューティング（地理、流体力学等）

## 制限
- **クォータ制限**：現在、アベイラビリティ ゾーンごとの各アカウントのスポットインスタンスには、合計で最大 50 個の vCPU コアを含めることができます（クォータを増やすには、[チケットを送信](https://console.cloud.tencent.com/workorder/category)してください）。
- **操作制限1**：スポットインスタンスの構成をアップグレードおよびダウングレードすることはできません。
- **操作制限2**：スポットインスタンスの課金方法をサブスクリプション制に切り替えることはできません。
- **操作制限3**：スポットインスタンスは「停止済みインスタンスの非課金化」機能をサポートしません。
- **操作制限4**：スポットインスタンスはシステムの再インストールをサポートしません。
- **操作制限5**：スポットインスタンスはシステムディスクとデータディスクの容量拡張をサポートしません。

## ベストプラクティス
### I. タスク分割
-  大きなタスクを小タスクに分割して、中断の可能性を低くします。
-  EMRのような切り分け思惟を持つビッグデータキットを利用します。

### II. ロードバランサーを使用してオンラインおよび Web サービスの安定性を確保する
- アクセス レイヤーでは、CLB などのロードバランサーを使用します。
- バックエンドリソースは一部の従量課金インスタンス + 大量のスポットインスタンスの組合せを使います。
- スポットインスタンスの中断状況をモニタリングし、 間もなく中断されるインスタンスをCLBから削除します。

### III. チェックポイントからの再起動をサポートするコンピューティングスケジューリングモードを使用する
- コンピューティングの中間結果をCOS/CFS/NASなどの永続ストレージサービスに保存します。
- インスタンスメタデータにより間もなく中断されるインスタンスを監視し、2分間の保留期間以内にコンピューティング結果を保存します。
- スポットインスタンスが再起動すると、前回のコンピューティングを続けます。
