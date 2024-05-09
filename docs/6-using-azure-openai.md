![A picture of the Microsoft Logo](./media/graphics/microsoftlogo.png)

# Using Azure OpenAI Service

![A picture of the Azure OpenAI Service logo](./media/ch6/azureopenai.png)

## Azure OpenAI Service

Azure OpenAI Service provides REST API access to OpenAI's powerful language models including the GPT-4, GPT-4 Turbo with Vision, GPT-3.5-Turbo, and Embeddings model series. In addition, the new GPT-4 and GPT-3.5-Turbo model series have now reached general availability. These models can be easily adapted to your specific task including but not limited to content generation, summarization, image understanding, semantic search, and natural language to code translation. Users can access the service through REST APIs, Python SDK, or our web-based interface in the Azure OpenAI Studio.

## Azure OpenAI Embeddings

1. Copy the following SQL and paste it into the SQL query editor.

```SQL
DECLARE @ret INT, @response NVARCHAR(MAX);

EXEC @ret = sp_invoke_external_rest_endpoint
    @url = N'https://build2024openai.openai.azure.com/openai/deployments/build2024-embeddings/embeddings?api-version=2024-02-01',
    @method = 'POST',
    @headers = '{"api-key": "OPENAI_KEY"}',
    @payload = '{"input": "The food was delicious and the waiter"}',
    @timeout = 230,
    @response = @response OUTPUT;

SELECT @ret AS ReturnCode, @response AS Response;
```
1. Replace the **OPENAI_KEY** text with the AI Language Key that was returned to you in the previous chapter when testing connectivity.

1. Execute the SQL statement with the run button.

1. View the return message.

## Azure OpenAI DALL-E 3

1. Copy the following SQL and paste it into the SQL query editor.

```SQL
DECLARE @ret INT, @response NVARCHAR(MAX);

EXEC @ret = sp_invoke_external_rest_endpoint
    @url = N'https://build2024openai.openai.azure.com/openai/deployments/build2024-dalle3/images/generations?api-version=2023-12-01-preview',
    @method = 'POST',
    @headers = '{"api-key": "OPENAI_KEY"}',
    @payload = '{
    "prompt": "An avocado chair",
    "size": "1024x1024",
    "n": 1,
    "quality": "hd", 
    "style": "vivid"
  }',
    @timeout = 230,
    @response = @response OUTPUT;

SELECT @ret AS ReturnCode, @response AS Response;
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
