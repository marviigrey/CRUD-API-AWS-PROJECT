Welcome to another AWS project. In this project, I will be creating a simple Create, read, update, and delete (CRUD) API. This project consists of:


DynamoDB: is a fully managed NoSQL database service that provides fast and predictable performance with seamless 
scalability. DynamoDB lets you offload the administrative burdens of operating and scaling a distributed database so
that you don't have to worry about hardware provisioning, setup, configuration, replication, software patching, 
or cluster scaling.

AWS Lambda: a compute service that lets you run code without provisioning or managing servers. Lambda runs your 
code only when needed and scales automatically, from a few requests per day to thousands per second. 

API-GATEWAY: a fully managed service that makes it easy for developers to publish, maintain, monitor, secure, and operate APIs at any scale.

Cloud9: he AWS Cloud9 IDE offers a rich code-editing experience with support for several programming languages and runtime debuggers, and a built-in terminal. It contains a collection of tools that you use to code, build, run, test, and debug software, and helps you release software to the cloud.

It's a simple project where we create a dynamo DB table and have our client/user send HTTP request via API-GW and the gateway routes the request to our lambda function where our lambda function interacts with our 
DynamoDB table and returns a response to our API-GW which then returns the response to our Client or User.

================================================================================================================================================================================================================
1. First step is to create a DynamoDB table. With the DynamoDB table, we can create a database that can store and retrieve
   any amount of data and serve any level of request traffic. Here, we will use a DynamoDB table to store data for our API.
   - visit https://us-east-1.console.aws.amazon.com/dynamodbv2/
   - create a table and name it "http-crud-tutorial-items".
   - partition key name should be "id".
   - leave everything at the default setting and click Create.
     
2. Second step is to create a lambda function. The lambda function creates, reads, updates, and deletes items from our table, the function uses events gotten from our HTTP API-GW to interact with our DynamoDB table.
   - create a function named "http-crud-tutorial-function" using the author from scratch.
   - The runtime should be "Node.js", the latest version.
   - under permission select "change execution role"
   - create a new role from the AWS policy template and name it "http-crud-tutorial-role".
   - For Policy templates, choose "Simple microservice permissions".
   - Create the function.
   - As soon as the function is created, input the ( https://github.com/marviigrey/CRUD-API-AWS-PROJECT/blob/main/lambda.js ) source code into the editor on the index.js file.
   - Deploy the code.

3. Third step is to create the HTTP API to send requests to our AWS Lambda function or to any publicly routable HTTP endpoint.
   - create HTTP API using HTTP API type named "http-crud-tutorial-api".
   - configure the routes which will be used to send incoming API requests to our backend resources such as Database.
   - configure for:
      Method - path.
      GET /items/{id}

      GET /items

      PUT /items

      DELETE /items/{id}
     
   - We input the methods and paths for every route we create, which will be four  routes.
   - Next up is creating integration that connects our routes to a backend solution or resources.
   - the integration type should be a lambda function and it should be the lambda we previously created "http-crud-tutorial-function".
   - attach the integration to the previously created routes.
  
4. We use AWS cloud9 to test our API:
   - We create an environment with the name API-workshop.
   - create any EC2 instance of your choice and use amazon Linux 2 AMI.
   - prepare the terminal in full screen.
   - test your API
   - copy the API invoke API URL link from the recently created API.
   - Paste this on your terminal 'export INVOKE_URL="https://**abcdef123**.execute-api.eu-west-1.amazonaws.com"'
   - create or update an item on your DB table: curl -X "PUT" -H "Content-Type: application/json" -d "{
    \"id\": \"abcdef234\",
    \"price\": 12345,
    \"name\": \"myitem\"
}" $INVOKE_URL/items

Lastly you can check your DB table via console or via cloud9 IDE to check for the recently added changes.

Here are some changes you can check via the cloud9 terminal:
- Use the following command to delete an item.
  
curl -X "DELETE" $INVOKE_URL/items/abcdef234

- Get all items to verify that the item was deleted.
  
curl -s $INVOKE_URL/items | js-beautify

That's it for this project, thank you for reading. 
MAKE SURE TO CLEAN UP ALL SERVICES USED IN THIS PROJECT TO AVOID BILLINGS.
