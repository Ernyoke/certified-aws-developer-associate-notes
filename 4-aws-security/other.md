# CloudWatch Logs - Encryption

- We can encrypt CloudWatch logs with KMS keys
- Encryption is enabled at the log group level by associating a CMK with a log group. This can be done when a group is created of afterwards
- We can not associate a CMK with a log group using the CloudWatch console, we must use the CloudWatch Logs API:
    - **associate-kms-key**: if the log group exists
    - **create-log-group**: if the log group does not exist yet

# CodeBuild Security

- To access resources in our VPC, we have to make sure we provide a VPC configuration to CodeBuild
- We should not store secrets in plaintext in env. variables
- Instead...
    - We can use env. variables which can reference parameter store parameters
    - We can use env. variables which can references secret manager secrets