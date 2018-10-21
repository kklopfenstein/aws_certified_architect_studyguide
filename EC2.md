EC2
-------------

* [EC2 Placement Groups](EC2_placement_groups.md)
* [EFS](EFS.md)
* [Lambda](lambda.md)

Study tips:
* Know the differences between
  * On Demand - pay by sec or hour
  * Spot - set bid price, if spot price == bid price your instances will be provision, if spot price > bid price your instances will be terminated,
    * if instances terminated within 1hr period you won't be charged for that hour, if you terminate then you will be charged
  * Reserved - reserve capacity, contracts run 12mo-36mo, more you pay up front, bigger discount
  * Dedicated hosts - for licensing reasons, not allowed to use shared hardware
  * Instance types - knowing instance families is a good idea
    * **F1** - Field Programmable Gate Array - Genomic research, financial analytics, real time video processing, big data, etc
    * **I3** - High Speed Storage - NoSQL DBs, Data Warehousing etc
    * **G3** - Graphics Intensive - Video Encoding/3D Application Streaming
    * **H1** - High Disk Throughput - MapReduce-based workloads, distributed file systems such as HDFS and MapR-FS
    * **T2** - Lowest Cost, General Purpose - Web Servers/Small DBs
    * **D2** - Dense Storage - Fileservers/Data Warehousing/Hadoop
    * **R4** - Memory Optimized - Memory Intensive Apps/DBs
    * **M5** - General Purpose - Application Servers
    * **C5** - Compute Optimized - CPU Intensive Apps/DBs
    * **P3** - Graphics/General Purpose GPU - Machine Learning, Bit Coin Mining etc
    * **X1** - Memory Optimized - SAP HANA/Apache Spark etc
  * Remembering trick - edward norton fighting a scottish duck FIGHT DR MCPX
    * F for FPGA
    * I for IOPS
    * G - Graphics
    * H - High Disk Throughput
    * T - cheap general purpose (think T2 Micro)
    * D - for density
    * R for RAM
    * M - main choice for general purpose apps
    * C - for Compute
    * P - Graphics (think Pics)
    * X - Extreme memory
  * EBS Consists of:
    * SSD, General Purpose - GP2 - (Up to 10,000 IOPS)
    * SSD, Provisioned IOPS - IO1 - (More than 10,000 IOPS)
    * HDD, Throughput Optimized - ST1 - frequently accessed workloads
    * HDD, Cold - SC1 - less frequently accessed data.
    * **Note: boot volumes can only be SSD (GP1, IO1), or HDD, Magnetic standard**
    * HDD, Magnetic - Standard - cheap, infrequently access storage
    * **Note: You cannot mount 1 EBS volume to multiple Ec2 instances; instead use EFS**
  * EC2 Lab Exam Tips
    * Termination Protection is turned off by default, you must turn it on.
    * On an EBS-backed instance, the default action is for the root EBS volume to be deleted when the instance is terminated.
    * EBS-backed Root volumes can now be encrypted using AWS API or console, or you can use a third party tool (such as bit locker etc) to encrypt the root volume.
    * Additional volumes can be encrypted
  * Volumes vs Snapshots
    * Volumes exist on EBS:
      * Virtual Hard Disk
    * Snapshots exist on S3.
    * You can take a snapshot of a volume, this will store that volume on S3.
    * Snapshots are point in time copies of Volumes.
    * Snapshots are incremental. This means that only the blocks that have changed since your last snapshot ar emoved to S3.
    * If this is your first snapshot, it may take some time to create.
  * Volumes vs Snapshots - Security
    * Snapshots of encrypted volumes are encrypted automatically.
    * Volumes restored from encrypted snapshots are encrypted automatically.
    * You can share snapshots, but only if they are unencrypted.
      * These snapshots can be shared with other AWS accounts or made public, but only if unencrypted.
  * Snapshots of Root Device Volumes
    * To create a snapshot for Amazon EBS volumes that serve as root devices, you should stop the instance before taking the snapshot.
  * EBS vs Instance Store - Exam Tips
    * Instance Store Volumes are sometimes called Ephemeral Storage.
    * Instance store volumes cannot be stopped. If the underlying host fails, you will lose your data.
    * EBS backed instances can be stopped. You will not lose the data on this instance if it is stopped.
    * You can reboot both, you will not lose your data.
    * By default, both ROOT bolumes will be deleted on termination. However, with EBS volumes, you can tell AWS to keep the root device volume.
  * How can you take a SNAPSHOT of RAID array
    * Problem - Take a snapshot, the snapshot excludes data held in the cache by applications and the OS. This tends not to matter on a single volume. Howveer, using multiple volumes in a RAID array, this can be a problem due to interdependencies of the array.
    * Solution - Take an application consistent snapshot.
      * Stop the app from writing to disk
      * flush all caches to the disk
      * how can we do this?
        * freeze the file system
        * unmount the raid array
        * shutting down the associated EC2 instance
  * Amazon Machine Images - Exam Tip
    * AMIs are regional. You can only launch an AMI from the regions in which it is stored. However, you can copy AMIs to other regions using the console, command line, or the Amazon EC2 API.
  * Exam tips
    * Standard Monitoring - 5 minutes
    * Detailed monitoring - 1 minute (costs extra)
    * CloudWatch is for performance monitoring
    * CloudTrail is for auditing
  * What can you do with CloudWatch
    * Dashboard - CloudWatch creates dashboards to see what is happening with your AWS environment.
    * Alwarms - Allows you to set Alarms that notify you when particular thresholds are hit.
    * Events - CloudWatch Events helps you to respond to state changes in your AWS resources.
    * Logs - CloudWatch Logs helps you to aggregate, monitor, and store logs
  * Roles Lab
    * Roles are more secure then storing your access key and secret access key on individual EC2 instances.
    * Roles are easier to manage.
    * Roles can be assigned to an EC2 instance AFTER it has been provisioned using both the command line and the AWS console.
    * Roles are universal - you can use them in any region.
  * Instance Meta-data
    * Used to get information about an instance (such as public ip)
    * curl http://169.254.169.254/latest/meta-data/
    * curl http://169.254.169.254/latest/user-data/
    * anything to do with the actual instance itself will be in `meta-data`
  * EFS Features
    * Supports the Network File System version 4 (NFSv4) protocol
    * You only pay for the storage you use (no pre-provisioning required.)
    * Can scale up to the petabytes
    * Can support thousands of concurrent NFS connections
    * Data is stored accross multiple AZs within a region.
    * Read After Write Consistency
  * What is Lambda
    * AWS Lambda is a compute service whree you can upload your coe and create a Lambda function. AWS Lambda takes care of provisioning and managing the servers that you use to run the code. You don't have to worry about OS, patching, scaling, etc. You can use Lambda in the following ways:
      * As an event-driven compute service where AWS Lambda runs your code in response to events. These events could be changes to data in an Amazon S3 bucket, or an Amazon DynamoDB table.
      * As a copute service to run your code in response to HTTP requests using Amazon API Gateway or API calls made using AWS SDKs. This is what we sue at A Cloud Guru.
  * What is a Placement Group?
    * Two Types of Placement Groups:
      * Clustered Placement Group - 1 AZ
      * Spread Placement Group - important EC2 instances, want them on separate hardware



