# Data Science and Machine Learning
Data science and machine learning is a workload that is usually undertaken by data scientists. It requires specialist tools, many of which are designed specifically for the type of interactive data exploration and modeling tasks that a data scientist must perform.

Machine learning solutions are built iteratively, and have two distinct phases:
* Data preparation and modeling
* Deployment and consumption of predictive services.

## Tools and Services for Data Preparation and Modeling
Data scientists typically prefer to work with data using custom code written in Python or R. This code is generally run interactively, with the data scientists using it to query and explore the data, generating visualizations and statistics to help determine the relationships with it.
There are many interactive environments for R and Python that data scientsits can use. A particular favorite is **Jupyter Notebooks**, which provides a browser-based shell that enables data scientists to create *notebook* files that contain R or Python code and markdown text; making it an effective way to collaborate by sharing and documenting code and results in a single document.

Other commonly used tools include:
* **Spyder**: The interactive development environment (IDE) for Python provided with thr Anaconda Python distribution.
* **R Studio**: An IDE for the R programming language.
* **Visual Studio Code**: A lighweight, multi-platform coding environment that supports Python as well as commonly used frameworks for machine learning and AI development.

In addition to these tools, data scientists can leverage Azure services to simplify code and model management.

### Azure Notebooks
Azure Notebooks is an online Jupyter Notebooks service that enables data scientists to create, run, and share Jupyter Notebooks in cloud-based libraries.

Key Benefits:
* Free service - no Azure subscription required.
* No need to install Jupyter and the supporting R or Python distributions locally - just use a browser.
* Manage your own online libraries and access them from any device.
* Share your notebooks with collaborators.

Considerations:
* You will be unable to access your notebooks when offline.
* Limited processing capabilities of the free notebook service may not be enough to train large or complex models.

### Data Science Virtual Machine
The data science virtual machine is an Azure virtual machine image that includes the tools and frameworks commonly used by data scientists, including R, Python, Jupyter Notebooks, Visual Studio Code, and libraries for machine learning modeling such as the Microsoft cognitive toolkit. These tools can be complex and time consuming to to install, and contain many inter-dependencies that often lead to version management issues. Having a preinstalled image can reduce the time data scientists spend troubleshooting environment issues, allowing them to focus on the data exploration and modeling tasks they need to perform.

Key Benefits:
* Reduced time to install, manage, and troubleshoot data science tools and frameworks.
* The latest versions of all commonly used tools and frameworks are included.
* VM options include highly scalable images with GPU capabilities for intensive data modeling.

Considerations:
* The VM cannot be accessed when offline.
* Running a VM incurs Azure charges, so you must be careful to have it running only when required.

### Azure Machine Learning
Azure Machine Learning is a cloud-based service for managing machine learning experiments and models. It includes an experimentation service that tracks data preparation and modeling training scripts, maintaining a history of all executions so you can compare model performance across iterations. A client tool named Azure Machine Learning Workbench provides a central interface for script management and history, while still enabling data scientists to create their scripts in their tool of choice; such as Jupyter Notebooks or Visual Studio Code.

From Azure Machine Learning workbench, you can use the interactive data preparation tools to simplify common data "wrangling" tasks, and you can configure the script execution environment to run model training scripts locally, in a scalable Docker container, or in Spark.

When you are ready to deploy your model, the Workbench environment enables you to package up the model and deploy it as a web service to a Docker container, Spark on Azure HDinsight, Microsoft Machine Learning Server, or SQL Server. The Azure Machine Learning Model Management service then enables you to track and manage model deployments in the cloud, on edge devices, or across the enterprise.

Key Benefits:
* Central managamenent of scripts and run history, making it easy to compare model versions.
* Interactive data wrangling through a visual editor.
* Easy deployment and management of models to the cloud or edge devices.

Considerations:
* Requires some familiarization with the model management model and Workbench tool environment.

### Azure Batch AI
Azure Batch AI enables you to run your machine learning experiments in parallel, using any framework and perform model training at scale across a cluster of Virtual Machines with GPUs. Batch AI training enables you to scale out deep learning jobs across clustered GPUs, using frameworks such as Cognitive Toolkit, Caffe, Chainer and TensorFlow.
Azure Machine Learning Model Management can be used to take models from Batch AI training to deploy, manage, and monitor them.  

### Azure Machine Learning Studio
Azure Machine Learning Studio is a cloud-based, visual development environment for creating data experiments, training machine learning models, and publishing them as web services in Azure.
It's visual "drag and drop" nature makes it possible for data scientists and power users to create effective machine learning solutions quickly and easily, while supporting custom R and Python logic, a wide range of established statistical algorithms and techniques for machine learning modeling tasks, and built-in support for Jupyter Notebooks.

Key Benefits:
* Interative visual interface enabling machine learning modeling with minimal code.
* Built-in Jupyter Notebooks for data exploration.
* Direct deployment of trained models as Azure web services

Considerations:
* Limited scalability - the maximum size of a training dataset is 10 GB.
* Online only - no offline development environment.
* No support for the latest deep learning models and frameworks.

## Tools and Services for Deploying Machine Learning Models
After a data scientist has created a machine learning model, you will typically need to deploy it and consume it from applications or in other data flows. There are a number of potential deployment targets for machine learning models.

### Spark on Azure HDInsight
Apache Spark includes *SparkML*, a framework and library for machine learning models. Additionally, the Microsoft Machine Learning library for Spark (*MMLSpark*) provides deep learning algorithms support for predictive models in Spark.

Key Benefits:
* Spark is a distributed platform that offers high scalability for  high-volume machine learning processes.
* You can deploy models directly to Spark in HDinsight from Azure Machine Learning Workbench, and manage them using the Azure Machine Learning Model Management service.

Considerations:
* Spark runs in an HDinsght cluster, which incurs charges the whole time it is running. If the machine learning service will only be used occassionally, this may result in unnecessary costs.

### Web Service in a Container
You can deploy a machine learning model as a Python web service in a docker container. This enables you to deploy the model to the cloud (in the Azure Container Service) or to an edge device where it can be used locally with the data on which it operates.

Key Benefits:
* Containers are a lightweight and generally cost effective way to package and deploy services.
* Azure Container Service makes it possible to scale your service in a Kubernates cluster.
* The ability to deploy to an edge device menables you to move your predictive logic closer to the data.
* You can deploy to a container directly from Azure Machine Learning Workbench.

Considerations:
* This deployment model is ased on Docker containers; so you should be familiar with this technology before deploying a web service this way.

### Microsoft Machine Learning Server
ML Server (formerly Microsoft R Server) is a scalable platform for R and Python code, specicially designed for Machine Learning scenarios.

Key Benefits:
* High scalability
* Direct deployment from Azure Machine Learning Workbench

Considerations:
* You need to deploy and manage ML Server in your enterprise.

### Microsoft SQL Server
Microsoft SQL Server supports R and Python natively, enabling you to encapsulate machine learning models built in these languages as Transact-SQL functions in a database.

Key Benefits:
* Encapsulate predictive logic in a database function, making it easy to include in data-tier logic.

Consideratons:
* Assumes a SQL Server database as the data-tier for your application.

### Azure Machine Learning Web Service
When you create a machine learning model using Azure Machine Learnign Studio, you can deploy it as a web service. This ca then be consumed through a REST interface from any client applications capable of communicating by HTTP.

Key Benefits:
* Ease of development and deployment
* Web Service management portal with basic monitoring metrics
* Built-in support for calling Azure Machine Learning web services from:
  * Azure Data Lake Analytics
  * Azure Data Factory
  * Azure Stream Analytics

Considerations:
* Only available for models built using Azure Machine Learning Studio.
* Web-based access only


