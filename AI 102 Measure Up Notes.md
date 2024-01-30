
### Anomaly Detection
#### Notes:
Detecting porno or offensive content is done with the Content Moderator.
Anomaly Detector finds data that is an outlier or is out of trend in time-series data. It does not analyze content supplied by users for offensive content such as adult, racy, gory images.
Personalizer determines best content to show a user.  Think shopping cart applications, NetFlix queue recommendations and stuff like that. Content Moderator is the AI service that deals with 'offensive' content.  The content is flagged for human review in the portal.
#### References
- [What is Anomaly Detector? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/anomaly-detector/overview)
- [What is Personalizer? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/personalizer/what-is-personalizer)
- [What is Azure Content Moderator? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/content-moderator/overview)
- [What is Azure AI Vision? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/computer-vision/overview)
- [What is Spatial Analysis? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/computer-vision/intro-to-spatial-analysis-public-preview)
- [What is question answering? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/language-service/question-answering/overview)



### Custom Vision
#### Notes:
Adding more images can make your model perform better. The images must be tagged before training the model. Smart Labeler will tag uploaded images automatically, reducing the manual effort needed to improve the model. The model must also be retrained in order to use the uploaded images to help improve predictions. Retraining creates a new iteration of the model. The new iteration must be published before applications will be able to use the improved model.

Smart Labeler will tag uploaded images automatically reducing the manual effort needed to improve the model.

You copy a project by exporting and importing the project. Adding and tagging new images alone is not sufficient to use the model in an application.


#### References:
- [Copy and back up Custom Vision projects - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/copy-move-projects)
- [Quickstart: Build an image classification model with the Custom Vision portal - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/getting-started-build-a-classifier)
- [Tag images faster with Smart Labeler - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/suggested-tags)
- [Use prediction endpoint to programmatically test images with classifier - Custom Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/use-prediction-api)


### Conversational Bot
#### Notes:
The higher level in the confidence score threshold would prioritize accuracy over coverage. As a result, more questions may be left unanswered if the returned answers score below the new threshold.

You can easily add chitchat to your bot using one of the predefined personalities in the custom question answering solution: Professional, Friendly, Witty, Caring, or Enthusiastic. This will add a curated list of question and answer data to the knowledge base. Chitchat content is available in several supported languages.

Alternate questions are useful when the same question can be asked in different ways. By enriching the knowledge base with alternate questions, you can improve the likelihood of a user's question being answered. However, it would not add a friendly personality to the bot's question answering functionality.
Default answer is used when custom question answering cannot find an answer. You can set it in the Settings configuration of your question answering project.


#### References
- [Confidence score - question answering - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/language-service/question-answering/concepts/confidence-score)
- [What is question answering? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/language-service/question-answering/overview)
- [Best practices - question answering - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/language-service/question-answering/concepts/best-practices)
- [Adding chitchat to a custom question answering project - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/language-service/question-answering/how-to/chit-chat)
- [Enrich your project with active learning - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/language-service/question-answering/tutorials/active-learning)
- [Get default answer - custom question answering - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/language-service/question-answering/how-to/change-default-answer)



















### Cognitive Search
#### Notes
Know about the enrichment pipeline.  Key here is the Projections when saving your enriched document.  The Knowledge store "projection" can be stored in Blob storage.  This is considered your knowledge store.  This term is used a lot in several scenarios on the test.

You can use file projections to save AI enrichment pipeline output to Blob storage. However, file projections are intended for binary objects like images extracted from documents and not for JSON content.  Look closely at what it's projecting TO: (Table, Object, File).  Look closely at the JSON examples.  I like the example of pulling it into a pandas DataFrame.

Object projections allow you to save enriched documents as JSON files to Blob storage. Saved documents retain content from the source documents as well as any enrichments and skill outputs in a JSON format.

You can use table projections to save a valid JSON output to Azure Table storage. Content for table projections is represented as rows and columns, allowing you to define a schematized shape. You do not save table projections to Blob storage, as is required in this scenario.

#### References
- [Projection concepts - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/search/knowledge-store-projection-overview)
- [Define projections - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/search/knowledge-store-projections-examples)
- [Explore data in Azure Blob storage with pandas - Azure Architecture Center | Microsoft Learn](https://learn.microsoft.com/en-us/azure/architecture/data-science-process/explore-data-blob)
- 




### Cognitive Search Indices - large application scenarios
#### Notes

In Azure AI Search, a _search index_ is your searchable content, available to the search engine for indexing, full text search, vector search, hybrid search, and filtered queries. An index is defined by a schema and saved to the search service, with data import following as a second step. This content exists within your search service, apart from your primary data stores, which is necessary for the millisecond response times expected in modern search applications. Except for indexer-driven indexing scenarios, the search service never connects to or queries your source data.

Know index types: (Filterable, Sorted, )
The filterable property specifies if the field in the index can be used as a filter and can restrict the list of documents returned by the search. The filterable property is a Boolean value defined on a field in the index.  Sortable property-By default, search results are ordered by score. The sortable property allows other fields to be used for sorting results.

*Restricting access*
You do not need to define access control lists on the source data. Test results are stored in ADLS G2. Indexes created using Azure Cognitive Search do not include security access information from Data Lake.
Each folder requires a separate data source. For example, researchers must not be allowed to search on sexual health test results. If a single data source is created for the entire container, all documents in the container will be indexed. Separate data sources can be defined for each folder using query to define virtual directories.  You can use Azure AD security groups to *filter* search results. Security filters can be used to trim the results from Azure Cognitive Search. You can define Azure AD security groups and then index the documents using the security groups. When a search is performed, Azure Cognitive Search will include or exclude documents based on the user's membership of the Azure AD security groups applied when indexing.

*Properties of knowledge store* - enhancing the data
You should define the source and tableName properties. Azure Cognitive Search can use the built-in Azure AI Language skills from Cognitive Services. One such skill is key phrase extraction. The key phrases extracted should be stored in Azure Table Storage, TAB3. When saving enrichments as a table projection to a knowledge store, you need to specify the source and tableName.
Source is the path of the projection. In this secnario, source will be /document/tableprojection/key Phrases/*.
Tablename is the name of the table to create in Azure Table storage.
You should not specify storageContainer. storageContainer is used for storing enrichments in Azure Blob storage as object projections.
You should not specify encryptionKey. encryptionKey is optional and used to reference an Azure Key Vault for the skillset, not for the knowledge store.
You should not specify referenceKeyName. referenceKeyName is used to relate data across projections.
If referenceKeyName is not specified, then the system will use generatedKeyName.

QQ:  You need to include the enhanced data created from SomeSkillSetFoo in the index. You need to set properties during index specification:

You should specify outputFieldMappings to add key phrases to the index. Projections are enriched documents from Cognitive Services that are stored in a knowledge store. Projections enhance and shape the data. The key phrase enrichment is projected as tabular data and stored in the Azure Table storage account, TAB3. Table projections require the data generated by the skillset be mapped to the knowledge store using outputFieldMappings with a sourceFieldName and targetFieldName. The key phrases extracted need to be added to the index. The indexer adds the output from the skillset to the index. The outputFieldMappings should be defined as follows:
```
"outputFieldMappings": [
{
"sourceFieldName": "/document/metadata_storage_content_type/keyphrases", "targetFieldName": "keyphrases"
}
```
You also need to specify the skillsetName, skillsetl, on the indexer. An indexer can be associated with a single skillset to enrich the data. To enrich the data, a skillset must be defined and specified on the indexer.
You should not specify fieldMappings. The fieldMappings property is used to map key fields. fieldMappings are optional. By default, the metadata_storage_path property is used.
You should not specify the storageConnectionString. The storageConnectionString is required when storing the skillset's output data into a knowledge store, but it is not required for the indexer. The indexer requires the skillsetName.
You should not specify the cognitiveServices. This property defines the Cognitive Services resource to use to enrich the data. This is required when defining the skillset, but it is not required for the indexer.

QQ: What REST API operation uses this
The Run Indexer REST API operation is an indexer that can be invoked on demand using the Run Indexer operation. For test results to be included in searches after they have been uploaded, the new documents must be indexed. Test results must therefore be indexed immediately after being uploaded. This operation will include new and updated documents in the index immediately and not wait for the next scheduled run.  Know the processing order. 

Reset Indexer operation will cause a full re-indexing of all source data on the next run of the indexer but does not execute the indexer itself.

The Update Indexer operation updates the definition of the indexer but does not execute the indexer.

The Update Index operation makes changes to the index such as hiding fields or setting Cross-Origin Resource Sharing (CORS) properties. Updating an index does not execute the indexer.

#### References
- Indices
	- [Index overview - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/azure/search/search-what-is-an-index)
	- [Create Index - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/searchservice/create-index)
	- [Security filters for trimming results - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/azure/search/search-security-trimming-for-azure-search)
	- [Security filters to trim results using MIcrosoft Entra ID - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/azure/search/search-security-trimming-for-azure-search-with-aad)
- Access Control / RBAC
	- [Access control lists in Azure Data Lake Storage Gen2 - Azure Storage | Microsoft Learn](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-access-control)
	- [Azure Data Lake Storage Gen2 indexer - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/azure/search/search-howto-index-azure-data-lake-storage)
- Skillsets
	- (important) [Create a skillset - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/azure/search/cognitive-search-defining-skillset)
	- [Create Skillset - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/searchservice/create-skillset) (REST API)
	- [Define projections - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/azure/search/knowledge-store-projections-examples)
- API calls / Endpoints
	- Know the generalities of these calls.  I recall the test scenario making you multi-pick several statements to correct the endpoints so you need to somewhat recall them or recognize them in snippets of JSON.
	- [Update Index - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/searchservice/update-index)
	- [Update Indexer - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/searchservice/update-indexer)
	- [Reset Indexe - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/searchservice/reset-indexer)
	- [Run Indexer - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/searchservice/run-indexer)
	- [Create Data Source - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/searchservice/create-data-source)


### Cognitive Services - Resource Creation
#### Notes
Azure Resource Manager (ARM) templates are in JavaScript Object Notation (JSON) data format. Define the infrastructure and configuration for your Azure AI Services resources in JSON format within your ARM template. Declarative syntax allows you to specify the type of Azure AI Services, their location, pricing tier and other required deployment parameters without writing any programming codes. You can then deploy your template using any of the supported deployment options such as Azure Portal, Azure Command-Line Interface (CLI), PowerShell, REST APIs or Azure Cloud Shell.
You should not use AVRO, HTML or XML formats. AVRO format was developed by the Apache Hadoop team to support data serialization and exchange. XML tags allow you to define the structure and meaning of your data. HTML is a markup language that is used to define the structure of a Web page and its content. ARM templates should always be defined in JSON format.

#### References
- [Create an Azure AI services resource using ARM templates - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/create-account-resource-manager-template?tabs=portal)
- [Microsoft.CognitiveServices/accounts - Bicep, ARM template & Terraform AzAPI reference | Microsoft Learn](https://learn.microsoft.com/en-us/azure/templates/microsoft.cognitiveservices/accounts?tabs=json&pivots=deployment-language-bicep)
- [Avro format - Azure Data Factory & Azure Synapse | Microsoft Learn](https://learn.microsoft.com/en-us/azure/data-factory/format-avro)
- [XML for the uninitiated - Microsoft Support](https://support.microsoft.com/en-us/office/xml-for-the-uninitiated-a87d234d-4c2e-4409-9cbc-45e4eb857d44)
- [HTML Basics | Microsoft Learn](https://learn.microsoft.com/en-us/cpp/mfc/html-basics?view=msvc-160)


### Cognitive Services - Document Intelligence deployment
#### Notes
This is absolutely on the test so know how to form the request.  If you've deployed this before it just seems natural and it's one of those ones you can noodle out.

The complete fully qualified container image name should look like this: mcr.microsoft.com/azure-ccognitive-services/custom-form/labeltool.
mcr.microsoft.com serves container images for Azure AI Services and other solutions from the Microsoft Container Registry (MCR). MCR’s syndicate container catalog is accessible at mcr.microsoft.com.
You should also use custom-form. Sample Labeling tool’s container image is stored in the azure-cognitive- services/custom-form repository.
You should also use /labeltool. labeltool is the name of the Sample Labeling tool’s container image.

Other MCR services:
admin.microsoft.com. This is a Microsoft 365 admin center address. You can use Microsoft 365 admin center to perform administrative tasks such as the management of your Microsoft 365 services, assignment of roles and licenses, and other similar tasks.
You should not use portal.azure.com. This is an Azure portal address. You can use Azure Portal to view and manage Microsoft Entra ID and all your other Azure resources.
The azure-cognitive-services/language repository is a common storage location for the Azure AI Services container images in the Language domain.
The azure-cognitive-services/vision repository is a common storage location for other Computer Vision container images such as Optical Character Recognition (OCR).
/keyphrase. keyphrase is the name of the Key Phrase Extraction service’s container image.
/sentiment, sentiment is the name of the Sentiment Analysis service’s container image.


#### References
- [Microsoft syndicates container catalog (mcr.microsoft.com) | Microsoft Azure Blog](https://azure.microsoft.com/en-us/blog/microsoft-syndicates-container-catalog/)
- [Use Azure AI containers on-premises - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/cognitive-services-container-support)
- [Microsoft security portals and admin centers | Microsoft Learn](https://learn.microsoft.com/en-us/microsoft-365/security/defender/portals?view=o365-worldwide)


### Cognitive Services - Sentiment Analysis app
#### Notes
; Planning / design an AI LLM container locally to avoid transferring senstitive info to the cloud. You downloaded the AI LLM container to a local host. You retrieve the API key and the endpoint URL http://mysentiment.cognativeservices.azure.com
Work out the docker command to bind to you local 8080 port of the local docker machine
KEY: required params Eula, Billing, and ApiKey.  This similar Docker scenario was seen several times on my exam.

You should run the container with the docker run --rm -it -p 8080:5000 --memory 2g --cpus 1 mcr.microsoft.com/azure-cognitive-services/textanalytics/sentiment Eula=accept
Billing=https://sentiment1.cognitiveservices.azure.com ApiKey= xxxyyyzzzl23 command. This correctly maps the Azure AI Language container’s port 5000 to your local host machine’s port 8080. This command also provides the correct values for the required three primary parameters. The Eula parameter for the end-user license agreement (EULA) has a value of accept. The Billing parameter has a value of the corresponding Azure AI Language resource’s endpoint URL. The APIKey is set to the API key value that you retrieved from Azure. Based on the configuration, your host machine allocates 1 core CPU and 2 GB of memory to the Azure AI Language container.

You should not run the container with the docker run --rm -it -p 8080:5000 --memory 2g --cpus 1 mcr.microsoft.com/azure-cognitive-services/textanalytics/sentiment
Billing=https://sentiment1.cognitiveservices.azure.com ApiKey= xxxyyyzzzl23 command. This correctly maps the container and host machine ports. However, the required Eula parameter is missing, so your container would not start.

You should not run the container with the docker run --rm -it -p 5000:8080 --memory 2g --cpus 1 mcr.microsoft.com/azure-cognitive-services/textanalytics/sentiment Eula=accept Billing=https://sentiment1.cognitiveservices.azure.com ApiKey= xxxyyyzzzl23 command. This incorrectly maps the container’s port 8080 to the host machine’s port 5000. To make your container run as expected, you should change the -p parameter’s value to 8080:5000.

You should not run the container with the docker run --rm -it -p 5000:8080 --memory 2g --cpus 1 mcr.microsoft.com/azure-cognitive-services/textanalytics/sentiment command. This incorrectly maps the container’s port 8080 to the host machine’s port 5000. It also does not assign values to the required Eula, Billing, and ApiKey parameters.

#### References 
- [Install and run Docker containers for Sentiment Analysis - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/language-service/sentiment-opinion-mining/how-to/use-containers)



### Cognitive Search - Deployment
#### Notes
; Cog Search 'Search1' deployed to RG1
; Allow an app ClientApp1 to query the index
; Create an API key do the query
; Understand the process around rotating keys (2nd key first then primary)

General format:
POST https://  ***management.azure.com***  /subscriptions/6088ECEl-5EB9-4260-3AA5-590F36359AE0/resourceGroups/RG 1/providers/
***"MicrosoftSearch"***
/searchServices/Search1/
**"createQueryLey"**
/ClientAppl?api-version=2020-08-01

management.azure.com is the endpoint for the management of Azure services, including the Search service, and it enables the management and creation of keys for the Search service.
You use the management.azure.com endpoint to create the key for ClientAppl.
You should not use Search1.search.windows.net. This is the endpoint for the Search service. The client application will use this to query the indexes, but you cannot use it to create a key for ClientAppl.

You should not use api.cognitive.microsoft.com. This endpoint is used by the Bing Search services.

You should use Microsoft.Search. This is the provider for the Search service. Using this provider, 
you can regenerate the admin keys or create query keys for the Search service. You require a query key to allow ClientAppl to perform queries on the indexes.

You should not use Microsoft.CognitiveServices. This is the provider for generic Cognitive Services. It can regenerate the primary and secondary keys for the service, but it cannot generate query keys for the Search service.

You should not use Microsoft.Authorization. This is the provider for managing resources in Azure and can be used to define Azure policies and apply locks to resources.

You should use createQueryKey. A query key only allows the client application to search and access indexes and documents. It does not allow the application to manage the service.
You should not use regenerateAdminKey/primary or regenerateAdminKey/secondary. These key kinds are used to regenerate the primary and secondary administration keys. With an administration key, an application can manage the entire service and create and delete indexes.

#### References
- [Admin Keys - Regenerate - REST API (Azure Search Management) | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/searchmanagement/admin-keys/regenerate?view=rest-searchmanagement-2023-11-01&tabs=HTTP)
- [Connect using API keys - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/azure/search/search-security-api-keys?tabs=portal-use%2Cportal-find%2Cportal-query)
- [Management REST APIs - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/searchmanagement/)
- [Accounts - Regenerate Key - REST API (Azure Cognitive Services) | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/cognitiveservices/accountmanagement/accounts/regenerate-key?view=rest-cognitiveservices-accountmanagement-2023-05-01&tabs=HTTP)
- [Create Index - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/searchservice/create-index)
- (KEY) [Bing Custom Search API v7 Reference | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/cognitiveservices-bingsearch/bing-custom-search-api-v7-reference)
- [Policy Set Definitions - Create Or Update - REST API (Azure Policy) | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/policy/policy-set-definitions/create-or-update?view=rest-policy-2023-04-01&tabs=HTTP)
- 


### Cognitive Serves - Local processing
#### Notes
; Fast food org deploying edge type devices in drive through.  Speech data should process localy, AI SpeechServices deployed in EastUS2.  App translates speech2Text.  Show the docker pull command.  It's gonna look something LIKE this in the end:
```bash
docker pull mcr.microsoft.com  /azure-cognitive-services/
speechservices    /    speach-to-text
```

Azure AI Services can be deployed to local devices as docker containers. You can obtain the prebuilt speech services container using the following command:

```
docker pull mcr.microsoft.com/azure-cognitive-services/speechservices/speech-to-text
```

You should use mcr.microsoft.com for the endpoint. The prebuilt docker container images for Azure AI Services are stored in the Microsoft Container Registry (MCR).
You should not use hub.docker.com. Docker Hub is a hosted repository service provided by Docker for finding and sharing container images. The Azure AI Services container images are not available on Docker Hub.
You should not use westus.api.cognitive.microsoft.com. This is the endpoint used for some of the regional Azure AI Services. Container images are not available from such endpoints.
You should use the speechservices service and the speech-to-text image to convert speech into text.
You should not use the textanalytics service. Text Analytics is part of the Azure AI Language service and it does not perform speech-to-text conversion.
You should not use sentiment. Sentiment is part of the Azure AI Language service and determines if the text has a positive or negative emotion.

#### References
- [Install and run Speech containers with Docker - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/speech-container-howto)
- [Publishing regions & endpoints - LUIS - Azure | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/luis/luis-reference-regions)
- [Speech to text overview - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/speech-to-text)
- [What are Azure AI services? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/what-are-ai-services)


### Responsible AI
; Know these three things: Fairness, Privacy and Security and Transparency
; It's common sense

#### Reference
[Responsible AI - Cloud Adoption Framework | Microsoft Learn](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/strategy/responsible-ai)



### Cognitive Services - Custom Speech Performance
; transcribe cx calls for analysis and insights
; CI/CD pipeline updates the speech recognition model.  Improving performance.

#### Notes
You can use Azure DevOps to run automated Cl workflows when updates to testing and training data are pushed to the main branch. You can use various Git services like GitHub or Azure DevOps to automate workflows execution in your Cl/CD pipeline. Depending on the tooling availability in a specific Git service, workflow configuration can be set up using a graphical user interface (GUI) option or a command line interface (CLI) command.

You **should not** test the newly trained model with the updated test data to calculate the revised benchmark Word Error Rate (WER). Instead, the revised benchmark WER should be calculated by retesting the current benchmark model with the updated test data. You can compare then WERs of both the new and benchmark models to verify potential WER improvement.

If the WER of the newly trained model improves compared to the benchmark model, the CD workflow should be executed to update your solution's endpoint. Triggering the CD workflow for the new model with a better WER ensures your solution’s endpoint serves the best performing Custom Speech model.

#### References
- [CI/CD for custom speech - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/how-to-custom-speech-continuous-integration-continuous-deployment)
- [Create a CI/CD pipeline with Azure Pipelines - Azure Architecture Center | Microsoft Learn](https://learn.microsoft.com/en-us/azure/architecture/data-science-process/ci-cd-flask)


### Cognitive Services - Key Rotation process
; Lost/stolen key scenario
#### Notes
- Update app to use Key2
- Reset Key1
- Update app to use Key2

#### Resources
- [Connect using API keys - Azure AI Search | Microsoft Learn](https://learn.microsoft.com/en-us/azure/search/search-security-api-keys?tabs=portal-use%2Cportal-find%2Cportal-query)
- [Create a multi-service resource for Azure AI services - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/multi-service-resource?tabs=windows&pivots=azportal)


### Cognitive Services - Deploying Translator service
Measure Up Question
![[Pasted image 20240129160907.png]]

#### Notes
A subscription key from the Azure AI Services resource can be used to authenticate requests for the Translator service API. Multi-service subscription keys are not tied to a specific Azure AI service. That is why you can use a single subscription key from the multi-service Azure AI Services resource to authenticate requests for the Azure AI services in the Vision, Speech, Language, and Decision domains.
Ocp-Apim-Subscription-Key is a mandatory header for a multi-service subscription key authentication against the Translator service API. You use the Ocp-Apim-Subscription-Key authentication header to provide your multi-service subscription key. You can also use the Ocp-Apim-Subscription-Key header to authenticate with the Translator resource’s single-service subscription key.
Ocp-Apim-Subscription-Region is not an optional header for a multi-service subscription key authentication against the Translator service API. The Ocp-Apim-Subscription-Region authentication header is required when you authenticate with a multi-service subscription key from your Azure AI Services resource. This header is optional when you use the Translator resource’s single-service subscription key.

#### References
- [Quickstart: Azure AI Translator REST APIs - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/Translator/quickstart-text-rest-api?tabs=csharp)
- [Authentication in Azure AI services - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/authentication?tabs=powershell)
- [Create a multi-service resource for Azure AI services - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/multi-service-resource?tabs=windows&pivots=programming-language-python)


AI Services - VNet Firewall deployment
![[Pasted image 20240129161436.png]]

#### Notes
You should set the Allow access from field to Disabled under Firewalls and virtual network. When you set this configuration option to Disabled, all public requests to consume Azure AI service resources are denied. Private Endpoint connections will be the exclusive way to access your Azure AI service.
You should also create a Private Endpoint under Private endpoint connections. When a Private Endpoint is enabled, traffic between the Azure AI service and the target VNet is routed through the Microsoft backbone network using private IP addresses only. The Azure AI service will be assigned with a private IP address from your VNet.
You should not set the Allow access from field to All networks under Firewalls and virtual network. All networks is a default value that allows access to your Azure AI service’s endpoint from clients on any networks, including the internet.
You should not add 10.1.1.0/24 under Firewall > Address Range. Firewall IP rules accept public IP addresses only. That is why you will get a warning that the private IP addresses are not supported for the use in IP rules. The firewall option is available only when you set the Allow access from field to Selected Networks and Private Endpoints.
You should not click Add new VNet, and create a service endpoint for an Azure AI service. Adding a new VNet will create a new Azure VNet with defined IP ranges. In this scenario, we already have an existing VNet where you deployed your new app’s components. The Add new VNet option is available only when you set the Allow access from field to Selected Networks and Private Endpoints.

#### References
- [Quickstart: Create a private endpoint - Azure portal - Azure Private Link | Microsoft Learn](https://learn.microsoft.com/en-us/azure/private-link/create-private-endpoint-portal?tabs=dynamic-ip)
- [What is a private endpoint? - Azure Private Link | Microsoft Learn](https://learn.microsoft.com/en-us/azure/private-link/private-endpoint-overview)
- [What is a private endpoint? - Azure Private Link | Microsoft Learn](https://learn.microsoft.com/en-us/azure/private-link/private-endpoint-overview)


#### AI Services - Diagnostic Logging
### Measure Up
![[Pasted image 20240129171848.png]]

#### Notes
You should use a Log Analytics workspace to send logs to a repository where they can be enriched with other monitoring logs collected by Azure Monitor to build powerful log queries. Log Analytics is a flexible tool for log data search and analysis. In a Log Analytics workspace you can combine your Azure AI Services logs with other logs and metrics data collected by Azure Monitor, use Kusto query language to analyze your log data and also leverage other Azure Monitor capabilities such as alerts and visualizations.
You should use Event Hub to stream data to external log analytics solutions. Event Hub can receive, transform and transfer millions of events per second. With Event Hub, you can stream real-time logs and metrics from your Azure AI Services to external systems such as Security Information and Event Management (SIEM) systems or third-party analytics solutions.
You should use Azure Blob storage to archive logs for audit, static analysis or backup purposes, keeping them in JSON format files. Blob storage is optimized for storing big volumes of unstructured data. With Blob storage you can keep your logs in a very granular format by the hour or even minutes, to assist with a potential investigation of specific incidents reported for your Azure AI Services.
#### References
- [Enable diagnostic logging - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/diagnostic-logging)
- [Azure AI Search monitoring data reference | Microsoft Learn](https://learn.microsoft.com/en-us/azure/search/monitor-azure-cognitive-search-data-reference)

AI Solutions - Endpoints
;OpenAI endpoint accessing Keyvault.  Cx accidentally exposes repo to git and key is compromised.
#### Measure Up
![[Pasted image 20240129173017.png]]

#### Notes
The complete Azure CLI command should be as follows:
az keyvault key rotate --name key-aoai-123 --vault-name keyvault-123
You should use the keyvault base command. The az keyvault command allows you to manage Azure Key Vault’s keys, secrets, and certificates.
You should use the rotate operation to rotate the relevant keys in Azure Key Vault. This operation will generate a new version of the key and return its URI. You would then need to update your Azure OpenAI resource to use URI of the new key version.
You should use key-aoai-123 as a value for the -name parameter and keyvault-123 as a value for the --vault- name parameter. The --name parameter expects the key name as its value, while the --vault-name parameter is used to specify the Azure Key Vault’s name.
You should not use the cognitiveservices or ml base commands. These are used to manage Azure Cognitive Services accounts and Azure Machine Learning resources respectively. In this scenario, you are asked to create a new version of the compromised key, and that is why you should perform a key rotate operation in Azure Key Vault.
You should not use the random or recover operations to rotate keys in Azure Key Vault. The random operation can be used to get random bytes from hardware security module (HSM). Number of bytes is specified by the value of the --count parameter. The recover operation can be used to recover deleted keys if Azure Key Vault or HSM have the soft-delete option enabled.
You also should not use aoai-123. The az keyvault key rotate CLI command requires the names of Azure Key Vault and the relevant key, not the name of the Azure OpenAI resource.

#### References
- [Azure OpenAI Service encryption of data at rest - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/openai/encrypt-data-at-rest)
- [az keyvault key | Microsoft Learn](https://learn.microsoft.com/en-us/cli/azure/keyvault/key?view=azure-cli-latest)
- [az cognitiveservices | Microsoft Learn](https://learn.microsoft.com/en-us/cli/azure/cognitiveservices?view=azure-cli-latest)
- [az ml | Microsoft Learn](https://learn.microsoft.com/en-us/cli/azure/ml?view=azure-cli-latest)


### AI - Anomaly Detector
#### Notes
Know the differences between univariate and multivariate anomaly detection.  Read the references.  Notice how it can be used without the need for machine learning knowledge or labeled data.  This was on the test but the question isn't even close to measure up so understand the use case.
#### Measure Up
![[Pasted image 20240129173833.png]]
You should use Streaming Detection to monitor credit card transactions in real-time for fraud detection. In this scenario, the data is streaming in real-time and you need to detect anomalies as they occur. Therefore, Streaming Detection allows real-time anomaly detection.
You should use Batch Detection to analyze historical sales data for periods of unusually high or low sales. Batch Detection allows the analysis of an entire dataset with historical time series data to detect potential abnormalities.
You should use Change Point Detection to identify significant changes in network traffic patterns, indicating potential cyberattacks. The Change Point Detection feature helps to identify points where the data trends change significantly. Therefore, it is the most appropriate feature of the Univariate Anomaly Detector to detect signs of potential cyberattacks in historical network traffic data records.

#### References
- [Best practices when using the Anomaly Detector univariate API - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/anomaly-detector/concepts/anomaly-detection-best-practices)
- [What is Anomaly Detector? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/anomaly-detector/overview)


### AI Anomaly Detection-Accuracy reduce false positives

#### Notes
You should use both isAnomaly and severity fields in the response to sift out anomalies that are not severe. While the isAnomaly field in the response from Azure AI Anomaly Detector API indicates if a point is considered an anomaly, it can lead to false positives if used alone. To reduce false positives, it is recommended to also consider the severity field in the response to sift out anomalies that are not severe.

You should not consider a data point as an anomaly only if the severity field value is equal to zero. The severity field value indicates the severity of an anomaly, with higher values highlighting more severe anomalies. Therefore this option would not be effective, as your solution would miss all actual anomalies.

You should not decrease the value of the slidingWindow training API parameter to use the lowest possible value. The slidingWindow training API parameter determines the segment of data points for anomaly detection. Setting this to the lowest possible value could make it harder to detect anomalies, as the model would become more sensitive to minor data fluctuations.

You should not move CSV data files into /year month day / sub-folders of a zip file to define date hierarchy. The data files inside sub-folders of a zip file are ignored during training and inference processes. Therefore, this option may compromise model accuracy.
#### References
- [Best practices for using the Multivariate Anomaly Detector API - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/anomaly-detector/concepts/best-practices-multivariate)
- [Streaming inference with trained model - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/anomaly-detector/how-to/streaming-inference)
- [What is Anomaly Detector? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/anomaly-detector/overview)


### AI Metrics Advisor

#### Notes
Company using AI Metrics Advisor and anomaly detection for time series data. You created an RG then:

You should perform the following steps in order:
1.	Onboard your data.
2.	Fine-tune anomaly detection configuration.
3.	Subscribe anomalies for notification.
4.	View diagnostic insights.
You should first onboard your data. As a part of this step, you will add relevant data feeds by configuring connection strings, loading data and configuring relevant schemas. Metrics Advisor can automatically perform aggregation and build data hierarchies that you can use in root case analysis.

Next, you should fine-tune anomaly detection configuration. In this step you will select the data feed added in the previous step and apply detection configuration. You can use one of the supported anomaly patterns such as spike, dip, increase, decrease, and steady. Additionally, you can tune detection configuration by applying a series of value preferences.

Then, you should subscribe anomalies for notification. When Metrics Advisor detects anomalies, it can trigger alert notification using a hook. In this step you can configure alert settings and choose one of the supported hooks such as email, Teams, webhook, and Azure DevOps.
Finally, you should view diagnostic insights. When Metrics Advisor detects anomalies that share the same root cause, it can automatically group them into a single incident. Metrics Advisor will also perform root cause analysis and provide you with viewable diagnostic insights.

You should not create an Anomaly Detector resource in the Azure portal or get the Endpoint URL and keys of the Anomaly Detector resource. These steps are part of the Anomaly Detector creation and connection process. Azure AI Anomaly Detector can be used to detect anomalies in your time-series data. However, in this scenario, you are expected to set up a new monitor in a different solution, Azure AI Metrics Advisor, and use its web portal.

#### Reference
- [What is the Azure AI Metrics Advisor service? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/metrics-advisor/overview)
- [Quickstart: Metrics Advisor web portal - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/metrics-advisor/quickstarts/web-portal)
- [Create an Anomaly Detector resource - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/anomaly-detector/how-to/create-resource)



### AI Content Saftey Studio

#### Notes
; Social media scenario, solution needs to improve user-generated content management.  Identify which features currently available in AI Content Safety Studio.  You have to read on the references here.
- Moderating text content
- Moderating image content

Moderating image content and text content is currently available in Azure AI Content Safety Studio.
Azure AI Content Safety Studio allows you to configure content filters and experiment with different sensitivity levels to ensure that the image moderation meets your company’s requirements. Once you have defined the optimal configuration, you can export the code for implementation in your solution.

Azure AI Content Safety Studio also provides you with a web portal interface to configure content filters and blocklist management. The fine-tuned configuration can be exported as code for direct implementation in your solution.

You should not identify creating trails and highlighting reels. Content creation is a feature of Azure AI Video Indexer, which allows you to create trailers, highlight reels, generate news clips, and social media content based on the insights extracted from your main content.

You should not identify hunting for security threats with search-and-query tools. Access to search-and- query tools to hunt for security threats can be enabled through Azure Sentinel. Azure Sentinel is a Security Information and Event Management (SIEM) and Security Orchestration, Automation, and Response (SOAR) solution that enables security analytics and threat intelligence at the company-wide level.

You should not identify moderating video content. Currently, Azure AI Content Safety does not allow you to moderate video content. Video moderation functionality is available in the Azure AI Content Moderator solution, where you can scan videos for explicit content and get its time markers.

#### References
- [What is Azure AI Content Safety? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/overview)
- [What is Azure AI Video Indexer? | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-video-indexer/video-indexer-overview)
- [Hunting capabilities in Microsoft Sentinel | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/sentinel/hunting)
- [What is Azure Content Moderator? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/content-moderator/overview)


#### AI Content Saftey-Image Moderation

#### Notes
I hope I don't see this one again because its so vague.  Exhibit shows a failed result score and you determine WHY it failed.

You did not test image moderation with a large dataset. Instead, image moderation was tested as a simple test against a single image. When you run a more comprehensive test against a larger set of data, its results will show severity details for each image entry.
Your image content was not rejected because of the severity threshold for the Hate category. It was rejected because of the severity threshold for the Self-harm category. Rejection or acceptance reasons will be summarized in Azure AI Content Safety Studio’s test results and visually highlighted for Violence, Hate, Sexual and Self-harm categories.
You can export your filter configuration as sample code in Python, Java, and Ctt programming languages. Code export functionality is supported for both text and image content moderation. The exported sample code will include filter configuration for supported severity categories, blocklist management, and moderation functions for Python, Java and Ctt programming languages.

#### References
- [What is Azure AI Content Safety? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/overview)
- [Quickstart: Content Safety Studio - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/content-safety/studio-quickstart)


### AI Content Personalization

#### Measure Up
You are an AI developer at a retail company. Your company wants to enable content personalization on its e-commerce website, so that customers receive tailored product suggestions. You plan to use Azure AI Personalizer to develop the required content personalization.
You need to determine what machine learning (ML) approach is used in Personalizer resource.
Which of the following options correctly describes how your solution would enable content personalization?

#### Notes

KEY: A reinforcement learning approach, with a reward function that provides feedback to the model based on the success of the product suggestions

Your solution would enable content personalization using a reinforcement learning approach, with a reward function that provides feedback to the model based on the success of the product suggestions. Azure AI Personalizer uses reinforcement learning, where the model learns from the feedback (rewards) it receives to select the best action for a given context. This allows Personalizer to improve its decision-making process over time.

Your solution would not use a semi-supervised learning approach, which combines both labelled data (customer feedback's sentiment) and unlabelled data (customer browsing history) for training. The semi- supervised learning approach is more appropriate for scenarios where you have a large amount of unlabelled data and a smaller amount of labelled data; for example internet content classification. Personalizer uses reinforcement learning, which learns from feedback after making decisions.

Your solution would not use a supervised learning approach, where the model is trained on historical data to classify customer’s product feedback as positive, neutral, or negative. This is an example of sentiment analysis, where the model is trained on historical data to predict or classify the sentiment of given product feedback. This approach is not suitable for dynamic personalization activities like content personalization in e-commerce where new categories of products may be introduced that the model was not aware of during its training process.

Your solution would not use an unsupervised learning approach, where the model identifies patterns in customer purchase data without any prior training. Unsupervised learning identifies patterns in data without any prior training, so it may identify common purchase patterns among customers from historical purchase data. It is different from reinforcement learning used by Azure AI Personalizer, where the model makes decisions and learns from their results based on the feedback of the reward function.

#### Resources
- [How to select a machine learning algorithm - Azure Machine Learning | Microsoft Learn](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-select-algorithms?view=azureml-api-1)
- [How Personalizer Works - Personalizer - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/personalizer/how-personalizer-works)
- [What is Personalizer? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/personalizer/what-is-personalizer)



### Scenario - Computer Vision

#### Measure Up
You build a computer vision app for a travel agency. The business team wants your app to generate a brief *description* of given images. They also want your app to detect famous *landmarks*.
You plan to use the Azure AI Vision API in Azure to enable the required functionality. You deploy an Azure AI Vision resource named cv1 in the *Azure West US* region. You retrieve its primary API key: abcdefgl2345hijklmnop67890.  You need to test cv1 functionality from the command-line interface (CLI). How should you construct your CLI request? 

#### Notes
You should complete the CLI request as follows;
```bash
curl https://westus.api.cognitive.microsoft.com/vision/v2.0/analyze? visualFeatures=Description&details=Landmarks -H "Ocp-Apim-Subscription-Key: abcdefgl2345hijklmnop67890" -H "Content-Type: application/json" -d "{'url' :
'https ://images.com/travel_picture.jpeg'}".
```
You should use westus. Your endpoint’s domain name should start with the Azure region where the Azure AI Vision API resource was provisioned.
You should also use Description. The visualFeatures parameter indicates what visual features to return. It should be set to Description to describe the image content with a complete sentence in supported languages. By default, descriptions are provided in English.
You should also use Landmarks. The details parameter indicates which domain-specific details to return. It currently supports two values: Landmarks - to identify famous landmarks if detected in the image, and Celebrities - to identify celebrities if detected in the image.
You should not use cv1. The API endpoint of the Azure AI Vision API does not require the name of your resource. Instead, it requires the resource’s region and API key.
You should not use westus2. Since you provisioned the Azure AI Vision resource in the West US region in California, you have to use the westus region name. westus2 is the name of the West US 2 region located in another state, Washington.
You should not use ImageType. ImageType is a feature type that can be assigned to the visualFeatures parameter. With ImageType, you can check whether an image is a clipart or a line drawing.

#### References
- [Image descriptions - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/concept-describing-images)
- (API Def, swagger) [Cognitive Services APIs Reference (microsoft.com)](https://westcentralus.dev.cognitive.microsoft.com/docs/services/computer-vision-v3-2/operations/56f91f2e778daf14a499f21b)


### Computer Vision API

#### Measure Up
You plan to use the Azure Computer Vision API to generate thumbnails for your images.
You deploy an Azure AI Vision cognitive service named cv01 in the Azure UK South region. You retrieve the API key and endpoint of your cognitive service from Azure.
Which two Azure AI Vision API endpoints should you use to generate image thumbnails? Each correct answer presents a complete solution.

#### Notes
Notice this is a little trick question to throw you off.  Don't ever use something with a auzre-api.net.  We DO NOT use hyphens here unless you have setup a custom DNS name with APIM.  Its not mentioned in the solution set so...
(USE) You should use https://cv01.cognitiveservices.azure.eom/vision/v3.1/generateThumbnail 
or https://uksouth.api.cognitive.microsoft.eom/vision/v3.1/generateThumbnail. Both of these endpoints can be used to access the Azure AI Vision API and generate the required image thumbnails. When using the cognitiveservices.azure.com domain, you should specify the name of your Azure AI Vision cognitive service.

(NOT) You should not use https://uksouth.azurewebsites.net/vision/v3.1/generateThumbnail. The azurewebsites.net subdomain is reserved for the use of Azure web apps. This subdomain is assigned to your custom web apps that you deploy in Azure.

(NOT) You should not use https://cvOl.azure-api.net/vision/v3.1/generateThumbnail. The azure-api.net subdomain is reserved for use by Azure API Management instances. API Management can potentially hide Azure AI Vision endpoints to act as a frontend interface. However, in this case you need to identify Azure AI Vision API endpoints.

#### References
- [Smart-cropped thumbnails - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/concept-generating-thumbnails)
- [Generate Thumbnail - REST API (Azure Cognitive Services - Computer Vision) | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/computervision/generate-thumbnail?view=rest-computervision-v3.1)
- (swagger) [Cognitive Services APIs Reference (microsoft.com)](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa)
- [Map existing custom DNS name - Azure App Service | Microsoft Learn](https://learn.microsoft.com/en-US/azure/app-service/app-service-web-tutorial-custom-domain?tabs=root%2Cazurecli)
- [Configure custom domain name for Azure API Management instance - Azure API Management | Microsoft Learn](https://learn.microsoft.com/en-us/azure/api-management/configure-custom-domain?tabs=custom)


### Computer Vision
#### Measure Up
You build a new computer vision app. Your app integrates with the Azure AI Vision API to enable cognitive image processing.  You need to complete the code for a method that returns a taxonomy-based classification of your image’s content. How should you complete the code? 

![[Pasted image 20240129191032.png]]
#### Notes
You should use *ComputerVisionClient*. ComputerVisionClient is a class in the Image Analysis .NET SDK that you should instantiate and use for image analysis operations.
You should also use *Categories.* The Categories visual feature type helps you to extract taxonomy-based categories detected in an image, for example animaLdog or outdoor_house.

(Not) You should not use ComputerVisionClientExtensions. ComputerVisionClientExtensions is a class in the Image Analysis .NET SDK that contains additional methods for the ComputerVisionClient class such as ListModelsAsync, ReadAsync, TaglmageAsync and others. For your image analysis, you require an instance of a ComputerVisionClient class only.

(Not) You should not use VisualFeatureTypes. The VisualFeatureTypes enum is used to specify visual features that you want to extract in your image analysis. VisualFeatureTypes is defined later in the method’s code to list selected image analysis types.
You should not use Description. With the Description visual feature, the Azure AI Vision API analyzes your image and generates a human-readable sentence describing the content of your image. It does not provide a taxonomy-based classification of your image.

(Not) You should not use Tags. Similar to Categories, Tags are used to provide details about the content found in your images. However, tags are not organized as a taxonomy.

#### References
- [Quickstart: Image Analysis - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/quickstarts-sdk/image-analysis-client-library?tabs=windows%2Ccli&pivots=programming-language-csharp)
- [Image categorization - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/concept-categorizing-images)
- [Image descriptions - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/concept-describing-images)
- [Content tags - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/concept-tagging-images)


### Computer Vision
#### Measure Up
![[Pasted image 20240129191449.png]]

#### Notes
Do not memorize the answer.  Look closely at the script.  The portions will likely be different from what I recall on the exam.  Screenshot will do you no good.

You should use *GetReadResultAsync. GetReadResultAsync* is a method of the
ComputerVisionClientExtensions class that returns optical character recognition (OCR) results of the read operation after processing the visible text in the image.
You should also use NotStarted. While the loop in your code already has a check for the Running status, for the read operations to remain active, another check should be included for the *NotStarted* status. This ensures that the loop is not aborted when you initiate the class and still waits for the OCR read operation to proceed.

(Not) You should not use DetectObjectAsync. DetectObjectAsync is a method of the
ComputerVisionClientExtensions class that returns results of the object detection operation after the analysis of the given image. In this scenario, you require OCR results.

(Not) You should not use ListModelsAsync. The ListModelsAsync method returns the list of the domain-specific models that are supported by the Azure AI Vision API.

(Not)You should not use Failed. If the OCR read operation failed, then the loop should end since no further read results can be retrieved.

(Not) You should not use Succeed. If the OCR read operation succeeded, then the loop retrieving read results should end as well.

#### Reference
- [Quickstart: Optical character recognition (OCR) - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/quickstarts-sdk/client-library?tabs=windows%2Cvisual-studio&pivots=programming-language-csharp)
- [OperationStatusCodes Enum (Microsoft.Azure.CognitiveServices.Vision.ComputerVision.Models) - Azure for .NET Developers | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cognitiveservices.vision.computervision.models.operationstatuscodes?view=azure-dotnet)
- [ComputerVisionClient Class (Microsoft.Azure.CognitiveServices.Vision.ComputerVision) - Azure for .NET Developers | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cognitiveservices.vision.computervision.computervisionclient?view=azure-dotnet)

### AI Vision Service

#### Measure Up
You are using Azure AI Vision service to manage media assets, and you plan to integrate and extract text from various image datasets for your organization. You plan to parse these datasets through the Azure AI Vision Read API and perform Optical Character Recognition (OCR).
You need to identify the prediction image datasets that can be analyzed using the Azure AI Vision model. Which three datasets should you choose? Each correct answer presents a complete solution.

![[Pasted image 20240129192453.png]]

#### Notes
You should choose JPEG and PNG image format datasets with images that have a maximum size of 3 megabytes (MB). The Azure AI Vision Read call supports both JPEG and PNG formats as well as GIF and BMP formats, with the image file size being less than 4 (MB).

You could also choose a BMP image dataset with dimensions greater than 100 x 100 pixels. The BMP format is supported, and the Azure AI Vision's Read API requires the dimensions of the image to be greater than 50 x 50 and at most 10000 x 10000 pixels.

You could also choose GIF images with a size of 2 MB and a dimension of 200 x 300 pixels. In the Azure AI Vision's Read API call, the image size should not be greater than 4 MB and the dimension should be greater than 50 x 50 pixels.

(Not) You should not choose a high-resolution image dataset with each image having a minimum size of 100 MB. In the Azure AI Vision's Read API call, the image size should not be greater than 4 MB.

(Not)You should not choose Photoshop Document (.psd) images with a maximum size of 40 MB. Azure AI Vision currently supports only JPEG, PNG, GIF, or BMP formats.

#### Reference
- [What is Azure AI Vision? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-in/azure/ai-services/computer-vision/overview)




### AI Vision
#### Measure Up
You develop an application that uses Azure AI Vision to find commercial logos and famous people in images.  You create an Azure AI Vision service *named cv1* in the *West US* region.
You want to test the cognitive service from the command line.  How should you create your request?

#### Notes
I recall some brand detection stuff on my recent test so look at the references and not just the answer here.

You should create the request as follows:
```bash
https ://cvl.cognitiveservices.azure.com/vision/v3.2/analyze? visualFeatures=Brands&details=Celebrities&language=en&model-version=latest
```
(Use) You should use cv1.cognitiveservices.azure.com. This is the endpoint for the Azure AI Vision resource you created.

(Use) You should use Brands for visualFeatures. This will cause the analyze method to return the name of the brands from the logos detected in the image along with their top left corner coordinates and their height and width.

(Use) You should use Celebrities for details. This will find famous people from a database of one million people.

(Not) You should not use cv1-prediction.cognitiveservices.azure.com. There is no separate prediction resource for the Azure AI Vision service. If you have created a Custom Vision service, then both training and prediction endpoints will be automatically created.

(Not) You should not use westus.cognitiveservices.azure.com. Regional endpoints have been replaced by endpoints for each resource. The regional endpoints are still available for some resources such as Translator. Other regional endpoints such as westus.api.cognitive.microsoft.com are still supported.

(Not) You should not use Categories. This will categorize the image based on an 86-class taxonomy of common classes of object for businesses, people, and places.

(Not) You should not use Objects. Objects is used to detect common objects in the image and provide their coordinates.

(Not) You should not use Landmarks. This is used to detect famous buildings and well-known landscapes from around the world.

#### Reference
- [Brand detection - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/concept-brand-detection)
- (swagger) [Cognitive Services APIs Reference (microsoft.com)](https://westcentralus.dev.cognitive.microsoft.com/docs/services/computer-vision-v3-2/operations/56f91f2e778daf14a499f21b)
- [Quickstart: Build an image classification model with the Custom Vision portal - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/getting-started-build-a-classifier)
- [Get translations status - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/reference/get-translations-status)
- (key) [Taxonomy of image categories - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/category-taxonomy)
- (key) [Object detection - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/concept-object-detection)
- (key) [Domain-specific content - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/concept-detecting-domain-content)


### AI Vision-Image Analysis

#### Measure Up
You are working for a nature reserve to help detecting common objects and animals. The reserve has a security system with over 400 cameras covering the complete area of the park, which take images every minute, storing them in a .jpeg format.  You need to use the Azure AI service to extract information from these images through REST API. The solution should not require any model training.  (3) Which three actions should you perform in sequence? Arrange in correct order!

#### Notes
Absolutely look at all three references below to understand this.  It was on the exam multiple times.

You should perform the following steps in order:
1.	Create an Azure AI Vision resource using the Azure portal. Navigate to the resource and retrieve your subscription key.
2.	Navigate to the Azure AI Vision API console under quick start from the Azure AI Vision resource menu.
3.	Generate and run the curl command using the Detect Objects API with your subscription key.

First, you should create an Azure AI Vision resource using the Azure portal. Once the resource is successfully deployed, you can navigate to the resource and retrieve your subscription key. Azure provides you with a primary and secondary key. These keys are used to access your Azure AI Service API. Do not share your keys. Only one key is necessary to make an API call.

Next, you should navigate to the Azure AI Vision API console under quick start from the Azure AI Vision resource menu. You can use the API Console to quickly try the API without writing code. Be sure to select the correct location for this resource. The API key and the location can be found in the Keys and Endpoint section in the left tab.

Finally, you should generate and run the curl command using the Detect Objects API with your subscription key. The Detect API will apply tags based on objects or living beings identified in the image. The Detect API only finds objects and living things, and therefore it will be able to identify common objects and animals in the nature reserve park.

(Not) You should not create a Custom Vision resource using the Azure portal, navigate to https://www.customvision.ai/, and create a new Custom Vision project. You are required to use a solution that does not involve model training. Using Custom Vision requires you to manually tag the images with labels and train the detector.

(Not) You should not select Object Detection under Project Types, manually upload and tag images, and train the detector. Object Detection is available through both the Custom Vision and Computer Vision services. Since you need to use an Azure AI service with no model training, this option should not be selected for common objects and animals. Manually uploading, tagging, and labeling images to train the detector are steps performed in the Custom Vision portal to train the detector model and identify objects of interest in a given image. With Azure AI Vision, a pre-trained model is used with no model training effort required to detect common objects.

#### Reference
- [Object detection - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-in/azure/ai-services/computer-vision/concept-object-detection)
- [What is Image Analysis? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-in/azure/ai-services/computer-vision/overview-image-analysis?tabs=4-0)
- [Quickstart: Image Analysis - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-in/azure/ai-services/computer-vision/quickstarts-sdk/image-analysis-client-library?tabs=windows%2Cvisual-studio&pivots=programming-language-python)


### AI Vision Service
#### Measure Up
You are analyzing images using the Azure AI Vision service.  You need to determine which visualFeatures to use for different requirements.  To answer, drag the appropriate visualFeature to each requirement. A visualFeature may be used once, more than once, or not at all.

![[Pasted image 20240129195602.png]]

#### Notes
(Use) You should use Tags to generate a list of words for the recognizable objects in the image. The Tags visualFeature tags the image with a detailed list of words related to the image content. Azure AI Vision can tag the image from thousands of recognizable objects, living beings, scenery, and actions. The API returns a simple list of the words and confidence levels.

(Use) You should use Categories to describe the image using a hierarchical taxonomy of buildings, food, outdoor, and animals. Categories classify the image using a hierarchical taxonomy of 86 classes including animals, building, food, people, plants, outdoor, indoor, and transport.

(Use) You should use Adult to detect if the image contains violent scenes. The Adult visualFeature can detect if the image contains nudity, sexual acts, sexually suggestive content, violence, or bloody scenes.

(Not) You should not use Brands. The Brands visualFeature detects well-known brand logos in the image.

(Not) You should not use Description. The Description visualFeature generates a complete sentence that describes the image.

(Not) You should not use Objects. The Objects visualFeature is used to detect objects within the image and their location.

#### Reference
- (Swagger) [Cognitive Services APIs Reference (microsoft.com)](https://westus.dev.cognitive.microsoft.com/docs/services/computer-vision-v3-2/operations/56f91f2e778daf14a499f21b)
- [Content tags - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-US/azure/ai-services/computer-vision/concept-tagging-images)
- [Taxonomy of image categories - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/category-taxonomy)
- [Detect Adult, racy, or gory content - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/concept-detecting-adult-content)
- [Brand detection - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/concept-brand-detection)
- [Image descriptions - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/concept-describing-images)


### AI Vision - Handwritten Text (OCR)

#### Notes
You are an AI developer at a historical research institution. Your institution has a collection of handwritten documents that it wants to digitize.  You need to develop a solution that converts the handwritten text into digital text. You plan to use Azure AI Vision to assist with the text conversion process.  Yes/No Statements

You can use Azure AI Vision’s Read API to extract handwritten text from documents. Optical Character Recognition (OCR) service is part of Azure AI Vision offering. Its Read API can extract both handwritten and printed text from documents and images.

Azure AI Vision APIs can extract text from documents with mixed languages. Read API uses deep learning models and can extract multilingual text without explicit specification of the different language codes. At the time of writing, Read API supports English, Chinese Simplified, French, German, Italian, Japanese, Korean, Portuguese and Spanish for handwritten text extraction.

IMPORTANT - You can run Azure AI Vision APIs on-premises as a container. Read APIs are available not only as an Azure- based cloud service, but also as a container for on-premises deployment. Fully qualified name of Read OCR container is mcr.microsoft.com/azure-cognitive-services/vision/read.

#### Reference
- [What is Azure AI Vision? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/overview)
- [OCR - Optical Character Recognition - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/overview-ocr)
- [Quickstart: Optical character recognition (OCR) - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/quickstarts-sdk/client-library?tabs=windows%2Cvisual-studio&pivots=programming-language-csharp)
- [Language support - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/language-support)




### Custom Vision-Custom Image Classifiers

#### Notes
You want to build a custom image classification model in the Custom Vision portal. You prepare THREE sets of images and save them all on your LOCAL machine.  
You need to train a custom image classification model.
Which four actions should you perform in sequence and in ORDER?

You should perform the following steps in order:

1.	Create a project.
2.	Upload all the images.
3.	Tag the images.
4.	Train the model.

You should create a project in the Custom Vision portal first. You can log in to https://customvision.ai/ and click the New Project button to create a new project. In the New Project dialog window, you can set the project type to Classification, indicate whether your model will be multiclass or multilabel and also select the domain closest to your custom vision scenario.

You should then upload all images. Click the Add images link and then select Browse local files to upload the images directly from your local machine. Alternatively, you can point to the remote URL if your images are accessible through the web.

You should tag the images next. Images can be tagged when you upload the images set by set. In this scenario, you mass upload all images and then selectively tag them by each set in the Custom Vision portal.

Finally, you should train the model. To do this, you should press the Train button and then monitor the training progress in the Performance tab. The model uses all the uploaded images listed in the Training Images tab.

(Not) You should not create Azure Files. Azure Files are fully managed file shares. You can mount them on Windows, Linux, and macOS machines using Server Message Block (SMB) or Network File System (NFS) protocols. You do not need Azure Files for the image upload process since the Custom Vision portal supports direct upload from the local drives.

(Not) You should not get the Prediction Key. Along with the Prediction URL, the Prediction Key is used to access your model’s prediction endpoint from external applications. You need to publish your model to enable the prediction endpoint.

- [Quickstart: Build an image classification model with the Custom Vision portal - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/custom-vision-service/getting-started-build-a-classifier)
- [Introduction to Azure Files | Microsoft Learn](https://learn.microsoft.com/en-us/azure/storage/files/storage-files-introduction)
- [Use prediction endpoint to programmatically test images with classifier - Custom Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/custom-vision-service/use-prediction-api)


### Custom Vision - Image Classification

#### Notes
You build a new cats and dogs image classification model in the Custom Vision portal. You train your model on a custom set of images.  You need to evaluate metrics from your last iteration, shown in the exhibit. Yes/No if true.

![[Pasted image 20240129201141.png]]

Precision indicates that out of 100 images identified as cats, 75 were indeed of cats. Precision indicates what is the proportion of true positives (TP) over the sum of all TP and False Positives (FP). It uses the formula: TP / (TP + FP).

Recall does not indicate that out of 100 images identified as cats, 43 were of dogs. Recall indicates the fraction of actual classifications that were correctly identified. If, for example, you had a total 100 images of cats, then recall of 43% would indicate that the model correctly identified 43 of them as cats. It uses the formula: TP / (TP + FN), where FN is the number of False Negatives.

Each iteration does not always improve the accuracy of your classifier. The accuracy of your model does not depend on the number of iterations. To improve the accuracy, you should add more images with varying backgrounds, lighting, object size, camera angle, and style. You also need to balance data to avoid a disproportional number of certain objects in comparison to others. Adding negative samples with images that do not match any of the other tags can also help to make your model more accurate.
#### Reference
- [Quickstart: Build an image classification model with the Custom Vision portal - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/custom-vision-service/getting-started-build-a-classifier)
- [Evaluate Model: Component Reference - Azure Machine Learning | Microsoft Learn](https://learn.microsoft.com/en-us/azure/machine-learning/component-reference/evaluate-model?view=azureml-api-2)
- (Key) [Improving your model - Custom Vision Service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/custom-vision-service/getting-started-improving-your-classifier)


### Custom Vision-Offline TensorFlow model
#### Notes
You train a new image classification model in the Custom Vision portal. You plan to use it offline with a TensorFlow framework.  You export your TensorFlow model from the Custom Vision service. You need to load your exported model’s files in your Python script.  Which TWO files should you use? 

(Use) You should use *labels.txt*. Your exported models will be downloaded in a .zip archive and contain labels.txt and model.pb files. The labels.txt file contains classification labels used by your image classification model.

(Use) You should also use *model.pb*. model.pb is a protocol buffer (ProtoBuf) file that contains your *exported TensorFlow* model. You can import it as a graph in your Python script.

(Not) You should not use PythonSettings.json. This is a workspace configuration file for the Python used in the Visual Studio integrated development environment (IDE). PythonSettings.json is not part of the package generated during the export of the TensorFlow model from the Custom Vision service.

(Not) You should not use requirements.txt. In Python, you can use requirements.txt to specify the external packages that your Python project requires. You can install them all using the Python pip installer.

#### Reference
- (Key) [Export your model to mobile - Custom Vision Service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/custom-vision-service/export-your-model) Also know how COMPACT models work here.
- [Tutorial: Run TensorFlow model in Python - Custom Vision Service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/custom-vision-service/export-model-python)
- [Unit test Python code with Test Explorer features - Visual Studio (Windows) | Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/python/unit-testing-python-in-visual-studio?view=vs-2019)
- [Manage Python package dependencies - Visual Studio (Windows) | Microsoft Learn](https://learn.microsoft.com/en-us/visualstudio/python/managing-required-packages-with-requirements-txt?view=vs-2019)


### Custom Vision - Bird detection

### Notes
You build a new bird detection model in the Custom Vision portal. You upload your training sets of bird images, tag them, and then train the model.  You need to evaluate the *performance* of your bird detection model. The Computer Vision portal calculates the precision of the model to be at 56%.  How should you interpret the results of the *precision calculation*?

(Use) You should interpret the results as: if *the model identified* 100 objects as birds, then 56 of them were actually birds. *Precision indicates how many* of the images that the *model labelled* as positive were actually positive. With 56% of precision for every 100 images that the model identifies as birds, 56 images were in fact of birds.

(Not) You should not interpret the results as: if the model identified 100 objects as birds, then 44 of them were actually birds. This interpretation would be valid if the model’s precision was calculated as 44%.

(Not)You should not interpret the results as: if there were 100 images of birds, then the model identified 44 as birds. This is the definition of recall (also known as the model’s sensitivity). With recall, you identify the ratio of the correctly identified images to all that were actually correct images. This interpretation would be valid for the model’s recall of 44%>.

(Not) You should not interpret the results as: if there were 100 images of birds, then the model identified 56 as birds. This interpretation would be valid for the model's *recall* of 56%.

#### Reference
- [Quickstart: Build an object detector with the Custom Vision website - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/custom-vision-service/get-started-build-detector)
- [Evaluate AutoML experiment results - Azure Machine Learning | Microsoft Learn](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-understand-automated-ml?view=azureml-api-2)


### Custom Vision-Domains
#### Notes
Important to notice the edge device here.  Read target shop as an edge device.

You build a new object detection solution for a retail company. Your solution must detect the real-time presence of certain products on the shop shelves. The company's marketing team wants your solution to run on edge devices because of the limited internet connectivity in the target shops.
You create a new object detection project in the Custom Vision portal. You need to choose the correct domain to support your requirements.  Which domain?

(Use) You should use the *General (compact)* [S1] *domain*. Compact domains are optimized for the *constraints of real-time image processing and object detection on edge devices*. The General (compact) [S1] model does not require post-processing logic, so it will allow you to get more consistent output from the various edge devices.

(Not) You should not use the Food or Retail domains. Both are image classification domains. In this case, you are building an object detection model.

(Not) You should not use the Products on shelves domain. Products on shelves is an object detection domain that can detect and classify products on shelves. However, it is not optimized to run on edge devices and cannot be exported from the Custom Vision portal for offline use. For these reasons, you need to use the General (compact) [SI] domain instead.

#### Reference
- [Quickstart: Build an object detector with the Custom Vision website - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/get-started-build-detector)
- [Select a domain for a Custom Vision project - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/select-domain)



### Custom Vision.Net-Code Completion
#### Notes
You are developing an object detection solution. You create a new project using the Custom Vision .Net software development kit (SDK).  You need to complete the code for a method that trains your project.  Complete the code.

#### CODE
```bash
private void TrainProject(CustomVisionTrainingClient trainingClient, Project project)
{
	var iteration = trainingClient. [*TrainProject*]	(project.Id);
	while (iteration.Status == " [*Training*] ”)
	{	
		Console.WriteLine("Training is in progress..");
		Thread.Sleep( 1000);
		iteration = trainingClient.GetIteration(project.Id, iteration.Id);
	}
Console.WriteLine('Training is complete.");
}
```

(Use) You should use the TrainProject method. TrainProject is a method of the
CustomVisionTrainingClientExtensions class that you use to train an object detection model. TrainProject returns an iteration object that you can query to understand the status of your training process.

(Use) You should also use the Training string. You can poll the status of your training by checking the value of the iteration object’s Status property. When training is in progress, the Status property will have its value assigned to the Training string.

(Not) You should not use the Exportiteration method. Exportiteration is a method of the
CustomVisionTrainingClientExtensions class that allows you to export your trained model for offline use. You can export your model in the CoreML, TensorFlow, Docker, or ONNX formats.

(Not) You should not use the Unpublishlteration method. Publishing the current iteration makes your model available for querying from outside. The Unpublishlteration method reverses the publishing process and removes your model’s exposed endpoint. Before you can publish your model, you should first train it using the TrainProject method.

(Not) You should not use the Completed string. In your while loop, you are checking whether the model's training is in progress. For this reason, you should use the Training string. The Completed string indicates that the model’s training is completed. However, you may use the Completed string with a ’not equal’ operation.


#### Reference
- [Quickstart: Object detection with Custom Vision client library - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/quickstarts/object-detection?tabs=windows%2Cvisual-studio&pivots=programming-language-python)
- [CustomVisionTrainingClientExtensions.TrainProject Method (Microsoft.Azure.CognitiveServices.Vision.CustomVision.Training) - Azure for .NET Developers | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cognitiveservices.vision.customvision.training.customvisiontrainingclientextensions.trainproject?view=azure-dotnet)
- [CustomVisionTrainingClientExtensions.ExportIteration Method (Microsoft.Azure.CognitiveServices.Vision.CustomVision.Training) - Azure for .NET Developers | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cognitiveservices.vision.customvision.training.customvisiontrainingclientextensions.exportiteration?view=azure-dotnet)
- [CustomVisionTrainingClientExtensions.UnpublishIteration Method (Microsoft.Azure.CognitiveServices.Vision.CustomVision.Training) - Azure for .NET Developers | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cognitiveservices.vision.customvision.training.customvisiontrainingclientextensions.unpublishiteration?view=azure-dotnet)


### Computer Vision
You are working for a nature reserve park to help in detecting the *presence* and *location* of animals of interest in the park, such as white tigers, lions, and pandas. The reserve has a security system with over 400 cameras covering the complete area of the park. The cameras take *images every minute*, storing them in a .jpeg format.  You need to use the Azure AI service to create your own model and extract information from these images.  Which three actions should you perform in sequence and order?

#### Notes
You should complete the following steps in order:

1.	Create a Custom Vision resource using the Azure portal. Navigate to https://www.customvision.ai/ and create a new Custom Vision project.
2.	Select Object Detection under Project Types. Manually upload and tag images and train the detector.
3.	Publish your model iteration and retrieve the prediction URL and prediction key to use in your application.

First, you should create a Custom Vision resource using the Azure portal before navigating to https://www.customvision.ai/ and creating a new Custom Vision project. The Custom Vision service helps in building your own model.

Next, you should select Object Detection under Project Types and manually upload and tag images before training the detector. Object Detection will help in detecting the presence and location of animals in the nature reserve Park. As you are building your own model, you will have to manually tag the uploaded images to create labels that will be used by the detector for training the model. You should only tag the animals of interest for the park, including white tigers, lions, and pandas, so that the custom model is trained to detect the presence and location of these animals.

Finally, you should publish your model iteration and retrieve the prediction URL and prediction key to use in your application. After successfully training the detector, the Custom Vision service creates a model iteration. Once published, this iteration will generate a prediction URL and a prediction key, which can be integrated into your application to make API calls to your model.

(Not) You should not create an Azure AI Vision resource using the Azure portal, navigate to the resource, and retrieve your key and endpoint. The Computer Vision service will use existing algorithms designed for specific use cases like brand detection, image description, etc. The nature reserve requires you to build a custom model that can be trained on its own data to increase model precision.

(Not) You should not select Classification under Project Types before manually uploading and tagging images and training the detector. With the classification type, you will only be able to apply labels to the images. You should use Object Detection, which, in addition to the applied labels, will return the coordinates within the image, helping to identify the location of the animals.

#### Reference
- [What is Custom Vision? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/overview)
- [Quickstart: Build an object detector with the Custom Vision website - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/get-started-build-detector)
- [Use prediction endpoint to programmatically test images with classifier - Custom Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/use-prediction-api)



### Custom Vision Classification Model
You have trained a Custom Vision classification model.
You need to retrieve the metrics that show the accuracy of the model. Which Rest API method should you use?


#### Notes
You should use GetlterationPerformance. GetlterationPerformance returns performance information about the iteration of a model's training. For a classification model, this includes the accuracy, precision, and recall metrics.

(Not) You should not use GetlmagePerformances. GetlmagePerformances returns the matching images for a specified tag. It does not include any performance metrics.

(Not) You should not use GetProject. GetProject just returns the name of the project.

(Not) You should not use Exportiteration. Exportiteration exports a trained model as a backup. It does not contain the model's metrics.

#### Reference
- [View or delete your data - Custom Vision Service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/export-delete-data)



### AI Bot
#### Notes
You are helping the customer support department of a global health insurance company to extract useful information from the daily customer queries and insurance claim requests that they receive through a bot.  You need to add additional functionality to your bot using Azure AI services to resolve the different requirements.

![[Pasted image 20240129210156.png]]

The requirement to understand and respond to customer voice inputs is fulfilled by the Speech service. Speech-enabled features can be added to an existing application using the Speech service, including various functionalities like speech translation, speech-to-text, text-to-speech, speaker recognition, etc.

The real-time transcription of audio into text using the Speech service will enable customers to have a conversation with the bot by speaking.

The requirement to process claim form images to extract customer information is fulfilled by the Computer Vision solution. The Azure AI Vision service provides you with access to advanced computer vision algorithms for processing images and returning information. The Image Analysis API can be used to extract customer information from the claim form images.
The requirement to flag undesirable or offensive text or images is fulfilled by the Content Moderator service. The Azure AI Content Moderator service is designed to handle potentially offensive, risky, or undesirable content. The service scans text, image, and video to apply content flags automatically powered by an AI content moderation engine. It also provides an online moderator environment for a team of human reviewers.

(Not) You should not select the Language service. The Azure AI Language service provides Natural Language Processing (NLP) features for text mining and text analysis, including sentiment analysis, opinion mining, key phrase extraction, language detection, and named entity recognition. Although these features are very useful, none of them satisfy any of the given requirements.

(Not) You should not select the Custom Vision service. Custom Vision is an image recognition service that lets you build, deploy, and improve your own image identifiers. Although this service is very useful, it does not satisfy any of the given requirements.

#### Reference
- [What are Azure AI services? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-in/azure/ai-services/what-are-ai-services)
- [What is the Speech service? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-in/azure/ai-services/speech-service/overview)
- [What is Azure AI Vision? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-in/azure/ai-services/computer-vision/overview)
- [What is Azure Content Moderator? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-in/azure/ai-services/content-moderator/overview)
- [What is Azure AI Language - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-in/azure/ai-services/language-service/overview)
- [What is Custom Vision? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-in/azure/ai-services/custom-vision-service/overview)




### AI Services - Patent Infringement
You are working for an intellectual property law firm. You need to protect clients' trademarks by looking for images that infringe the trademarks.  You build an application to check a set of images. You plan to use Azure AI Services to assist you.  You need to create a resource that you can use to identify images that contain logos that potentially infringe trademarks.  Which five actions should you perform in sequence and order?
#### Measure Up
![[Pasted image 20240129210722.png]]

#### Notes
You should perform the following actions in order:
1.	Create a Custom Vision resource.
2.	Create an Object Detection project.
3.	Upload and tag images.
4.	Train the model.
5.	Retrieve the prediction URL and key to use in your application.

(1) First, you should create a Custom Vision resource. Computer Vision only identifies well-known brands. You need to use Custom Vision and create a custom model to identify trademarks for your clients.

(2) Then, you should create an Object Detection project. Object Detection can locate and identify logos in images. You can only create an Object Detection project after you have created a Custom Vision resource in Azure.

(3) Then, you should upload and tag images of your clients' logos. You can only upload images after creating a project and selecting the type of project. You must tag the images before you train the model.

(4) Next, you should train the model. You must train the model before you can use the model for predictions.

(5) Finally, you should retrieve the prediction URL and key to use in your application. There are two endpoints: one for training and one for prediction. You use the prediction URL to find your logos in images that might infringe on your clients' trademarks.

(Not) You should not create an Azure AI Vision resource. You cannot upload your own images into Azure AI Vision. The Azure AI Vision service can only identify logos for well-known brands.

(Not) You should not create a Classification project. A classification model cannot detect logos. Classification models for Custom Vision analyze and describe images. You must use an object detection model for logos.

(Not) You should not retrieve the training URL and key to use in your application. The training URL is used to build and train the model, not for predictions. The Custom Vision portal automatically retrieves the training URL for you.

#### Reference
- [Tutorial: Use custom logo detector to recognize Azure services - Custom Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/logo-detector-mobile)
- [Quickstart: Build an object detector with the Custom Vision website - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/get-started-build-detector)
- [Quickstart: Build an image classification model with the Custom Vision portal - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/getting-started-build-a-classifier)



### Custom Vision-Food model
You build a new classification solution for a fresh food section of a supermarket. Your solution must be lightweight, compatible to run on edge devices, and detect the presence of fruit and vegetable products on the shop shelves.  You create a new classification project in the Custom Vision portal. Which domain?

#### Notes
You should use the food(compact) domain. The food(compact) domain will help you classify photographs of fruit and vegetables. Compact models are lightweight and can be exported to run on *edge devices*.

(Not) You should not use the food domain. Although the food domain will help you classify photographs of fruit and vegetables, it is not optimized to run on edge devices and cannot be exported from the Custom Vision portal for offline use.

(Not) You should not use the retail(compact) domain. The retail domain is optimized for images that are found in a shopping catalog or shopping website. If you want high precision classification between dresses, pants, and shirts, etc., you should use this domain.

(Not) You should not use the products on shelves domain. Products on shelves is an object detection domain that can detect and classify products on shelves. However, it is not optimized to run on edge devices and cannot be exported from the Custom Vision portal for offline use.

#### Reference
- [Quickstart: Build an image classification model with the Custom Vision portal - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/getting-started-build-a-classifier)
- [Select a domain for a Custom Vision project - Azure AI Vision - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/select-domain)



### Custom Vision SDK-Complete the code
You are developing an image classification solution. You create a new project using the Custom Vision .Net software development kit (SDK).  You need to complete the code for a method that publishes the current *iteration* of your trained image classification model.  Complete the code.

#### Code
#### Notes
The complete code of your method should be as follows:

```bash
private static void Publishlteration(**CustomVisionTrainingClient** trainingApi, Project project)
{
trainingApi.**Publishlteration**(project.Id, iteration.Id, publishedModelName, predictionResourceld);
Console.WriteLine("Current iteration published !\n");
}
```

(Use) You should use the *CustomVisionTrainingClient* class. This class can be used to create, train, and publish your custom vision models. In your method, an instance of CustomVisionTrainingClient is passed through the trainingApi variable.

(Use) You should use the *Publishlteration* method. This method can be used to publish the current iteration of your trained custom vision model and make it available for querying.

(Not) You should not use ComputerVisionClient. The ComputerVisionClient class can be used to analyze images, generate thumbnails, and get a description of an image when interacting with Azure AI Computer Vision service. This class is not intended for use with the Custom Vision service.

(Not) You should not use CustomVisionPredictionClient. The CustomVisionPredictionClient class can be used to query your published custom vision models for image classification predictions. It cannot be used to train and publish a model.

(Not) You should not use Exportiteration. The Exportiteration method can be used to export the current iteration of your trained custom vision model. At the time of writing, this method supports export into CoreML, TensorFlow, DockerFile, and ONNX formats.

(Not) You should not use TrainProject. The TrainProject method can be used to create iterations and train your custom vision project. To publish individual iterations, you should use the Publishlteration method.

#### Reference
- [Quickstart: Image classification with Custom Vision client library or REST API - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/custom-vision-service/quickstarts/image-classification?tabs=windows%2Cvisual-studio&pivots=programming-language-csharp)
- [CustomVisionTrainingClient Class (Microsoft.Azure.CognitiveServices.Vision.CustomVision.Training) - Azure for .NET Developers | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cognitiveservices.vision.customvision.training.customvisiontrainingclient?view=azure-dotnet)
- [ComputerVisionClient Class (Microsoft.Azure.CognitiveServices.Vision.ComputerVision) - Azure for .NET Developers | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cognitiveservices.vision.computervision.computervisionclient?view=azure-dotnet)
- [CustomVisionPredictionClient Class (Microsoft.Azure.CognitiveServices.Vision.CustomVision.Prediction) - Azure for .NET Developers | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/microsoft.azure.cognitiveservices.vision.customvision.prediction.customvisionpredictionclient?view=azure-dotnet)


### AI Video Indexer
You plan to use Azure AI Video Indexer to analyze the content of your custom videos.
You upload videos to the Azure AI Video Indexer website. You want to segment your videos into time-related units based on each video’s structural and semantic properties.  You need to determine what units can be detected by the Azure AI Video Indexer. Matchbox UI.

#### Measure Up
![[Pasted image 20240129212314.png]]
#### Notes
*Shots* are the consecutive frames taken from the same camera at the same time. Shots are determined by the changes in the visual content such as sudden or gradual transitions in the color scheme of adjoining frames. Each shot has a start and an end time. Shots metadata also includes the list of keyframes within that shot.

*Keyframes* are the representative frames selected from the entire video based on aesthetic properties. Keyframes best represent each shot within your video and are selected based on such properties as contrast and stableness.

*Scenes* are single events composed of a series of semantically related consecutive shots. A video is divided into scenes based on semantic aspects of your videos, for example, color consistency or transition across consecutive shots. Each scene has a start and an end time. A scene also has a thumbnail that is typically the first keyframe of its underlying shot.

#### Reference
- [Azure AI Video Indexer scenes, shots, and keyframes | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-video-indexer/scenes-shots-keyframes)
- [What is Azure AI Video Indexer? | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-video-indexer/video-indexer-overview)



### AI Video Indexer-people detection
You want to test the people detection functionality of Azure AI Video Indexer. You prepare a sample video to process.  You need to analyze your sample video using a free trial of Azure AI Video Indexer.  Which three actions should you perform in sequence and order?

#### Notes
Actions in order:

1.	Sign into the Azure AI Video Indexer website.
2.	Use the Upload button.
3.	Check your e-mail and click the link provided.

(Use) You should sign into the Azure AI Video Indexer website. Azure AI Video Indexer is accessible at https://www.videoindexer.ai. With a free trial, you can use up to 600 minutes of free video indexing using the Azure AI Video Indexer website or up to 2,400 minutes when accessing it through API.

(Use) You should then use the Upload button. This allows you to browse for a file on your local machine or enter a file URL to retrieve it remotely. Once your sample video is uploaded, Azure AI Video Indexer starts its processing by indexing and analyzing the video’s content.

(Use) Finally, you should check your e-mail and click the link provided. When the processing of your video is completed, you will receive an email with a link to your processed video and a brief overview of people, brands, named entities, and other details found. You can click the link to check the findings on the Azure AI Video Indexer website.

(Not) You should not sign into the Azure portal. The use of the free trial does not require any explicit configuration in Azure. You may need to log in to Azure if you want to pre-create an Azure AI Video Indexer account for a paid option. Alternatively, you can create a new Azure AI Video Indexer account directly from the Azure AI Video Indexer website by clicking the Create unlimited account option.

(Not) You should not use the Share Account button. The Share Account option can help you to collaborate with others by inviting them to your Azure AI Video Indexer account.

(Not) You should not check the People section of the Content model customization. The Content model customization option allows you to manage Person, Brands, and Language models, for example, to add custom faces or exclude certain brands.


#### Reference
- [Sign up for Azure AI Video Indexer and upload your first video - Azure | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-video-indexer/video-indexer-get-started)
- [Create a classic Azure AI Video Indexer account connected to Azure | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-video-indexer/connect-to-azure)
- [Manage access to an Azure AI Video Indexer account | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-video-indexer/restricted-viewer-role)
- [Customize a Person model with Azure AI Video Indexer website | Microsoft Learn](https://learn.microsoft.com/en-us/azure/azure-video-indexer/customize-person-model-with-website)


### AI Vision Spatial Analysis
You are an AI developer at a large retail company. Your company has recently installed new security cameras in all its stores and wants to gain a better understanding of customer behavior and ensure compliance with local regulations. You plan to use Azure AI Vision Spatial Analysis to extract insights from the video streams. You need to determine which scenarios can be enabled by the Spatial Analysis service.  Which two scenarios?

#### Notes
- Counting the number of people entering a retail store over time
- Detecting if people in an elevator are wearing face masks

(Use) You should consider counting the number of people entering a retail store over time. Azure AI Spatial Analysis can detect the *presence and movement of people in video*. It provides a *functionality for counting people in a specific zone* over time, for example, how many customers enter a store during lunchtime.

(Use) You should consider detecting if people in an elevator are wearing face masks. Azure AI Spatial Analysis can be configured to detect if a person is wearing a mask. You can enable this functionality for Spatial Analysis PersonCount, PersonCrossingLine and PersonCrossingPolygon operations.

(Not) You should not consider extracting key information from printed sales receipts. The ability to analyze and extract key information from documents is part of Azure AI Document Intelligence solutions. It provides a pre-built receipt model that can extract the vendor name, contact details, transaction line items and other key information from printed and handwritten receipts.

(Not) You should not consider transcribing speech from audio streams in real time. Speech-to-text is a feature of the Azure AI Speech service. It can recognize speech and transcribe it into text in real time or as a batch operation.

(Not) You should not consider using face recognition to greet your frequent customers. Face recognition is a feature of the Azure AI Vision service. It can be used to verify and identify people by their faces.  Think how creepy it is when Alexa recognizes and uses you own name.  It feels uncomfortable. 

#### Reference
- [What is Spatial Analysis? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/intro-to-spatial-analysis-public-preview)
- [Receipt data extraction - Document Intelligence (formerly Form Recognizer) - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/concept-receipt?view=doc-intel-4.0.0)
- [Speech to text overview - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/speech-to-text)
- [Face recognition - Face - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/concept-face-recognition)


### AI Vision Spatial Analysis-Security cameras
You develop an application that uses Azure AI Vision Spatial Analysis to analyze video content from your company’s security cameras.  You deploy a Spatial Analysis container and make its service available at the sa1.company1.int internal endpoint. You then create an index named my-index1 and add your videos to it. Your API subscription key abcdefgl23456. You want to verify that the video ingestion process is completed. You need to use a curl request.
Complete the curl command.

#### Notes
Command:
```bash
curl -v -X    GET    "https://sal.companyl.int/  computervision /retrieval/indexes/my- indexl/ingestions?api-version=2023-05-01-previews$top=20" -H "ocp-apim- subscription-key: abodefgl23456"
```

(Use) You should use the *GET* request method. The Get Ingestion API of the Spatial Analysis service expects requests of the GET HTTP method. GET is the default method for curl, so you can either explicitly specify it with the -X GET flag, or omit it.

(Use) You should use *computervision* in the API call's URL. Spatial Analysis is part of the Azure AI Vision service, and the URL structure of enabled API endpoints contains the computervision hierarchy node.

(Not) You should not use the POST request method. The POST method is used to send data to the API backend and you can use it with the Search By Text API of the Spatial Analysis service to perform a search for a keyword or phrase within the video’s metadata, where your keyword or phrase will be sent as a part of the POST request’s payload.
You should not use the PUT request method. The PUT method is also used to send data to the API backend. The Spatial Analysis service accepts GET requests to the Create Index API to create an index for storing and organizing videos and their metadata, and to the Create Ingestion API to add video files to the index.

(Not) You should not use customvision in the API call's URL. The customvision hierarchy node is part of the Azure AI Custom Vision API endpoint. The Custom Vision service can be used to build and deploy custom image identifier models.

(Not) You should not use videoindexer in the API call’s URL. The videoindexer domain name is used by API endpoints of the Azure AI Video Indexer service. Azure AI Video Indexer is built on Azure AI Services including Azure AI Vision to extract insights from your videos.

#### Reference
- [What is Spatial Analysis? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/intro-to-spatial-analysis-public-preview)
- [Do video retrieval using vectorization - Image Analysis 4.0 - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/how-to/video-retrieval)
- (openAI) [Cognitive Services APIs Reference (microsoft.com)](https://westus2.dev.cognitive.microsoft.com/docs/services/Custom_Vision_Training_3.3/operations/5eb0bcc6548b571998fddebd)
- [APIs: Details - Microsoft Azure API Management - developer portal (videoindexer.ai)](https://api-portal.videoindexer.ai/api-details#api=Operations&operation=Get-Account)



### Sentiment Analysis
You want to test the Sentiment Analysis feature of the Azure AI Language API.
You submit your document for analysis. The Azure AI Language API labels your document as mixed with a confidence score of 0.9.  What combination of sentences can generate such results?

- At least one sentence is positive, and the rest are negative.
#### Notes
Such results can be generated when at least one sentence is positive and the rest are negative. For your document to be labeled as mixed, at least one sentence should be positive and at least one sentence should be negative.

A combination where all the sentences in the document are neutral will not be labeled as mixed. When all the sentences in the document are labeled as neutral, then on the document level the Azure AI Language API will also return the neutral label.
A combination where at least one sentence is negative and the rest are neutral will not be labeled as mixed.

If there is at least one negative sentence, no positive sentences, and the rest are neutral, then the Azure AI Language API will label the document as negative.

A combination where at least one sentence is positive and the rest are neutral will not be labeled as mixed. If there is at least one positive sentence, no negative sentences, and the rest are neutral, then the Azure AI Language API will label the document as positive.

#### Reference
- [What is Azure AI Language - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/language-service/overview)
- [How to perform sentiment analysis and opinion mining - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/language-service/sentiment-opinion-mining/how-to/call-api)
- [What is sentiment analysis and opinion mining in the Language service? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/language-service/sentiment-opinion-mining/overview?tabs=prebuilt)


### AI Language-Submitted Essays
You build a new app to analyze submitted essays. You plan to use Azure AI Language to extract key phrases from the essays. You create a new Azure AI Language resource named ta1 in Azure.
You need to test key phrase extraction in your app using the Azure AI Language REST API.
Which three actions should you perform in sequence? Box ordering counts.

#### Notes
Steps in order:

1.	Structure your POST request.
2.	Call https://ta1.cognitiveservices.azure.eom/language/:analyze-text endpoint.
3.	Process the JSON results in your app.

(1) You should structure your POST request first. Key phrase extraction requests should be of the POST type. You should provide an access key from your ta1 Azure AI Language resource in the header of your POST request and define the JSON documents collection in the request’s body with the essays to analyze.

(2) You should then call https://ta1.cognitiveservices.azure.eom/language/:analyze-text endpoint. The Azure AI Language API accepts calls at the /:analyze-text endpoint. The body of your POST request should also contain JSON element named kind that is set to KeyPhraseExtraction value. The inclusion of this feature instructs your Azure AI Language resource to perform the key phrase extraction operation.

(3) Finally, you should process the JSON results in your app. The results of the key phrase extraction are returned in a JSON formatted response. You can parse these in your app and retrieve the key phrases for each document from your JSON collection.

(Not) You should not structure your GET request. Requests to Azure AI Language API’s /analyze endpoint should always be of the *POST *type.

(Not) You should not call https://ta1.cognitiveservices.azure.eom/language/:query-knowledgebase endpoint. This is a valid endpoint of the Azure AI Language API. However, it is intended for answering the specified question *using your knowledge base*.

(Not) You should not process the XML results in your app. POST requests to the Azure AI Language API *always* receive responses in a *JSON format*.



### AI Language Detection-JSON Response

#### Notes
You plan to enable the language detection feature in your app so that you can provide a more customized service to your customers.  You integrate your app with the Azure AI Language API. Upon calling the API's language detection endpoint, your app receives the following JSON response:
```shell
{
	"kind": "LanguageDetectionResults",
	"results": {
		"documents": [{
			"id": "1",
			"detectedLanguage": {
				"name": "Spanish",
				"iso6391Name": "es",
				"confidenceScore": 0.99
			},
			"warnings": []
		}],
		"errors": [],
		"modelVersion": "2022-10-01"
	}
}
```

For each of the following statements, select Yes if the statement is true. Otherwise, select No.

(NO) The confidence score value does not range from 0 to 100. It ranges from 0 to 1, with 1.0 indicating the highest possible confidence level of the language detection model.

(YES) The Azure AI Language API uses US as the default country code for language detection in ambiguous input content. You can set the countryHint parameter in your input JSON document to an empty string to remove US as the default country code. You can also set the countryHint parameter explicitly to any other valid ISO 3166-1 alpha-2 country/region code, if the origin of the input content is known to be coming from that specific country or region.

(NO) You cannot use the document ID to retrieve the language detection history for the last 30 days. Azure AI Language is a stateless service. Language detection results are returned immediately in the API response and not stored in Azure. That is why you cannot retrieve any language detection history.

#### Reference
- [What is language detection in Azure AI Language? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/language-service/language-detection/overview)



### AI Sentiment Analysis

You are working for a global news media organization that publishes articles on social media platforms like X, Facebook, etc. They want your help in extracting useful information from the comments sections of their published articles.  You need to identify the Azure AI Language API features to address the below key requirements:
•	Categorize the comments into negative, neutral and positive.
•	Identify the main talking points in a given comment.

Which two features should you use? 

#### Notes
- Key phrase extraction
- Sentiment analysis

(Use) You should use sentiment analysis. Sentiment analysis features help in determining what people think of your brand or topic by mining the text for clues about positive or negative sentiment. This feature will help in categorizing the user comments into negative, neutral, and positive labels. It also returns a confidence score between 0 and 1 for each sentence or comment for the respective sentiment. Sentiment analysis works best when you give it smaller amounts of text to work on.

(Use) You should also use key phrase extraction. The key phrase extraction feature will help you to quickly identify the main concepts in a given text. Key phrase extraction works best when you give it larger amounts of text to work on. This feature can extract and identify the main talking points in a given user comment.

(Not) You should not use language detection. The language detection feature generates a single language code and confidence score against the given input text.

(Not) You should not use Named Entity Recognition. The Named Entity Recognition feature helps to identify and categorize entities in your input text.

#### Reference
- [What is Azure AI Language - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/language-service/overview)



### AI Language-Data Redaction / PII Data
You are an AI developer at a healthcare company. Your company wants to redact the contact details of the patients from their medical records to prevent data leakage when using internal AI solutions.  You plan to use Azure AI Language to develop the required data redaction.
Which feature is offered by Azure AI Language for this purpose?

#### Notes
(Use) You should select Pll detection. Pll detection is a feature of Azure AI Language that you can use to identify, categorize, and redact personal data. When dealing with a patient's medical records, you may remove or replace sensitive details with generic placeholders before making the data available to internal AI solutions.

(Not) You should not select Entity linking. Entity linking is a feature of Azure AI Language that can link entities in a given text to corresponding entries in a knowledge base like Wikipedia. For example, in the sentence “I visited the Colosseum yesterday”, the word “Colosseum” will be linked to an article on Wikipedia about the famous amphitheater in Rome.

(Not) You should not select Key phrase extraction. Key phrase extraction is a feature of Azure AI Language that can identify the main points and key information in a given text. However, it cannot remove or mask personal information as required in this case.

(Not) You should not select Sentiment analysis. Sentiment analysis is a feature of Azure AI Language that can detect negative, positive, or neutral sentiment at a sentence or document level.

#### Reference
- [What is the Personally Identifying Information (PII) detection feature in Azure AI Language? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/language-service/personally-identifiable-information/overview)
- [What is entity linking in Azure AI Language? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/language-service/entity-linking/overview)
- [What is key phrase extraction in Azure AI Language? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/language-service/key-phrase-extraction/overview)
- [What is sentiment analysis and opinion mining in the Language service? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/language-service/sentiment-opinion-mining/overview?tabs=prebuilt)



### Custom Neural Voice (CNV)
Your company wants to enrich the web interface of its marketing solution with a customized synthetic voice. You are provided with some marketing text samples and asked to create natural-sounding multi-lingual voices for each of your premium brands. You want to use Custom Neural Voice (CNV) technology to create custom synthetic voices. You need to determine the sequence of applying CNV technologies.  Matchbox UI.
- 1 - Text input
- 2 - Text analuzer
- 3 - Neural acoustic model
- 4 - Neural vocoder
- 5 - Audio output

#### Notes
The first step in creating custom CNV voices is to get a text input. You can group text inputs by target language and brand so that they can be fed to the relevant synthetic CNV voice channel.

Next, you should use text analyzer. The text analyzer processes your input text to generate distinct units of sounds, called phonemes, in the specified language. A sequence of phonemes is then fed into the neural acoustic model. This helps to define speech signals specific to your synthetic voice such as speed, intonation, timbre, and others.

Output from the neural acoustic model should be sent to a neural vocoder. The neural vocoder converts the acoustic features generated by the model into a continuous voice signal.

You can save the synthetic voice signal as an audio output. Common audio output formats are WAV and AIFF files. You may record them at 44.1 kHz 16-bit monophonic (CD quality) or better. 
Recording at 48 kHz 24-bit is also very common and is recommended for a higher quality synthetic voice recording.

#### Reference
- [Custom neural voice overview - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/custom-neural-voice)
- [Neural Text to Speech extends support to 15 more languages with state-of-the-art AI quality - Microsoft Community Hub](https://techcommunity.microsoft.com/t5/ai-azure-ai-services-blog/neural-text-to-speech-extends-support-to-15-more-languages-with/ba-p/1505911)
- [Recording custom voice samples - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/record-custom-voice-samples)

7

### AI Text To Speech
You want to enable the text-to-speech functionality in your app. You deploy the Azure AI Speech service in the US West region and retrieve the subscription key aabbcc1l22ddeeff.
You need to complete the code for a method that outputs generated speech directly to a computer’s speaker. Complete the code segment drop lists.

#### Notes
Code
```bash
static async Task SpeechToSpeaker(string myText)
{
	varconfig = SpeechConfig.FromSubscription("aabbccll22ddeefF',    "westus"    );
	using var speechGenerator = new     SpeechSynthesizer   (config);
	await speechGenerator.SpeakTextAsync(myText)
}
```
- westus
- SpeechSythesizer

(Use) You should use “westus”. Your Azure AI Speech service instance is deployed in the West US region in California. For this reason, you should use “westus” as a region code along with the subscription key to instantiate the SpeechConfig object in your code.

(Use) You should also use SpeechSynthesizer. The SpeechSynthesizer class performs the text-to-speech conversion and can redirect the audio output to your computer’s speakers, file, or audio output streams.

(Not) You should not use “westeurope”. Your Azure AI Speech service is deployed in the West US region, not in West Europe.

(Not) You should not use “westus2”. West US 2 region is in Washington. In this scenario, the Azure AI Speech service is deployed in West US, that is in California. You have to use “westus” for your target region.

(Not) You should not use IntentRecognizer. The IntentRecognizer class can recognize intents using the Conversational Language Understanding (CLU). IntentRecognizer cannot convert input text into speech.

(Not) You should not use SpeechRecognizer. The SpeechRecognizer class transcribes your input speech into text. To perform text-to-speech conversion, you should use SpeechSynthesizer.


#### Reference
- [Speech to text overview - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/speech-service/speech-to-text)
- [Text to speech quickstart - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/speech-service/get-started-text-to-speech?tabs=windows%2Cterminal&pivots=programming-language-csharp)
- [Choose the Right Azure Region for You | Microsoft Azure](https://azure.microsoft.com/en-gb/explore/global-infrastructure/geographies/#overview)
- [Intent recognition with CLU quickstart - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/speech-service/get-started-intent-recognition-clu?tabs=windows&pivots=programming-language-csharp)
- [Speech to text quickstart - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-gb/azure/ai-services/speech-service/get-started-speech-to-text?tabs=windows%2Cterminal&pivots=programming-language-csharp)



### AI Speech service - transcription
Your company uses the Azure AI Speech service to transcribe your call center’s audio recordings into text format.  The Business team finds that the speech-to-text model provides poor performance when *transcribing some product-specific* words.  You need to retrain your model with options that can improve its accuracy.  Which two options should you use to *improve the model’s accuracy*? 

#### Notes
- Additional marketing text documents
- Calls transcribed by humans

(Use) You should retrain your model by adding additional marketing text documents. The accuracy of your speech-to-text model can be improved by adding new training data that fall into three main categories: related text sentences, audio with human-labeled transcripts, and new words with pronunciation. Additional marketing data, product brochures, and other related text sentences can improve the accuracy of your retrained model.

(Use) You could also retrain your model by adding calls transcribed by humans. Sample audios should cover the full spectrum of speech related to your company’s products. Such human-labeled transcripts provide the greatest accuracy improvement.

(Not) You should not retrain your model by adding exact transcripts of videos. In the question scenario, you are dealing with the audio recordings from your company’s call center. Exact transcripts of videos can help to improve model accuracy in scenarios of video closed captioning.

(Not) You should not retrain your model by adding lists that use all combinations of commands and entities. This option works for scenarios in which you need to retrain a Voice Assistant related model, since it has to recognize end-user commands and extract entities from user utterances.

#### Reference
- https://learn.microsoft.com/en-gb/azure/ai-services/speech-service/how-to-custom-speech-evaluate-data




### AI SpeechRecognizer-audio microphone
You are developing an app that takes input from a microphone.
You need to convert the audio into text. The audio messages are between 10 seconds and 2 minutes in duration. You need to *improve the accuracy of the recognition of the name of your product*, ProductA.  Complete the code (drop list).

#### Notes
- SpeechRecognizer
- addPhrase
- start_continuous_recognition

Code
```bash
speech_recognizer = speechsdk.SpeechRecognizer
(speech_config=speech_config/ audio_config=audio_config)
productlist = speechsdk. PhraseListGrammar.from_recognizer(speech_recognizer)
productlist.  addPhrase ("ProductA")

done = False 

def stop_cb(evt):
	speech_recognizer.stop_continuous_recognition() 
	nonlocal done 
	done = True

speech_recognizer.session_stopped.connect(stop_cb)

speech_recognizer. start_continuous_recognitionv () 
while not done: 
	time.sleep(.S)
```

(Use) You should use the SpeechRecognizer class to start the speech service. SpeechRecognizer can perform speech-to-text processing.

(Not) You should not use AudioDataStream. AudioDataStream represents an audio data stream when using speech synthesis in speech-to-text.

(Use) You should use addPhrase to add the product name to improve recognition of the product name.

(Use) You should use the start_continuous_recognition method to start the processing of the audio. The method starts speech recognition until an end event is raised. Continuous recognition can easily process the audio duration described in the scenario.

(Not) You should not use recognize_once or recognize_once_async. These methods only listen to audio for a maximum of 15 seconds.





### Speech SDK-TextToSpeech
You are developing a real-time text-to-speech application with the Speech SDK.
You need to improve the quality of the speech synthesis and user experience. What should you use for the following requirements? 
- SSML
- AudioDataStream
- Tuning file

(Use) You should use Speech Synthesis Markup Language (*SSML*) to adjust the pitch and speaking rate. SSML can adjust the pitch, pronunciation, speaking rate, and volume of the synthesized speech output from the speech service.

(Use) You should use *AudioDataStream* to minimize the time before the user hears the speech after submitting text. To lower latency, you should use streaming. In your code you can start playback when the first audio chunk is received instead of waiting for the whole audio to be received. You can use AudioDataStream in the Speech software development kit (SDK) to enable streaming.

(Use) You should use a *tuning file to optimize* text-to-speech voice output by adjusting speech attributes in an online tool. Tuning files can be uploaded into the Audio Content Creation tool to fine-tune speech outputs.

(Not) You should not use Long Audio API. Long Audio API is not used for real-time speech. Instead, it synthesizes long-form text such as articles and documents into speech.

(Not) You should not use custom neural voices. Custom neural voices are created with neural networks and create more fluid and natural-sounding outputs. You can create your own custom neural voice by uploading voice samples and training a voice model.
(Not) You should not use Visemes. Visemes are used to lip-sync animations of faces to speech. Visemes use the position of the lips, jaw, and tongue when making particular sounds.

#### Reference
- [Speech Synthesis Markup Language (SSML) overview - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/speech-synthesis-markup)




### AI Speech SDK-speech to text / Intent Recognition

You have an application that performs speech-to-text and takes action on behalf of the user. You need to recognize what the user wants to do using the Azure AI Speech SDK.
What are two possible ways to achieve this?
- Conversational language understanding (CLU)
- Pattern matching
#### Notes
(Use) You should use pattern matching or conversational language understanding (CLU). The Azure AI Speech software development kit (SDK) has two ways to recognize intents. 

(Use) The first is pattern matching, which can be used for *simple instructions or specific phrases* that the user is instructed to use. CLU model can be integrated using the Speech SDK to recognize more complex intents with natural language.

(Not) You should not use Speech Synthesis Markup Language (SSML). SSML adjusts the pitch, pronunciation, speaking rate, and volume of the synthesized speech output from the speech service.

(Not) You should not use key phrase extraction. Key phrase extraction is part of the Azure AI Language API and extracts the main talking points from text. Key phrase extraction is not integrated with the Azure AI Speech SDK.

(Not) You should not use Visemes. Visemes are used to lip-sync animations of faces to speech. Visemes use the position of the lips, jaw, and tongue when making particular sounds.

### Reference
- [Intent recognition overview - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/intent-recognition)
- [Speech Synthesis Markup Language (SSML) overview - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/speech-synthesis-markup)
- [What is key phrase extraction in Azure AI Language? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/language-service/key-phrase-extraction/overview)
- [Get facial position with viseme - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/how-to-speech-synthesis-viseme?tabs=visemeid&pivots=programming-language-csharp)


### AI SpeechService-Sythesized Speech SSML
You are developing an app that will read out news articles. You want to use Azure AI Speech service to convert text into human-like synthesized speech.  You need to ensure that your app uses natural pauses and intonation. You have the following Speech Synthesis Markup Language (SSML) code sample to test how its silence feature works.
```bash
<speak version="'l. 0" xmlns="http : //www. w3 . org/2001/10/synthesis" xmlns:mstts="http://www.w3.org/2001/mstts" xml :lang="en-US">
Cvoice name="en-US-JennyNeural">
Cmstts: silence type="Sentenceboundary" value="250ms"/>
Scientists have made a major breakthrough in the field of quantum computing. They are now using a novel technique to create qubits that are more stable than ever before.
</voice>
</speak>
```

#### Notes
(YES) Your SSML code sample uses a neural voice. en-US-JennyNeural is one of the US English text-to-speech neural voices supported by Azure AI Speech service. Neural voices use deep neural networks to generate human-like speech.

(NO) The mstts:silence element does not insert pauses after the given sample text. The mstts:silence element, depending on its attributes, inserts pauses before or after text, or between two adjacent sentences. In the SSML code sample, the type attribute of the msttsisilence element is set to Sentenceboundary, meaning that 250ms of silence will be added between the two given sentences.

(YES) You can also use the break element to add pauses. You can use the break element to add pauses anywhere in the text, in contrast to the msttsisilence element, which inserts pauses only at the beginning or end of input text, or between two adjacent sentences.

#### Reference
- [Speech Synthesis Markup Language (SSML) overview - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/speech-synthesis-markup)
- [Speech Synthesis Markup Language (SSML) document structure and events - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/speech-synthesis-markup-structure)
- [Language support - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/language-support?tabs=stt)




### AI Speech Service-Custom Speech
You are an AI developer at a consultancy agency. Your customers want to evaluate Azure AI Speech service's capabilities for their use case scenarios.
You need to determine which feature of the Azure AI Speech service would be most relevant for the following scenarios. You should choose the feature that requires the least amount of effort to implement an maintain.
•	A robotic arm that can understand industry-specific jargon in a given voice command
•	An audio book app for children that can convert text to speech using a human-like voice
•	A voice assistant that can speak in the voice of a celebrity.
Match the boxes

#### Notes
Use) You should use a *Custom Speech model* for a robotic arm that can understand industry-specific jargon in a given voice command. You can use industry-specific content to train and deploy a Custom Speech model that is tailored to your specific scenario and environment. Custom Speech models can improve the accuracy and quality of speech recognition by adapting it to specific vocabulary.

(Use) You should use *prebuilt neural voice* for an audio book app for children that can convert text to speech using a human-like voice. The Azure AI Speech service offers a variety of prebuilt neural voices that allow you to convert text to natural and expressive speech. In this scenario, a prebuilt neural voice can match the genre and style of the book.

(Use) You should use *Custom Neural Voice* for a voice assistant that can speak in the voice of a celebrity. The Custom Voice feature in the Azure AI Speech service allows you to train a custom neural voice with your own audio data and transcripts. Custom Neural Voice can generate speech to sound like your own voice or that of a celebrity.

(Not) You should not use speech translation for any of these scenarios. Speech translation can be used to perform real-time and multi-language speech-to-speech and speech-to-text translation of an input audio stream.

#### Reference
- [What is the Speech service? - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/overview)
- [Custom speech overview - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/custom-speech-overview)
- [Custom neural voice overview - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/custom-neural-voice)
- [Speech translation overview - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/speech-translation)



### AI Speech Service-Keyword Recognition
You are an AI developer at an automotive company. Your company wants to develop an in-car virtual assistant.  You plan to use the Azure AI Speech service to train an on-device model for custom keyword recognition. You need to determine which types of models can be generated by the Custom Keyword portal in Azure AI Speech Studio. Which two types of models should you choose? 

#### Notes
- Basic
- Advanced

(Use) You should choose the Advanced model type. Advanced on-device model types are trained for up to 48 hours by fine-tuning a common base model with simulated custom keyword training data. Advanced models are best suited for production use scenarios.

(Use) You should also choose the Basic model type. Basic on-device model types take minutes to train and are based on a common base model. They might have less optimal accuracy characteristics compared to Advanced model types and are intended for demo or rapid prototyping purposes.

(Not) You should not choose the Custom, MLflow or Triton model types. None of these model types are used in the custom keyword recognition process. Instead, these are the model types supported by the Azure Machine Learning solution. Custom type refers to a model file or folder trained with a custom standard, MLflow defines the packaging of machine learning models that can be understood by downstream MLflow- compatible real time and batch inference solutions, while Triton model types are optimized to run on NVIDIA Triton Inference platform.

#### Reference
- [Keyword recognition overview - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/keyword-recognition-overview)
- [Register and work with models - Azure Machine Learning | Microsoft Learn](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-manage-models?view=azureml-api-2&tabs=cli%2Cuse-local)
- [MLflow and Azure Machine Learning - Azure Machine Learning | Microsoft Learn](https://learn.microsoft.com/en-us/azure/machine-learning/concept-mlflow?view=azureml-api-2)
- [High-performance model serving with Triton - Azure Machine Learning | Microsoft Learn](https://learn.microsoft.com/en-us/azure/machine-learning/how-to-deploy-with-triton?view=azureml-api-2&tabs=azure-cli%2Cendpoint)



### AI Translation Service-realtime chat translation
You want to enable real-time text translation in your chat application. You integrate your application with the Azure AI Translator service.  You need to ensure that swear words and offensive words are removed from the translated text without replacement.  What should you do?

#### Notes
- Set the profanityAction parameter to Deleted.
(Use) You should set the *profanityAction parameter to Deleted*. Setting profanityAction to Deleted removes profanity, for example, swear words or offensive words, from the translation even if profane words are present in the source text. Other values accepted by the profanityAction parameter are NoAction and Marked. With NoAction, profane words are translated and passed through. With Marked, profane words may be replaced with asterisks or surrounded by profanity XML tags.

(Not) You should not set the includeAlignment parameter to true. With the includeAlignment parameter set to true, you receive alignment information that maps the positions of the words in the source and target texts.

(Not) You should not use a dynamic dictionary. A dynamic dictionary allows you to supply words or phrases as markup within your request if you want to apply a specific translation to your source text. It cannot be used to remove swear words from the translated text without replacement.

(Not) You should not use the notranslate tag. The notranslate tag allows you to tag content in your source text so that it can be passed to the target text without translation. Such content may include brand names or certain words and phrases which may lose their meaning if translated.

#### Reference
- [Profanity filtering - Translator - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/translator/profanity-filtering)
- [Word alignment - Translator - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/translator/word-alignment)
- [Dynamic Dictionary - Translator - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/translator/dynamic-dictionary)
- [Prevent content translation - Translator - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/translator/prevent-translation)


### AI Speech SDK-Deployment
You want to enable speech-to-speech translation in your app. You deploy a new Azure AI Speech service resource in your Azure subscription and install the Speech software development kit (SDK) for .Net on your computer.  You need to call the Azure AI Speech service using the Speech SDK.
Which class should you instantiate first?

#### Notes
- SpeechTranslationConfig

You should instantiate the *SpeechTranslationConfig* class first. SpeechTranslationConfig creates an instance of a speech translation configuration. You pass through its constructor’s parameters all the relevant access details of your Speech service such as your key, associated region, endpoint, host, or authorization token.

(Not) You should not instantiate the SpeechRecognizer class first. SpeechRecognizer can be used to transcribe into text the speech that arrives via the computer’s microphone, from an audio file, or from other audio input streams.

(Not) You should not instantiate the SpeechSynthesizer class first. SpeechSynthesizer can be used to synthesize speech and output it to the computer’s speakers, an audio file, or an audio stream.

(Not) You should not instantiate the TranslationRecognizer class first. TranslationRecognizer can be used to translate an input speech into a text or speech output. However, you should create an instance of the SpeechTranslationConfig class first before you can instantiate the TranslationRecognizer class.

#### Reference
- [Speech translation overview - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/speech-translation)
- [Speech translation quickstart - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/get-started-speech-translation?tabs=windows%2Cterminal&pivots=programming-language-csharp)
- [SpeechRecognizer Class (Microsoft.CognitiveServices.Speech) - Azure for .NET Developers | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/microsoft.cognitiveservices.speech.speechrecognizer?view=azure-dotnet)
- [SpeechSynthesizer Class (System.Speech.Synthesis) | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/system.speech.synthesis.speechsynthesizer?view=netframework-4.8)
- [TranslationRecognizer Class (Microsoft.CognitiveServices.Speech.Translation) - Azure for .NET Developers | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/microsoft.cognitiveservices.speech.translation.translationrecognizer?view=azure-dotnet)




### AI Speech service-SpeechToText
You test the speech-to-text translation functionality of the Azure AI Speech service.
You write the following method using the Speech .Net software development kit (SDK):

code
```bash
static async Task MySpeechToTextTranslator()
{
	var translationConfig =
		SpeechTranslationConfig.FromSubscription(KEY, REGION); 
	var language1 = "en-US";
	var language2 = new List<string> { "es", "pt" }; translationConfig.SpeechRecognitionLanguage = language1; language2.ForEach(translationConfig.AddTargetLanguage);
	
	using var recognizer = new TranslationRecognizer(translationConfig); 
	Console.Write("Waiting for your input speech");
	
	var result = await recognizer.RecognizeOnceAsync(); 
	if (result.Reason == ResultReason.TranslatedSpeech)
	{
		Console.WriteLine($"Recognized speech: "{result.Text}":"); 
		foreach (var (language, translation) in result.Translations)
		{
			Console.WriteLine($"In '{language}' it will be: {translation}")
		}
	}
}
```

Yes if the statement is true. Otherwise, select No.
#### Notes
(YES) Your method uses the default microphone input. If audio configuration is not provided when you instantiate translation recognizer as in your method example, then your instance uses the default microphone as an input channel. With the audio configuration, you may specify whether your recognizer should receive an input from a microphone, an audio file, or an audio stream.

(NO) Your method cannot recognize input speech and translate from Spanish and Portuguese. The SpeechRecognitionLanguage property of the SpeechTranslationConfig class is set to en-US. This means your recognizer is configured to recognize American English. Spanish and Portuguese are set as the target languages of translation.

(NO) Your method does not use continuous speech recognition and translation. To start continuous speech recognition and translation, you should use the StartContinuousRecognitionAsync method. In this scenario, the translation recognizer uses RecognizeOnceAsync as a single asynchronous speech translation operation.


#### Reference
- [Speech translation quickstart - Speech service - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/get-started-speech-translation?tabs=windows%2Cterminal&pivots=programming-language-csharp)
- [TranslationRecognizer Class (Microsoft.CognitiveServices.Speech.Translation) - Azure for .NET Developers | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/microsoft.cognitiveservices.speech.translation.translationrecognizer?view=azure-dotnet)



### AI Translation Service
Complete the API call.
You are developing an app that takes simplified Chinese text and converts it into English. The translated text must be transliterated into the Latin script.  How should you complete the API call? 

#### Notes
- from
- to
- toScript

The API call should be completed as follows:
```bash
https ://api.cognitive.microsofttranslator.com/translate?api-version=3.0&from=zh- hans&to=en&toScript=Latn
```
(Use) You should use the *from *parameter for the source language simplified Chinese, with language code zh-hans.

(Use) You should use the *to* parameter for the target language English, with language code en.

(Use) You should use the *toScript* parameter to require the translated text to be converted into the Latin script, Latn.

(Not) You should not use fromScript. Although you could specify that the script is in Chinese Simplified (Hans), this will be automatically detected.
#### Reference 
- [Translator Translate Method - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/translator/reference/v3-0-translate)
- [Language support - Translator - Azure AI services | Microsoft Learn](https://learn.microsoft.com/en-us/azure/ai-services/translator/language-support)


## Stopping Point --- QQ 85/130













































