Mega Quiz 2
----------

* Questions to view
  * Q: When you create new subnets within a custom VPC, by default they can communicate with each other, across availability zones. A: true
  * Q: It is possible to transfer a reserved instance from one Availability Zone to another. A: True
  * Q: In order to enable encryption at rest using EC2 and Elastic Block store you need to A: Configure encryption when creating the EBS Volume (review http://aws.amazon.com/about-aws/whats-new/2014/05/21/Amazon-EBS-encryption-now-available/)
  * Q: Amazon's Redshift uses which block size for its columnar storage? A: 1024KB / 1MB
  * Q: You are hosting a MySQL database on the root volume of an EC2 instance. The database is using a large amount of IOPS and you need to increase the IOPS available to it. What should you do? A: Add 4 additional EBS SSD volumes and create a RAID 10 using these volumes. (Review https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/raid-config.html)
  * Q: You work for a cosmetic company which has their production website on AWS. The site itself is in a two-tier configuration with web servers in the front end and database servers at the back end. The site uses using Elastic Load Balancing and Auto Scaling. The databases maintain consistency by replicating changes to each other as and when they occur. This requires the databases to have extremely low latency. Your website needs to be highly redundant and must be designed so that if one availability zone goes offline and Auto Scaling cannot launch new instances in the remaining Availability Zones the site will not go offline. How can the current architecture be enhanced to ensure this? A: (You require very low latency for synchronous replication, therefore doing anything across regions would be incorrect.) (In this scenario if you lost an availability zone, you would still have 2 other Availability Zones available each that is configured to handle only 33% peak load per zone. 33% + 33% = 66% peak load, so your application would fall over if your load exceeded 66%.) Deploy your site in three different AZ's within the same region. Configure the Auto Scaling minimum to handle 50 percent of the peak load per zone.
  * Q: You are a systems administrator and you need to monitor the health of your production environment. You decide to do this using Cloud Watch, however you notice that you cannot see the health of every important metric in the default dash board. Which of the following metrics do you need to design a custom cloud watch metric for, when monitoring the health of your EC2 instances? A: Memory usage
  * Q: You work for a toy company that has a busy online store. As you are approaching Christmas, you find that your store is getting more and more traffic. Your web tier is behind an Auto Scaling group, but you notice that is is frequently scaling, sometimes multiple times in an hour, only to scale back down after peak usage. You need to keep Auto Scaling from scaling up and down so rapidly. Which of the following options would help you to achieve this? A: Modify the Auto Scaling group cool-down timers & modify the Amazon CloudWatch alarm period that triggers your Auto Scaling scale down policy
  * Q: You work in the genomics industry and you process large amounts of genomic data using a nightly Elastic Map Reduce (EMR) job. This job processes a single 3 Tb file which is stored on S3. The EMR job runs on 3 on-demand core nodes and four on-demand task nodes. The EMR job is now taking longer than anticipated and you have been asked to advise how to reduced the completion time? A: You should reduce the input split zie in the MapReduce job configuration and then adjust the number of simultaneous mapper tasks so that more tasks can be processed at once.
  * Q: By definition a public subnet within a VPC is one that; A: In it's routing table it has at least one route that uses an Internet Gateway (IGW)
  * Q: You are a solutions architect working for a biotech company who is pioneering research in immunotherapy. They have developed a new cancer treatment that may be able to cure up to 94% of cancers. They store their research data on S3, however recently an intern accidentally deleted some critical files. You've been asked to prevent this from happening in the future. What options below can prevent this? A: Enable S3 versioning on the bucket & enable Enable Multifactor Authentication (MFA) on the bucket
  * Q: You are a solutions architect who has been asked to do some consulting for a US company that produces re-useable rocket parts. They have a new web application that needs to be built and this application must be stateless. Which three services could you use to achieve this? A: RDS, DynamoDB & Elasticache
  * Q: Your company has decided to set up a new AWS account for test and dev purposes. They already use AWS for production, but would like a new account dedicated for test and dev so as to not accidentally break the production environment. You launch an exact replica of your production environment using a cloudformation template that your company uses in production. However cloudformation fails. You use the exact same CloudFormation template in production so the failure is something to do with your new AWS account. The CloudFormation template is trying to launch 60 new EC2 instances in a single availability zone. After some research you discover that the problem is; A: For all new AWS accounts there is a soft limit of 20 EC2 instances per region. You should submit the limit increase form and retry the template after your limit has been increased.
  * Q: You work for a famous bakery who are deploying a hybrid cloud approach. Their legacy IBM AS400 servers will remain on premise within their own datacenter however they will need to be able to communicate to the AWS environment over a site to site VPN connection. What do you need to do to establish the VPN connection? A: Assign a public IP address to your Amazon VPC Gateway.
  * Q: You work for a construction company that has their production environment in AWS. The production environment consists of 3 identical web servers that are launched from a standard Amazon linux AMI using Auto Scaling. The web servers are launched in to the same public subnet and belong to the same security group. They also sit behind the same ELB. You decide to do some test and dev and you launch a 4th EC2 instance in to the same subnet and same security group. Annoyingly your 4th instance does not appear to have internet connectivity. What could be the cause of this? A: Remember that an EC2 instance in a public subnet is only publicly accessible if it has a public ip address or is behind an elastic load balancer. The correct answer is to assign an elastic IP address to the fourth instance. 