- The Amazon Elastic File System (EFS) is the only storage solution in the list that provides a file system interface. It also supports millions of files as requested.
- EFS uses NFS (Network File System) protocol and FsX uses SMB (Server Message Block) protocol.
- EFS and FsX both are file system not block.
---
## A Solutions Architect needs to design a solution for providing a shared file system for company users in the AWS Cloud. The solution must be fault tolerant and should integrate with the company’s Microsoft Active Directory for access control. Which storage solution meets these requirements?
### ANS -
- Create a file system with Amazon FSx for Windows File Server and enable Multi-AZ. Join Amazon FSx to Active Directory.
- ** "Create an Amazon EFS file system and configure AWS Single Sign-On with Active Directory" is incorrect. You cannot configure AWS SSO for an EFS file system with Active Directory.**
