 Advanced Analytics

**In this article**

[About]()  
[Machine Learning](#machinelearning)  
[Deep Learning](#deeplearning)  
[Artificial Intelligence](#ai)  
[Model Deployment](#operationalization)   
[Where to go from here](#wheretogo)  


<a name="about"></a>
Advanced analytics goes beyond the historical reporting and "slice and dice" data aggregation of traditional business intelligence (BI), and uses mathematical, probabilistic and statistical modeling techniques to enable predictive processing and automated decision making.

Advanced analytics solutions typically involve the following workloads:

* Interactive data exploration and visualization
* Machine Learning model training
* Real-time or batch predictive processing

Consider an advanced analytics architecture when you need to:

* Empower data scientists to experiment with large volumes of data
* Train (or retrain) machine learning models
* Provide predictive capabilities or Artificial Intelligence (AI) services

![Overall data pipeline with Machine Learning diagram](./images/data-pipeline-ml.png)

Most advanced analytics architectures include some or all of the following components:

* **Data storage**: Advanced analytics solutions require data to train machine learning models. Data scientists typically need to explore the data to identify its predictive *features* and the statistical relationships between them and the values they predict (known as a *label*). The predicted label can be a quantative value, like the financial value of something in the future or the duration of a flight delay in minutes; or it might represent a categorical *class*, like "true" or "false", "flight delay" or "no flight delay", or categories like "low risk", "medium risk", or "high risk". 

* **Batch processing**: To train a machine learning model, you typically need to process a large volume of training data, and the training of the model can take some time (on the order of minutes to hours). This training can be performed using scripts written in languages such as Python or R, and can be scaled out to reduce training time using distributed processing platforms like Apache Spark hosted in HDInsight or a Docker container.

* **Real-time message ingestion**: In production, many advanced analytics feed real-time data streams to a predictive model that has been published as a web service. The incoming data stream is typically captured in some form of queue and a stream processing engine pulls the data from this queue and applies the prediction to the input data in near real time.  

* **Stream processing**: Once you have a trained model, prediction (or scoring as it is sometimes called) is typically a very fast operation (on the order of milliseconds) for a given set of features.  After capturing real-time messages, the relevant feature values can be passed to the predictive service to generate a predicted label.

* **Analytical data store**: In some cases, the predicted label values are written to the analytical data store for reporting and future analysis.

* **Analysis and reporting**: As the name suggests, advanced analytics solutions usually produce some sort of report or analytical feed that includes predicted data values. Often, predicted label values are used to populate real-time dashboards.

* **Orchestration**: Although the initial data exploration and modeling is performed interactively by data scientists, many advanced analytics solutions periodically re-train models with new data- continually refining the accuracy of the models. This retraining can be automated using an orchestrated workflow.

### <a name="machinelearning"></a> Machine Learning
Machine Learning is a mathematical modeling technique used to train a predictive model. The general principle is to apply a statistical algorithm to a large dataset of historical data to uncover relationships between the fields it contains.

Machine Learning modeling is usually performed by data scientists, who need to thoroughly explore and prepare the data before training a model. This exploration and preparation typically involves a great deal of interactive data analysis and visualization - usually using languages such as Python and R in interactive tools and environments that are specifically designed for this task.

In some cases, you may be able to use [pre-trained models](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) that come with training data obtained and developed by Microsoft. The advantage of pre-trained models is that you can score and classify new content right away, even if you don't have the necessary training data, the resources to manage large datasets or train complex models.

There are two broad categories of machine learning:

* **Supervised Learning**: In a supervised learning model, the source data consists of a set of *feature* data fields that have a mathematical relationship with one or more *label* data fields. During the *training* phase of the machine learning process, the data set includes both features and known labels, and an algorithm is applied to fit a function that operates on the features to calculate the corresponding label predictions. Typically, a subset of the training dataset is held back and used to validate the performance of the trained model. Model validation seeks to answer questions like- how accurate is the model in correctly predicting the outcome? Does it perform better then random chance? When it makes it mistakes, what kind of mistakes does it make? 

When the model has been trained, it can be deployed into production and used with new datasets for which the label values are unknown, and apply the algorithm to predict the unknown values. Supervised learning models include *classification* (in which the label represents a specific *class* or category) and *regression* (in which the label is a quantitative numeric value). Supervised learning is the most common approach taken by machine learning. 

* **Unsupervised Learning**: In an unsupervised learning model, the training data does not include known label values. Instead, the algorithm makes its predictions based on its first exposure to the data. The most common form of unsupervised learning is *clustering*, where the algorithm determines the best way to split the data into into a specified number of clusters based on statistical similarities in the features. In clustering, the predicted outcome is the cluster number to which the input features belong. While they can sometimes be used directly to generate useful predictions, such as using clustering to identify groups of users in a database of customers, unsupervised learning approaches are most commonly used during data wrangling to identify the most useful data to provide to a supervised learning algorithm in training a model.  

Relevant Azure services:

- [Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/)
- [Machine Learning Server (R Server) on HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview)

### <a name="deeplearning"></a> Deep Learning

Machine learning models based on mathematical techniques like linear or logistic regression, and matrix factorization have been established for some time. More recently, the use of *deep learning* techniques based on neural networks has increased - driven largely by advances in research in this area along with the availability of highly scalable processing systems that leverage CPU and GPU hardware to reduce the time taken to train these complex models and combined with the ability to train the learners against big data.

Consequently, when designing a cloud architecture for advanced analytics, you should consider the need for large-scale processing of deep learning models; which can be provided through distributed processing platforms like Apache Spark and the latest generation of virtual machines that include access to GPU hardware and native capabilities to handle big data.

Relevant Azure services:

- [Deep Learning Virtual Machine](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/deep-learning-dsvm-overview)
- [Apache Spark on HDInsight](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-overview)

### <a name="ai"></a> Artificial Intelligence

Artificial Intelligence (AI) refers to scenarios where a machine mimics the cognitive functions associated with human minds, such as learning and problem solving. Because AI leverages machine learning algorithms, it is viewed as an umbrella term under which Machine Learning sits. Most AI solutions rely on a combination of predictive services, often implemented as web services, and natural langauge interfaces, such as chatbots that interact via text or speech, that are presented by AI apps running on mobile devices or other clients. In some cases, the machine learning model is embedded with the AI app, such as an iOS app that leverages a local model using Core ML.  

### <a name="operationalization"></a> Model Deployment
The predictive services that support AI applications may leverage custom machine learning models, or off-the-shelf cognitive services that provide access to pre-trained models. The process of deploying custom models into production is known as operationalization, where the same AI models that are trained and tested within the processing environment are serialized and made available to external applications and services for batch or self-service predictions. To utilize the predictive capability of the model, it is deserialized and loaded using the same machine learning library that contains the algorithm that was used to train the model in the first place. This library provides predictive functions (often called score or predict) that take the model and features as input and return the prediction. This logic is then wrapped in a function that an application can call directly or can further be exposed as a web service that is then invoked by applications. 


Relevant Azure services:

- [Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/)
- [Machine Learning Server (R Server) on HDInsight](https://docs.microsoft.com/azure/hdinsight/r-server/r-server-overview)

## <a name="wheretogo"></a>Where to go from here

Read Next: [Machine Learning pipeline pattern](../pipeline-patterns/machine-learning-at-scale.md)

See Also:

Related Common Architecture
- [Interactive Data Exploration](../common-architectures/interactive-data-exploration.md)

Related Pipeline Patterns
- [Machine Learning](../pipeline-patterns/machine-learning-at-scale.md)
- [Processing CSV and JSON files](../pipeline-patterns/processing-csv-and-json-files.md)

Related Technology Choices
- [Data Science and Machine Learning](../technology-choices/data-science-and-machine-learning.md)
- [Cognitive Services](../technology-choices/cognitive-services.md)

