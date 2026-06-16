# Active Directory Fundamentals Lab

## Overview

This project demonstrates the deployment and administration of a Windows Active Directory environment using VirtualBox. The lab includes the installation and configuration of Windows Server 2025, Active Directory Domain Services (AD DS), DNS, Group Policy, user and group administration, and the deployment of a domain-joined Windows 11 client workstation.

## Technologies Used

- Windows Server 2025 Standard Evaluation (Desktop Experience)
- Windows 11 Pro
- Active Directory Domain Services (AD DS)
- DNS
- Group Policy Management
- VirtualBox
- Windows Networking

## Environment Configuration

### Network Configuration 

- DC1: 10.10.10.10
- WIN-CLIENT: 10.10.10.20
- DNS Server: 10.10.10.10
 
### Domain Controller (DC1)

- Windows Server 2025
- Active Directory Domain Services
- DNS Server
- Domain: adlab.local
- Static IP: 10.10.10.10

### Client Workstation

- Windows 11
- Domain JoinedActive Directory Fundamentals Lab
- Static IP: 10.10.10.20
- DNS Server: 10.10.10.10

![Network Configuration](Screenshots/01_Network_Config.png)

## Active Directory Deployment

- Installed Windows Server 2025
- Installed AD DS role
- Promoted server to Domain Controller
- Created the adlab.local domain

## Organizational Structure

### Created Organizational Units (OUs):

- IT
- HR
- Sales
- Servers
- Workstations

![Organizational Units](Screenshots/02_OU_Structure.png)
 
## User Administration

### Created user accounts:

- IT User: Alex Admin UPN: aalex@adlab.local
- HR User: Sarah Smith UPN: ssmith@adlab.local
- Sales User: John Davis UPN: jdavis@adlab.local

### Configured:

- User passwords
- Account management (disable/enable accounts)
- Password resets
- Group membership

## Group Management

### Created security groups:

- IT_Admins
- HR_Users
- Sales_Users

Assigned users to appropriate security groups.

![User Group Membership](Screenshots/03_User_Group_Membership.png)
 
## Group Policy

- Created and linked a Group Policy Object (GPO)
- Explored password policy settings
- Verified Group Policy Management functionality

![Group Password Policy Object](Screenshots/04_Group_Policy.png)
 
## Client Deployment
- Installed Windows 11 virtual machine
- Configured networking
- Joined Windows 11 workstation to the adlab.local Active Directory domain using administrator credentials.
- Successfully authenticated using domain user credentials (image below)

![User Domain Login Success](Screenshots/05_Domain_Login.png)

![WIN-CLIENT DNS Configuration](Screenshots/06_Client_DNS_Config.png)

## Troubleshooting Log:

### EFI Boot Failure

**Issue:** VM would not boot.<br>
**Resolution:** Enabled EFI in VirtualBox settings.

### Black Screen During Installation

**Issue:** Windows Server displayed a black screen.<br>
**Resolution:** Changed graphics controller to VMSVGA.

### Installed Server Core Instead of Desktop Experience

**Issue:** Windows Server installed without GUI.<br>
**Resolution:** Reinstalled using Windows Server 2025 Standard Evaluation (Desktop Experience).

### DNS Resolution Failure

**Issue:** The Client could reach DC1 by IP address but could not resolve adlab.local as the hostname attached to that IP address.<br>
**Resolution:** Disabled DHCP, and configured static IP addresses and pointed client DNS to DC1.

## For a walk-through and detailed troubleshooting notes, see:

- [Lab-Walkthrough.md](Detailed-Notes/Lab-Walkthrough.md)
- [Detailed-Troubleshooting.md](Troubleshooting/Detailed-Troubleshooting.md)

## Key Lessons Learned

- Active Directory depends heavily on DNS.
- Domain joins can fail even when network connectivity appears functional.
- Windows Server Core and Desktop Experience provide different administration experiences.
- Virtual machine settings can impact operating system installation and functionality.

## Skills Demonstrated

- Active Directory Administration
- DNS Configuration
- User and Group Management
- Group Policy Management
- Windows Server Administration
- Virtualization
- Network Troubleshooting
- Domain Deployment
- Windows Client Management

## Future Enhancements

- DHCP Deployment
- File Shares and NTFS Permissions
- Advanced Group Policy Configuration
- Help Desk Ticket Simulation
- Multi-Client Domain Environment

