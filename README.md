<p align="center">
<img width="750" height="340" alt="what-is-active-directory-and-why-is-it-used" src="https://github.com/user-attachments/assets/a7707de8-8111-4851-a1d1-d536d941249a" />
</p>

<h1>Active Directory & User Management</h1>
This project shows how I set up and managed a company’s "Digital ID Office." I used Active Directory to create user accounts, organize them into departments, and manage their access to the company's network.<br />




<h2>Environments and Technologies Used</h2>

- **Microsoft Azure** (Virtual Machines)
- **Remote Desktop** (RDP)
- **Active Directory Domain Services** (AD DS)
- **Windows Server 2022** (The Domain Controller)
- **Remote Desktop** (RDP)

<h2>Operating Systems Used </h2>

- **Windows Server 2022** (The "Brain" of the network)
- **Windows 11** (The Employee Workstation)

<h2>List of Prerequisites</h2>

- **Step 1:** Building the Server (The Domain Controller)
- **Step 2:** Building the "Org Chart" (Organizational Units)
- **Step 3:** Issuing Digital IDs (User Management)
- **Step 4:** Joining the Network (Connecting the Workstation)
<h2>Deployment and Configuration Steps</h2>
<h2>Step 1: Building the Server (The Domain Controller)</h2>

<p>
<img width="927" height="615" alt="image" src="https://github.com/user-attachments/assets/cabfd231-293a-4f8b-b349-04b105e4e304" />



</p>
<p>
Before you can manage a company, you need a central hub. I set up a Windows Server in Azure and promoted it to a "Domain Controller." This makes it the master computer that holds all the rules and account info for the entire organization.
</p>
<br />
<h2>Step 2: Building the "Org Chart" (Organizational Units) </h2>
<p>
<img width="1299" height="800" alt="Screenshot 2026-05-11 113026" src="https://github.com/user-attachments/assets/d2dab1b5-1f6b-4f64-b95a-fdaffd16b113" />
</p>
<p>
To keep things tidy, I built an "Org Chart" inside the system. By creating these folders (Organizational Units), I can group employees by their department, making it much easier to manage their permissions and access later on.
</p>
<br />
<h2>Step 3: Issuing Digital IDs (User Management)</h2>
<p>
<img width="946" height="550" alt="Screenshot 2026-05-11 115129" src="https://github.com/user-attachments/assets/aebc1f03-8b13-4599-8a61-b2b0aae9603a" />


</p>
<p>
This is where I create the actual employee accounts. I set up unique usernames and temporary passwords so new hires can log into the network securely.
</p>
<br />
<h2>Step 4: Joining the Network (Connecting the Workstation)</h2>
<p>
<img width="1415" height="700" alt="Screenshot 2026-05-11 170436" src="https://github.com/user-attachments/assets/c38cbf38-5817-45be-86fc-188a450cfb0a" />


</p>
<p>
The final step is "introducing" the employee's computer to the server. Once the workstation is joined to the domain, the server is officially in charge. This allows any authorized employee to sit down at that computer and log in with their company ID.
</p>
<br />

