
# Azure Cosmos DB の Azure Synapse Link を活用した IoT 異常検出
架空のシナリオは、蒸気タービンからの信号が分析され、異常な信号が検出される発電所です。Azure Synapse Spark を使用して Azure Cosmos DB にストリーミングとバッチ IoT データを取り込み、Azure Synapse Link を使用して結合と集計を実行し、Azure Cognitive Services on Spark (MMLSpark) を使用して異常検出を実行します。

### 環境のセットアップ
メインの [README](../README.md) ファイルの前提条件に従っていることを確認してください。以下の手順を順番に実行してください。
1. Synapse ワークスペースの Data / Linked タブを使用して、Synapse ワークスペースに接続されているストレージアカウントのルートディレクトリ内に IoTData フォルダーを作成します。このリポジトリの "IoTData" ディレクトリの下に配置されている "IoTDeviceInfo.csv" ファイルをこのフォルダにアップロードします。
 
![upload_datasets](images/upload_datasets.png)

2.  Azure Portal を使用して、Synapse ワークスペースに関連付けられているストレージアカウントのアクセス制御 (IAM) タブに移動し、+Add をクリックして、役割の割り当てを追加し、自分をデータ共同作成者の役割に追加します。これは、Azure Synapse Spark Pool を使用したデータベースやテーブルの作成など、Spark メタデータの操作に必要です。

3. Azure Portal を使用して、Azure Cosmos DB アカウントのデータエクスプローラーに移動し、CosmosDBIoTDemo というデータベースを作成します。 

4. 同じデータエクスプローラーで、分析ストア対応の 2 つのコンテナー、IoTSignals と IoTDeviceInfo を作成します。ポータルインターフェイスでは、container id はコンテナー名です。スループットをオートスケールに変更し、上限を4,000に設定します。Cosmos DB コンテナーで分析ストレージを有効にする方法の詳細については、[こちら](https://docs.microsoft.com/ja-jp/azure/cosmos-db/configure-synapse-link#create-analytical-ttl)をクリックしてください。
    * 両方のコンテナーのパーティションキーとして /id を使用します
    * 両方のコンテナーで分析ストアが有効になっていることを確認してください

5. Azure Synapse ワークスペースで、Manage / Linked Services タブに移動し、上記の手順 3 で作成された Cosmos DB データベースを指す CosmosDBIoTDemo というリンクされたサービスを作成します。Cosmos DB を指す Synapse リンクサービスの作成の詳細については、[こちら](https://docs.microsoft.com/ja-jp/azure/synapse-analytics/synapse-link/how-to-connect-synapse-link-cosmos-db#connect-an-azure-cosmos-db-database-to-a-synapse-workspace)をクリックしてください。

### ノートブックの実行

以下の 4 つのSynapse Spark ノートブックを "IoT/spark-notebooks/pyspark/" ディレクトリーの下の Synapse ワークスペースにインポートし、前提条件で作成された Spark プールをノートブックに接続します。
1. [01-CosmosDBSynapseStreamIngestion: 構造化ストリーミングを使用して Azure Cosmos DB コレクションにストリーミングデータを取り込む](../IoT/spark-notebooks/pyspark/01-CosmosDBSynapseStreamIngestion.ipynb)

    このノートブックは、構造化ストリーミングを使用して、ドキュメントを "IoTSignals" コレクションに取り込みます。"04-CosmosDBSynapseML" ノートブックの異常検出に必要なドキュメントが十分に入ってくるように、2 ～ 5 分程度のストリーミングを行った後、このノートブックの実行を停止してください。
    ノートブックの実行が停止したら、Azure Cosmos DB アカウントポータルのデータエクスプローラーに移動し、データが "IoTSignals" コレクションに読み込まれていることを確認します。

2. [02-CosmosDBSynapseBatchIngestion: Azure Synapse Spark を使用してバッチデータを Azure Cosmos DB コレクションに取り込む](../IoT/spark-notebooks/pyspark/02-CosmosDBSynapseBatchIngestion.ipynb)

    このノートブックは、"IoTDeviceInfo.csv" から "IoTDeviceInfo" コレクションにドキュメントを取り込みます。
    ノートブックの実行が完了したら、Azure Cosmos DB アカウントポータルのデータエクスプローラーに移動し、データが "IoTDeviceInfo" コレクションに読み込まれていることを確認します。   

3. [03-CosmosDBSynapseJoins: Azure Synapse Link を使用して Azure Cosmos DB コレクション全体で結合と集計を実行する](../IoT/spark-notebooks/pyspark/03-CosmosDBSynapseJoins.ipynb)

    このノートブックは、Azure Cosmos DB 分析ストアのコレクションを指す Spark テーブルを作成し、コレクション全体で結合、フィルター、集計を実行し、plotly を使用してデータを可視化します。

4. [04-CosmosDBSynapseML: Synapse Spark (MMLSpark) で Azure Synapse Link と Azure Cognitive Services を使用して異常検出を実行する](../IoT/spark-notebooks/pyspark/04-CosmosDBSynapseML.ipynb)

    このノートブックは、Azure Cognitive Services on Spark を使用して異常検出を実行し、異常を plotly を使用して可視化できるようにします。

