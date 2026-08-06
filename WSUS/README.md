# Windows Server Update Services (WSUS)

## Overview

Windows Server Update Services (WSUS) is a Windows Server role that allows administrators to centrally manage and distribute Windows updates within an organization.

Instead of each client computer downloading updates directly from Microsoft, WSUS provides a centralized solution where updates can be synchronized, reviewed, and deployed to domain-joined computers.

---

## Objectives

- Install the WSUS role.
- Configure a dedicated content directory to store downloaded updates.
- Complete the WSUS post-installation configuration.
- Configure Group Policy to enable clients to receive updates from the WSUS server.
- Verify that client computers successfully communicate with WSUS and receive approved updates.

---

## Deployment

Installed the WSUS role using Server Manager.

During the installation of the WSUS service, I noticed that the IIS service was also installed.



Selected C:\bank.lab\WSUS as the content directory.

<img width="829" height="577" alt="The Container" src="https://github.com/user-attachments/assets/a1fe446c-d396-4374-8ecf-8eb84d379c49" />


During the installation of the WSUS service, I noticed that the IIS service was also installed.

## WSUS and IIS

Windows Server Update Services (WSUS) depends on Internet Information Services (IIS) to communicate with client computers.

When the WSUS role is installed, IIS is automatically installed (if it is not already available) because WSUS uses web services over HTTP/HTTPS to deliver updates and receive status reports from clients.

In simple terms:

- **WSUS** manages update synchronization, approvals, and deployment.
- **IIS** hosts the web services that allow client computers to download updates and report their installation status.

Without IIS, WSUS cannot communicate with clients or distribute updates.


During the post-installation configuration, an error occurred.

image

I used this command via PowerShell to complete the setup, and it worked.

image


