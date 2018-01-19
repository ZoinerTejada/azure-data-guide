# Interactive Data Exploration
<!--No "In this article" necessary for this one?>
In many corporate business intelligence (BI) solutions, reports and semantic models for analysis are created by BI specialists and managed centrally. However, increasingly organizations are seeking to empower users to make data-driven decisions by providing access to it<!--not completely sure what it refers to here? The data? maybe say, "that data" normally I don't like to be repetitive, but I think it would help here.--> for self-service analytics. Additionally, a growing number of organizations are hiring *data scientists* to build advanced analytical models, and empowering these users to explore data interactively using specialist tools for statistical modeling and analysis.

## Self-service BI
Self-service BI is a name given to a modern approach to business decision making in which users are empowered to find, explore, and share insights from data across the enterprise. To accomplish this, the data ecosystem must support:
* Discovery of business data sources through a data catalog.
* Master data management to ensure consistency of data entity defintions and values.
* Interactive data modeling and visualization tools for business users.

In a self-service BI solution, business users typically find and consume data sources that are relevant to their particular area of the business, and use intuitive tools and productivity applications to define personal data models and reports that they can share with their colleagues.

Relevant Azure service:
- [Azure Data Catalog](https://docs.microsoft.com/azure/data-catalog/data-catalog-what-is-data-catalog)
- Microsoft Office 365 - in particular Excel and Power Pivot
- [Microsoft Power BI](https://powerbi.microsoft.com/)

## Data science experimentation
When an organization requires advanced analytics and predictive modeling, the initial preparation work is usually undertaken by specialists data scientists who need to explore the data and apply statistical analytical techniques to determine relationships between data *features* and the desired predicted *labels*. Such data exploration is typically conducted using programming languages such as Python or R that inherently support statistical modeling and visualization. Typically, the scripts used to explore the data are hosted in specialized environments such as Jupyter Notebooks to enable data scientists to explore the data programmatically while documenting and sharing the insights they find.

Relevant Azure service:  
- [Azure Notebooks](https://notebooks.azure.com/)
- [Azure Machine Learning Studio](https://docs.microsoft.com/azure/machine-learning/studio/what-is-ml-studio)
- [Azure Machine Learning Experimentation Services](https://docs.microsoft.com/azure/machine-learning/preview/experimentation-service-configuration)
- [The Data Science Virtual Machine](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview)

## <a name="wheretogo"></a>Where to go from here

Read next: [Relational Data Common Architecture](./relational-data.md)

See also:

Related common architectures
- [Transactional Data](./transactional-data.md)
- [Non-Relational & NoSQL Data](./non-relational-data.md)
- [Semantic Modeling](./semantic-modeling.md)

Related pipeline patterns
- [Online Analytical Processing](../pipeline-patterns/online-analytical-processing.md)
- [Online Transaction Processing](../pipeline-patterns/online-transaction-processing.md)
- [Data Warehousing](../pipeline-patterns/data-warehousing.md)

Related technology choices
- [Analysis, Visualizations and Reporting](../technology-choices/analysis-visualizations-reporting.md)
- [Data Warehouses](../technology-choices/data-warehouses.md)
