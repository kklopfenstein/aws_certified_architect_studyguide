SQS
----------

* What is SQS?
  * SQS is a web service that gives you access to a message queue that can be used to store messages while waiting for a computer to process them.
  * Amazon SQS is a distributed queue system that enables web service applications to quickly and reliably queue messages that one component in the application generates to be consumed by another component. A queue is a temporary repository for messages that are awaiting processing.
  * SQS is a pull based system, not a push based system.
  * Using Amazon SQS, you can decouple the components of an application so they run independently, easing message management between components.
  * Any component of a distributed application can store messages in the queue. Messages can contain up to 256 KB of text in any format. Any component can later retrieve the messages programmatically using the Amazon SQS API.
  * The queue acts as a buffer between the component producing and saving data, and the component receiving the data for processing. This means the queue resolves issues that arise if the producer is producing work faster than the consumer can process it, or if the producer or consumer are only intermittently connected to the network.
* Types of queues
  * Standard queue
    * Standard default queue type. A standard queue lets you have a nearly-unlimited number of transactions per second. Standard queues guarantee that a message is delivered at least once. However, occasionally ( because of the highly-distributed architecture that allows high throughput), more than one copy of a message might be delivered out of order. Standard queues provide best-effort ordering which ensures that messages are generally delivered in the same order as they are sent.
  * FIFO Queues
    * The FIFO queue complements the standard queue. The most important features of this queue type are FIFO (first-in-first-out) delivery and exactly-once processing: The order in which messages are sent and received is strictly preserved and a message is delivered once and remains available until a consumer processes and deletes it; duplicates are not introduced into the queue. FIFO queues also support message groups that allow multiple ordered message groups within a single queue. FIFO queues are limited to 300 transactions per second (TPS), but have all the capabilities of standard queues.
* SQS Key Facts
  * SQS is pull-based, not pushed-based.
  * Messages are 256 KB in size
  * Messages can be kept in the queue from 1 minute to 14 days
  * Default retention period is 4 days
  * SQS guarantees that your messages will be processes at least once.
* SQS Visibility Timeout
  * The Visibility Timeout is the amount of time that the message is invisible in the SQS queue after a reader picks up that message. Provided the job is processes before the visibility time out expires, the message will then be deleted from the queue. If the job is not processes within that time, the message will become visible again and another reader will process it. This could result in the same message being delivered twice.
  * Default Visibility Timeout is 30 seconds
  * Increase it if your task takes >30 seconds
  * Maximum is 12 hours
  * SQS is pull-based, not pushed-based
  * Messages are 256 KB in size
  * Message can be kept in the queue from 1 minute to 14 days
  * Defult retention period is 4 days
  * SQS guarantees that your messages will be processed at least once.
* Short polling - returned immediately if no messages are in the queue
* SQS Long Polling
  * SQS long polling is a way to retrieve messages from your Amazon SQS queues.
  * While the regular short polling returns immediately (even if the message queue being polled is empty), long polling doesn't return a response until a message arrives in the message queue, or the long poll times out.
  * As such, long polling can save you money.
  


