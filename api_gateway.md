API Gateway
-----------

* What is API Gateway?
  * Fully managed service that makes it easy for developers to publish, maintain, monitor, and secure APIs at any scale. With a few clicks in the AWS Management Console, you can create an API that acts as a "front door" for applications to access data, business logic, or functionality from your back-end services, such as applications running on Amazon Elastic Compute Cloud (EC2), code running on AWS Lambda, or any web application.
  * You can enable API caching in Amazon API Gateway to cache your endpoint's response. With caching, you can reduce the number of calls made to your endpoint and also improve the latency of the requests to your API. When you enable caching for a stage, API Gateway caches responses from your endpoint for a specified time-to-live (TTL) period, in seconds. API Gateway then responds to the request by looking up the endpoint reponse from the cache instead of making the request to your endpoint.
  * Low cost and Efficient
  * Scales Effortlessly
  * You can Throttle Requests to prevent attacks
  * Connect to Cloudwatch to log all requests
* Same Origin Policy
  * In computing, the same-origin policy is an important concept in the web app security model. Under the policy, a web browser permits the scripts contained in a first web page to access data in a second web page, but only if both web pages have the same origin.
* Cross-Origin Resource Sharing (CORS)
  * CORS is one way the server at the other end (not the client code in the browser) can relax the same-origin policy.
  * Cross-origin resource sharing (CORS) is a mechanism that allows restricted resources (e.g. fonts) on a web page to be requested from another domain outside the domain from which the first resource was served.
  * Error - "Origin policy cannot be read at the remote resource?" . You need to enable CORS on API Gateway.

