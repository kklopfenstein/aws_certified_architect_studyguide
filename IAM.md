# IAM

## MFA devices
- Virtual MFA device
- Universal 2nd Factor (u2f) security key
- Hardware key fob MFA device
- Hardware key fob mfa device for AWS GovCloud

## IAM best practices
- don't use root account except for AWS account setup
- one physical user = One AWS user
- assign users to groups and assign permissions to groups
- create a strong password policy
- use and enforce MFA
- use and create roles for giving permissions to AWS services
- use access keys for programmatic access
- audit perm of account with IAM Credential report
- never share IAM users & access keys

## Summary

- users - mapped to phs user, has password for AWS console
- groups - contain users only
- policies - JSON document that outlines permissions for users or groups
- roles - for EC2 instances or AWS services
- security - MFA + Password Policy
- access keys - access AWS using CLI or SDK
- audit - IAM cred reports & IAM access advisor

