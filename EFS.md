EFS
----------

* Amazon Elastic File System is a file storage service for Amazon Elastic Compute Cloud (Amazon EC2) instances. Amazon EFS is easy to use and provides a simple interface that allows you to create and configure file systems quickly and easily. With Amazon EFS, storage capacity is elastic, growing and shrinking automaticaly as you add and remove files, so your applications have the storage they need, when they need it.
* Supports the Network File System version 4 (NFSv4) protocol
* You only pay for the storage you use (no pre-provisioning required)
* Can scale up to the petabytes
* Can support thousands of concurrent NFS connections
* Data is stored across multiple AZ's within a region
* EFS is block-based storage (vs Object based)
* Read After Write Consistency
* Use case: file server, centralized repository, multiple EC2 instances connecting to same NFS repo. Apply user-level, dir level permissions.
