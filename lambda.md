Lambda
----------

* Lambda launched in 2015
* Lambda encapsulates
  * Data Centres
  * Hardware
  * Assembly Code/Protocols 
  * High Level Languages
  * Operating Systems
  * Application Layer/AWS APIs
  * AWS Lambda
* Upload code, create lambda function
* AWS takes care of provisioning and maintaining the servers that run the code
* No need to worry about OS, patching, scaling etc
* Using lambda:
  * Event driving compute service. AWS lambda runs code in response to events. Could be changes to data in S3, Dynamo DB.
  * Compute service to run code in response to HTTP request using API Gateway or API calls made using AWS SDKs.
* scales out automatically
* available runtimes
  * C#/Powershell
  * Go
  * Java 8
  * Node.js (4.3,6.10,8.10)
  * Python (2.7,3.6)
* understand core types of lambda triggers
  * API Gateway
  * AWS IoT
  * Alexa Skills Kit
  * Alexa Smart Home
  * CloudFront
  * CloudWatch Events
  * CloudWatch Logs
  * CodeCommit
  * Cognito Sync Trigger
  * DynamoDB
  * Kinesis
  * S3
  * SNS
* Pricing
  * num of requests
    * first 1 mill/month(?) requests are free. $0.20 per million req thereafter.
    * Duration
      * calculated from the time code starts executing util it returns or otherwise terminates, rounded up to the nearest 100ms.
      * price depends on the amount of memory you allocate to your function. You are charged $0.00001667 for every GB-second used.
* Note on duration: **function cannot exceed 5 min duration**
* Exam tips
  * Lambda scales out (not up) automatically
  * Lambda functions are independent, 1 event = 1 function
  * Lambda is serverless
  * Know what services are serverless!
    * S3/API Gateway/Lambda/DynamoDB - serverless
    * EC2 - not serverless
  * Lambda functions can trigger other lambda functions, 1 event can = x functions if functions trigger other functions
  * Architectures can get extremely complicated, AWS X-ray allows you to debug what is happening
  * Lambda can do things globally... you can use it to back up S3 buckets to other S3 buckets, etc
  * Know triggers (see above)
