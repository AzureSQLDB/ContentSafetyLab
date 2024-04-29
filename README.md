# ContentSafetyLab

### Outline
1) First 5-10 minutes will be an overview of what they will be doing today
      2-5 slides on the components such as Azure SQL, OpenAI components, etc

2) 45 Minutes will be the lab itself. Depending on how much content we want, we can have most of the components created with ARM templates I believe.
Here is the exercise proposed flow:

Azure SQL Database
      DB Creation (this could be up for debate on if we want students to create or not)
      DB connection
            Add IP to Firewall
            Connection string in azure portal
            Choose client: Query editor or ADS

Azure OpenAI REST endpoints and coponents
     AI Language
          Students will use the code template in the GitHub repository to call the following AI Language endpoints              
Identify PII
Extract Key Phrases
Analyze sentiment and opinions
Answer questions (with SQL Data)
Using adventureworks data, set session context and ask questions
     Content Safety
Next, the students will call content safety endpoints
      Moderate Text content
      Evaluate prompts for prompt jailbreaking
Translation
Using the translation REST endpoints is next. Students will use the adventure works product descriptors
      Pass the product descriptions to have them translated
      Use JSON functions to extract the exact test back from the payload
Maps
Maps/Weather Endpoints
      Get the weather for a Lat/Long we supply
      Using the same lat/long, call the timezone endpoint to get sunrise/set information
DALL-E 3
Image Creation
      Using a DALL-E 3 endpoint, create images from product descriptions using the adventure works data for a mock        marketing campaign

3) Leave 5 minutes for questions
