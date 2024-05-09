![A picture of the Microsoft Logo](./media/graphics/microsoftlogo.png)

# Using Azure OpenAI Service

![A picture of the Azure OpenAI Service logo](./media/ch6/azureopenai.png)

## Azure OpenAI Service

Azure OpenAI Service provides REST API access to OpenAI's powerful language models including the GPT-4, GPT-4 Turbo with Vision, GPT-3.5-Turbo, and Embeddings model series. In addition, the new GPT-4 and GPT-3.5-Turbo model series have now reached general availability. These models can be easily adapted to your specific task including but not limited to content generation, summarization, image understanding, semantic search, and natural language to code translation. Users can access the service through REST APIs, Python SDK, or our web-based interface in the Azure OpenAI Studio.

## Azure OpenAI Embeddings

```SQL
DECLARE @ret INT, @response NVARCHAR(MAX);

EXEC @ret = sp_invoke_external_rest_endpoint
    @url = N'https://build2024openai.openai.azure.com/openai/deployments/build2024-embeddings/embeddings?api-version=2024-02-01',
    @method = 'POST',
    @headers = '{"api-key": "8c28b25be2f54d28838fa7287c2d0bee"}',
    @payload = '{"input": "The food was delicious and the waiter"}',
    @timeout = 230,
    @response = @response OUTPUT;

SELECT @ret AS ReturnCode, @response AS Response;
```


## Azure OpenAI DALL-E 3

```SQL
DECLARE @ret INT, @response NVARCHAR(MAX);

EXEC @ret = sp_invoke_external_rest_endpoint
    @url = N'https://build2024openai.openai.azure.com/openai/deployments/build2024-dalle3/images/generations?api-version=2023-12-01-preview',
    @method = 'POST',
    @headers = '{"api-key": "8c28b25be2f54d28838fa7287c2d0bee"}',
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
