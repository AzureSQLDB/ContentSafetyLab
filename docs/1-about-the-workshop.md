![A picture of the Microsoft Logo](./media/graphics/microsoftlogo.png)

# About the AI Language and AI Content Safety Workshop
#### LAB331 Use Azure SQL DB and REST endpoints to enable AI content moderation

This lab will guide you through contacting REST endpoints for Azure AI Language, Azure OpenAI, and Azure AI Content Safety. The workshop utilizes the always free Azure SQL Database and the ability to call external REST endpoints via a system stored procedure ([sp_invoke_external_rest_endpoint](https://learn.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-invoke-external-rest-endpoint-transact-sql?view=azuresqldb-current&tabs=request-headers)).

The lab contains 5 chapters:
* Creating and connecting to your free Azure SQL Database
* Getting started with REST in the database
* Using the Azure AI Language REST endpoints
* Using the Azure AI Content Safety endpoints
* Using Azure OpenAI with your data
* Expanding your knowledge

The last chapter contains exercises you can work through on expanding on the REST endpoints. It covers creating stored procedures that encapsulate the REST call as well as using the native JSON functions of the Azure SQL Database to extract information from the response messages.

To get started with chapter 2, click [here](./2-create-azure-SQL-database.md)