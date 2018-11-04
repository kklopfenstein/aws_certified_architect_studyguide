Well Architected Framework
----------

What is a well architected framework?

* This has been developed by the Solutions Architecture team based on their experience with helping AWS customers. The well architected framework is a set of questions that you can use to evaluate how well your architecture is aligned to AWS best practices.

5 Pillars of the Well-Architected Framework

* Security
* Reliability
* Performance Efficiency
* Cost Optimization
* Operational Excellence

Structure of each pillar

* Design principles
* Definition
* Best practices
* Key AWS Services
* Resources


General Design Principles
* Stop guessing your capacity needs
* Test systems at production scale.
* Automate to make architectural experimentation easier.
* Allow for evolutionary architectures
* Data-Driven architectures
* Improve through game days

Pillar 1: Security
---------

Design Principles
* Apply security at all layers
* Enable traceability
* Automate responses to security events
* Focus on securing your system
* Automate security best practices
* AWS Shared Responsibility Model
  * https://d0.awsstatic.com/logos/compliance/shared_responsibility.jpg

Definition
* Security in the cloud consists of 4 areas:
  * Data protection
  * Privilege management
  * Infrastructure protection
  * Detective controls

Best Practices - Data protection
* Before you begin to architect security practices across your environment, basic data classification should be in place. You should oragnize and classify your data in to segments such as publicly available, available to only members of your organization, available to only certain members of your organization, available only to the board etc. You should also implement a least privilege access system so that people are only able to access what they need. However most importantly, you should encrypt everything where possible, whether it be at rest or in transit.
* In AWS the following practices help protect your data:
  * AWS customers maintain full control over their data.
  * AWS makes it easier for you to encrypt your data and manage keys, including regular key rotation, which can be easily automated natively by AWS or maintained by a customer.
  * Detailed logging is available that contains important content, such as file access and changes.
  * AWS has designed storage systems for exception resiliency. As an example, Amazon Simple Storage Serviec (S3) is designed for 11 nines durability. (For example, if you store 10,000 objects with Amazon S3, you can on average expect to incur a loss of a single object once every 10,000,000 years.)
  * Versioning, which can be part of a larger data lifecycle-management process, can protect against accidental overwrites, deletes , and similar harm.
  * AWS never initiates the movement of data between regions. Content placed in a region will remain in that region unless the customer explicitly enable a feature or leverages a service that provides functionality.

Best Practices - Data Protection Questions
* How are you encrypting and protecting your data at rest?
* How are you encrypting and protection your data in transit? (SSL)

Best Practicse - Privilege Management
* Privilege Management ensures that only authorized and authenticated users are able to access your resources, and only in a manner that is intended. In can include
  * Access Control Lists (ACLs)
  * Role Based Access Controls
  * Password Management (such as password rotation policies)

Best Practices - Privilege Management Questions
* How are you protecting access to and use of the AWS root account credentials?
* How are you defining roles and responsibilities of system users to control human access to the AWS Management Console and APIs?
* How are you limiting automated access (such as from applications, scripts, or third-party tools or services) to AWS resources?
* How are managing keys and credentials?

Best Practices - Inrastructure Protection
* Outside of Cloud, this is how you protect your data centre. RFID controls, security, lockable cabinets, CCTV etc. Within AWS they handle this, so really Infrastucture protection exists at a VPC level.

Best Practices - Infrastructure Protection Questions
* How are you enforcing network and host-level boundary protection?
* How are you enforcing network and  AWS service level protection?
* How are you protecting the integrity of the operating systems on your Amazon EC2 instances?

Best Practices - Detective Controls
* You can use detective controls to detect or identify a security breach.
* AWS services to achieve this include:
  * AWS CloudTrail
  * Amazon CloudWatch
  * AWS Config
  * Amazon Simple Storage Service (S3)
  * Amazon Glacier

Best Practices - Detective Control Questions
* How are you capturing and analyzing AWS logs?

Key AWS Services
* Data protection
  * You can encrypt your data both in transit and at rest using: ELB, EBS, S3 & RDS
* Privilege management
  * IAM, MFA
  * Infrastucture protection
    * VPC
      * AWS Cloud Trail, AWS Config, Amazon Cloud Watch

Well Architected Framework - Pillar Two Reliablity

* The reliability pillar covers the ability of a seystem to recover from service or infrastructure outages/disruptions as well as the ability to dynamically aquire computing resources to meet demand.

Design Principles
* Test recovery procedures
* Automatically recover from failure
* Scale horizontally to increase aggregate system availability
* Stop guessing capacity

Best Practices - Foundations
* Before building a house, you always make sure that the foundations are in place before you lay the first brick. Similarly before architecting any system, you need to make sure you have the prerequisite foundations. In traditional IT one of the first things you should consider is the size of the comms link between your HQ and your datacenter. If you misprovision this link, it can take 3 - 6 months to upgrade which can cause a huge disruption to your traditional IT estate.
* With AWS, they handle most of the foundations for you. The cloud is designed to be essentially limitless meaning that AWS handle the networking and compute requirements themselves. However, they do set service limits to stop customers from accidentally over-provisioning resources.

Best Practices - Foundation Questions
* How are you managing AWS service limits for your account?
* How are you planning your network topology with AWS?
* Do you have an escalation path to deal with technical issues?
* With AWS things are a lot easier, you can use CloudWatch to monitor your environment and services such as autoscaling to automate change in response to changes on your production environment.

Best Practices - Change Management Questions
* How does your system adapt to changes in demand?
* How are you monitoring AWS resourcse?
* How are you executing change management?

Best Practices - Failure Management
* WIth cloud you should always architect your systems with the assumptions that failure will occur. You should become aware of these failures, how they occurred, how to respond to them and then plan on how to prevent these from happening again.

Best Practices - Failure Management Questions
* How are you backing up your data?
* How does your system withstand component failures?
* How are you planning for recovery?

Key AWS Services
* Foundations
  * IAM, VPC
* Change Management
  * AWS CloudTrail
* Failure Management
  * AWS CloudFormation

Well Architected Framework - Performance Efficiency

* The Performance Efficiency pillar focuses on how to use computing resources efficiently to meet your requirements and how to maintain that efficiency as demand changes and technology evolves.

Design Principles
* Democratize advanced technologies.
* Go global in minutes
* Use server-less architectures
* Experiment more often

Definition
* Performance Efficiency in the cloud consists of 4 areas:
  * Compute
  * Storage
  * Database
  * Space time tradeoff
* Best practicse - Compute
  * When architecting your system it is important to choose the right kind of server. Some applications require heavy CPU utilization, some require heavy memory utilization etc.
  * With AWS servers are virtualized and at the click of a button (or API call) you can change the type of server in which your environment is running on. You can even switch to running with no servres at all and use AWS Lambda.
  * At A Cloud Guru, this is how we have designed our environment. If you are watching this video on our platform right now, you are interacting with Lambda in a server less fashion.

Best Practices - Compute Questions
* How do you select the appropriate instance type for your system?
* How do you ensure that you continue to have the most appropriate instance type as nwe instance types and features are introduced?
* How do you monitor your instances post launch to enusre they are performing as expected?
* How do you ensure that the quantity of your instances matches demand?

Best Practices - Storage
* The optimal storage solutions for your environment depends on a number of factors. For example:
  * Access method - Block, File or Object
  * Patterns of Access - Random or Sequential
  * Throughput Required
  * Frequency of Access - Online, Offline or Archival
  * Frequency of Update - Worm, Dynamic
  * Availability Constraints
  * Durability Constraints

  * With AWS the storage is virtualized. With S3 you can have 11 x9's durability, Cross Region Replication etc. With EBS you can choose between different storage mediums (such as SSD, Magnetic, PIOPS etc). You can also easily move volumes between the different types of storage mediums.

  * How do you select the appropriate storage solution for your system?
  * How do ensure that you continue to have th emost appropriate storage solution as the new storage solutions and features are launched?
  * How do you monitor your storage solution to ensure it is performing as expected?
  * How do you ensure that the capacity and throughput of your storage solutions matches demand?

Best Practices - Databases
  * The optimal database solution depends on a number of factors. Do you need database consistency, do you need high avilability, do you need No-SQL, do you need DR etc?
  * With AWS you get a LOT of options. RDS, DynamoDB, Redshift etc.

Best Practices - Database Questions
* How do you select the appropriate database solution for your system?
* Hwo do you ensure that you continue to have the most appropriate database solution and features as new database solution and features are launched?
* How do you monitor your databases to ensure performance is as expected?
* How do you ensure the capacity and throughput of your databases matches demand?

Best Practices - Space-Time trade-off
* Using AWS you can use services such as RDS to add read replicas, reducing the load on your database and creating multiple copies of your database. This helps to lower latency.
* You can use Direct Connect to provide predictable latency between your HQ and AWS.
* You can use the global infrastucture to have multiple copies of your environment, in regions that is closest to your customer base.
* You can also use caching services such as ElastiCache or CloudFront to reduce latency

Best Practices - Space-Time trade-off questions
* How do you select the appropriate proximity and caching solutions for your system
* How do you ensure that you continue to have the most appropriate proximity and caching solutions as new solutions are launched?
* How do you monitor your proximity and caching solutions to ensure performance is as expected?
* How do you ensure that the proximity and caching solutions you have matches demand?

Key AWS Services
* Compute
  * Autoscaling
* Storage
  * EBS, S3, Glacier
* Database
  * RDS, DynamoDB, Redshift
* Space-Time Trade-Off
  * CloudFront, ElastiCache, Direct Connect, RDS Read Replicas etc
