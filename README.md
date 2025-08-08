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

- Setup Domain Controller and Client in Azure
- Install Active Directory
- Create a Domain Admin user within the domain
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="746" height="274" alt="Screenshot 2025-08-07 123359" src="https://github.com/user-attachments/assets/fcbcab9a-a436-49e5-b30a-422656942baf" />


</p>
<p>
In Microsoft Azure, Create a Resource group, A Virtual Network and subnet. Inside of The virtual network, Create a Domain controller Virtual Machine with Windows Server 20222, name it "DC-1".


</p>
<br />


<p>
  <img width="1436" height="744" alt="Screenshot 2025-08-07 124336" src="https://github.com/user-attachments/assets/3763ac03-56e8-4d0f-9fcf-c0ec9ae9b6f2" />
  After you've created the VM, set its NIC Private address to be static. (go to DC-1 -> Network settings -> Click on the Network interface -> Click on ipconfig1 at the bottom of the page -> set Allocation to "Static".
 <p>
   <img width="785" height="640" alt="Screenshot 2025-08-07 133250" src="https://github.com/user-attachments/assets/b04b82ba-5dd9-40f6-bf42-4e96df3d75cb" />

  Next, Log into the DC-1 VM and open windows firewall (right click start menu -> select "Run" -> type in "wf.msc") in the firewall, select "Windows Defender Firewall Properties" and turn off the firewall state for Domain, Private, and Public proflie.
</p>
<br />

<p>
<img width="915" height="636" alt="Screenshot 2025-08-07 133632" src="https://github.com/user-attachments/assets/98e58d8d-a732-4228-b2be-d1c4d9d5cdd6" />

</p>
<p>
Create another VM with the Windows 10 image and name it Client-1, Make sure it is on the same region and Virtual Network as DC-1. Once you have made the VM, set its DNS settings to DC-1s Private IP address. (copy DC-1 private ip address in microsoft azure, go to client-1 VM -> Netowrking Settiings -> Network interface -> DNS servers -> select custom, then paste th Private IP address). Once that is completed, restart the Client-1 VM from Azure Portal, then log into Client-1, open Powershell, and run the ping command with DC-1's Private IP Adress.


</p>
<br />

<p>
<img width="1092" height="767" alt="Screenshot 2025-08-07 164215" src="https://github.com/user-attachments/assets/44341ea2-24e8-4c47-9e5b-27d6adc019d9" />

</p>
<p>
Installing Active Directory: Log into DC 1 and install "Active Directory Domain Services" (open Windows Start menu, open "Server Manager" -> Add roles and features -> navigate to "Server Roles" and mark the box called "Active directory Domain Services", Contnue pressing next through the rest of the tabs, and then install.

<p>
  <img width="1542" height="690" alt="image" src="https://github.com/user-attachments/assets/fa9d2b37-2277-48e2-9e95-87a3995fc0e6" />

</p>
Next, Click on the flag on the top right of the server manager, and click "Promote this server to a domain controller", Select "Add a new forest", set the name as "mydomain.com", and set your password on the next page. After you set the password, you can navigate through the wizard without changing anything else, once you get to the prerequisites check, you can select install. Afer its installed, log out of the VM and log back in with the username "mydomain.com\labuser"

<p>
<img width="1333" height="964" alt="Screenshot 2025-08-08 104235" src="https://github.com/user-attachments/assets/9cfd4011-f369-4fa2-a2bf-b6ff5fe74576" />


</p>
<p>
Once logged back into DC-1, open "active directory users and computers" in the windows start menu. In the ADUC window, right click "mydomain.com", select New -> Organizational Unit (OU) and name it "_EMPLOYEES",then create another OU named "_ADMINS". Right click _ADMINS and create a new user with the name "jane Doe", set the username as "jane_admin" and set a password you can remember(ex. Cyberlab123!). Next, locate the new user in "_ADMINS", Right click the user and select properties, select "Member of", and enter the name "domain admins", then click the "Check Names" option, Make sure to click "OK" and "Apply" once you have added the domain admins user. Once you have completed the last step, log out of DC-1 and log back in as "mydomain.com\jane_admin"


</p>
<br />

<p>
<img width="1123" height="866" alt="Screenshot 2025-08-08 110857" src="https://github.com/user-attachments/assets/18824156-ae93-42e9-a997-a694226aeee2" />


</p>
<p>
Log in to your Windows 10 VM (client-1), open Settings -> About -> on the right side, Click "Rename this PC" -> under the Computer Name tab, Click Change -> Select member of "Domain" and type in "mydomain.com" and select OK, Set the username to "mydomain.com\jane_admin" and use the same password previously used (Cyberlab123!). Once completed, you will have to restart the VM, after the VM closes, log back into DC-1 VM and go into ADUC -> mydomain.com -> Computers, and make sure client-1 is inside the folder. Inside ADUC, right click mydomain.com and create a new OU, name it "_CLIENTS", go into the computers folder and drag clent-1 into the new folder.

</p>
<br />
