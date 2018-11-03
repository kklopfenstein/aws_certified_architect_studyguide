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
