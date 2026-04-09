# Active Directory IAM RBAC Lab

## Objective
Build an Identity and Access Management lab in Active Directory to implement role-based access control using security groups, department-based users, and group-based folder permissions.

## Lab Environment
- **Domain Controller:** Windows Server 2025
- **Client System:** Windows client VM
- **Domain:** `terrylab.local`
- **Virtualization Platform:** VirtualBox

## Skills Demonstrated
- Identity and Access Management
- Role-Based Access Control (RBAC)
- Least privilege
- Active Directory administration
- Organizational Unit (OU) design
- Security group management
- NTFS and share permissions
- Identity lifecycle administration

## Project Overview
This lab simulates how organizations manage access based on job role rather than assigning permissions directly to individual users. Users were created by department, assigned to role-based security groups, and granted access to shared resources through group membership.

## Environment Setup

### Organizational Units Created
- HR
- IT
- Security
- Finance

### Users Created
- `hr.user1`
- `it.user1`
- `sec.user1`
- `fin.user1`

### Security Groups Created
- `HR Access`
- `IT Support Access`
- `Security Access`
- `Finance Access`

## Access Model
Permissions were assigned to **security groups**, not directly to user accounts.

Examples:
- `hr.user1` → `HR Access`
- `it.user1` → `IT Support Access`
- `sec.user1` → `Security Access`
- `fin.user1` → `Finance Access`

This allowed access to be managed centrally through group membership and supports least-privilege administration.

## Protected Resources
The following folders were created on the domain controller:

- `C:\Shares\HR`
- `C:\Shares\IT`
- `C:\Shares\Security`
- `C:\Shares\Finance`

Each folder was shared and secured with role-based permissions.

## Permission Design
For each department folder:
- `Administrators` → Full Control
- `SYSTEM` → Full Control
- `CREATOR OWNER` → Full Control
- Matching department access group → Modify

Examples:
- `HR Access` → Modify on `C:\Shares\HR`
- `Security Access` → Modify on `C:\Shares\Security`

Broad access groups were removed where appropriate after inheritance was disabled.

## Testing Performed

### Allowed Access Validation
Verified that users could access only the resources assigned to their department.

Examples:
- `hr.user1` successfully accessed the HR share
- `sec.user1` successfully accessed the Security share

### Denied Access Validation
Verified that users were denied access to unauthorized department shares.

Examples:
- `hr.user1` was denied access to the Security share
- `sec.user1` was denied access to the Finance share

## Identity Lifecycle Actions
This project also supports basic IAM lifecycle administration:

- **Joiner:** create a new user and place them in the correct OU and security group
- **Mover:** remove a user from one access group and add them to another
- **Leaver:** disable a user account to simulate offboarding

These actions demonstrate how IAM changes can be managed centrally through Active Directory.

## Challenges Encountered
During setup, I worked through:
- Active Directory and DNS configuration issues
- domain controller promotion troubleshooting
- domain join troubleshooting
- file sharing and SMB access configuration
- inherited NTFS permission cleanup
- group-based access validation from a domain-joined client

This improved my understanding of how identity, DNS, group membership, and file permissions work together in a domain environment.

## Outcome
Successfully built an IAM lab in Active Directory that demonstrates role-based access control, least-privilege access, and identity lifecycle administration across shared domain resources.

## Screenshots

### OU Structure
![OU Structure](https://github.com/Tl39455/active-directory-iam-rbac-lab/blob/241ff4755f7089afd96a8711ce848dc57d2b8bf7/iam-ou-structure.png)

### IAM Users
![IAM Users](https://github.com/Tl39455/active-directory-iam-rbac-lab/blob/0f7092ccba6e46de52b90d2da190ab3e6ddfffb7/iam-users.png)

### Security Groups
![Security Groups](https://github.com/Tl39455/active-directory-iam-rbac-lab/blob/08492878d3d1ddeecaf5019609a53bbed9868e7d/iam-security-group.png)

### Group Membership
![Group Membership](https://github.com/Tl39455/active-directory-iam-rbac-lab/blob/78b448b45faaa775a91e7b0a608723bff2da48ae/iam-group-members.png)

### Folder Permissions
![Folder Permissions](https://github.com/Tl39455/active-directory-iam-rbac-lab/blob/684fd1028fec35168823939ab433885d0e872fa1/iam-folder-permissions.png)

### Allowed Access
![Allowed Access](https://github.com/Tl39455/active-directory-iam-rbac-lab/blob/3f047efdc94f651f6987c636fb1cbbea92e822f1/iam-hr-folder-access.png)

![]()

### Denied Access
![Denied Access](screenshots/denied-access.png)

![](https://github.com/Tl39455/active-directory-iam-rbac-lab/blob/3f047efdc94f651f6987c636fb1cbbea92e822f1/iam-hr-folder-access.png)

### Disabled Account
![Disabled Account](screenshots/disabled-account.png)

## Resume Bullet
- Built an IAM lab in Active Directory to implement role-based access control using security groups, least-privilege folder permissions, and identity lifecycle administration across domain resources.
