<p align="center">
<img width="750" height="340" alt="what-is-active-directory-and-why-is-it-used" src="https://github.com/user-attachments/assets/a7707de8-8111-4851-a1d1-d536d941249a" />
</p>

<h1>Active Directory & User Management (Azure): From Server Setup to Employee Login</h1>

**Quick Note:** This project builds on top of my cloud network setup. If you want to see how I configured the virtual machines and networks first, check out that guide here: [Link to your Azure VM Setup Repo].
</p>
This project is all about setting up the central "brain" of a company's network. I deployed a Windows Server in Azure, turned it into a Domain Controller, created organized departments, used a PowerShell script to bulk-create thousands of employee accounts, and finally linked a Windows 10 workstation to the domain to test a user login.<br />




<h2>Environments and Technologies Used</h2>

- **Microsoft Azure** (Virtual Machines)
- **Remote Desktop** (RDP)
- **Active Directory Domain Services** (AD DS)
- **Powershell** (For Automation Scripting)

<h2>Operating Systems Used </h2>

- **Windows Server 2022** (The "Brain" of the network)
- **Windows 11** (The Employee Workstation)

<h2>What You Need Before Starting (Prerequisites)</h2>

- **An Azure Account:** You need an active subscription to build the virtual machines.
- **A Virtual Network (VNet):** A configured digital space in Azure so your machines can communicate.
- **A Windows Server VM:** This acts as the backbone of the project where Active Directory is installed.
- **A Windows 11 Client VM:** A separate machine to act as the employee workstation for testing.
<h2>How I Built It (Step-by-Step)</h2>
<h2>Step 1: Installing Active Directory & Promoting the Server</h2>

<p>
<img width="1031" height="600" alt="Screenshot 2026-06-09 103049" src="https://github.com/user-attachments/assets/7a2f0987-93d2-498e-ad06-71673154c484" />





</p>
<p>
  
**Before managing any users, I needed to turn my basic Windows Server into a master Domain Controller.**
  
**1:** Logged into the Windows Server VM using Remote Desktop.
  
**2:** Opened Server Manager, clicked Add Roles and Features, and clicked Next until reaching Server Roles.

**3:** Checked the box for Active Directory Domain Services (AD DS), accepted the required features, and hit Install.

**4:** Once the install finished, I clicked the Yellow Notification Flag at the top right of the screen and selected Promote this server to a domain controller.

**5:** Chose Add a new forest, named my root domain (like mydomain.com), set a recovery password, and let the wizard finish and reboot the server.

<img width="1318" height="600" alt="Screenshot 2026-06-09 103932" src="https://github.com/user-attachments/assets/30e58e1b-4eba-4f5f-aa88-11bc6bc1a2d5" />

</p>
<br />
<h2>Step 2: Creating the Org Chart (Organizational Units) </h2>
<p>
<img width="941" height="500" alt="2A" src="https://github.com/user-attachments/assets/90e0d106-6f43-4769-a3de-0d68dacf4707" />

</p>
<p>
  
**With the server upgraded, I needed to build out the company's "org chart" using folders called Organizational Units (OUs) to keep the departments separated.**
  
**1:** On the rebooted server, went to Server Manager -> Tools -> Active Directory Users and Computers.
  
**2:** Right-clicked my domain name, went to New -> Organizational Unit.

**3:** Created a main folder named _Employees.

**4:** Inside that new folder, I right-clicked again to make sub-folders for different departments: _ADMINS, _ACCOUNTING, and _IT.
<img width="952" height="500" alt="2B" src="https://github.com/user-attachments/assets/0f13a425-8c84-4e0f-a977-bd3b8b3d1669" />


</p>
<br />
<h2>Step 3: Mass-Creating Users with a PowerShell Script</h2>
<p>
<img width="1285" height="660" alt="Screenshot 2026-06-10 115024" src="https://github.com/user-attachments/assets/d3e4bf3a-18ed-43b7-a85a-5357960d4ac0" />




</p>
<p>
  
**Instead of spending days manually typing in names and creating accounts one by one, I used automation to spin up hundreds of dummy accounts in seconds**
  
**1:** Opened PowerShell ISE as an Administrator on the server. ( Windows Server )
  
**2:** Opened the lab's user-generation script that pulls names from a .csv file and assigns them to our _Employees folder.

**3:** Run the script and watch the host screen loop through and output the newly generated usernames.

**4:** Went back to Active Directory Users and Computers and refreshed the folders to verify all the new employees were sitting in their proper spots.
<img width="982" height="500" alt="Screenshot 2026-06-10 115839" src="https://github.com/user-attachments/assets/a2095584-42dd-405b-b758-66da5f8c8948" />


</p>
<br />
<h2>Step 4: Connecting the Windows 10 Workstation to the Domain</h2>
<p>
<img width="623" height="570" alt="Screenshot 2026-05-13 123209" src="https://github.com/user-attachments/assets/f2ffb586-702b-463e-9161-3ca84411c913" />



</p>
<p>
  
**Next, I had to "introduce" the employee's computer to the server so the domain could take control of it.**
  
**1:** Switched over and logged into the Windows 10 Client VM.
  
**2:** Opened network adapter settings, changed the Preferred DNS Server to match the Private IP Address of my Windows Server, and saved it. (This points the client directly to our Domain Controller).

**3:** Opened the Windows menu, searched for About your PC, and clicked Advanced system settings.

**4:** Went to the Computer Name tab, clicked Change..., toggled the member settings from Workgroup to Domain, typed my domain name, and hit OK.

**5:** Logged in with the Server’s Admin credentials when the prompt popped up, got the "Welcome to the domain" message, and restarted the PC.

</p>
<br />
<h2>Step 5: Testing the Employee Login</h2>
<p>
<img width="623" height="570" alt="Screenshot 2026-05-13 123209" src="https://github.com/user-attachments/assets/f2ffb586-702b-463e-9161-3ca84411c913" />



</p>
<p>
  
**The final test to prove the setup works perfectly is logging into the client computer using one of the random user accounts created by the script.**
  
**1:** On the restarted Windows 10 login screen, clicked Other User in the bottom left corner.
  
**2:** Typed in the username of one of the script-created users (like jdoe) and their password.

**3:** Opened the Windows menu, searched for About your PC, and clicked Advanced system settings.

**4:** Verified that the command returned mydomain\jdoe, proving the workstation is fully communicating with our cloud Active Directory server.




