# Active Directory Fundamentals Lab - Detailed Notes Objective

Built a Windows Server 2025 Active Directory environment with a Windows 11 client workstation using VirtualBox.

## Environment

### Domain Controller

- Windows Server 2025 Standard Evaluation (Desktop Experience)
- Hostname: DC1
- Domain: adlab.local
- IP Address: 10.10.10.10

### Client Workstation

- Windows 11
- Hostname: WIN-CLIENT
- IP Address: 10.10.10.20

## Part 1 - Create the Domain Controller VM

1.	Open VirtualBox.
2.	Create a new virtual machine named DC1.
3.	Select Windows Server 2025 ISO (after the ISO has been properly mounted after download).
4.	**Enable EFI.**
5.	Configure memory (4096-60GB) and CPU resources (2) 
6.	Disable pre-allocated memory
7.	Create a virtual hard disk.
8.	Mount the Windows Server ISO.
9.	Change Graphics Controller from VBoxSVGA to VMSVGA if a black screen occurs.
10.	Install Windows Server 2025 Standard Evaluation (Desktop Experience).


## Part 2 - Initial Server Configuration

1.	Configure administrator password.
2.	Log into Windows Server.
3.	Verify networking.
4.	Open Server Manager.
5.	Rename server to DC1.
6.	Restart the server.

## Part 3 - Install Active Directory Domain Services

1.	Open Server Manager.
2.	Select Add Roles and Features.
3.	Install: Active Directory Domain Services
5. Select/ensure DNS Server is an included feature in the Active Directory installation.
6. Complete installation.

## Part 4 - Promote the Server to a Domain Controller

1.	In the Server Manager home page, select the "Promote this server to a domain controller." notification.
2.	Create a new forest.
3.	Domain name: adlab.local
4.	Configure Directory Services Restore Mode password.
5.	Complete prerequisite checks.
6.	Install and reboot.

## Part 5 - Create Organizational Units

In the Server Manager home page, under the  **Tools** tab, select **Active Directory Users and Computers**. Right-click on the domain name, select **New**, then select **Organizarional Unit**:

Create OUs:

- IT
- HR
- Sales
- Servers
- Workstations

## Part 6 - Create User Accounts

Right-click on the appropriate OU and select **New**, then select **User**

Create:

### IT

Alex Admin
UPN: aalex@adlab.local

### HR

Sarah Smith
UPN: ssmith@adlab.local

### Sales

John Davis
UPN: jdavis@adlab.local

Configure user passwords and account settings.

## Part 7 - Create Security Groups

Right-click on the appropriate OU and select **New**, then select **Group**

Create:

- IT_Admins
- HR_Users
- Sales_Users

Add users to their corresponding groups.

## Part 8 - Create Group Policy

1.	Open Group Policy Management.
2.	Create: Password Policy Lab
3.	Link policy to adlab.local.
4.	Verify policy appears in Group Policy Management.

## Part 9 - Create the Windows 11 Client

1.	Create WIN-CLIENT VM.
2.	Memory- 4096 (60GB) CPU- 2
3.	Enable EFI
4.	Disable pre-allocated memory
5.	Install Windows 11.
6.	Press any key when prompted or it won’t boot from EFI and try to boot from an empty disc (after the initial setup, ignore the prompt because it’ll make you repeat the installation process).
7.	Complete initial setup.
8.	Verify connectivity with **ping** and **ipconfig /all** commands.

## Part 10 - Configure Networking

### VirtualBox Internal Network:

ADLAB

### Domain Controller

- IP Address: 10.10.10.10
- Subnet Mask: 255.255.255.0 
- DNS Server: 10.10.10.10 

### Client

- IP Address: 10.10.10.20 
- Subnet Mask: 255.255.255.0 
- DNS Server: 10.10.10.10 

## Part 11 - Join Client to Domain

1.	**Windows + R**, then type **sysdm.cpl**
2.	Open System Properties.
3.	Select **Change**.
4.	Join domain: adlab.local
5.	Authenticate using domain administrator credentials.
6.	Restart workstation.

## Part 12 - Verify Domain Authentication

1.	Select **Other User**.
2.	Log in as: ADLAB\aalex
3.	Verify successful domain authentication.

## Troubleshooting Log:

### EFI Boot Failure

- **Issue:** VM would not boot.
- **Resolution:** Enabled EFI in VirtualBox settings.

### Black Screen During Installation

- **Issue:** Windows Server displayed a black screen.
- **Resolution:** Changed graphics controller to VMSVGA.

### Installed Server Core Instead of Desktop Experience

- **Issue:** Windows Server installed without GUI.
- **Resolution:** Reinstalled using Windows Server 2025 Standard Evaluation (Desktop Experience).

### DNS Resolution Failure

- **Issue:** The Client could reach DC1 by IP address but could not resolve adlab.local as the hostname attached to that IP address.
- **Resolution:** Disabled DHCP, and configured static IP addresses and pointed client DNS to DC1.

## Key Lessons Learned

- Active Directory depends heavily on DNS.
- Domain joins can fail even when network connectivity appears functional.
- Windows Server Core and Desktop Experience provide different administration experiences.
- Virtual machine settings can impact operating system installation and functionality.

