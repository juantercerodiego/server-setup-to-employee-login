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

- **A Domain Controller:** A server acting as the central hub for the network.
- **Network Connection:** Ensuring the employee computer can "see" and talk to the server.
- **Admin Access:** Permission to create and delete users.
<h2>Management Steps</h2>
<h2>Step 1: Building the "Org Chart" (Organizational Units)</h2>

<p>
<img width="927" height="615" alt="image" src="https://github.com/user-attachments/assets/cabfd231-293a-4f8b-b349-04b105e4e304" />



</p>
<p>
Before adding people, you need a way to organize them. I created "Folders" (Organizational Units) that match the company's departments. This makes it easy to apply rules to a whole group of people at once instead of one by one.
</p>
<br />
<h2>Step 2: Issuing Digital IDs (Creating New Users) </h2>
<p>
<img width="1299" height="800" alt="Screenshot 2026-05-11 113026" src="https://github.com/user-attachments/assets/d2dab1b5-1f6b-4f64-b95a-fdaffd16b113" />
</p>
<p>
This is where I create the actual accounts for employees. Just like getting a badge at a real office, these accounts give employees a unique username and password so they can log into any computer on the company network.
</p>
<br />
<h2>Step 3: Joining the Network (Connecting the Workstation)</h2>
<p>
<img width="946" height="550" alt="Screenshot 2026-05-11 115129" src="https://github.com/user-attachments/assets/aebc1f03-8b13-4599-8a61-b2b0aae9603a" />


</p>
<p>
A computer doesn't just "know" it belongs to a company. I had to manually "introduce" the employee's computer to the server. Once they are linked, the server can manage that computer and keep it secure.
</p>
<br />
<h2>Step 4: The First Login (Verification)</h2>
<p>
<img width="1415" height="700" alt="Screenshot 2026-05-11 170436" src="https://github.com/user-attachments/assets/c38cbf38-5817-45be-86fc-188a450cfb0a" />


</p>
<p>
I just finished the final check. By logging in with a new account, I’ve confirmed that the Digital ID Office is correctly managing users and workspaces.
</p>
<br />

