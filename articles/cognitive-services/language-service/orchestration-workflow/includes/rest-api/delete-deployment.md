---
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: language-service
ms.topic: include
ms.date: 01/27/2022
ms.author: aahi
ms.custom: ignite-fall-2021
---


Create a **DELETE** request using the following URL, headers, and JSON body to delete a conversational language understanding deployment.


### Request URL

```rest
{ENDPOINT}/language/authoring/analyze-conversations/projects/{projectName}/deployments/{deploymentName}?api-version={API-VERSION}
```

|Placeholder  |Value  | Example |
|---------|---------|---------|
|`{ENDPOINT}`     | The endpoint for authenticating your API request.   | `https://<your-custom-subdomain>.cognitiveservices.azure.com` |
|`{PROJECT-NAME}`     | The name for your project. This value is case-sensitive.   | `myProject` |
|`{DEPLOYMENT-NAME}`     | The name for your deployment name. This value is case-sensitive.   | `staging` |
|`{API-VERSION}`     | The version of the API you are calling. The value referenced here is for the latest released [model version](../../../concepts/model-lifecycle.md#choose-the-model-version-used-on-your-data). | `2022-05-01` |

### Headers

Use the following header to authenticate your request. 

|Key|Value|
|--|--|
|`Ocp-Apim-Subscription-Key`| The key to your resource. Used for authenticating your API requests.|


Once you send your API request, you will receive a `202` response indicating success, which means your deployment has been deleted.
