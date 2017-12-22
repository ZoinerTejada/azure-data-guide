
# Cognitive services technology choices

[About]()  
[What are your options when choosing amongst the cognitive services?](#options)  
[How do you choose?](#howtochoose)  
[Key selection criteria](#criteria)  
[Capability matrix](#matrix)   
[Where to go from here](#wheretogo)  

Microsoft cognitive services are cloud-based APIs that you can leverage in artificial intelligence (AI) applications and data flows. In essence they provide you with pretrained models that are ready to use within your application, requiring no data and no model training on your part. The cognitive services are developed by Microsoft's AI and Research team and leverage the latest deep learning algorithms. They are consumed over HTTP REST interfaces and software development kits (SDKs) for many common application development frameworks are available.

The cognitive services include:
* Text analysis
* Computer vision
* Video analytics
* Speech recognition and generation
* Natural language understanding
* Intelligent search

Key benefits:
* Minimal development effort for state-of-the-art AI services.
* Easy integration into apps via HTTP REST interfaces.
* Built-in support for consuming cognitive services in Azure Data Lake Analytics.

Considerations:
* Only available over the web&mdash;Internet connectivity is generally required. The primary exception to this is the Custom Vision Service, whose trained model you can export for prediction on devices and at the IoT edge.
* Although considerable customization is supported, the available services may not suit all predictive analytics requirements.

## <a name="options"></a> What are your options when choosing amongst the cognitive services?
In Azure, there are dozens of Cognitive Services available. The current listing of these is available in a directory categorized by the functional area they support:
- [Vision](https://azure.microsoft.com/en-us/services/cognitive-services/directory/vision/)
- [Speech](https://azure.microsoft.com/en-us/services/cognitive-services/directory/speech/)
- [Knowledge](https://azure.microsoft.com/en-us/services/cognitive-services/directory/know/)
- [Search](https://azure.microsoft.com/en-us/services/cognitive-services/directory/search/)
- [Language](https://azure.microsoft.com/en-us/services/cognitive-services/directory/lang/)

## <a name="howtochoose"></a> How do you choose?
Each cognitive service is purpose built to meet a particular application requirement and as such brings with it a unique set of capabilities.  

## <a name="criteria"></a> Key Selection Criteria

The following tables summarize the key differences in capabilities between each of the cognitive services. <!--See note from analysis-visualizations-reporting.md-->A good way to begin finding the right service is by answering these questions:
- What type of data are you dealing with?
    - Narrow your options by choosing from the set of services based on the type of input data you are working with&mdash;text, images/video, or speech. For example, if your input is text, select from the services that have an input type of text. 
- Do you have the data to train a model?
    - If yes, consider the custom services that enable you to train their underlying models with data you provide for improved accuracy and performance. 


## <a name="matrix"></a> Capability matrix

### Uses prebuilt models
| | Input type | Key benefit |
| --- | --- | --- |
| Text Analytics API | Text | Easily evaluate sentiment and topics to understand what users want |
| Entity Linking API| Text | Power your app's data links with named entity recognition and disambiguation |
| Language Understanding Intelligent Service (LUIS)| Text |  Teach your apps to understand commands from your users |
| QnA Maker Service| Text | Distill FAQ formatted information into conversational, easy-to-navigate answers |
| Linguistic Analysis API | Text | Simplify complex language concepts and parse text |
| Knowledge Exploration Service | Text | Enable interactive search experiences over structured data via natural language inputs | 
| Web Language Model API | Text | Use the power of predictive language models trained on web-scale data | 
| Academic Knowledge API | Text | Tap into the wealth of academic content in the Microsoft Academic Graph populated by Bing |
| Bing Autosuggest API | Text | Give your app intelligent autosuggest options for searches |
| Bing Spell Check API | Text | Detect and correct spelling mistakes in your app |
| Translator Text API | Text | Easily conduct machine translation |
| Recommendations API | Text | Predict and recommend items your customers want |
| Bing Entity Search API | Text (web search query) | Enrich your experiences by identifying and augmenting entity information from the web |
| Bing Image Search API | Text (web search query) | Search for images and get comprehensive results |
| Bing News Search API | Text (web search query) | Search for news and get comprehensive results |
| Bing Video Search API | Text (web search query) | Search for videos and get comprehensive results |
| Bing Web Search API | Text (web search query) | Get enhanced search details from billions of web documents |
| Bing Speech API | Text or Speech | Convert speech to text and back again |
| Speaker Recognition API | Speech | Use speech to identify and authenticate individual speakers |
| Translator Speech API | Speech | Easily <!-- Is it really easy?-->conduct real-time speech translation |
| Computer Vision API | Images (or frames from video) | Distill actionable information from images, automatically create description of photos, derive tags, recognize celebrities, extract text, and create accurate thumbnails |
| Content Moderator | Text, Images or Video | Automated image, text, and video moderation |
| Emotion API | Images (photos with human subjects) | Identify the range emotions of human subjects |
| Face API | Images (photos with human subjects) | Detect, identify, analyze, organize, and tag faces in photos |
| Video Indexer | Video | Unlock video insights such as sentiment, transcript speech, translate speech, recognize faces and emotions, and extract keywords | 

### Trained with custom data you provide
| | Input type | Key benefit |
| --- | --- | --- |
| Custom Vision Service | Images (or frames from video) | Easily customize your own state-of-the-art computer vision models for your unique use case |
| Custom Speech Service | Speech | Overcome speech recognition barriers like speaking style, background noise, and vocabulary | 
| Custom Decision Service | Web content (for example, RSS feed) | Use machine learning to automatically select the appropriate content for your home page |
| Bing Custom Search API | Text (web search query) | An easy to use, ad free, commercial-grade search tool that lets you deliver the results you want |


## <a name="wheretogo"></a>Where to go from here
Read next: [Data Science and Machine Learning](../technology-choices/data-science-and-machine-learning.md)

See also:

Related pipeline patterns
- [Machine learning at scale](../pipeline-patterns/machine-learning-at-scale.md)
- [Processing CSV and JSON files](../pipeline-patterns/processing-csv-and-json.md)
- [Processing free-form text data](../pipeline-patterns/processing-free-form-text.md)