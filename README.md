<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<!--
<h2>Video Demonstration</h2>
--
- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)
-->

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines;Domain Controller/Client PC)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Domain Controller and Client within a VNET
- Set a static IP for the DC
- Set DNS on Client VM
- Install Active Directory
- Create Users
- Perform Simulated Scenarios

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/SwZBdko.png" height="80%" width="80%"/>
</p>
<p>
Create the Domain Controller (DC) VM
</p>
<br />

<p>
<img src="https://i.imgur.com/T0wWexA.png" height="80%" width="80%"/>
</p>
<p>
Create the Client VM
</p>
<br />

<p>
<img src="https://i.imgur.com/ru3aa1C.png" height="80%" width="80%"/>
</p>
<p>
Set the DC to a Static IP
</p>
<br />

<p>
<img src="https://i.imgur.com/uAHZrg1.png" height="80%" width="80%"/>
</p>
<p>
Confirm that the Client and DC are both in the same VNET 
</p>
<br />

<p>
<img src="https://i.imgur.com/e5ta2Sq.png" height="80%" width="80%"/>
</p>
<p>
Open Windows Defender Firewall>Click on Inbound Rules>Sort by Protocol>Enable the two rules shown.<br>
This will insure that that the Client and communicate with the DC
</p>
<br />

<p>
<img src="https://i.imgur.com/6DWUEkJ.png" height="80%" width="80%"/>
</p>
<p>
Install Active Directory on the DC
</p>
<br />

<p>
<img src="https://i.imgur.com/ZknKnK0.png" height="80%" width="80%"/>
</p>
<p>
Finish installing Active Directory Domain Services. After the installation is complete, your machine will reboot. Log back in to proceed.
</p>
<br />

<p>
<img src="https://i.imgur.com/ca8R6BN.png" height="80%" width="80%"/>
</p>
<p>
When you go to log back in, you'll need to make sure you use the domain name you created to log in to the machine
</p>
<br />

<p>
<img src="https://i.imgur.com/v27QxrX.png" height="80%" width="80%"/>
</p>
<p>
For this example lab, we'll create two organizational units: _EMPLOYEES, and _ADMINS <br>
Once those organizational units are created, create a new user in the _ADMINS folder
</p>
<br />

<p>
<img src="https://i.imgur.com/kRmwwkD.png" height="80%" width="80%"/>
</p>
<p>
Be sure to give that user admin access
</p>
<br />

<p>
<img src="https://i.imgur.com/FIzlVcf.png" height="80%" width="80%"/>
</p>
<p>
Log out of the DC and log back into the DC as the newly created admin user
</p>
<br />

<p>
<img src="https://i.imgur.com/nmT95PU.png" height="80%" width="80%"/>
</p>
<p>
Set the DC aside for now. We're going to configure the Client's DNS settings in Azure to the DC's static IP.
</p>
<br />

<p>
<img src="https://i.imgur.com/kU1JfnP.png" height="80%" width="80%"/>
</p>
<p>
Log into the Client VM. We're going to add it to the network. System>Rename this PC (advanced)>Change>Select Domain and input the domain name you created for your organization. <br>
After accepting and applying the changes, you'll be asked to log in with admin credntials to confirm the change. You can use the admin you created in the previous steps. Accept and confirm the changes and restart the Client machine.<br>
Congrats, you've now joined the Client machine to the domain. So, any user within the domain will now be able to log into the Client machine - assuming you've given them permissions to do so. <br>
Next, we'll create many "dummy" user accounts that will be able to access the Client machine.
</p>
<br />

<p>
<img src="https://i.imgur.com/K3Op64t.png" height="80%" width="80%"/>
</p>
<p>
Before creating the multiple user accounts. I logged back into the Client to make sure everyone in the domain has access to the Client machine as noted above.
</p>
<br />

<p>
<img src="https://i.imgur.com/t7dARn4.png" height="80%" width="80%"/>
</p>
<p>
-Now, to create a large amount of "dummy" users, we're going to use a script from [github](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1).<br>
-Copy the code from the Raw file.<br>
-In your DC machine, search for PowerShell ISE and right-click PowerShell ISE to Open as Administrator.<br>
-Create a new file and paste the script. NOTE* The script defaults to create 10,000 user accounts. I change it to 500.<br>
-Finally, run the script (F5) and the users will output to "_EMPLOYEES" Organizational Unit.
</p>
<br />

<p>
<img src="https://i.imgur.com/eN45Xac.png" height="80%" width="80%"/>
</p>
<p>
CONGRATS! You can now log in to the Client machine with any of these _EMPLOYEE users.<br><br>
  Try it out!
</p>
<br />
