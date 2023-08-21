Welcome to another AWS project. In this project, I will be creating a simple Create, read, update, and delete (CRUD) API. This project consists of:


DynamoDB: is a fully managed NoSQL database service that provides fast and predictable performance with seamless 
scalability. DynamoDB lets you offload the administrative burdens of operating and scaling a distributed database so
that you don't have to worry about hardware provisioning, setup, configuration, replication, software patching, 
or cluster scaling.

AWS Lambda: a compute service that lets you run code without provisioning or managing servers. Lambda runs your 
code only when needed and scales automatically, from a few requests per day to thousands per second. 

It's a simple project where we create a dynamo DB table and have our client/user send HTTP request via API-GW and the gateway routes the request to our lambda function where our lambda function interacts with our 
DynamoDB table and returns a response to our API-GW which then returns the response to our Client or User.

================================================================================================================================================================================================================
1. First step is to create a DynamoDB table. With the DynamoDB table, we can create a database that can store and retrieve
   any amount of data and serve any level of request traffic. Here, we will use a DynamoDB table to store data for our API.
   - visit https://us-east-1.console.aws.amazon.com/dynamodbv2/
   - create a table and name it "http-crud-tutorial-items".
   - partition key name should be "id".
   - leave everything at the default setting and click Create.
     
3. Second step is to create a lambda function. The lambda function creates, reads, updates, and deletes items from our table, the function uses events gotten from our HTTP API-GW to interact with our DynamoDB table.
   - create a function named "http-crud-tutorial-function" using the author from scratch.
   - The runtime should be "Node.js", the latest version.
   - under permission select "change execution role"
   - create a new role from the AWS policy template and name it "http-crud-tutorial-role".
   - For Policy templates, choose "Simple microservice permissions".
   - Create the function.
   - As soon as the function is created, input the source code into the editor on the index.js file
   
