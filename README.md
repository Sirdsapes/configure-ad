<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>


<p>
-Create a new Virtual Machine in Azure.
-Create a new Resource Group. I named it AD-Lab.
-Name the VM DC-1; it'll be used as a domain controller (a server with Active Directory installed, essentially).
-The Image will use Windows Server 2022 and size will use 2 VCPUs.
-Enter your own username and password.
-Click Review + create and then Create to start the VM deployment.
</p>
<br />

<p>
<a href="https://imgtr.ee/image/IV1ZL"><img src="https://imgtr.ee/images/2023/07/02/bd1996a8e7db3d3d6291a7b734a5d43d.png" alt="bd1996a8e7db3d3d6291a7b734a5d43d.png" border="0"></a>
<a href="https://imgtr.ee/image/IVqnU"><img src="https://imgtr.ee/images/2023/07/02/d1e72fae32d86523d5e14e4a7db46f0b.png" alt="d1e72fae32d86523d5e14e4a7db46f0b.png" border="0"></a>
<a href="https://ibb.co/MPSKTk9"><img src="https://i.ibb.co/P1jJpGt/Vm-Deploy2.png" alt="Vm-Deploy2" border="0"></a>
</p>
<p>
-Next, we'll create a Client VM. Create a new VM using the AD-Lab resource group and name it Client-1.
-The image will be Windows 10 instead of Windows Server.
-Use same username/password as before to keep it simple.
-Click Next and Next to get to Networking.
-It will automatically put you in the VNET of the resource group.
-Click Review + create and Create and the VM will begin deploying.
</p>
<br />

<p>
<a href="https://imgtr.ee/image/IV1ZL"><img src="https://imgtr.ee/images/2023/07/02/bd1996a8e7db3d3d6291a7b734a5d43d.png" alt="bd1996a8e7db3d3d6291a7b734a5d43d.png" border="0"></a>
<a href="https://imgtr.ee/image/IVgdu"><img src="https://imgtr.ee/images/2023/07/02/d0fe9898f1c54b25c7681d7a24d8448b.png" alt="d0fe9898f1c54b25c7681d7a24d8448b.png" border="0"></a>
<a href="https://imgtr.ee/image/IVTIL"><img src="https://imgtr.ee/images/2023/07/02/f7eb728f0f4238f4ab712068ad8a8c54.png" alt="f7eb728f0f4238f4ab712068ad8a8c54.png" border="0"></a>
</p>
<p>
-Go back to Virtual Machines and reopen the DC-1 VM. Click Networking in the left bar and click Networking Interface.
-Click IP configurations in the left box and open ipconfig so we can change the IP from Dynamic to Static and click Save.
</p>
<br />

<p>
<a href="https://imgtr.ee/image/IVczF"><img src="https://imgtr.ee/images/2023/07/02/d21a3140bf34f4c88095b3b20c62c00d.png" alt="d21a3140bf34f4c88095b3b20c62c00d.png" border="0"></a>
<a href="https://imgtr.ee/image/IVE9H"><img src="https://imgtr.ee/images/2023/07/02/dffb37f8f125810f1e6594b2fbb1f2b4.png" alt="dffb37f8f125810f1e6594b2fbb1f2b4.png" border="0"></a>
<a href="https://imgtr.ee/image/IVt4U"><img src="https://imgtr.ee/images/2023/07/02/633cf0f03c29f11b8f527e4a27969bb5.png" alt="633cf0f03c29f11b8f527e4a27969bb5.png" border="0"></a>
</p>
<p>
-Next we're going to ensure connectivity between the DC and Client by enabling ICMP so we can ping the Client.
-Go to the DC-1 VM and copy the Public IP address. We'll use that IP to remote login via Window's Remote Desktop Connection.
-Open Remote Desktop Connection and paste the IP. Login using the username/password used to create the VM.
</p>
<br />

<p>
<a href="https://imgtr.ee/image/IFUmW"><img src="https://imgtr.ee/images/2023/07/02/f2a71197416c0980a3a7d0f75393e17b.png" alt="f2a71197416c0980a3a7d0f75393e17b.png" border="0"></a>
<a href="https://imgtr.ee/image/IFr4A"><img src="https://imgtr.ee/images/2023/07/02/c852408654db9f32d11cfa012a95df95.png" alt="c852408654db9f32d11cfa012a95df95.png" border="0"></a>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
