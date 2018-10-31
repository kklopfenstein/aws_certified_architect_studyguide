SWF - Simple Workflow Service
----------

What is SWF
  * Amazon Simple Workflow Service (Amazon SWF) is a web service that makes it easy to coordinate work across distributed application components. Amazon SWF enables applications for a rnage of use cases, including media processing, web application back-ends, business process workflows, and analytics pipelines, to be designed as a coordination of tasks.
  * Tasks represent involcations of various processing steps in an application which can be performed by executable code, web service calls, human actions, and scripts.

SWF Workers
  * Workers are programs that interact with Amazon SWF to get tasks, process received tasks, and return the results.
SWF Deciders
  * Decider is a program that controls the coordination of tasks, i.e. their ordering, concurrency, and scheduling according to the application logic.
* The workers and the decider can run on cloud infrastucture, such as Amazon EC2, or on machines behind firewalls. Amazon SWF brokers the interactions between workers and the decider. It allows the decider to get consistent views into the progress of tasks and to initiate new tasks in an ongoing manner.
* At the same time, Amazon SWF stores tasks, assigns them to workers when they are ready, and monitors their progress. It ensures that a task is assigned only once and is never duplicated. Since Amazon SWF maintains the application's state durably, workers and deciders don't have to keep track of execution state. They can run independently, and scale quickly.
  
* Your workflow and activity types and the workflow execution itself are all scoped to a domain. Domains isolate a set of types, executions, and task lists from others within the same account.
* You can register a domain by using the AWS Management Console or by using the RegisterDomain action in the Amazon SWF API.
* SWF Domains
  * Parameters are specified in JSON format.
    * E.g.
      ```
      https://swf.us-east-1.amazonaws.com
      RegisterDomain
      {
        "name":"867530901",
        "description":"music",
        "workflowExecutionRetentionPeriodInDays": "60"
      }
      ```
  * Maximum Workflow can be 1 year and the value is always measured in seconds.
* SWF vs SQS
  * SWF presents a task-oriented API, whereas SQS offers a message-oriented API.
  * Amazon SWF ensures a task is assigned only once and is never duplicated. With SQS, you need to handle duplicated messages and may also need to ensure that a message is processed only once.
  * Amazon SWF keeps track of all the tasks and events in an application. With Amazon SQS, you need to implement your own application-level tracking, especially if your application uses multiple queues.

