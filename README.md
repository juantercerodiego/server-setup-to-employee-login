<p align="center">
<img width="750" height="340" alt="what-is-active-directory-and-why-is-it-used" src="https://github.com/user-attachments/assets/a7707de8-8111-4851-a1d1-d536d941249a" />
</p>

<h1>Active Directory & User Management</h1>
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
<img width="1001" height="550" alt="step 1" src="https://github.com/user-attachments/assets/5d0d973a-0b01-443d-a542-1eaca247c96a" />




</p>
<p>
  
**Before managing any users, I needed to turn my basic Windows Server into a master Domain Controller.**
  
**1:** Logged into the Windows Server VM using Remote Desktop.
  
**2:** Opened Server Manager, clicked Add Roles and Features, and clicked Next until reaching Server Roles.

**3:** Checked the box for Active Directory Domain Services (AD DS), accepted the required features, and hit Install.

**4:** Once the install finished, I clicked the Yellow Notification Flag at the top right of the screen and selected Promote this server to a domain controller.

**5:** Chose Add a new forest, named my root domain (like mydomain.com), set a recovery password, and let the wizard finish and reboot the server.
</p>
<br />
<h2>Step 2: Creating the Org Chart (Organizational Units) </h2>
<p>
<img width="783" height="500" alt="Screenshot 2026-05-13 115239" src="https://github.com/user-attachments/assets/269985ec-2a11-4ad2-a58f-f8af5521ac7c" />

</p>
<p>
To keep things tidy, I built an "Org Chart" inside the system. By creating these folders (Organizational Units), I can group employees by their department, making it much easier to manage their permissions and access later on.
</p>
<br />
<h2>Step 3: Issuing Digital IDs (User Management)</h2>
<p>
<img width="808" height="548" alt="Screenshot 2026-05-13 120309" src="https://github.com/user-attachments/assets/5f565de1-eace-4bd0-bdf0-4ee7670fff02" />



</p>
<p>
This is where I create the actual employee accounts. I set up unique usernames and temporary passwords so new hires can log into the network securely.
</p>
<br />
<h2>Step 4: Joining the Network (Connecting the Workstation)</h2>
<p>
<img width="623" height="570" alt="Screenshot 2026-05-13 123209" src="https://github.com/user-attachments/assets/f2ffb586-702b-463e-9161-3ca84411c913" />



</p>
<p>
The final step is "introducing" the employee's computer to the server. Once the workstation is joined to the domain, the server is officially in charge. This allows any authorized employee to sit down at that computer and log in with their company ID.
</p>
<br />

