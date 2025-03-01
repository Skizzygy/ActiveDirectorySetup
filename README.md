<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Seting up an Active Directory Network within the Cloud (Azure)</h1>
This project details how you can set up an example of an Active Directory within Azure using Virtual Machines and a Virtual Network.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Resource Groups, Virtual Machines and Networks)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022 Datacenter: Azure Edition
- Windows 10 Pro (Version 22H2)

<h2>Deployment and Configuration Steps</h2>

<p align="center">
Create a Resource Group where all of your services will reside. <br/>
<img src=https://github.com/user-attachments/assets/b3decc0c-b7dc-430c-ab05-d1d168951315 />
<br/>
<br/>
Create your Virtual Network, making sure to select the Resource Group you created in the first step. <br/>
<img src=https://github.com/user-attachments/assets/3ae5ef69-6da1-495b-ac12-f75ef0aff344 />
<br/>
<br/>
Create the first Virtual Machine that will be the Domain Controller, making sure it's in the same resource group that the Virtual Netowrk is located in. Select Windows Server 2022 as the OS for this first VM. <br/>
<img src=https://github.com/user-attachments/assets/bd6c2cde-dc82-4051-af5e-c9688dbf3b18 />
<br/>
<br/>
Under the Networking Tab, make sure to select the Virtual Network that you created. Review and Create once you're done here. <br/>
<img src=https://github.com/user-attachments/assets/b8dfcf6d-d594-4fd4-9c01-34a0dde2a9d8 />
<br/>
<br/>  
Create your second VM, making sure it's within the same Resource group as before, and select Windows 10 as your Operating System. <br/>
<img src=https://github.com/user-attachments/assets/ead2cd77-7a0b-4c03-b738-2eca011c5e40 />
<br/>
<br/>
Make sure to select the same Virtual Netowrk that the Domain Controller VM is located in as well. <br/>
<img src=https://github.com/user-attachments/assets/1e43e359-e6a3-470c-a80a-15936b2a18aa />
<br/>
<br/>
Once both machines are created, make your way into the Netowrk Settings for the Domain Controller VM. You can get there by navigating to the Virtual Machines list, clicking on the Domain Controller VM, and clicking on the Network Settings. You should be at this screen: <br/>
<img src=https://github.com/user-attachments/assets/dd89fc98-d19b-4fb8-b8c2-a63a8c1b7cff />
<br/>
<br/>
Once here, click on the Network Interface Card to pull up it's settings, then click on ipconfig1 near the bottom. <br/>
<img src=https://github.com/user-attachments/assets/a2dd8a27-c90a-4df3-bfe5-24f0b0fab983 />
<br/>
<br/>
Change the IP Allocation from Dynamic to Static and press Save. <br/>
<img src=https://github.com/user-attachments/assets/a3ca1425-d1ae-436c-8411-05b6f43ba300 />
<br/>
<br/>
Head into the Network Settings for the 'Client' Virtual Machine, and into the settings for the Network Interface Card. <br/>
<img src=https://github.com/user-attachments/assets/f2c9f542-0252-47b1-8ed1-2f9cef4f2a4d />
<br/>
<br/>
In the 'Settings' Dropdown box, click on DNS servers and change the DNS Server setting from 'Inherit from Virtual Network' to 'Custom', and enter the Domain Controller VM's Private IP in the box, which you can find in the overview of the DC VM. Then click 'Save', and restart the VM from the Virtual Machine Directory. <br/>
<img src=https://github.com/user-attachments/assets/f9ad9bb2-5591-4b03-9b75-8431e1d13a4c />
<br/>
<br/>
Once set up, connect to the VM's using the 'Remote Desktop Connection' Program, using the Public IP Addresses for both Machines, and log in using the username and Password you created whenever setting up the machines. <br/>
<img src=https://github.com/user-attachments/assets/1049ff49-45ad-4b1c-8a89-852d30045a14 />
<br/>
<br/>
Within the DC Machine, in the Server Manager window, click 'Add roles and features'<br/>
<img src=https://github.com/user-attachments/assets/6f06cbea-2d8a-454a-925b-d2c722e151d0 />
<br/>
<br/>
Click Next through the dialouge box until you get to 'Select Server Roles', and select 'Active Directory Domain Services', then Add Features. <br/>
<img src=https://github.com/user-attachments/assets/da707642-b0c1-4835-8375-6e12be677e0a />
<br/>
<br/>
Click Next until you can press Install, then press Install and wait for the Wizard to finish.<br/>
<img src=https://github.com/user-attachments/assets/6ffd8925-09a8-465a-868e-32d2603a03d9 />
<br/>
<br/>
Once Finished, Press on the flag, which now has a Yellow Triangle with a Exclamation Mark within it, and click on "Promote this server to a domain controller". <br/>
<img src=https://github.com/user-attachments/assets/549283c4-cdad-4ce2-af17-98722c86e32e />
<br/>
<br/>
Select 'Add a new forest', then type in whatever domain you would like to use, set a password on the next screen, then uncheck Create DNS Delegation. <br/>
<img src=https://github.com/user-attachments/assets/344aad06-eba4-4c19-bc94-9d42b89ef3d3 />
<br/>
<br/>
Continue through the Configuration Wizard, keeping everything else default, then press Install whenever possible. The system will restart once completed. <br/>
<img src=https://github.com/user-attachments/assets/97a4677d-57c1-41b4-8035-8bb7b4e86fe7 />
<br/>
<br/>
Once it has Restarted, sign back into the DC VM using [YOUR DOMAIN HERE]\[Your username], then wait for the system to fully load in. <br/>
<br/>
<br/>
Open Active Directory Users and Computers on the DC VM for later. <br/>
<img src=https://github.com/user-attachments/assets/a575b6cf-f901-4a1b-b253-4fa3491b30df />
<br/>
<br/>
Turn off the firewall for the Domain, Private, and Public Profile on the DC VM, for testing purposes only. You can open the window by typing 'wf.msc' in the search bar. <br/>
<img src=https://github.com/user-attachments/assets/28bafcd3-90a7-449e-bcd1-d131b254fa18 />
<br/>
<br/>
Now, sign into the 'Client' VM using the regular credentials you created when setting up the VM. <br/>
<br/>
<br/>
Open Powershell, then try to ping the local IP address of the DC VM. <br/>
<img src=https://github.com/user-attachments/assets/e0bc101f-3610-4de4-a39f-2d5e5f4dde7c />
<br/>
<br/>
If successful, right click on the start menu and click on the 'System' option. <br/>
<img src=https://github.com/user-attachments/assets/ba065ae4-58a0-43bc-bc0c-81b1303f46c1 />
<br/>
<br/>
Click 'Rename this PC (advanced)', click 'Change...', then change the 'Member of' Option from Workgroup to Domain, and enter your domain in the box. <br/>
<img src=https://github.com/user-attachments/assets/4020324f-6f8c-4e38-8d79-5bbe60be343a />
<br/>
<br/>
Enter your credentials for the DC VM, which is [Your Domain here]\[Your username]. If successful, a dialoge box will appear. Then, restart the VM. <br/>
<img src=https://github.com/user-attachments/assets/cd55143b-d522-4ed5-986a-df9b638268e5 />
<br/>
<br/>
Sign back into the 'Client' VM once finished, now using the same login as the one you would use to log into the DC VM. <br/>
<br/>
<br/>
Back on the DC VM, open the window for Active Directory Users and Computers, then right click on your domain tree and refresh. <br/>
<img src=https://github.com/user-attachments/assets/cdb9eb8d-6f76-4070-b5d1-d3ea4e136d76 />
<br/>
<br/>
Press on the Dropdown arrow, then open the 'Computers' Folder to confirm the 'Client' VM is listed. If so, you've set up a basic Active Directory! <br/>
<img src=https://github.com/user-attachments/assets/da639b52-244e-476c-883c-c88eb898ff1f />
<br/>
<br/>






















