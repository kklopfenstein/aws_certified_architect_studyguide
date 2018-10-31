VPC
----------

* VPC overview
  * VPC: virtual datacenter in the cloud
  * Amazon Virtual Private Cloud (Amazon VPC) lets you provision a logically isolated section of the Amazon Web Services (AWS) Cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including selection of your own IP address range, creation of subnets, and configuration of route tables and network gateways.
  * You can easily customize the network configuration for your Amazon Virtual Private Cloud. For example, you can create a public-facing subnet for your webservers that has access to the Internet, and palce your backend systems such as databases or application servers in a private-facing subnet with no Internet access. You can leverage multiple layers of security, including security groups and network access control lists, to help control access to Amazon EC2 instances in each subnet.
  * Additionally, you can create a Hardware Virtual Private Network (VPN) connection between your corporate datacenter and your VPC and leverage the AWS cloud as an extension of your corporate datacenter.
  * 1 subnet = 1 AZ
  * What can you do with a VPC?
    * Launch instances into a subnet of your choosing
    * Assign custom IP address ranges in each subnet
    * Configure internet gateway and attach it to our VPC
    * Much better security control over your AWS resources - network ACL's to block specific ip addresses
    * Instance security groups - can span AZ's
    * Subnet network access control lists (ACLS) 
  * Default VPC vs Custom VPC
    * Default VPC is user friendly, allowing you to immediately deploy instances.
    * All Subnets in default VPC have a route out to the internet.
    * Each EC2 instance has both a public and private IP address.
  * VPC Peering
    * Allow you to connect one VPC with another via a direct network route using private IP addresses.
    * Instances behave as if they were on the same private network
    * You can peer VPC's with other AWS accounts as well as other VPCs in the same account.
    * Peering is in a star configuration: ie 1 central VPC peers with 4 others. NO TRANSITIVE PEERING
    * Exam Tips
      * Think of a VPC as a logical datacenter in AWS.
      * Consists of IGWs (Or Virtual Private Gateways), Route Tables, Network Access Control Lists, Subnets, and Security Groups
      * 1 Subnet = 1  AZ
      * Security Groups are Stateful; Network Access Control Lists are Stateless
        * With security groups you can open up port 80 and incoming and outgoing traffic will work
        * With NAC's you have to open 80 for inbound and outbound separately
      * NO TRANSITIVE PEERING
  * VPC Building Lab Notes
    * https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html#VPC_Sizing - see reserved IP addresses in each subnet
    * You can only attach 1 internet gateway to a VPC
    * `::/0` - all IPv6 IPs
    * by default when you create a subnet it won't auto-assign public ip addresses
    * security groups don't span VPNs
  * NAT lab
    * NAT instance
      * NAT instance must be able to send/receive traffic when the source or destination is not itself. By default each EC2 instance performs source/destination checks by default. You must disable source/destination checks on the NAT instance.
      * Must be a route out of the private subnet to the NAT instance, in order for this to work.
      * The amount of traffic that NAT instances can support depends on the instance size. If you are bottlenecking, increase the instance size.
      * You can create high availability using Autoscaling Groups, multiple subnets in different AZ's, and a script to automate failover.
      * Behind a security Group.
    * NAT gateway
      * Preferred by the enterprise
      * Scale automatically up to 10Gbps
      * No need to patch
      * Not associated with security groups
      * Automatically assigned a public ip address
      * Remember to update you route tables.
      * No need to disable Source/Destination checks
      * More secure than a NAT instance
      * Egress Only Internet Gateway - IPv6 only
    * need NAT gateway in each AZ
  * Network Access Control Lists vs Security Groups
    * You can only associate a subnet to one ACL
    * When you create an ACL inbound/outbound is deny for all
    * ACL changes are instantaneous
    * Your VPC automatically comes with a default network ACL, and by default it allows all outbound and inbound traffic.
    * You can create custom network ACLs. By default, each custom network ACL denies all inbound and outbound traffic until you add rules.
    * Each subnet in your VPC must be associated with a network ACL. If you don't explicitly associate a subnet with a network ACL, the subnet is automatically associated with the default network ACL.
    * You can associate a network ACL with multiple subnets; however, a subnet can be associated with only one network ACL at a time. When you associate a network ACL with a subnet, the previous association is removed.
    * Network ACLs contain a numbered list of rules that is evaluated in order, starting with the lowest numbered rule.
    * Network ACLs have separate inbound and outbound rules, and each rules can either allow or deny traffic.
    * Network ACLs are stateless; responses to allowed inbound traffic are subject to the ruels for outbound traffic (and vice versa)
    * Block IP addresses using network ACLs not Security Groups
  * Load Balancers and Custom VPC's
    * You need to have your LB in two public subnets. So you'll need at least two public subnets in your VPC.
  * VPC Flow Logs
    * VPC Flow Logs is a feature that enables you to capture information about the IP traffic going to and from network interface in your VPC. Flow log data is stored using Amazon CloudWatch Logs. After you've created a flow log, you can view and retrieve its data in Amazon CloudWatch Logs.
    * Flow logs can be created at 3 levels:
      * VPC
      * Subnet
      * Network interface level
    * You cannot enable flow logs for VPCs that are peered with your VPC unless the peer VPC is in your account.
    * You cannot tag a flow log.
    * After you've created a flow log, you cannot change its configuration; for example, you can't associate a different IAM role with the flow log.
    * Not all IP traffic is monitored:
      * Traffic generated by instances when they contact the Amazon DNS server. If you use your own DNS server, then all traffic to that DNS server is logged
      * Traffic generated by a Windows instance for Amazon Windows license activation
      * Traffic to and from 169.254.169.254 for instance metadata.
      * DHCP traffic
      * Traffic to the reserved IP address for the default VPC router
  * NAT vs Bastion
    * Bastions need to be highly available
      * bastion in each subnet
      * autoscaling groups
      * route 53 health checks
    * Exam tips
      * A NAT is used to provide internet traffic to EC2 instances in private subnets
      * A bastion is used to securely administer EC2 instances (using SSH or RDP) in private subnets. In Austrailia we call them jump boxes.
  * VPC End Points
    * Two types
      * Gateway - Highly available
      * Interface -  
    * VPC End Points are used to make AWS services available without needing public network access from your EC2 instance
  * Quiz 
    * Allowed 5 VPC's by default 
