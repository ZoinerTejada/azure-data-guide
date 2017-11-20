# Advanced Analytics

**In this article**

[About]()  
[Machine Learning](#machinelearning)  
[Deep Learning](#deeplearning)  
[Artificial Intelligence](ai)  
[Where to go from here](#wheretogo)  

<a name="about"></a>
Advanced analytics goes beyond the historical reporting and "slice and dice" data aggregation of traditional business intelligence (BI), and uses mathematical and statistical modeling techniques to enable predictive processing and automated decision making.

Advanced analytics solutions typically involve the following workloads:

* Interactive data exploration and visualization
* Machine Learning model training
* Real-time or batch predictive processing

Consider an advanced analytics architectures when you need to:

* Empower data scientists to experiment with large volumes of data
* Train (or retrain) machine learning models
* Service predictive analytics clients or Artificial Intelligence (AI) services

![Overall data pipeline with Machine Learning diagram](./images/data-pipeline-ml.png)

Most advanced analytics architectures include some or all of the following components:

* **Data storage**: Advanced analytics solutions require data to train machine learning models. Data scientists typically need to explore the data to identify its predictive *features* and the statistical relationships between them and the *labels* they predict.

* **Batch processing**: To train a machine learning model, you typically need to process a large volume of training data. This training can be performed using scripts written in languages such as Python or R, and can be scaled out to reduce training time using distributed processing platforms like Apache Spark hosted in HDInsight or a Docker container.

* **Real-time message ingestion**: In production, many advanced analytics feed real-time data streams to a predictive model that has been published as a web service. This requires capturing the incoming real-time data.

* **Stream processing**: After capturing real-time messages, the relevant feature values can be passed to the predictive service to generate a predicted label.

* **Analytical data store**: In some cases, the predicted label values are written to the analytical data store for reporting and future analysis.

* **Analysis and reporting**: As the name suggests, advanced analytics solutions usually produce some sort of report or analytical feed that includes predicted data values. Often, predicted label values are used to populate real-time dashboards.

* **Orchestration**: Although the initial data exploration and modeling is performed interactively by data scientists, many advanced analytics solutions periodically re-train models with new data - continually refining the accuracy of the models. This retraining can be automated using an orchestrated workflow.

### <a name="machinelearning"></a> Machine Learning
Machine Learning is a mathematical modeling technique used to train a predictive model. The general principle is to apply a statistical algorithm to a large dataset of historical data to uncover relationships between the fields it contains.

Machine Learning modeling is usually performed by data scientists, who need to thoroughly explore and prepare the data before training a model. This exploration and preparation typically involves a great deal of interactive data analysis and visualization - usually using languages such as Python and R in interactive tools and environments that are specifically designed for this task.

In some cases, you may be able to use [pre-trained models](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) that come with training data obtained and developed by Microsoft. The advantage of pre-trained models is that you can score and classify new content right away, even if you don't have the resources to obtain large datasets or train complex models.

There are two broad categories of machine learning:

* **Supervised Learning**: In a supervised learning model, the source data consists of a set of *feature* data fields that have a statistical relationship with one or more *label* data fields. During the *training* phase of the machine learning process, the data set includes both features and known labels, and a statistical algorithm is applied to fit a function that operates on the features to calculate the corresponding labels. Typically, a subset of the training dataset is held back and used to validate the trained model. Then when the model has been trained, it can be deployed into production and used with new datasets for which the label vales are unknown, and apply the algorithm to predict the unknown values. Supervised learning models include *classification* (in which the label represents a specific *class* or category) and *regression* (in which the label is a quantitative numeric value).

* **Unsupervised Learning**: In an unsupervised learning model, the training data does not include known label values. Instead, the model is trained to allocate data entities into a specified number of clusters based on statistical similarities in the features.

Relevant Azure services:

- [Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/)
- [Machine Learning Server (R Server) on HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview)

### <a name="deeplearning"></a> Deep Learning

Machine learning models based on statistical techniques like linear or logistic regression, and matrix factorization have been established for some time. More recently, the use of *deep learning* techniques based on neural networks has increased - driven largely by advances in research in this area along with the availability of highly scalable processing systems that leverage CPU and GPU hardware to reduce the time taken to train these complex models.

Consequently, when designing a cloud architecture for advanced analytics, you should consider the need for large-scale processing of deep learning models; which can be provided through distributed processing platforms like Apache Spark and the latest generation of virtual machines that include access to GPU hardware.

Relevant Azure services:

- [Deep Learning Virtual Machine](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/deep-learning-dsvm-overview)
- [Apache Spark on HDInsight](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-overview)

### <a name="ai"></a> Artificial Intelligence

Artificial intelligence (AI) is a fast-growing type of solution that is built on machine learning. Most AI solutions rely on predictive services, often implemented as web services that are consumed by AI apps running on mobile devices or other clients.

In production, the predictive services that support AI applications may be custom machine learning models deployed as web services, or off-the-shelf cognitive services. This is known as machine learning model operationalization, where the same AI models that are developed and tested within the processing environment are made available to external applications and services for batch or self-service predictions.

Relevant Azure services:

- [Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/)
- [Machine Learning Server (R Server) on HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview)

## <a name="wheretogo"></a>Where to go from here

Read Next: [Machine Learning solution pattern](../solution-patterns/machine-learning.md)

See Also:

Related Solution Patterns
- [Interactive Data Exploration](../solution-patterns/interactive-data-exploration.md)
- [Machine Learning](../solution-patterns/machine-learning.md)
- [Processing CSV and JSON files](../solution-patterns/processing-csv-and-json-files.md)

Related Technology Choices
- [Data Science and Machine Learning](../technology-choices/data-science-and-machine-learning.md)
- [Cognitive Services](../technology-choices/cognitive-services.md)

