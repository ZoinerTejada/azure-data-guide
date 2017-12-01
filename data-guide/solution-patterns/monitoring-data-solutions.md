# Monitoring Data Solutions

[About]()  
[When to use this data architecture](#whentouse)  
[Benefits](#benefits)  
[Challenges](#challenges)  
[Monitoring data solutions in Azure](#inazure)   
[Where to go from here](#wheretogo)  

<a name="about"></a>

Cloud applications are complex with many moving parts. Monitoring provides data to ensure that your applications and data pipelines stay up and running in a healthy state. It also helps you to stave off potential problems or troubleshoot past ones. In addition, you can use monitoring data to gain deep insights about your various solutions. This knowledge can help you to improve performance or maintainability, or automate actions that would otherwise require manual intervention.

When dealing with data, the range of things you need to monitor is both deep and wide. For instance, you might using memory-optimized database tables, putting pressure on your available memory. When you run out of memory, the system will no longer allow most write operations. If you're not using alerting features in Azure, you are at risk of discovering the issue when it's too late. Another example is monitoring data [pipeline orchestration](../technology-choices/pipeline-orchestration-data-movement.md) for moving and transforming data. Monitoring your orchestration pipeline will ensure that your [ETL/ELT or data flow & control flow](../common-architectures/data-pipeline.md) tasks are running as expected.

### Performance Monitoring

### Alerting

### Troubleshooting & Diagnostics



## <a name="whentouse"></a>When to use this architecture

Ideally, monitoring your data solutions should practiced from the moment of inception. Realistically, monitoring and alerting should be applied in production to your most critical services and components. The earlier you apply data monitoring practices, the better chance you have at selecting the right things to monitor and be alerted on, and will have a better sense of your solution's overall capacity and resiliency, based on real evidence. 

## <a name="benefits"></a>Benefits

Monitoring offers the following benefits:

* Detect emerging issues before they become real problems.
* Gain insight on the current state of your solution, based on historical records and having established a baseline.
* Know when performance is taking a hit so you can scale accordingly, and research into what has changed to cause the issue.
* You have a better chance at being proactive in ensuring smooth operation of your solution, rather than always reactively responding to issues and putting out fires that shouldn't have started in the first place.
* Gather valuable data that will help you troubleshoot issues.

## <a name="challenges"></a>Challenges

Establishing monitoring can have some of the following challenges:

* Aggregate diagnostic and performance data into a single overall view, as opposed to viewing the monitoring information in multiple locations.
* Make huge diagnostic logs usable by adding search and alerting mechanisms.
* Configure alerts on the services you need most.
* Predict problems before they happen.

## <a name="inazure"></a>Monitoring in Azure



![Time Series Insights](./images/monitoring.png)


## <a name="wheretogo"></a>Where to go from here
Read Next:
[Data ingest technology choices](../technology-choices/data-ingest.md)

See Also:

Related Technology Choices
- [Analysis, Visualizations, & Reporting](../technology-choices/analysis-visualizations-reporting.md)
- [Data Serving Storage](../technology-choices/data-serving-storage.md)
- Real-time Processing