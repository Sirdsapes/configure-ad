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

- Creating necessary Virtual Machines in Azure: Domain Controller and Client (user).
- Creating a new user in Active Directory who will be Admin.
- Connecting a user's VM to the Domain for Admin purposes.
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
-Open Windows Defender Firewall with Advanced Security.
-Click Inbound Rules in the left box and enable the Core Networking Echo Requests.
</p>
<br />

<p>
<a href="https://imgtr.ee/image/IFUmW"><img src="https://imgtr.ee/images/2023/07/02/f2a71197416c0980a3a7d0f75393e17b.png" alt="f2a71197416c0980a3a7d0f75393e17b.png" border="0"></a>
<a href="https://imgtr.ee/image/IFr4A"><img src="https://imgtr.ee/images/2023/07/02/c852408654db9f32d11cfa012a95df95.png" alt="c852408654db9f32d11cfa012a95df95.png" border="0"></a>
<a href="https://imgtr.ee/image/IFyq5"><img src="https://imgtr.ee/images/2023/07/02/9ad8d258b3089191dead1425efa3c184.png" alt="9ad8d258b3089191dead1425efa3c184.png" border="0"></a>
</p>
<p>
-Next, we'll install Active Directory Domain Services in the DC-1 VM.
-Open Server Manager, click Add roles and features. Click next and make sure DC-1 is the server -- it should be the only one -- click next and click Active Directory Domain Services and Add Features.
-Click next and let it install.
-You'll see a yellow warning sign in the top bar after ADDS is set up. Click it and Promote this server to a domain controller. 
-In the new window, click Add a new forest and name it something simple; ex: mydomain.com. Click next until you reach the Prerequistes page and click Install. It should take a bit.
-Set up a password and click Next.
-When it is installed, it will restart the VM, i.e. log you out, and you will have to reopen the remote connection as before using the DC-1 Public IP.
-Since DC-1 is now a Domain Controller, you cannot sign back in using the regular username. You'll need to use mydomain.com\ followed by your username, ex: mydomain.com\labuser. The mydomain.com was set up earlier as your root domain. So make sure it matches.
-
</p>
<br />

<p>
<a href="https://imgtr.ee/image/IFR1g"><img src="https://imgtr.ee/images/2023/07/02/8ad8ed036d9ff902ea43116d7463f625.png" alt="8ad8ed036d9ff902ea43116d7463f625.png" border="0"></a>
<a href="https://imgtr.ee/image/IF95l"><img src="https://imgtr.ee/images/2023/07/02/7747fc5b58d008d06ea416edcab8e155.png" alt="7747fc5b58d008d06ea416edcab8e155.png" border="0"></a>
<a href="https://imgtr.ee/image/IFlYu"><img src="https://imgtr.ee/images/2023/07/02/609086116d0cff5ee1c5469f157df863.png" alt="609086116d0cff5ee1c5469f157df863.png" border="0"></a>
<a href="https://imgtr.ee/image/IFoVs"><img src="https://imgtr.ee/images/2023/07/02/64182195b164b5e7de1dc42664b77be2.png" alt="64182195b164b5e7de1dc42664b77be2.png" border="0"></a>
<a href="https://imgtr.ee/image/Ich6G"><img src="https://imgtr.ee/images/2023/07/02/95b479ad36047a88905944b36a6264db.png" alt="95b479ad36047a88905944b36a6264db.png" border="0"></a>
</p>
<p>
-In the DC-1 VM, open Active Directory Users and Computers. In the mydomain.com category, create a new Organization Unit named _EMPLOYEES. Right-click mydomain.com, New, Organizational Unit and name it _EMPLOYEES. Do this again but name the new OU _admins.
-In the _admins group, create a new user. I named them Jane Doe. Their logon name will be whatever you chose, but since they'll be an admin, use jane_admin. Click next and create a password and uncheck User must change password at next logon and click Next to finish creating the user.
-To make Jane an actual admin, we have to assign the account the role. Right click Jane Doe and open Properties and the Member Of tab and click Add. Add Jane to the Domain Admins group and click OK. Click Apply and OK.
-Next, we'll be logging back into the DC VM with the user account we just created, i.e. Jane. So, log out of the VM and remote back in using the same Public IP as before. However, we need to log in using Jane's credentials, i.e. mydomain.com\jane_admin, and the password with that account. It will look the same, you're just now using Jane's account.
</p>
<br />

<p>
<a href="https://imgtr.ee/image/IclJT"><img src="https://imgtr.ee/images/2023/07/02/54f68e3618b9a3d62450365f7ffbce09.png" alt="54f68e3618b9a3d62450365f7ffbce09.png" border="0"></a>
<a href="https://imgtr.ee/image/IcNZU"><img src="https://imgtr.ee/images/2023/07/02/110cb618b48c0cd2a339b8436f5c9510.png" alt="110cb618b48c0cd2a339b8436f5c9510.png" border="0"></a>
<a href="https://imgtr.ee/image/IlIc2"><img src="https://imgtr.ee/images/2023/07/02/73465897c45834f02a59330c0ec3c725.png" alt="73465897c45834f02a59330c0ec3c725.png" border="0"></a>
<a href="https://imgtr.ee/image/IlCuo"><img src="https://imgtr.ee/images/2023/07/02/9598ba1aa0a43cc85f33db2cb1b7aacd.png" alt="9598ba1aa0a43cc85f33db2cb1b7aacd.png" border="0"></a>
<a href="https://imgtr.ee/image/Ilzfu"><img src="https://imgtr.ee/images/2023/07/02/9cddcda76774c8572ec2c7dab24a0098.png" alt="9cddcda76774c8572ec2c7dab24a0098.png" border="0"></a>
</p>
<p>
-Next, we'll be connecting the Client-1 VM to the domain. First, we'll need to set Client-1's DNS settings to the DC's Private IP Address. 
-Remote into the Client-1 VM using the Public IP and the username/password you set up earlier.
-Go back to the Azure portal and find the Private IP of the DC-1 VM. Listed under Networking or found in the Networking group by opening it from the left box. Copy the Private IP and go to the Client-1 VM.
-Open Client-1's Networking page and click Network Interface. Click DNS servers, click Custom, paste the DC VM's Private IP, and then Save. Make sure there are no spaces in the IP or it will fail to change.
-Restart the Client-1 VM and the remote connection should close, which closes the remote window. So, remote back into Client-1 same as before.
-Once back into the remote connection, open System (right-click the Windows icon on the start bar and click System), and click Rename this PC (advanced). In the new window, click Change, and set the Domain to mydomain.com.
-You will be prompted to enter in the credentials for someone with permission to join the domain. Use the Domain Admin account made earlier, i.e. mydomain.com\jane_admin, and click OK.
-The remote connection will close due to needing to restart.
</p>
<br />

<p>
<a href="https://imgtr.ee/image/IEIh7"><img src="https://imgtr.ee/images/2023/07/02/b3b9a0642169e4ed8a1360b9dbe8e572.png" alt="b3b9a0642169e4ed8a1360b9dbe8e572.png" border="0"></a>
<a href="https://imgtr.ee/image/IEj9F"><img src="https://imgtr.ee/images/2023/07/02/a6285fddb378b8bcd063b31bdf9e1101.png" alt="a6285fddb378b8bcd063b31bdf9e1101.png" border="0"></a>
<a href="https://imgtr.ee/image/IEKk5"><img src="https://imgtr.ee/images/2023/07/02/c50256effffa71fca466623e8e3e8a55.png" alt="c50256effffa71fca466623e8e3e8a55.png" border="0"></a>
<a href="https://imgtr.ee/image/IEuNM"><img src="https://imgtr.ee/images/2023/07/02/a7815f70e913727f28f96de727cc6fc8.png" alt="a7815f70e913727f28f96de727cc6fc8.png" border="0"></a>
</p>
<p>
-Next, we will remote back into the Client-1 VM, however we will use Jane's credentials to sign in, i.e. mydomain.com\jane_admin
-Once in, open the System window, click Remote Desktop, and Select users that can remotely access this PC. Add Domain Users and click OK.
-Go back to the DC-1 remote window. If it's closed, remote back in using Jane's credentials. If it's still open, make sure it's still Jane's account by checking the account in cmd.
-Open PowerShell ISE as Admin.
-We are going to paste a script that generates X amount of users in Active Directory (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1).
-Click New Script and paste the code. Click the green arrow to Run the code. It will place these new accounts in the previously-made _EMPLOYEES Organizational Unit.
-Open Active Directory Users and Computers and click the _EMPLOYEES group to see the new profiles.
</p>
<br />

<p>
<a href="https://imgtr.ee/image/IElY5"><img src="https://imgtr.ee/images/2023/07/02/90f864f431ece9f88b0753dbfa56273e.png" alt="90f864f431ece9f88b0753dbfa56273e.png" border="0"></a>
<a href="https://imgtr.ee/image/INCCK"><img src="https://imgtr.ee/images/2023/07/02/0954b462b5b7e9265a91819ffafea64a.png" alt="0954b462b5b7e9265a91819ffafea64a.png" border="0"></a>
<a href="https://imgtr.ee/image/IN1KM"><img src="https://imgtr.ee/images/2023/07/02/2b8a86d1d94ee62ab5bec79c6e7f352c.png" alt="2b8a86d1d94ee62ab5bec79c6e7f352c.png" border="0"></a>
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
