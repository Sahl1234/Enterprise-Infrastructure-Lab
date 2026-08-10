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


<img width="829" height="577" alt="Updates Container" src="https://github.com/user-attachments/assets/1d97732e-4cd3-4d16-bc29-bbc96815f77a" />



During the installation of the WSUS role, I noticed that IIS was also installed as part of the required components.

WSUS relies on IIS to communicate with client computers and deliver updates over the network.

In simple terms:

* **WSUS** is responsible for managing updates, synchronization, approvals, and reporting.
* **IIS** provides the web services used by client computers to communicate with the WSUS server and download updates.

So, WSUS manages the updates, while IIS provides the web-based communication and delivery mechanism between the WSUS server and its clients.



During the post-installation configuration, an error occurred.


![Post Deployment error](images/post_deploymnt_error.JPG)


I used this command via PowerShell to complete the setup, and it worked.


![PowerShell command](images/PowerShell.JPG)


### Initial Configuration

After completing the post-installation configuration, I opened the WSUS management console and started the Initial Configuration Wizard.

![WSUS Initial Configuration Wizard](imaages/upstream_servers.JPG)

At this stage, WSUS connects to Microsoft Update to retrieve information about available updates, products, classifications, and languages.
