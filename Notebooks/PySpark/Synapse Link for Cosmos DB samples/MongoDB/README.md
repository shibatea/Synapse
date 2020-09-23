
# Azure Cosmos DB API for MongoDB によるロード、クエリおよびスキーマの更新

このノートブックでは、MongoDB クライアントを使用してデータを取り込む方法と、Synapse Link with Cosmos DB API for MongoDB を使用してこのデータをクエリする方法を示すシンプルなデータセットが作成されます。また、スキーマの更新を含む 2 つめのデータセットを取り込み、Synapse Link によってどのようにスキーマ管理が行われるのかを示します。

## 環境設定

メインの [README](../README.md) ファイルの前提条件に従っていることを確認してください。その上で、以下の手順を順番に実行してください。

1. Azure ポータルを使用して、Synapse ワークスペースに関連付けられているストレージアカウントのアクセス制御 (IAM) タブに移動し、+Add をクリック、役割の割り当てを追加し、自分をデータ共同作成者の役割に追加します。これは、Azure Synapse Spark プールを使用したデータベースやテーブルの作成など、Spark メタデータの操作のために必要になります。
1. ノートブックの手順に従って、MongoDB API の新しい Cosmos DB アカウントを作成します。このリポジトリ内の他の 2 つのノートブックように作成された Cosmos DB アカウントは SQL API 用に作成されたもののため、ここでは同じアカウントを使用することはできません。
1. ノートブックの手順に従って、MongoDB API の Azure Cosmos DB アカウント内にデータベースとコレクションを作成します。
1. ノートブックの手順に従って、linked service を作成します。

## ノートブックの実行

ノートブックの説明に従ってください:

[Azure Cosmos DB API for MongoDB の Synapse Spark を使用したデータの取り込みとクエリ](../MongoDB/spark-notebooks/pyspark/01-CosmosDBSynapseMongoDB.ipynb)