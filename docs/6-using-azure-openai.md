![A picture of the Microsoft Logo](./media/graphics/microsoftlogo.png)

# Using Azure OpenAI Service

![A picture of the Azure OpenAI Service logo](./media/ch6/azureopenai.png)

## Azure OpenAI Service

Azure OpenAI Service provides REST API access to OpenAI's powerful language models including the GPT-4, GPT-4 Turbo with Vision, GPT-3.5-Turbo, and Embeddings model series. In addition, the new GPT-4 and GPT-3.5-Turbo model series have now reached general availability. These models can be easily adapted to your specific task including but not limited to content generation, summarization, image understanding, semantic search, and natural language to code translation. Users can access the service through REST APIs, Python SDK, or our web-based interface in the Azure OpenAI Studio.

Azure OpenAI Service is powered by a diverse set of models with different capabilities:


|Models	|Description|
--------|-----------|
|GPT-4 Turbo | The latest most capable Azure OpenAI models with multimodal versions which can accept both text and images as input.|
|GPT-4 | A set of models that improve on GPT-3.5 and can understand and generate natural language and code.|
|GPT-3.5 | A set of models that improve on GPT-3 and can understand and generate natural language and code.|
|Embeddings	| A set of models that can convert text into numerical vector form to facilitate text similarity.|
|DALL-E	| A series of models that can generate original images from natural language.|
|Whisper | A series of models in preview that can transcribe and translate speech to text.|
|Text to speech (Preview) |	A series of models in preview that can synthesize text to speech.|

**Table 1:** Azure OpenAI Models

TODO

Update messages/input with Adventure Works data
Change T-SQL format to example on bottom


## Azure OpenAI Embeddings

An embedding is a special format of data representation that machine learning models and algorithms can easily use. The embedding is an information dense representation of the semantic meaning of a piece of text. Each embedding is a vector of floating-point numbers, such that the distance between two embeddings in the vector space is correlated with semantic similarity between two inputs in the original format. For example, if two texts are similar, then their vector representations should also be similar.

1. Copy the following SQL and paste it into the SQL query editor.


    ```SQL
    declare @url nvarchar(4000) = N'https://build2024openai.openai.azure.com/openai/deployments/build2024-embeddings/embeddings?api-version=2024-02-01';
    declare @headers nvarchar(300) = N'{"api-key": "OPENAI_KEY"}';
    declare @message nvarchar(max);
    SET @message = (SELECT [Description]
                    FROM [SalesLT].[ProductDescription]
                    WHERE ProductDescriptionID = 457);
    declare @payload nvarchar(max) = N'{"input": "' + @message + '"}';

    declare @ret int, @response nvarchar(max);

    exec @ret = sp_invoke_external_rest_endpoint 
        @url = @url,
        @method = 'POST',
        @headers = @headers,
        @payload = @payload,
        @timeout = 230,
        @response = @response output;

    select @ret as ReturnCode, @response as Response;
    ```

1. Replace the **OPENAI_KEY** text with the AI Language Key that was returned to you in the previous chapter when testing connectivity.

1. Execute the SQL statement with the run button.

1. View the return message.

## Azure OpenAI DALL-E 3

The image generation API creates an image from a text prompt.

1. Copy the following SQL and paste it into the SQL query editor.

    ```SQL
    declare @url nvarchar(4000) = N'https://build2024openai.openai.azure.com/openai/deployments/build2024-dalle3/images/generations?api-version=2023-12-01-preview';
    declare @headers nvarchar(300) = N'{"api-key": "OPENAI_KEY"}';
    declare @message nvarchar(max);
    SET @message = (SELECT [Description]
                    FROM [SalesLT].[ProductDescription]
                    WHERE ProductDescriptionID = 457);
    declare @payload nvarchar(max) = N'{
        "prompt": "' + @message + '",
        "size": "1024x1024",
        "n": 1,
        "quality": "hd", 
        "style": "vivid"
    }';

    declare @ret int, @response nvarchar(max);

    exec @ret = sp_invoke_external_rest_endpoint 
        @url = @url,
        @method = 'POST',
        @headers = @headers,
        @payload = @payload,
        @timeout = 230,
        @response = @response output;

    select @ret as ReturnCode, @response as Response;
    ```

1. Replace the **OPENAI_KEY** text with the AI Language Key that was returned to you in the previous chapter when testing connectivity.

1. Execute the SQL statement with the run button.

1. View the return message.


```SQL
declare @url nvarchar(4000) = N'https://languagebuild2024.cognitiveservices.azure.com/language/:analyze-text?api-version=2023-04-01';
declare @headers nvarchar(300) = N'{"Ocp-Apim-Subscription-Key":"LANGUAGE_KEY"}';
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
    @response = @response output;

select @ret as ReturnCode, @response as Response;
```
