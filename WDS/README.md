

# Windows Deployment Services (WDS)

## Objectives

The main objective of this lab was to deploy Windows 7 over the network using Windows Deployment Services (WDS).

In this lab, I wanted to understand how WDS works with Active Directory, DHCP, PXE, and Windows installation images to deploy an operating system to a new client machine without using an ISO directly on the client.

The main objectives were:

- Install and configure WDS on Windows Server.
- Integrate WDS with the existing Active Directory domain.
- Configure the Remote Installation Folder.
- Configure WDS to work with DHCP and PXE.
- Add a Windows 7 boot image (`boot.wim`) to WDS.
- Add a Windows 7 installation image (`install.wim`) to WDS.
- Create a new virtual machine to act as a PXE client.
- Boot the client over the network using PXE.
- Deploy Windows 7 Professional to the client through WDS.

---

## Deployment

### 1. Installing WDS

The first step was to install the Windows Deployment Services role on the Windows Server.

![WDS Installation](WDS_Instaltion.PNG)

After the installation was completed, I verified that the installation was successful.

![Installation Succeeded](Installation_succeeded.PNG)

---

### 2. Mounting the Windows 7 ISO

After installing WDS, I needed the Windows 7 installation media because I would use its image files with WDS.

I mounted the Windows 7 ISO inside the Windows Server virtual machine using VirtualBox.

From the VirtualBox menu, I went to:

**Devices → Optical Drives → Choose a Disk File**

Then, I selected the Windows 7 ISO file.

After mounting the ISO, I opened **This PC** and verified that the Windows 7 installation media appeared as a CD/DVD drive.

![Windows 7 ISO Mounted](wds_iso_mounted.png)

---

### 3. Configuring WDS

After preparing the Windows 7 installation media, I moved to the WDS console to configure the WDS server and integrate it with the existing server and domain environment.

Initially, the WDS console showed a yellow warning icon next to the server because the WDS service had not been configured yet.

![Configure WDS Server](Configure_Server.PNG)

I started the WDS configuration wizard.

---

### 4. Active Directory Integration

One of the important options during the configuration was the installation mode.

I selected:

**Integrated with Active Directory**

This allows WDS to work with the existing Active Directory domain.

---

### 5. Remote Installation Folder

The next step was to specify the location of the **Remote Installation Folder**.

This folder is used by WDS to store the files and images required for the deployment process.

I selected the appropriate storage location and continued with the configuration.

---

### 6. DHCP Options

The next important step was configuring the DHCP options.

Since DHCP was running on the same Windows Server, I enabled both DHCP options presented by the WDS configuration wizard.

These settings allow WDS to work correctly with DHCP during the PXE boot process.

---

### 7. PXE Response Settings

After configuring DHCP options, I reached the **PXE Response Settings** page.

There were three options available. I selected the third option to allow WDS to respond to PXE requests from client computers.

![PXE Response Configuration](wds_pxe_response_config.png)

This allows a new client connected to the network to send a PXE request and communicate with the WDS server.

---

### 8. WDS After Configuration

After completing the WDS configuration, the WDS console changed and several folders became available.

![WDS After Configuration](after_configr_Server.PNG)

The two main folders I worked with at this stage were:

- **Boot Images**
- **Install Images**

The Boot Image is used to start the client and load the Windows PE environment, while the Install Image contains the actual Windows operating-system files that will be installed on the client.

---

### 9. Adding the Boot Image

The next step was to add the Windows 7 boot image to WDS.

The boot image is stored inside the Windows 7 installation media as:

`Sources\boot.wim`

I opened the mounted Windows 7 ISO, navigated to the `Sources` folder, and selected `boot.wim`.

I then followed the WDS wizard to add the image to the **Boot Images** folder.

![WDS Boot Image](WDS_boot_image.PNG)

During the wizard, I provided a suitable name for the boot image and continued.

WDS then processed the image, which took some time to complete.

---

### 10. Adding the Install Image

After adding the boot image, I repeated a similar process to add the Windows 7 installation image.

The installation image is stored as:

`Sources\install.wim`

I selected `install.wim` from the mounted Windows 7 ISO and started the WDS installation-image wizard.

During this process, WDS displayed the Windows editions available inside the image.

In my case, the ISO contained only one edition:

**Windows 7 Professional**

![Windows 7 Install Image](wds_select_install_images.png)

I selected Windows 7 Professional and continued with the wizard.

WDS then processed the installation image and added it to the **Install Images** section.

---

### 11. Creating the PXE Client

After preparing the WDS server and adding the required images, I created a new virtual machine to act as the Windows 7 PXE client.

I named the virtual machine:

**Windows 7 PXE**

I left the ISO image field empty because the purpose of this lab was to install Windows 7 through the network using WDS.

The client would boot from the network instead of booting directly from an ISO file.

---

### 12. Configuring the Client Network

The next step was connecting the new client to the same network as the WDS server.

In VirtualBox, I configured **Adapter 1** as:

**Internal Network**

Then, I selected the same internal network used by the domain:

**BANK-LAN**

![Client Network Configuration](vbox_client_network_boot.png)

This allows the PXE client to communicate with the WDS server and obtain its network configuration through DHCP.

---

### 13. Configuring Network Boot

The final configuration on the client was changing the boot order.

I configured the virtual machine to boot from the network first.

This allows the client to send a PXE request when it starts and look for a WDS server on the network.

![Network Boot Configuration](Internal_Network.PNG)

At this point, the WDS server, DHCP, PXE client, and Windows images were ready for the deployment process.

---

## Challenges

During the first deployment attempt, I faced several problems when trying to boot the Windows 7 PXE client using VirtualBox.

After configuring the WDS server, adding the Boot Image and Install Image, and preparing the new client machine, I started the client and tried to boot it from the network.

However, the PXE boot process did not work as expected.


![PXE Boot F12](wds_pxe_boot_f12.png)

I also encountered additional startup issues during the network boot process.

![Startup Issues](Start_issus.PNG)


I tried several troubleshooting steps to solve the problem. I changed different WDS settings, modified the boot configuration, and tested different options related to the virtual machine and network boot process.

I also tried using a Windows 10 Boot Image instead of the Windows 7 Boot Image to check whether the problem was related to the boot image itself.

However, the problem remained.

At this point, I suspected that the issue could be related to the PXE boot process or TFTP communication between the VirtualBox client and the WDS server.

Since I had already tried several possible solutions without success, I decided to move the client machine from VirtualBox to VMware Workstation and repeat the deployment.

In VMware Workstation, I created a new virtual machine and configured it as a PXE client using the same WDS server.

This time, the PXE boot process worked successfully without the problems I experienced in VirtualBox.

The client was able to communicate with the WDS server, load the Boot Image, and continue to the Windows installation process.

![Windows 7 Installation](Instaling.PNG)

![Windows 7 Installation](Instaling2.PNG)

Finally, the Windows 7 installation started successfully through WDS.

![WDS Credentials](WDS_Credentials.PNG)



## Lessons Learned

I spent a lot of time trying to fix the PXE boot issue in VirtualBox, but it just kept failing no matter what I tweaked. Switching to VMware Workstation changed everything. I always assumed VirtualBox would be lighter and better for my specs, but VMware turned out to be much smoother, more responsive, and handled WDS without a single problem. This lab taught me not to stay stuck on one tool when it isn't working, and that real hands-on testing beats assumptions every time.