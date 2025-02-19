

ここでは、CVMインスタンスの機能、一般的なビジネスシナリオ、注意事項およびベストプラクティスといった面から、インスタンスのタイプを選択する方法をご説明します。実際のビジネスシナリオと結び付けてCVMを選択、購入する方法を理解する上で役立ちます。インスタンスのタイプ選択の分析プロセスを次の図に示します：
<img src="https://qcloudimg.tencent-cloud.cn/raw/fe5a425f921cbb796910257cc3c220d2.png" style="width:60%"/>

## リージョンとアベイラビリティーゾーン
#### リージョン
リージョン(Region)は、購入したクラウドコンピューティングリソースの地理的な場所を定め、お客様やお客様の顧客がリソースにアクセスするためのネットワーク条件をダイレクトに決定するものです。
中国本土以外のリージョンを購入する必要がある場合は、ネットワーク品質要因、関連するコンプライアンスポリシー要因およびいくつかのイメージ使用制限に特に注意してください（例えば、WindowsシステムとLinuxシステムを中国本土以外のリージョンで切り替えることはできません）。

#### アベイラビリティーゾーン
リージョンには1つ以上のアベイラビリティーゾーン(Zone)が含まれており、同じリージョン内の異なるアベイラビリティーゾーン間で販売されるCVMインスタンスのタイプは異なる場合があります。また、異なるアベイラビリティーゾーン間のリソースの相互アクセスには、ある程度のネットワーク遅延に差がある場合があります。

リージョンとアベイラビリティーゾーンの詳細情報については、[リージョンとアベイラビリティーゾーン](https://intl.cloud.tencent.com/document/product/213/6091)をご参照ください。

## インスタンスタイプ
Tencent Cloudはさまざまなタイプのインスタンスを提供しており、各インスタンスタイプには複数のインスタンス仕様が含まれています。アーキテクチャに応じて、x86Compute、ARMCompute、ベアメタルCompute、異種Compute(GPU/FPGA)、Batch Computeなどに分けられます。特性・機能により、標準型、計算型、メモリ型、High IO型、ビッグデータ型などに分けられます。ここでは、インスタンスの特性・機能に応じて区分しており、詳細情報は次のとおりです：

<dx-accordion>
::: 標準型
標準型インスタンスの各性能パラメータはバランスが取れており、WebサイトやMiddlewareといったほとんどの通常業務に適しています。標準型インスタンスの主なシリーズは次のとおりです。
- SおよびSAシリーズ：SシリーズはIntelコアであり、SAシリーズはAMDコアです。SAシリーズと比較して、同じ世代および構成のSシリーズは、より強力なシングルコアパフォーマンスを備えていますが、SAシリーズはよりコストパフォーマンスに優れています。
- ストレージ最適化型S5seシリーズ：最新の仮想化テクノロジーSPDKに基づいて、ストレージプロトコルスタックのみを最適化し、CBSの機能を全面的に引き上げるので、大規模データベースやNoSQLデータベースなどのIOバウンド型サービスに適しています。
- ネットワーク最適化型SN3neシリーズ：プライベートネットワークの最大送受信能力は600万ppsで、パフォーマンスは標準型S3インスタンスの約8倍です。プライベートネットワークの帯域幅は最大25Gbpsをサポートしており、プライベートネットワーク帯域幅は標準型S3に比べて2.5倍にもなります。これは、弾幕、ライブストリーミング、ゲームといった高ネットワークパケットの送受信シナリオに適しています。

::: 
::: 計算型
計算型Cシリーズインスタンスは、最高のシングルコアコンピューティング性能を備えており、バッチ処理、ハイパフォーマンスコンピューティング、大規模ゲームサーバーなど、コンピューティング集約型アプリケーションに適しています。例えば、高トラフィックのWebフロントエンドサーバー、MMO（マッシブリー・マルチプレイヤー・オンライン）ゲームサーバーおよびその他のコンピューティング集約型サービスなど。
:::
::: メモリ型
メモリ型Mシリーズのインスタンスは大容量メモリという特徴を持ち、CPUとメモリの比率が1：8で、メモリ価格が最も安く、主に高性能データベース、分散メモリキャッシュなど、大容量メモリ操作や検索、コンピューティングを必要とするMySQL、Redisなどのアプリケーションに適しています。
:::
::: High IO型
High IO型ITシリーズインスタンスデータディスクはローカルディスクストレージであり、最新のNVME SSDストレージを搭載し、高いランダムIOPS、高スループット、低アクセスレイテンシーといった特徴を備えており、低コストで非常に高いIOPSを提供します。ハードディスクの読み取り・書き込みや遅延に対して高い要件のある高性能データベースなど、例えば、高性能のリレーショナルデータベース、ElasticsearchといったIOバウンド型業務などのI/Oバウンド型アプリケーションに適しています。
<dx-alert infotype="explain" title="">
ITシリーズインスタンスのデータディスクはローカルストレージであるため、データが失われるリスクがあります（ホストがダウンした場合など）。お客様のアプリケーションにデータ信頼性アーキテクチャがない場合は、CBSをデータディスクとして選択できるインスタンスの使用を強く推奨します。
</dx-alert>
:::
::: ビッグデータ型
ビッグデータ型Dシリーズインスタンスはマスストレージリソースを搭載し、高スループットという特徴を備えており、Hadoop分散コンピューティング、大量のログ処理、分散ファイルシステム、大型データウェアハウスなど、スループット集約型アプリケーションに適しています。

<dx-alert infotype="explain" title="">
ビッグデータモデルDシリーズインスタンスのデータディスクはローカルディスクであるため、データが失われるリスクがあります（ホストがダウンしている場合など）。アプリケーションにデータ信頼性アーキテクチャがない場合は、CBSをデータディスクとして選択できるインスタンスの使用を強く推奨します。
</dx-alert>
:::
::: 異種Compute
異種コンピューティングインスタンスはGPU、FPGAなどの異種ハードウェアを搭載し、リアルタイムの高速並列計算と浮動小数点演算機能を備え、ディープラーニング、科学計算、ビデオコーデック、グラフィックワークステーションなどの高性能アプリケーションに適しています。
NVIDIA GPUシリーズのインスタンスは、主流のT4/V100や最新世代のA100などを含めたNVIDIA TeslaシリーズのGPUを採用しており、優れた汎用コンピューティング機能を提供します。ディープラーニングのトレーニング/推論、計算科学などのアプリケーションシナリオでのベストな選択肢です。
:::
::: Cloud Physical Machine2.0
Cloud Physical Machine2.0は、Tencent Cloudの最新仮想化テクノロジーに基づいて開発された究極のパフォーマンスを備えたECSベアメタルCVMです。Cloud Physical Machine2.0は、仮想マシンの柔軟性と物理マシンの高い安定性を兼ね備え、NetworkingやデータベースといったTencent Cloudの全製品とシームレスに統合します。Cloud Physical Machine2.0インスタンスマトリックスは、標準、High IO、ビッグデータおよび異種Computeのシナリオを網羅し、クラウド専用の高性能かつ安全に分離された物理サーバークラスターを分単位で構築できます。同時に、サードパーティの仮想化プラットフォームをサポートでき、高度にネストされた仮想化テクノロジーによって、AnyStackのハイブリッドデプロイを実現し、先進的かつ効率的なハイブリッドクラウドソリューションを構築することができます。
:::
::: 高性能Computeクラスター
高性能Computeクラスターは、Cloud Physical Machine2.0をコンピューティングノードとして使用し、高速RDMA相互接続ネットワークサポートを提供するクラウド上のComputeクラスターです。自動車シミュレーション、流体力学、分子動力学といった大規模なコンピューティングシナリオを幅広くサポートできます。また、大規模な機械学習トレーニングなどのシナリオをサポートできる、高性能の異種リソースを提供します。
:::  
</dx-accordion>

<br>
CVMのインスタンスタイプの関連情報の詳細については、<a href="https://intl.cloud.tencent.com/document/product/213/11518">インスタンス仕様</a>をご参照ください。


## 一般的なビジネスシナリオのタイプ選択に関する推奨事項
<table>
<tr>
<th style="width: 14%;">ビジネスシナリオ</th><th style="width: 19%;">一般的なソフトウェア</th>
<th style="width: 47%;">シナリオ紹介</th><th style="width: 20%;">推奨モデル</th>
</tr>
<tr>
<td>Webサービス</td>
<td>Nginx<br>Apache</td>
<td>Webサービスには通常、個人のWebサイト、ブログおよび大規模なeコマースのWebサイトなどが含まれており、コンピューティング・ストレージ・メモリなどのリソースに対してはバランスが要求されるため、業務上のニーズを満たす標準型インスタンスをお勧めします。</td>
<td>標準型SおよびSAシリーズ</td>
</tr>
<tr>
<td>Middleware</td>
<td>Kafka<br> MQ</td>
<td>メッセージキュー業務のコンピューティングやメモリリソースに対する要件は比較的バランスが要求されるので、標準型モデルにはストレージとしてCBSを搭載することをお勧めします。</td>
<td>標準型Sシリーズ<br>計算型Cシリーズ</td>
</tr>
<tr>
<td>データベース</td>
<td>MySQL</td>
<td>データベースにはIO性能に対する非常に高い要件があるので、SSD CBSとローカルディスクを使用することをお勧めします（ローカルディスクモデルはデータが失われるリスクがあるため、データのバックアップに注意してください）。</td>
<td>High IO型シリーズ<br>メモリ型Mシリーズ</td>
</tr>
<tr>
<td>キャッシュ</td>
<td>Redis<br>Memcache</td>
<td>キャッシュ型業務はメモリに対して高い要件がありますが、コンピューティングに対する要件は低めですので、メモリ比率の高いメモリ型インスタンスをお勧めします。</td>
<td>メモリ型Mシリーズ</td>
</tr>
<tr>
<td>ビッグデータ</td>
<td>Hadoop<br>ES</td>
<td>ビッグデータ業務はマスストレージを必要とし、IOスループットに所定の要件があるため、専用のビッグデータ型Dシリーズをお勧めします（ローカルディスクモデルはデータが失われるリスクがあるため、データのバックアップに注意してください）。</td>
<td>ビッグデータ型Dシリーズ</td>
</tr>
<tr>
<td>高性能Compute</td>
<td>StarCCM<br>WRF-Chem</td>
<td>高性能Computeの業務には、究極とも言える単一マシンの計算機能が必要であるとともに、効率的なマルチマシン拡張も必要です。高速RDMAネットワークを搭載した高性能Computeクラスターまたは計算型インスタンスファミリーをお勧めします。</td>
<td>高性能Computeクラスター<br>計算型Cシリーズ</td>
</tr>
<tr>
<td>仮想化</td>
<td>Kvm<br>OpenStack</td>
<td>仮想化アプリケーションでは、クラウド上のサーバーが、パフォーマンスのオーバーヘッドを追加することなく、ネストされた仮想化の機能を備え、仮想化機能を従来の物理マシンと一貫性のある状態に保つ必要があります。Cloud Physical Machine2.0製品をお勧めします。</td>
<td>高性能Computeクラスター<br>Cloud Physical Machine2.0</td>
</tr>
<tr>
<td>ビデオレンダリング</td>
<td>Unity<br>UE4</td>
<td>ビデオレンダリングシナリオには、DirectXやOpenGLなどのグラフィック・画像処理APIのサポートが必要です。 GPUレンダリングタイプGN7vwをお勧めします。</td>
<td>GPUレンダリング型GN7vw</td>
</tr>
<tr>
<td>AI Compute</td>
<td>TensorFlow<br>CUDA</td>
<td>AI Compute業務には並列処理機能が必要であり、GPUコンピューティング機能やグラフィックメモリに対する明確な要件があります。</td>
<td>GPU計算型<br>高性能Computeクラスター</td>
</tr>
</table>



## 関連製品
### 一般的なクラウド製品のマッチングに関する推奨事項
実際のビジネスシナリオと結び付けて、他のTencent Cloud製品を組み合わせて使用することができます。ここでは、​​典型的なWebサイトのアーキテクチャを例として取り上げます。下図に示すように、クラウド製品と組み合わせることをお勧めします。
<img src="https://qcloudimg.tencent-cloud.cn/raw/d7956269e64809420aecb71229a6bd9d.png" style="width:70%"/>

### 他のクラウド製品
実際のニーズに応じて、他のクラウド製品を選択、使用することもできます。例えば、基本的な業務のデプロイが完了したら、所定の障害復旧対策を講じて、システムアーキテクチャの堅牢性を確保するとともに、データセキュリティを確保することができます。次のTencent Cloud製品と組み合わせて、障害復旧を実現することができます。
- **[スナップショット](https://intl.cloud.tencent.com/document/product/362/31638)**
スナップショットは、手軽で効率的なデータ保護サービスであり、非常に重要で効果的なデータ障害復旧対策でもあります。日常的なデータバックアップ、迅速なデータリカバリ、本番データの複数レプリカアプリケーション、迅速なデプロイ環境といったビジネスシナリオで使用することをお勧めします。スナップショットの作成には少額の料金がかかります。詳細については、[スナップショットの料金概要](https://intl.cloud.tencent.com/document/product/362/32415)をご参照ください。
- **[BCM](https://intl.cloud.tencent.com/document/product/248/32799)**
クラウドリソースのBCMアラームの設定は、業務の保証にとって同様に重要な役割を果たします。BCMを使用して、クラウド製品のリソース使用率、アプリケーション性能やクラウド製品の実行状況を全面的に理解することができます。BCMは、マルチインデックスモニタリング、カスタムアラーム、クロスリージョン/クロスプロジェクトインスタンスのグループ化、カスタムモニタリング、視覚化DashboardおよびPrometheusホスティングサービスといった機能もサポートします。クラウド製品に生じた緊急事態をタイムリーに制御かつ対処できるよう支援することによって、システムの安定性を高め、運用・保守の効率を向上させ、運用・保守のコストを削減します。
- **[CLB](https://intl.cloud.tencent.com/document/product/214/524)**
業務にシングルポイントのオペレーショナルリスクを発生させたくない場合は、CLBの設定を選択できます。CLBサービスは、仮想サービスアドレス(VIP)を設定することにより、同じリージョンにある複数のCVMリソースを高性能で可用性の高いアプリケーションサービスプールに仮想化します。アプリケーションで指定された方法に従って、クライアントからのネットワークリクエストをCVMプールに配信します。
CLBサービスは、CVMプール内のCVMインスタンスのヘルスステータスをチェックし、異常な状態のインスタンスを自動的に隔離し、CVMのシングルポイントの問題を解消するとともに、アプリケーションの全体的なサービス機能を向上させます。


## 関連ドキュメント
- [リージョンとアベイラビリティーゾーン](https://intl.cloud.tencent.com/document/product/213/6091)
-[インスタンス仕様](https://intl.cloud.tencent.com/document/product/213/11518)



