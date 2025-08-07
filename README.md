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

- Setup Domain Controller in Azure
- Setup Client-1 in Azure
- Step 3
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
  After you've created the VM, set its NIC Private address to be static. (go to DC-1 -> Network settings -> Click on the Network interface -> Click on ipconfig1 at the bottom of the page -> set Allocation to "Static". Next, Log into the DC-1 VM and open windows firewall (right click start menu -> select "Run" -> type in "wf.msc") in the firewall, select "Windows Defender Firewall Properties" and turn off the firewall state for Domain, Private, and Public proflie.
</p>
<br />

<p>
<img width="915" height="636" alt="Screenshot 2025-08-07 133632" src="https://github.com/user-attachments/assets/98e58d8d-a732-4228-b2be-d1c4d9d5cdd6" />

</p>
<p>
Create another VM with the Windows 10 image and name it Client-1, Make sure it is on the same region and Virtual Network as DC-1. Once you have made the VM, set its DNS settings to DC-1s Private IP address. (copy DC-1 private ip address in microsoft azure, go to client-1 VM -> Netowrking Settiings -> Network interface -> DNS servers -> select custom, then paste th Private IP address). Next, restart the Client-1 VM from Azure Portal, then log into Client-1 and run the ping command with DC-1's Private IP Adress.


</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create another VM with the Windows 10 image and name it Client-1, Make sure it is on the same region and Virtual Network as DC-1. Once you have made the VM, set its DNS settings to DC-1s Private IP address.
