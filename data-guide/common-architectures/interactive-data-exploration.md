# Interactive Data Exploration

In many corporate business intelligence (BI) solutions, reports and semantic models for analysis are created by BI specialists and managed centrally. However, increasingly organizations are seeking to empower users to make data-driven decisions by providing access to it for self-service analytics. Additionally, a growing number of organizations are hiring *data scientists* to build advanced analytical models, and empowering these users to explore data interactively using specialist tools for staistical modeling and analysis.

## Self-Service BI
Self-service BI is a name given to a modern approach to business decision making in which users are empowered to find, explore, and share insights from data across the enterprise. To accomplish this, the data ecosystem must support:
* Discovery of business data sources though a data catalog
* Master data management to ensure consistency of data entity defintions and values.
* Interactive data modeling and visualization tools for business users.

In a self-service BI solution, business users typically find and consume data sources that are relevant to their particular area of the business, and use intutitive tools and productivity applications to define personal data models and reports, which they can share with their colleagues.

### Relevant Services
Tools and services used to implement self-service BI include:
* Azure Data Catalog
* Microsoft Office 365 - in particular Excel and Power Pivot
* Microsoft Power BI

## Data Science Experimentation
When an organization requires advanced analytics and predictive modeling, the initial preparation work is usually undertaken by specialists data scientists who need to explore the data and apply statistical analytical techniques to determine relationships between data *features* and the desired predicted *labels*. Such data exploration is typically conducted using programming languages such as Python or R that inherently support statistical modeling and visualization. Typically, the scripts used to explore the data are hosted in specialized environments such as Jupyter Notebooks to enable data scientists to explore the data programmatically while documenting and sharing the insights they find.

### Relevant Services
Tools and services used to empower data scientists to explore data include:
* Azure Notebooks
* Azure Machine Learning Studio
* Azure Machine Learning Experimentation Services
* The Data Science Virtual Machine

## <a name="wheretogo"></a>Where to go from here

Read Next: [Relational Data Common Architecture](./relational-data.md)

See Also:

Related Common Architectures
- [Transactional Data](./transactional-data.md)
- [Non-Relational & NoSQL Data](./non-relational-data.md)
- [Semantic Modeling](./semantic-modeling.md)

Related Solution Pipelines
- [Online Analytical Processing](../pipeline-patterns/online-analytical-processing.md)
- [Online Transaction Processing](../pipeline-patterns/online-transaction-processing.md)
- [Data Warehousing](../pipeline-patterns/data-warehousing.md)

Related Technology Choices:
- [Analysis, Visualizations and Reporting](../technology-choices/analysis-visualizations-reporting.md)
- [Data Warehouses](../technology-choices/data-warehouses.md)