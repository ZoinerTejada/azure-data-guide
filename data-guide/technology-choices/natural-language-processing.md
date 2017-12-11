# Natural Language Processing Technology Choices

[About]()  
[What are your options when choosing an NLP service?](#options)  
[How do you choose?](#howtochoose)  
[Key Selection Criteria](#criteria)  
[Capability Matrix](#matrix)   
[Where to go from here](#wheretogo)  

<a name="about"></a>
Free-form text processing is performed against documents containing paragraphs of text, typically for the purpose of supporting search, but is also used to perform other natural language processing (NLP) tasks such as sentiment analysis, topic detection, language detection, key phrase extraction and document categorization. This article focuses on the technology choices that act in support of the latter.

## <a name="options"></a> What are your options when choosing an NLP service?
In Azure, all of the following services provide Natural Language Processing capabilities:
- [Azure HDInsight with Spark and Spark MLlib](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview)
- [Microsoft Cognitive Services](https://docs.microsoft.com/en-us/azure/#pivot=products&panel=cognitive)


## <a name="howtochoose"></a> How do you choose?
Each service brings with it a unique set of capabilities, giving you options in selecting the one that most closely meets your requirements. 

## <a name="criteria"></a> Key Selection Criteria

The following table summarize the key differences in capabilities between each. For NLP scenarios, begin choosing the appropriate service for your needs by answering these questions:
- Do you want to leverage pre-built models instead of training your own models with your own data?
    - If yes, then consider using the API's offered by Microsoft Cognitive Services.
- Do you need to train custom models against a large corpus of text data?
    - If yes, then consider using Azure HDInsight with Spark MLlib and Spark NLP.
- Do you need low level NLP capabilities like tokenization, stemming, lemmatization, and TF/IDF?
    - If yes, consider using Azure HDInsight with Spark MLlib and Spark NLP. 
- Do you need simple, high-level NLP capabilities like entity and intent identification, topic detection, spell check or sentiment analysis?
    - If yes, consider using the API's offered by Microsoft Cognitive Services.     


## <a name="matrix"></a> Capability Matrix

### General Capabilities
| | Azure HDInsight | Microsoft Cognitive Services |  
| --- | --- | --- | 
| Provides pre-trained models as a service | No | Yes |  
| REST API | Yes | Yes |  
| Programmability | Python, Scala, Java | C#, Java, Node.js, Python, PHP, Ruby |  
| Support processing of big data sets and large documents | Yes | No |


### Low-Level Natural Langauge Processing Capabilities
| | Azure HDInsight | Microsoft Cognitive Services |  
| --- | --- | --- | 
| Tokenizer | Yes - using Spark NLP | Yes - using Linguistic Analysis API |  
| Stemmer | Yes - using Spark NLP | No |
| Lemmatizer | Yes - using Spark NLP | No |
| Part of speech tagging | Yes - using Spark NLP | Yes - using Linguistic Analysis API |
| Term-Frequency/Inverse-Document Frequency (TF/IDF) | Yes - using Spark MLlib | No |
| String similarity - edit distance calculation | Yes - using Spark MLlib | No |
| N-gram calculation | Yes - using Spark MLlib | No |
| Stop word removal | Yes - using Spark MLlib | No |


### High-Level Natural Langauge Processing Capabilities
| | Azure HDInsight | Microsoft Cognitive Services |  
| --- | --- | --- | 
| Entity/Intent identification & extraction | No | Yes - using LUIS API |    
| Topic detection | Yes - using Spark NLP | Yes - using the Text Analytics API |  
| Spell Checking | Yes - using Spark NLP | Yes - using the Bing Spell Check API |
| Sentiment analysis | Yes - using Spark NLP | Yes - using the Text Analytics API |
| Language detection | No | Yes - using the Text Analytics API |
| Supports multiple languages besides English | No | Yes - Language support varies by API | 


## <a name="wheretogo"></a>Where to go from here
See Also:

Related Pipeline Patterns
- Working with text data
    - [Processing CSV and JSON files](../pipeline-patterns/processing-csv-and-json.md)
    - [Processing free-form text data](../pipeline-patterns/processing-free-form-text.md)
- [Machine Learning](../pipeline-patterns/machine-learning.md)
