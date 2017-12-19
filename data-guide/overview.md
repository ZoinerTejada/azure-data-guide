# Azure Data Architecture Guide

This guide presents a structured approach for designing data-centric solutions on Azure. It is based on proven practices derived from customer engagements and is intended as an entry point for all data related topics in Azure. The guide covers the ‘big picture’ concepts in common data architectures, which lead you to the pipeline patterns used by that architecture. The pipeline patterns are used to describe how the various processing and storage components fit together in handling the data. Finally, the technology choices will help you narrow the list of candidate Azure services—that are appropriate to your solution pipeline—down to those services that are most appropriate to your specific requirements.

The [Implementation Examples](#implementation-examples) section below offers a snapshot of recommended services for our top customer scenarios. The examples show you a possible technology implementation and lead you into the content to understand the right technology choices for your business.

![Overview of the structure of the guide](./images/overview-flowchart.png)

# Introduction

The cloud is changing the way applications are designed, including how data is processed and stored. Instead of a single general-purpose database that handles all of a solution's data, the _polyglot persistence_ approach is to use multiple, specialized databases and datastores — each optimized to provide specific capabilities needed by the solution. This approach is called polyglot persistence. The perspective on data in the solution changes as a result. It is no longer the case that there are multiple layers of business logic and a single data layer. Instead modern, polyglot persistence solutions are designed around the notion of a data pipeline which describe how data flows through a solution, where it is processed, where it is stored and how its consumed by the next component in the pipeline. 

Owing to the fundamental importance of the data pipeline throughout modern data architectures, this guide demonstrates all data pipelines as variants of the following canonical data pipeline:  

![Overview Data Pipeline](./images/overall-data-pipeline.png)

# <a name="implementation-examples"></a>Implementation Examples

The following examples are technology implementations we have seen directly in our customer engagements. The examples can help lead you into the content to make the right technology choices for your business.

## On-Demand Big Data Analytics

Create cloud-scale, enterprise-ready Hadoop clusters in a matter of minutes for batch and real-time data processing. With Azure, you can build your entire big data processing and analytics pipeline from massive data ingest to world-class business intelligence and reporting, using the technology that's right for you.

COLD PATH: Source data (web, mobile) --> Azure Blob storage --> HDInsight Interactive Query (Hive LLAP) --> Power BI (HDI Interactive Query connector)

HOT PATH: Source data (web, mobile) --> Event Hubs --> Azure Stream Analytics (windowing queries for pre-aggregation) --> Azure SQL Server (in-memory columnstore) --> Power BI

4-8 service icons

### Highlighted services

* [Service1]()
* [Service2]()
* [Service3]()
* [Service4]()

### In this guide

* Common Data Architectures
    * [Big Data](./common-architectures/big-data.md)
    * [Advanced Analytics](./common-architectures/advanced-analytics.md)
* Pipeline Patterns
    * [Processing CSV and JSON files](./pipeline-patterns/processing-csv-and-json-files.md)
    * [Processing free-form text](./pipeline-patterns/processing-free-form-text.md)
* Technology Choices
    * [Batch processing](./technology-choices/batch-processing.md)
    * [Real-time processing](./technology-choices/real-time-processing.md)
    * [Data serving storage](./technology-choices/data-serving-storage.md)
    * [Data ingest](./technology-choices/data-ingest.md)
    * [Analysis, visualizations, and reporting](./technology-choices/analysis-visualizations-reporting.md)

## Advanced Analytics & Deep Learning

Go beyond historical reporting and exploratory analysis of your data by enabling predictive processing and automated decision making with Azure services like [Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/preview/overview-what-is-azure-ml) and [Apache Spark on HDInsight](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-jupyter-spark-sql). When you need to harness the power of multiple GPUs to build sophisticated deep neural architectures and train them on a large data set, get a jump start on the task with [Deep Learning Virtual Machines](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/deep-learning-dsvm-overview) and [CNTK](https://github.com/Microsoft/CNTK/wiki), the unified deep-learning toolkit by Microsoft.

ADVANCED ANALYTICS: Apache Spark on HDInsight (or Databricks?) to train and run model --> Azure Machine Learning services (containerized Docker-based web services to expose trained ML model through REST API) --> Web/mobile application that consumes the model

DEEP LEARNING: Images (Azure Blob storage) / Metadata (Cosmos DB) --> Deep Learning Virtual Machine (train model) --> Azure Machine Learning services (containerized Docker-based web services to expose trained ML model through REST API) --> Azure App Services (host web app that consumes web services and displays scored images)

Deep learning sample arch: https://github.com/Azure/cortana-intelligence-product-detection-from-images/tree/master/technical_deployment

4-8 service icons

### Highlighted services

* [Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/preview/overview-what-is-azure-ml)
* [Deep Learning Virtual Machines](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/deep-learning-dsvm-overview)
* [Apache Spark on HDInsight](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-jupyter-spark-sql)
* [Service4]()

### In this guide

* Common Data Architectures
    * [Link1]()
    * [Link2]()
* Pipeline Patterns
    * [Link1]()
    * [Link2]()
* Technology Choices
    * [Link1]()
    * [Link2]()

## Hybrid

When you need hybrid on-premises and cloud options, nothing comes close to Azure. Use [Azure Stack](https://docs.microsoft.com/azure/azure-stack/azure-stack-poc) to deliver Azure services from your own datacenter, using the same tools in both environments for unmatched consistency, allowing you to deploy your data solution to the location that best meets your needs. [Use ExpressRoute](https://docs.microsoft.com/azure/azure-stack/azure-stack-connect-expressroute) for a private, dedicated and high speed connection that extends your on-premises network into Azure.

[Azure Stack hosting functions/web apps] - [express route or internet] -> [App Services that consume data from on-premises]
[SQL Server Database on-premises] - [express route or internet] -> [Azure stretch database]

Sample architecture:
https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/expressroute-vpn-failover

4-8 service icons

### Highlighted services

* [Azure Stack](https://docs.microsoft.com/azure/azure-stack/azure-stack-poc)
* [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction)
* [Service3]()
* [Service4]()

### In this guide

* Common Data Architectures
    * [Link1]()
    * [Link2]()
* Pipeline Patterns
    * [Link1]()
    * [Link2]()
* Technology Choices
    * [Link1]()
    * [Link2]()

## Clickstream Analysis

Engage with your customers and uncover insights from data generated by clickstream logs in real-time using Azure. Rapidly ingest incoming data through Event Hubs (replace with Kafka?), process with Spark streaming and Spark ML for predicting product recommendations, then use the Spark to Azure Cosmos DB connector to save the processed data to Cosmos DB for global distribution to your customers, wherever they are.

Source (web/mobile) --> Event Hubs or Apache Kafka --> Apache Spark on HDInsight (Spark ML) -- Spark Connector --> Cosmos DB --> web/mobile apps for personalized product recommendations

4-8 service icons

### Highlighted services

* [Event Hubs](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-introduction)
* [Apache Spark on HDInsight](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-jupyter-spark-sql)
* [Service3]()
* [Service4]()

### In this guide

* Common Data Architectures
    * [Link1]()
    * [Link2]()
* Pipeline Patterns
    * [Link1]()
    * [Link2]()
* Technology Choices
    * [Link1]()
    * [Link2]()

## Business Intelligence

Azure offers a rich data and analytics platform so you can build scalable BI and reporting solutions. Create rich, interactive reports with Power BI by having it connect to Azure Analysis Services, which uses a highly optimized in-memory engine to provide responses to queries against user-friendly semantic models within a fraction of a second. The underlying data is provided by Azure SQL Data Warehouse, acting as a central repository of integrated data from one or more disparate sources.

Source data --> SQL Data Warehouse --> Azure Analysis Services --> Power BI
-------------------------------------
Azure Data Factory drives the process
-------------------------------------

4-8 service icons

### Highlighted services

* [Power BI]()
* [Azure Analysis Services]()
* [Azure SQL Data Warehouse]()
* [Service4]()

### In this guide

* Common Data Architectures
    * [Link1]()
    * [Link2]()
* Pipeline Patterns
    * [Link1]()
    * [Link2]()
* Technology Choices
    * [Analysis, Visualizations, & Reporting](./technology-choices/analysis-visualizations-reporting.md)

## Smart Applications (MS term is Intelligent Applications)

Quickly add intelligence to your applications with Cognitive Services, and coordinate automated interactions using Azure Bot Service. This can save you months of creating and refining sophisticated algorithms to naturally interact with your users through speech, text, vision, knowledge, and search capabilities.

Azure Active Directory B2C   Cognitive Services
   ^                              ^
   |                              |
Web/mobile app <--> Azure Bot Service --> Azure SQL Database
   ^
   |
   v
Custom Speech Service

4-8 service icons

### Highlighted services

* [Service1]()
* [Service2]()
* [Service3]()
* [Service4]()

### In this guide

* Common Data Architectures
    * [Link1]()
    * [Link2]()
* Pipeline Patterns
    * [Link1]()
    * [Link2]()
* Technology Choices
    * [Link1]()
    * [Link2]()

## Data Warehousing

Store data coming in from multiple sources into Azure Data Lake in their native format. SQL Data Warehouse can directly query against the data with a combination of external tables and schema on read capabilities through PolyBase. Use Azure Data Factory to store the data you need within your warehouse, and quickly analyze and visualize the combined data with Power BI.

Multiple data sources (IoT, logs, internal sources, social media) --> Azure Data Lake Store --> SQL Data Warehouse --> Power BI
                                                                      ---------------------------
                                                                      Orchestration: PolyBase/ADF
                                                                      ---------------------------

4-8 service icons

### Highlighted services

* [Service1]()
* [Service2]()
* [Service3]()
* [Service4]()

### In this guide

* Common Data Architectures
    * [Link1]()
    * [Link2]()
* Pipeline Patterns
    * [Link1]()
    * [Link2]()
* Technology Choices
    * [Link1]()
    * [Link2]()

## ETL

Capture web application logs and custom telemetry with Application Insights, and create, schedule, and manage your ETL data pipeline using Azure Data Factory. Deploy your SSIS packages to Azure with the Azure-SSIS integration runtime (IR) in Azure Data Factory to apply data transformation as a step in the ETL pipeline before loading the transformed data into Azure SQL Database.

Application Insights --> Blob Storage --> Azure Data Factory (transform with SSIS packages and load transformed data to destination) --> Azure SQL Database

4-8 service icons

### Highlighted services

* [Azure Data Factory]()
* [Azure-SSIS integration runtime](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure)
* [Service3]()
* [Service4]()

### In this guide

* Common Data Architectures
    * [Link1]()
    * [Link2]()
* Pipeline Patterns
    * [Link1]()
    * [Link2]()
* Technology Choices
    * [Link1]()
    * [Link2]()

# How this guide is structured

This guide is structured so that your entry point to the content can be at the level of the common architecture, the pipeline pattern or the technology choices for a particular pipeline scenario. 

At the end of each article is provided a Read Next link which you can follow to take a linear path thru the content. In addition, links to alternate and related content are provided to guide you to related content that provides you a perspective on the options, as well as provides links back up to the related parent topics and links to drill down into further detail.


## <a name="wheretogo"></a>Where to go from here

Read Next:
[Common Data Architectures](./common-architectures/overview.md)

See Also:

Alternative Common Architectures
- [Non-Relational Data](./common-architectures/non-relational-data.md)
- [Big Data](./common-architectures/big-data.md)

Related Common Architectures
- [Relational Data](./common-architectures/relational-data.md)
- [Transactional Data](./common-architectures/transactional-data.md)
- [Semantic Modeling](./common-architectures/semantic-modeling.md)
- [Advanced Analytics](./common-architectures/advanced-analytics.md)
- [Data Pipeline](./common-architectures/data-pipeline.md)
- [Interactive Data Exploration](./common-architectures/interactive-data-exploration.md)
