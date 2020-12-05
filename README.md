This application is simple example of creating an AWS lambda functions using aws java core library.

How to build - 
    `mvn clean package`

There are two ways to deploy this library - 


1.  Manual deployment
    1.  Login to AWS Console with credentials which has appropriate permissions.
    2.  Search for Lambda and go to lambda home page.
    3.  Create a new function of Java type.
    4.  Go to code and upload the jar file "awslambda-java-httpendpoint.jar" from target directory.
    5.  Edit our entry point and specify the Handler method with full class name. in this example "com.sourabh.aws.lambda.handleRequest".
    6.  In top panel click on test and create a test event which will trigger this lambda.
    7.  Click test now. We can see logs on the UI as well as in cloudwatch.
    
2.  Serverless framework
    1. Install npm server less framework by `npm install serverless -g`
    2. Now go to project root directory and run serverless deploy.
        1.  The serverless framework will read serverless.yml from root folder and create a cloud formation template.
        2.  It will upload the template and jar to one newly created s3 bucket.
        3.  Sample cloud formation template generated i this case has been attached in resource folder.
        4.  Next, It will create all resources based on this template.
     
    
    Notes -   
    1. To remove all resources created run command - `serverless remove`. I t will remove function, files, S3 bucket and everything created for tis project.
    2. Manual uploading of artifact has size limit of 10 MB, so if you have bigger artifact upload to s3 first and then use from there. 
    
    
    
    
Sample Output from serverless deploy
````
     serverless deploy
     Serverless: Deprecation warning: Starting with next major version, API Gateway naming will be changed from "{stage}-{service}" to "{service}-{stage}".
                 Set "provider.apiGateway.shouldStartNameWithService" to "true" to adapt to the new behavior now.
                 More Info: https://www.serverless.com/framework/docs/deprecations/#AWS_API_GATEWAY_NAME_STARTING_WITH_SERVICE
     Serverless: Packaging service...
     Serverless: Creating Stack...
     Serverless: Checking Stack create progress...
     ........
     Serverless: Stack create finished...
     Serverless: Uploading CloudFormation file to S3...
     Serverless: Uploading artifacts...
     Serverless: Uploading service awslambda-java-httpendpoint.jar file to S3 (2.17 MB)...
     Serverless: Validating template...
     Serverless: Updating Stack...
     Serverless: Checking Stack update progress...
     ..............................
     Serverless: Stack update finished...
     Service Information
     service: awslambda-java-httpendpoint
     stage: dev
     region: us-east-1
     stack: awslambda-java-httpendpoint-dev
     resources: 11
     api keys:
       None
     endpoints:
       GET - https://w6ybctx1cl.execute-api.us-east-1.amazonaws.com/dev/ping
     functions:
       currentTime: awslambda-java-httpendpoint-dev-currentTime
     layers:
       None
````

Sample output from serverless remove 
````
serverless remove
Serverless: Deprecation warning: Starting with next major version, API Gateway naming will be changed from "{stage}-{service}" to "{service}-{stage}".
            Set "provider.apiGateway.shouldStartNameWithService" to "true" to adapt to the new behavior now.
            More Info: https://www.serverless.com/framework/docs/deprecations/#AWS_API_GATEWAY_NAME_STARTING_WITH_SERVICE
Serverless: Getting all objects in S3 bucket...
Serverless: Removing objects in S3 bucket...
Serverless: Removing Stack...
Serverless: Checking Stack removal progress...
..............
Serverless: Stack removal finished...

Serverless: Stack removal finished...
````