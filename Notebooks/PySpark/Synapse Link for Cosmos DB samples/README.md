---
page_type: sample
languages:
- pySpark
- SparkSQL
- python
products:
- Azure Cosmos DB
- Azure Synapse Link
- MMLSpark
description: "Sample Azure Cosmos DB - Synapse Link notebooks "
urlFragment: "cosmosdb-synapse-link-samples"
---

# Azure Cosmos DB 用 Azure Synapse Link - サンプル
このリポジトリには、Azure Cosmos DB 用 Azure Synapse Link を使用したエンドツーエンドのソリューションを示す詳細な Synapse Spark サンプルノートブックが含まれています。

## 前提条件

* [Azure Cosmos DB アカウント](https://docs.microsoft.com/ja-jp/azure/cosmos-db/create-cosmosdb-resources-portal)
* [Spark pool](https://docs.microsoft.com/ja-jp/azure/synapse-analytics/quickstart-create-apache-spark-pool) で構成された [Azure Synapse ワークスペース](https://docs.microsoft.com/ja-jp/azure/synapse-analytics/quickstart-create-workspace)

## シナリオ 1 - Internet of Things (IoT)

このシナリオでは、Azure Synapse Spark を使用して Azure Cosmos DB にストリーミングとバッチ IoT データを取り込み、Azure Synapse Link を使用して結合と集計を実行し、Azure Cognitive Services on Spark (MMLSpark) を使用して [Anomaly Detector](https://azure.microsoft.com/ja-jp/services/cognitive-services/anomaly-detector/) を実行します。

![IoT-components-dataflow](images/dataflow.PNG)
### ノートブックの実行

Import the below four synapse spark notebooks under the "IoT/spark-notebooks/pyspark/" dir on to the Synapse workspace and attach the Spark pool created in the prerequisite to the notebooks.
1. [01-CosmosDBSynapseStreamIngestion: 構造化ストリーミングを使用してAzure Cosmos DBコレクションにストリーミングデータを取り込む](IoT/spark-notebooks/pyspark/01-CosmosDBSynapseStreamIngestion.ipynb)
1. [02-CosmosDBSynapseBatchIngestion: Azure Synapse Spark を使用してバッチデータを Azure Cosmos DB コレクションに取り込む](IoT/spark-notebooks/pyspark/02-CosmosDBSynapseBatchIngestion.ipynb)
1. [03-CosmosDBSynapseJoins: Azure Synapse Link を使用して Azure Cosmos DB コレクション全体で結合と集計を実行する](IoT/spark-notebooks/pyspark/03-CosmosDBSynapseJoins.ipynb)
1. [04-CosmosDBSynapseML: Synapse Spark (MMLSpark) で Azure Synapse Link と Azure Cognitive Services を使用して異常検出を実行する](IoT/spark-notebooks/pyspark/04-CosmosDBSynapseML.ipynb)



## シナリオ 2 - 小売予測

In this scenario, you will ingest Retail data into Azure Cosmos DB using Azure Synapse Spark, perform joins and aggregations using Azure Synapse Link and perform Forecasting using [Azure Automated Machine Learning](https://docs.microsoft.com/ja-jp/azure/machine-learning/concept-automated-ml).


![IoT-components-dataflow](images/pipeline.PNG)


### ノートブックの実行

Import the below two synapse spark notebooks under the "Retail/spark-notebooks/pyspark/" dir on to the Synapse workspace and attach the Spark pool created in the prerequisite to the notebooks.
1. [Synapse Spark での売上予測データのバッチ取り込み](Retail/spark-notebooks/pyspark/1CosmoDBSynapseSparkBatchIngestion.ipynb)
1. [Synapse Spark で Azure Synapse Link と Azure Automated Machine Learning を使用して販売予測を実行する](Retail/spark-notebooks/pyspark/2SalesForecastingWithAML.ipynb)


## 重要な概念
* [Azure Cosmos DB 用 Azure Synapse Link](https://docs.microsoft.com/ja-jp/azure/cosmos-db/synapse-link)
* [Azure Cosmos DB 分析ストア](https://docs.microsoft.com/ja-jp/azure/cosmos-db/analytical-store-introduction)
* [Azure Cosmos DB 用 Synapse Link を構成する](https://docs.microsoft.com/ja-jp/azure/cosmos-db/synapse-link-frequently-asked-questions)
* [Synapse Studio から Synapse Link に接続する](https://docs.microsoft.com/ja-jp/azure/synapse-analytics/synapse-link/how-to-connect-synapse-link-cosmos-db)
* [Synapse Spark を使用した Cosmos DB 分析ストアのクエリ](https://docs.microsoft.com/ja-jp/azure/synapse-analytics/synapse-link/how-to-query-analytical-store-spark)


## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
