# Natural language processing technology choices

[About]()  
[What are your options when choosing an NLP service?](#options)  
[How do you choose?](#howtochoose)  
[Key selection criteria](#criteria)  
[Capability matrix](#matrix)   
[Where to go from here](#wheretogo)  

<a name="about"></a>
Free-form text processing is performed against documents containing paragraphs of text, typically for the purpose of supporting search, but is also used to perform other natural language processing (NLP) tasks such as sentiment analysis, topic detection, language detection, key phrase extraction, and document categorization. This article focuses on the technology choices that act in support of the NLP tasks.

## <a name="options"></a> What are your options when choosing an NLP service?

In Azure, the following services provide natural language processing (NLP) capabilities:

- [Azure HDInsight with Spark and Spark MLlib](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview)
- [Microsoft Cognitive Services](https://docs.microsoft.com/en-us/azure/#pivot=products&panel=cognitive)

## <a name="howtochoose"></a> How do you choose?

Each service brings with it a unique set of capabilities, giving you options in selecting the one that most closely meets your requirements. 

## <a name="criteria"></a> Key selection criteria

For NLP scenarios, begin choosing the appropriate service for your needs by answering these questions:
- Do you want to leverage prebuilt models instead of training your own models with your own data?
    - If yes (you want prebuilt models), then consider using the APIs offered by Microsoft Cognitive Services.
- Do you need to train custom models against a large corpus of text data?
    - If yes, then consider using Azure HDInsight with Spark MLlib and Spark NLP.
- Do you need low-level NLP capabilities like tokenization, stemming, lemmatization, and term frequency/inverse document frequency (TF/IDF)?
    - If yes, consider using Azure HDInsight with Spark MLlib and Spark NLP.
- Do you need simple, high-level NLP capabilities like entity and intent identification, topic detection, spell check, or sentiment analysis?
    - If yes, consider using the APIs offered by Microsoft Cognitive Services.

## <a name="matrix"></a> Capability matrix

Based on your responses to the questions above, the following tables will help you select the choice that's right for you.

### General capabilities

| | Azure HDInsight | Microsoft Cognitive Services |
| --- | --- | --- |
| Provides pretrained models as a service | No | Yes |
| REST API | Yes | Yes |
| Programmability | Python, Scala, Java | C#, Java, Node.js, Python, PHP, Ruby |
| Support processing of big data sets and large documents | Yes | No |

### Low-level natural language processing capabilities

| | Azure HDInsight | Microsoft Cognitive Services |  
| --- | --- | --- | 
| Tokenizer | Yes&mdash;using Spark NLP | Yes&mdash;using Linguistic Analysis API |
| Stemmer | Yes&mdash;using Spark NLP | No |
| Lemmatizer | Yes&mdash;using Spark NLP | No |
| Part of speech tagging | Yes&mdash;using Spark NLP | Yes&mdash;using Linguistic Analysis API |
| Term frequency/inverse-document frequency (TF/IDF) | Yes&mdash;using Spark MLlib | No |
| String similarity&mdash;edit distance calculation | Yes&mdash;using Spark MLlib | No |
| N-gram calculation | Yes&mdash;using Spark MLlib | No |
| Stop word removal | Yes&mdash;using Spark MLlib | No |

### High-level natural language processing capabilities

| | Azure HDInsight | Microsoft Cognitive Services |
| --- | --- | --- | 
| Entity/intent identification & extraction | No | Yes&mdash;using Language Understanding Intelligent Service (LUIS) API |    
| Topic detection | Yes&mdash;using Spark NLP | Yes&mdash;using the Text Analytics API |
| Spell checking | Yes&mdash;using Spark NLP | Yes&mdash;using the Bing Spell Check API |
| Sentiment analysis | Yes&mdash;using Spark NLP | Yes&mdash;using the Text Analytics API |
| Language detection | No | Yes&mdash;using the Text Analytics API |
| Supports multiple languages besides English | No | Yes&mdash;language support varies by API |

## <a name="wheretogo"></a>Where to go from here

See also:

Related pipeline patterns
- Working with text data
    - [Processing CSV and JSON files](../pipeline-patterns/processing-csv-and-json.md)
    - [Processing free-form text data](../pipeline-patterns/processing-free-form-text.md)
- [Machine Learning](../pipeline-patterns/machine-learning.md)
