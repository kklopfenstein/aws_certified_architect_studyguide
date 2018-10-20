EC2 Placement Groups
----------

* General
  * **Name you specify for a placement group must be unique within your AWS account.**
  * **Only certain types of instances can be launched in a placement group (Compute Optimized, GPU, Memory Optimized, Storage Optimized)**
  * **AWS recommend homogenous instances within placement groups.**
  * **You can't merge placement groups**
  * **You can't move an existing instance into a placement group. You can create an AMI from your existing instance and then launch a new instance frmo the AMI into a placement group.**

* Clustered Placement Group
  * **Grouping of instances within a single AZ**
  * Apps that need low network latency, high network throughput, or both.
  * Only certain instances can be launched into Clustered Placement Group.
  * On exam, generaly Clustered Placement Groups will be referred to

* Spread Placement Group (Re:invent 2017)
  * Instances that are placed on distinct underlying hardware.
  * Used for apps that need small number of critical instances that need to be separate.
  * **Spread placement group can span multiple AZ's**



