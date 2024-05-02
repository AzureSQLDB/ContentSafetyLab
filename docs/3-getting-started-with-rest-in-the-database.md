# Getting started with REST in the Azure SQL Database


```SQL
DECLARE @ret INT, @response NVARCHAR(MAX);

EXEC @ret = sp_invoke_external_rest_endpoint
  @url = N'https://restmcrestface.azurewebsites.net/api/resttest',
  @method = 'GET',
  @headers = '{"Accept": "text/*"}',
  @payload = null,
  @timeout = 230,
  @response = @response OUTPUT;

SELECT @ret AS ReturnCode, @response AS Response;
```

