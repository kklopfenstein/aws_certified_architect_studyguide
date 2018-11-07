Additional Exam Tips
-----------

* Kinesis
  * Amazon Kinesis is a fully managed service for real-time processing of streaming data at massive scale. You can configure hundreds of thousands of data proucers to continuously put data into an Amazon Kinesis stream.
  * For example, data from website clickstreams, application logs, and social media feeds. Within less than a second, the data will be available for your Amazon Kinesis Applications to read and process from the stream.
  * Used to consume big data
  * Stream large amounts of social media, news feeds logs etc in to the cloud
  * Think Kinesis
  * Process large amounts of data:
    * Redshift for business intelligence
    * Elastic Map Reduce for Big Data Processing
* EC2 - EBS Backed vs Instance Store
  * EBS backed volumes are persistent
  * Instance Store backed volumes are not persistent (ephemeral)
  * EBS Volumes can be detached and reattached to other EC2 isntances
  * Instance store volume cannot be detached and reattached to other instances - they exist only for the life of that instance
  * EBS volumes can be stopped; data will persist
  * Instance store volumes cannot be stopped - if you do this data will be wiped
  * EBS Backed = Store Data Long Term
  * Instance Store = Shouldn't be used for long-term data storage
* OpsWorks
  * Orchestration Service that uses Chef
  * Chef consists of recipes to maintain a consistent state
  * Look for the term "chef" or "recipes" or "cook bookes" and think OpsWorks
* Elastic Transcoder
  * Media Transcoder in the cloud
  * Convert media files from their original source format in to different formats that will play on smartphones, tablets, PC's, etc
  * Provides transcoding presets for popular output formats, which means that you don't need to guess about which settings work best on particular devices
  * Pay based on the minutes that you transcode and the resolution at which you transcode
* SWF Actors
  * Workflow Starters - An application that can initiate (start) a workflow. Could be your e-commerce website when placing an order or a mobile app searching for bus times.
  * Deciders - Control the flow of activity tasks in a workflow execution. If something has finished in a workflow (or fails) a Decider decides what to do next.
  * Activity Workers - Carry out the activity tasks
* EC2 - Get Public IP Address
  * Need to query the instance metadata:
    * curl http://169.254.169.254/latest/meta-data/
    * wget http://169.254.169.254/latest/meta-data/
    * Key thing to remember is that it's an isntances META DATA, not user data
* AWS Organizations & Consolidated Billing
  * AWS Organizations is an account management service that enables you to consolidate multiple AWS accounts into an organization that you create and centrally manage.
  * Available in two feature sets:
    * Consolidated Billing
    * All Features
  * Consolidated Billing
    * Paying account is independent. Cannot access resources of other accounts.
    * All linked accounts are independent.
    * Currently a limit of 20 linked accounts for consolidated billing
  * Advantages
    * One bill per AWS account
    * Very easy to track charges and allocate costs
    * Volume pricing discount
  * Our Tes/Dev account uses 600 GB, Production uses 900 GB and Back Office uses 500 GB
  * Without consolidated billing we would pay
    * 600 x $0.03 = $18
    * 900 x $0.03 = $27
    * 500 x $0.03 = $15
    * Total bill = $60 for 2TB of storage.
  * With consolidated billins
    * 1TB x 0.03 = $30
    * Next 1TB x 0.0295 = $29.50
    * Total bill of $59.50
  * Best practices
    * Always enable multi-factor authentication on the root account
    * Always use a strong and complex password on the root account
    * Paying account should be used for billing purposes only. Do not deploy resources into a paying account.
  * Other things to note
    * Linked Accounts
      * 20 linked accounts
      * To add more visit https://aws-portal.amazon.com/gp/aws/html-forms-controller/contactus/aws-account-and-billing
    * Billing alerts
      * When monitoring is enabled on the paying account the biling data for all linked accounts is included.
      * You can still create billing alerts per individual account
    * Cloud trail
      * Per aws account and is enabled per region.
      * Can consolidate logs using an S3 bucket
        * 1. Turn on CloudTrail in the paying account
        * 2. Create a bucket policy that allows cross account access
        * 3. Turn on CloudTrail in the other accounts and use the bucket in the paying account
  * Exam Tips
    * Consolidated billing allows you to get volume discounts on all your accounts
    * Unused reserved instances for EC2 are applied across the group.
    * CloudTrail is on a per account and per region basis but can be aggregated in to a single bucket in the paying account.
* AWS Organizations
  * Functions
    * Centrally Manage Policies Across Multiple AWS Accounts
    * Control Access to AWS Services
    * Automate AWS Account Creation and Management
    * Consolidate Billing Across Multiple AWS Accounts
  * Central Management
    * AWS Organizations allows you to manage multiple AWS accounts at once. You can create groups of accounts, and then attach policies to a group to ensure the correct policies are applied across the accounts. Organizations enables you to centrally manage policies across multiple accounts, without requiring custom scripts and manual processes.
    * Control Access
      * With AWS Organizations, you can create Service Control Policies (SCPs) that centrally control AWS service use across multiple AWS accounts. You can specifically Allow or Deny individual AWS Services. For example you could deny the use of Kinesis or DynamoDB to your HR group within your AWS Organization. Even if IAM in that account allows it, SCP will override it.
    * Automate AWS Account Creation
      * You can use the AWS Organizations APIs to automate the creation and management of new AWS accounts. The Organizations APIs enable you to create new accounts programmatically, and to add the new accounts to a group. The policies attached to the group are automatically applied to the new account.
    * Consolidated Billing
      * AWS Organizations enables you to set up a single payment method for all the AWS accounts in your organization through consolidated billing. With consolidated billing, you can see a combined view of charges incurred by all your accounts, as well as take advantage of pricing benefits from aggregated usage, such as volume discounts for Amazon EC2 and Amazon S3.
      
* Cross Account Access?
  * Many AWS customers use separate AWS accounts for their development and production resources. This separation allows them to cleanly separate different types of resources and can also provide some security benefits.
  * Cross account access makes it easier for you to work productively within a multi-account (or multi-role) AWS Environment by making it easy for you to switch roles within the AWS Management Console. You can now sign in to the console using your IAM user name then switch the console to manage another account without having to enter (or remember) another use name and password.
  * Steps
    * Identify our account numbers
    * Create a group in IAM - Dev
    * Create a user in IAM - Dev
    * Log into production
    * Create a "read-write-app-bucket" policy
    * Create the "UpdateApp" cross account role
    * Apply the newly created policy to the role
    * Log in to the Developer Account
    * Create a new inline policy
    * Apply it to the Developer group
    * Login as John
    * Switch Accounts
* Tagging & Resource Groups
  * What are tags?
    * Key Value Pairs attached to AWS resources
    * Metadata (data about data)
    * Tags can sometime be inherited
      * Autoscaling, CloudFormation, and Elastic Beanstalk can create other resources
  * What are resource groups?
    * Resource groups make it easy to group your resources using the tags that are assigned to them. You can group resources that share one or more tags.
    * Resource groups contain information such as:
      * Region
      * Name
      * Health Checks
    * Specific information
      * For EC2 - Public & Private IP Addresses
      * For ELB - Port Configurations
      * For RDS - Database Engine etc
    * Types
      * Classic resource groups
      * AWS Systems Manager
        * Per region basis
        * Execute commands based on resource groups
  * Lab notes
    * Tags are case sensitive
    * Tag everything, you can create resource groups (classic or systems manager)
    * Classic resource groups across world or region, systems manager groups across region only
    * Systems manager groups give you a lot more control

* VPC Peering
  * VPC peering is a connection between two VPCs that enables you to route traffic between them using private IP addresses. Instances in either VPC can communicate with each other as if they are within the same network. You can create a VPC peering connection between your own VPCs, or with a VPC in another AWS account within a single region.
  * AWS uses the existing infrastucture of a VPC to create a VPC peering connection; it is neither a gateway nor a VPN connection, and does not rely on a separate piece of physical hardware. There is no single point of failure for communication or bandwidth bottleneck.
  * Can't overlap CIDR block.
  * Transitive peering is not supported.
  * Can't peer VPC's in different regions.

* Direct Connect
  * makes it easy to establish a dedicated network connection from your premises to AWS. Using AWS direct connect, you can establish private connectivity between AWS and your datacenter, office,m or colocation environment, which in many cases can reduce your network costs, increase bandwidth throughput, and provide a more consistent network experience than Internet-based connections.
  * Reduce costs when using large volumes of traffic
  * Increase reliability
  * Increase bandwidth
  * VPN Connections can be configured in minutes and are a good solution if you have an immediate need, have low to modest bandwidth requirements, and can tolerate the inherent variability in Internet-based connectivity
  * AWS Direct Connect does not involve the Internet; instead, it uses dedicated, private network connections between your intranet and Amazon VPC
  * Availble in 10Gbps, 1Gbps, Sub 1 Gbps can be purchased through AWS Direct Connect Partners
  * Uses Ethernet VLAN trunking (802.1Q)

* Security Token Service (STS)
  * Grants users limited and temporary access to AWS resources. Users can come from three sources:
    * Federation (typically Active Directory)
      * Uses Security Assertion Markup Language (SAML)
      * Grants temporary access based off the users Active Directory credentials. Does not need to be a user in IAM.
      * Single sign on allows users to log in to AWS console without assigning IAM credentials
      * Federation with Mobile Apps
        * Use Facebook/Amazon/Google or other OpenID providers to log in
      * Cross Account Access
        * Let's users from one AWS account access resources in another
  * Understanding the key terms
    * Federation
      * Combining or joining a list of users in one domain (such as IAM) with a list of users in another domain (such as Active Directory, Facebook, etc)
    * Identity Broker
      * A service that allows you to take an identity from point A to join it (federate it) to point B
    * Identity store
      * Services like Active Directory, Facebook, Google etc.
    * Identities
      * A user of a service like Facebook etc
  * Scenario
    * You are hosting a company website on some EC2 web servers in your VPC. Users of the website must log in to the site which then authenticates against the companies active directory servers which are based on site at the companies head quarters.
    * Your VPC is connected to your company HQ via a secure IPSEC VPN. Once logged in the users can only have access to their own S3 bucket. How do you set this up?
    * 4 values - access key, secret access key, token, duration (1-36hrs)
    * View image: https://imgur.com/a/Ou3nMcI
    * Scenario
      * Employee enters their username and password
      * The application calls an Identity Broker. The broker captures the username and password.
      * The Identity Broker uses the organization's LDAP directory to validate the employee's identity.
      * The Identity Broker calls the new GetFederationToken function using IAM credentials. The call must include an IAM policy and a duration (1 to 36 hours), along with a policy that specifies the permissions to be granted to the temporary security credentials.
      * The Security Token Service confirms that the policy of the IAM user making the call to the GetFederationToken gives permission to create new tokens and then returns four values to the application: An access key, a secret access key, a token, and a duration (the token's lifetime)
    
      * The Identity Broker returns the temporary security credentials to the reporting application
      * The data storage application uses the temporary security credentials (including the token) to make requests to Amazon S3
      * Amazon S3 uses IAM to verify that the credentials allow the requested operation on the given S3 bucket and key
      * IAM provides S3 with the go-ahead to perform the requested operation
    * Exam
      * Develop an Identity Broker to communicate with LDAP and AWS STS.
      * Identity broker always auth with LDAP first, then AWS STS
      * App gets temporary access to AWS resources

* Active Directory Integration
  * https://imgur.com/a/QViJRM3
  * You can authenticate with active directory using SAML.
  * You authenticate to active directory first, receive a temporary security credential.

* Workspaces
  * Basically a VDI. A WorkSpace is a cloud-based replacement for a traditional desktop. A WorkSpace is available as a bundle of compute resources, storage space, and software application access that allow a user to perform day-to-day tasks just like using a traditional desktop. A user can connect to a WorkSpace from any supported device (PC, Mac, Chromebook, iPad, Kindle Fire, or Android tablets) using a free Amazon WorkSpaces client application and credentials set up by an administrator, or their existing Active Directory credentials if Amazon WorkSpaces is integrated with an existing Active Directory domain.
  * Windows 7 Experience, provided by Windows Server 2008 R2.
  * By default, users can personalize their WorkSpaces with their WorkSpaces with their favorite settings for items such as wallpaper, icons, shortcuts, etc. This can be locked down by an administrator however.
  * By default you will be given local admin access, so you can install your own applications
  * Workspaces are presistent
  * All data on D:\ is backed up every 12 hours
  * You do not need an AWS account to login to workspaces

* ECS Part 1 - What is Docker
  * Docker
    * Docker is a software platform that allows you to build, test, and deploy applications quickly.
    * Docker is highly reliable: you can quickly deploy and scale applications into any environment and know your code will run.
    * Docker is infinitely scalable: Running Docker on AWS is a great way to run distributed applications at any scale.
    * Docker packages software into standardized units called Containers:
      * Containers allow you to easily package an application's code, configurations, and dependencies into easy to use building blocks that deliver environmental consistency, operational efficiency, developer productivity, and version control.
    * Virtualization vs containerisation
      * Traditional Virtual Machine
    * Containerization Benefits
      * Escape from dependency hell
      * Consistent progression from DEV -> TEST -> QA -> PROD
      * Isolation - performance or stability issues with App A in container A, won't impact App B in Container B.
      * Much better resource management
      * Extreme code portability
      * Micro-Services
    * Docker Components
      * Docker image
      * Docker container
      * Layers / Union File System
      * DockerFile
      * Docker Daemon / Engine
      * Docker Client
      * Docker Registries / Docker Hub
  * ECS
    * Amazon EC2 Container Service (Amazon ECS) is a highly scalable, fast, container management service that makes it easy to run, stop, and manage Docker containres on a cluster of EC2 instances. Amazon ECS lets you launch and stop container-based applications with a simple API calls, allows you to get the state of your cluster of a centralized service, and gives you access to many familiar Amazon EC2 features.
    * ECS is a Regional service that you can use in one or more AZs accross a new, or existing, VPC to schedule the placement of containers across your cluster based on your resource needs, isolation policies, and availability requirements.
    * Amazon ECS eliminates the need for you to operate your own cluster management and configuration management systems, or to worry about scaling your management infrastructure.
    * ECS can also be used to create a consistent deployment and build experience, manage and scale batch ETL workloads, and build sophisticated application architectures on a microservices model.

  * Containers
    * Containers are a method of operating system virtualization that allow you to run an application and its dependencies in resource-isolated processes.
    * Containers have everything the software needs to run - including libraries, system tools, code, and runtime.
    * Containers are created from a read-only template called an Image.
  * What's a Docker Image?
    * An Image is a read-only template with instructions for creating a Docker container. It contains:
      * an ordered collection of root filesystem changes and the corresponding execution parameters for use within a container runtime
    * An Image is created from a Dockerfile, a plain text file that specifies the components taht are to be included in the container.
    * Images are stored in a Registry, such as DockerHub or AWS ECR.
  * ECR
    * Amazon EC2 Container Registry (Amazon ECR) is a managed AWS Docker registry service that is secure, scalable, and reliable. Amazon ECR supports private Docker repositories with resource-based permissions using AWS IAM so that specific users or Amazon EC2 instances can access repositories and images. Developers can use the Docker CLI to push, pull, and manage images.
    * A Task Definition is required to run Docker containers in Amazon ECS.
    * Task Definitions are text files in JSON format that describe one or more containers that form your application.
    * Some of the parameters you can specify in a task definitions include:
      * Which Docker images to use with the containers in your task
      * How much CPU and memory to use with each container
      * Whether containers are linked together in a task
    * The docker networking mode to use for the containers in your task
    * What (if any) ports from the container are mapped to the host container instance
    * Whether the task should continue to run if the container finishes or fails
    * The command the container should run when it is started
    * What (if any) environment variables should be passed to the container when it starts
    * Any data volumes that should be used with the containers in the task
    * What (if any) IAM role your tasks should use for permissions
    * An amazon ECS service allows you to run and maintain a specified number (or, the "desired count") of instances of a task definition simultaneously in an ECS cluster.
    * Think of services like Auto-Scaling groups for ECS.
    * If a task should fail or stop, the Amazon ECS service scheduler launches another instance of your task definition and replace it and maintain the desired count of tasks in the service.
  * ECS Clusters
    * An Amazon ECS cluster is a logical grouping of container instances that you can place tasks on. When you first use the Amazon ECS service, a default cluster is created for you, but you can create multiple clusters in an account to keep your resources separate.
    * Concepts:
      * Clusters can contain multiple different container instance types.
      * Clusters are region-specific
      * Container instances can only be part of one cluster at a time.
      * You can create IAM policies for your clusters to allow or restrict users' access to specific clusters
    * Service scheduler:
      * Ensures that the specified number of tasks are constantly running and reschedules tasks when a task fails (for example, if the underlying container instanece fails for some reason)
      * Can ensure tasks are registered against an ELB.
    * Custom Scheduler
      * You can create your own schedulers that meet your business needs.
      * Leverage third-party schedulers, such as Blox.
    * The Amazon ECS schedulers leverage the same cluster state information provided by the Amazon ECS API to make appropriate placement decisions.
  * ECS Container Agent
    * The Amazon ECS container agent allows container instances to connect to your cluster. The Amazon ECS container agent is included in the Amazon ECS-optimized AMI, but you can also install it on any EC2 instance that supports the Amazon ECS specification. The Amazon ECS container agent is only supported on EC2 instances.
    * Pre-installed on special ECS AMIs.
    * Linux-based:
      * Works with Amazon Linux, Ubuntu, Red Hat, CentOS, etc
      * Will not work with Windows
  * ECS Security
    * IAM Roles:
      * EC2 instances use an IAM role to access ECS.
      * ECS tasks use an IAM role to access services and resources.
    * Security Groups attach at the instance-level (i.e. the host.. not the task or container)
    * You can access and configure the OS of the EC2 instances in your ECS cluster.
  * Soft Limits
    * Clusters per region (default = 1000)
    * Instances per Cluster (default = 1000)
    * Services per Cluster ( default = 500)
  * Hard Limits
    * One Load Balancer per Service
    * 1000 Tasks per Service (the "desired count")
    * Max. 10 Containers per Task Definition
    * Max. 10 Tasks per instance (host)
  * ECS Exam Tips
    * ECS - Amazon's managed EC2 container service. Allows you to manage docker containers on a cluster of EC2 instances.
    * Containres are a method of operating system virtualization that allow you to run an application and its dependencies in resource-isolated processes.
    * Containers are create from a read-only template called an Image.
    * An Image is a read-only template with instructions for creating a Docker container.
    * Images are stored in a Registry, such as DockerHub or AWS ECR.
    * Amazon EC2 Container Registry (Amazon ECR) is a managed AWS Docker registry service
    * A task definition is required to run docker containers in Amazon ECS
    * Task definitions are text files in a JSON format that describe one or more containers that form your application.
    * Think of a task definition as a cloud formation template but for docker. Configure things such as the amount of CPU, RAM etc
    * An Amazon ECS service allows you to run and maintain a specified number (or, the "desired count") of instances of a task definition simultaneously in an ECS cluster
    * Think of Services like Auto-Scaling groups for ECS
    * An amazon ecs cluster is a logical grouping of container instances that you can place tasks on
    * Clusters can contain multiple different container instance types.
    * Clusters are region-specific
    * Container instances can only be part of one cluster at a time
    * You can create IAM policies for your clusters to allow or restrict users access to specific clusters
    * You can schedule ECS in two ways
      * Service scheduler
      * Custom scheduler
    * ECS agent to connect EC2 instances to your ECS cluster. LINUX ONLY
    * IAM with ECS to restrict access
    * Security groups operate at the instance level, not at the task or container level.
