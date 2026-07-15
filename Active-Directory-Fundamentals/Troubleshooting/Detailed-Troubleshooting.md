# Detailed Troubleshooting and Lessons Learned

## EFI Boot Failure

### Problem

After creating the Windows Server virtual machine, the operating system failed to boot successfully.

### Investigation

In the DC1 virtual machine storage settings the hard disk and installation media were attached correctly, indicating the issue was likely related to the VM firmware configuration.

### Root Cause

EFI support was not enabled for the virtual machine so the VM had nothing to boot from.

### Resolution

I enabled EFI within the VirtualBox System settings and restarted the virtual machine. The server successfully booted and continued with installation.

### Lesson Learned

Virtual machine firmware settings can directly affect operating system installation and startup behavior.

---

## Black Screen During Installation

### Problem

During the Windows Server installation process, the virtual machine displayed a black screen and appeared unresponsive.

### Investigation

Because the VM remained powered on, I suspected a display compatibility issue rather than a failed installation. I reviewed the display settings within VirtualBox.

### Root Cause

The default graphics controller configuration was incompatible with the guest operating system.

### Resolution

I changed the default graphics controller setting to **VMSVGA** and restarted the virtual machine.

### Result

The Windows Server installation displayed normally and continued without issue.

### Lesson Learned

Display-related problems may be caused by virtualization settings rather than the operating system itself.

---

## Installed Server Core Instead of Desktop Experience

### Problem

After installation completed, Windows Server launched into a command-line environment rather than a graphical desktop.

### Investigation

I reviewed the installation options selected during setup and discovered that Server Core had been installed instead of Desktop Experience.

### Root Cause

An incorrect installation option was selected during the Windows Server setup process.

### Resolution

I reinstalled the operating system using **Windows Server 2025 Standard Evaluation (Desktop Experience)**.

### Result

The graphical user interface became available, allowing the remainder of the Active Directory lab to be completed using Server Manager and other administrative tools.

### Lesson Learned

Windows Server installation choices significantly affect the available management tools and administrative experience.

---

## DNS Resolution Failure

### Problem

The client workstation could successfully ping the domain controller's IP address but could not resolve the domain name `adlab.local`. Because of this, the client could not properly communicate with Active Directory services.

### Investigation

I performed several tests to isolate the issue:

* Verified network connectivity by pinging the domain controller's IP address (10.10.10.10).
* Attempted to communicate by pinging the domain name `adlab.local`, the ping failed.
* Reviewed IP and DNS configuration using `ipconfig /all`.
* Verified Active Directory Domain Services and DNS services were running on the domain controller.

**Results showed that communication by IP address succeeded while communication by hostname failed.**

### Root Cause

The client was not using the domain controller as its DNS server.

Although network connectivity existed, DNS name resolution was failing.

### Resolution

1. Disabled DHCP.
2. Configured static IP addresses.
3. Assigned the domain controller as the preferred DNS server.
4. Verified successful name resolution.
5. Retested domain communication.

### Result

The client successfully resolved **adlab.local** and was able to join and authenticate against the Active Directory domain.

### Lesson Learned

This issue reinforced one of the most important Active Directory concepts:

**Active Directory depends on DNS. If DNS is not functioning correctly, many AD services will fail even when network connectivity appears normal.**

---

# Overall Lessons Learned

* DNS is a foundational service for Active Directory.
* Troubleshooting requires validating one layer at a time rather than making assumptions.
* Virtual machine settings can have a significant impact on operating system installation and behavior.
* Understanding the difference between network connectivity and name resolution is critical when diagnosing domain-related issues.
* Documenting problems and resolutions creates a valuable reference for future deployments and troubleshooting efforts.

