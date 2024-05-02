# Using the Azure AI Language Service

## PII and Redaction

```SQL
declare @url nvarchar(4000) = N'https://languagebuild2024.cognitiveservices.azure.com/language/:analyze-text?api-version=2023-04-01';
declare @headers nvarchar(300) = N'{"Ocp-Apim-Subscription-Key":"xxxxxxxx"}';
declare @payload nvarchar(max) = N'{
    "kind": "PiiEntityRecognition",
    "analysisInput":
    {
        "documents":
        [
            {
                "id":"1",
                "language": "en",
                "text": "abcdef@abcd.com, this is my phone is 6657789887, and my IP: 255.255.255.255 127.0.0.1 fluffybunny@bunny.net, My Addresses are 1 Microsoft Way, Redmond, WA 98052, SSN 543-55-6654, 123 zoo street chickenhouse, AZ 55664"
            }
        ]
    }
}';

declare @ret int, @response nvarchar(max);

exec @ret = sp_invoke_external_rest_endpoint 
	@url = @url,
	@method = 'POST',
	@headers = @headers,
	@payload = @payload,
    @timeout = 230,
--	@credential = [https://motherbrain.cognitiveservices.azure.com],
	@response = @response output;

select @ret as ReturnCode, @response as Response;

SELECT A.[value] as "Redacted Text"
FROM OPENJSON(@response,'$.result.results.documents') AS D
CROSS APPLY OPENJSON([value]) as A
where A.[key] = 'redactedText'

select JSON_VALUE(B.[value],'$.category') as "PII Category",
JSON_VALUE(B.[value],'$.text') as "PII Value",
CONVERT(FLOAT,JSON_VALUE(B.[value],'$.confidenceScore'))*100 as "Confidence Score"
from OPENJSON(
(
    SELECT A.[value] --D.[key] as "PII Type", JSON_VALUE(A.[value],'$.Text') as "PII Value"
FROM OPENJSON(@response,'$.result.results.documents') AS D
CROSS APPLY OPENJSON([value]
) AS A 
where A.[key] = 'entities'
), '$') AS B

GO
```

### Answer Questions

```SQL
declare @url nvarchar(4000) = N'https://languagebuild2024.cognitiveservices.azure.com/language/:query-text?api-version=2023-04-01';
declare @headers nvarchar(300) = N'{"Ocp-Apim-Subscription-Key":"xxxxxxx"}';
declare @payload nvarchar(max) = N'{
  "question": "how long it takes to charge surface?",
  "records": [
    {
      "id": "1",
      "text": "Power and charging. It takes two to four hours to charge the Surface Pro 4 battery fully from an empty state. It can take longer if you’re using your Surface for power-intensive activities like gaming or video streaming while you’re charging it."
    },
    {
      "id": "2",
      "text": "You can use the USB port on your Surface Pro 4 power supply to charge other devices, like a phone, while your Surface charges. The USB port on the power supply is only for charging, not for data transfer. If you want to use a USB device, plug it into the USB port on your Surface."
    }
  ],
  "language": "en"
}';

declare @ret int, @response nvarchar(max);

exec @ret = sp_invoke_external_rest_endpoint 
	@url = @url,
	@method = 'POST',
	@headers = @headers,
	@payload = @payload,
    @timeout = 230,
--	@credential = [https://motherbrain.cognitiveservices.azure.com],
	@response = @response output;

select @ret as ReturnCode, @response as Response;
```


### Document summarization

```SQL
declare @url nvarchar(4000) = N'https://languagebuild2024.cognitiveservices.azure.com/language/analyze-text/jobs?api-version=2023-04-01';
declare @headers nvarchar(300) = N'{"Ocp-Apim-Subscription-Key":"xxxxxxx"}';
declare @payload nvarchar(max) = N'{
  "displayName": "Document ext Summarization Task Example",
  "analysisInput": {
    "documents": [
      {
        "id": "1",
        "language": "en",
        "text": "At Microsoft, we have been on a quest to advance AI beyond existing techniques, by taking a more holistic, human-centric approach to learning and understanding. As Chief Technology Officer of Azure AI services, I have been working with a team of amazing scientists and engineers to turn this quest into a reality. In my role, I enjoy a unique perspective in viewing the relationship among three attributes of human cognition: monolingual text (X), audio or visual sensory signals, (Y) and multilingual (Z). At the intersection of all three, there’s magic—what we call XYZ-code as illustrated in Figure 1—a joint representation to create more powerful AI that can speak, hear, see, and understand humans better. We believe XYZ-code will enable us to fulfill our long-term vision: cross-domain transfer learning, spanning modalities and languages. The goal is to have pre-trained models that can jointly learn representations to support a broad range of downstream AI tasks, much in the way humans do today. Over the past five years, we have achieved human performance on benchmarks in conversational speech recognition, machine translation, conversational question answering, machine reading comprehension, and image captioning. These five breakthroughs provided us with strong signals toward our more ambitious aspiration to produce a leap in AI capabilities, achieving multi-sensory and multilingual learning that is closer in line with how humans learn and understand. I believe the joint XYZ-code is a foundational component of this aspiration, if grounded with external knowledge sources in the downstream AI tasks."
      }
    ]
  },
  "tasks": [
    {
      "kind": "ExtractiveSummarization",
      "taskName": "Document Extractive Summarization Task 1",
      "parameters": {
        "sentenceCount": 6
      }
    }
  ]
}';

declare @ret int, @response nvarchar(max);

exec @ret = sp_invoke_external_rest_endpoint 
	@url = @url,
	@method = 'POST',
	@headers = @headers,
	@payload = @payload,
    @timeout = 230,
--	@credential = [https://motherbrain.cognitiveservices.azure.com],
	@response = @response output;

select @ret as ReturnCode, @response as Response;
```

```SQL
declare @url nvarchar(4000) = N'https://languagebuild2024.cognitiveservices.azure.com/language/analyze-text/jobs/000000000?api-version=2023-04-01';
declare @headers nvarchar(300) = N'{"Ocp-Apim-Subscription-Key":"xxxx"}';
declare @ret int, @response nvarchar(max);

exec @ret = sp_invoke_external_rest_endpoint 
	@url = @url,
	@method = 'GET',
	@headers = @headers,
	--@payload = @payload,
    @timeout = 230,
--	@credential = [https://motherbrain.cognitiveservices.azure.com],
	@response = @response output;

select @ret as ReturnCode, @response as Response;
```

### Sentiment analysis

```SQL
declare @url nvarchar(4000) = N'https://languagebuild2024.cognitiveservices.azure.com/language/:analyze-text?api-version=2023-04-01';
declare @headers nvarchar(300) = N'{"Ocp-Apim-Subscription-Key":"xxxxx"}';
declare @payload nvarchar(max) = N'{
	"kind": "SentimentAnalysis",
	"parameters": {
		"modelVersion": "latest",
		"opinionMining": "True"
	},
	"analysisInput":{
		"documents":[
			{
				"id":"1",
				"language":"en",
				"text": "The food and service were unacceptable. The concierge was nice, however."
			}
		]
	}
} ';

declare @ret int, @response nvarchar(max);

exec @ret = sp_invoke_external_rest_endpoint 
	@url = @url,
	@method = 'POST',
	@headers = @headers,
	@payload = @payload,
    @timeout = 230,
--	@credential = [https://motherbrain.cognitiveservices.azure.com],
	@response = @response output;

select @ret as ReturnCode, @response as Response;
```

### Language detection

```SQL
declare @url nvarchar(4000) = N'https://languagebuild2024.cognitiveservices.azure.com/language/:analyze-text?api-version=2023-04-01';
declare @headers nvarchar(300) = N'{"Ocp-Apim-Subscription-Key":"XXXX"}';
declare @payload nvarchar(max) = N'{
    "kind": "LanguageDetection",
    "parameters": {
        "modelVersion": "latest"
    },
    "analysisInput":{
        "documents":[
            {
                "id":"1",
                "text": "This is a document written in English."
            }
        ]
    }
}';

declare @ret int, @response nvarchar(max);

exec @ret = sp_invoke_external_rest_endpoint 
	@url = @url,
	@method = 'POST',
	@headers = @headers,
	@payload = @payload,
    @timeout = 230,
--	@credential = [https://motherbrain.cognitiveservices.azure.com],
	@response = @response output;

select @ret as ReturnCode, @response as Response;
```

### Named Entity Recognition (NER)

```SQL
declare @url nvarchar(4000) = N'https://languagebuild2024.cognitiveservices.azure.com/language/:analyze-text?api-version=2023-04-01';
declare @headers nvarchar(300) = N'{"Ocp-Apim-Subscription-Key":"XXXX"}';
declare @payload nvarchar(max) = N'{
    "kind": "EntityRecognition",
    "parameters": {
        "modelVersion": "latest"
    },
    "analysisInput":{
        "documents":[
            {
                "id":"1",
                "language": "en",
                "text": "I had a wonderful trip to Seattle last week."
            }
        ]
    }
}';

declare @ret int, @response nvarchar(max);

exec @ret = sp_invoke_external_rest_endpoint 
	@url = @url,
	@method = 'POST',
	@headers = @headers,
	@payload = @payload,
    @timeout = 230,
--	@credential = [https://motherbrain.cognitiveservices.azure.com],
	@response = @response output;

select @ret as ReturnCode, @response as Response;
```

### Entity Linking

```SQL
declare @url nvarchar(4000) = N'https://languagebuild2024.cognitiveservices.azure.com/language/:analyze-text?api-version=2023-04-01';
declare @headers nvarchar(300) = N'{"Ocp-Apim-Subscription-Key":"XXXX"}';
declare @payload nvarchar(max) = N'{
    "kind": "EntityLinking",
    "parameters": {
        "modelVersion": "latest"
    },
    "analysisInput":{
        "documents":[
            {
                "id":"1",
                "language":"en",
                "text": "Microsoft was founded by Bill Gates and Paul Allen on April 4, 1975."
            }
        ]
    }
}';

declare @ret int, @response nvarchar(max);

exec @ret = sp_invoke_external_rest_endpoint 
	@url = @url,
	@method = 'POST',
	@headers = @headers,
	@payload = @payload,
    @timeout = 230,
--	@credential = [https://motherbrain.cognitiveservices.azure.com],
	@response = @response output;

select @ret as ReturnCode, @response as Response;
```