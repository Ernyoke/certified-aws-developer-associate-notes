# Active Directory Services (AD)

## Microsoft Active Directory

- Software found on any Windows Server with AD Domain Services
- It is a database of objects: User, Account, Computers, Printers, File Shares, Security Groups
- Centralized security management
- Objects are organized in trees
- A group of trees is a forest

## AWS Directory Services

### AWS Managed Microsoft AD

- Allows to create our own AD in AWS, we can manage users locally, supports MFA
- We can establish *trust* connection with our on-premise AD

### AD Connector

- Direct Gateway (proxy) to redirect to on-premise AD
- Users are managed on the on-premise AD

### Simple AD

- AD-compatible managed directory on AWS
- Can not be joined with on-premise AD