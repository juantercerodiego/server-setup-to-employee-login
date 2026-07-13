<p align="center">
<img width="750" height="340" alt="what-is-active-directory-and-why-is-it-used" src="https://github.com/user-attachments/assets/b4bd93fc-9939-498e-b2dd-2ec1fa64b737" />
</p>

<h1>Active Directory & User Management (Azure): From Server Setup to Employee Login</h1>

**Quick Note:** This project builds on top of my cloud network setup. If you want to see how I configured the virtual machines and networks first, check out that guide here: [https://github.com/juantercerodiego/azure-vm-network-setup](https://github.com/juantercerodiego/azure-vm-network-setup).

This project is all about setting up the central "brain" of a company's network. I deployed a Windows Server in Azure, turned it into a Domain Controller, created organized departments, used a PowerShell script to bulk-create thousands of employee accounts, and finally linked a Windows 11 workstation to the domain to test a user login.<br />

<h2>Environments and Technologies Used</h2>

- **Microsoft Azure** (Virtual Machines)
- **Remote Desktop** (RDP)
- **Active Directory Domain Services** (AD DS)
- **PowerShell** (For Automation Scripting)

<h2>Operating Systems Used </h2>

- **Windows Server 2022** (The Server-VM)
- **Windows 11** (The Client-VM Workstation)

<h2>What You Need Before Starting (Prerequisites)</h2>

- **An Azure Account:** You need an active subscription to build the virtual machines.
- **A Virtual Network (VNet):** A configured digital space in Azure so your machines can communicate.
- **A Windows Server VM (Server-VM):** This acts as the backbone of the project where Active Directory is installed.
- **A Windows 11 Client VM (Client-VM):** A separate machine to act as the employee workstation for testing.

<br />

---

<h2>How I Built It (Step-by-Step)</h2>

<h2>Step 1: Installing Active Directory & Promoting the Server</h2>

**Before managing any users, I needed to establish a Remote Desktop connection and turn my basic Windows Server into a master Domain Controller.**

1. Opened the **Remote Desktop Connection (RDP)** app on my physical computer.
2. Entered the **Public IP address** of the **Server-VM**, inputted the local administrator credentials I created during deployment, and accepted the security certificate to log into the desktop interface.
3. Opened **Server Manager**, clicked **Add Roles and Features**, and clicked Next until reaching Server Roles.
4. Checked the box for **Active Directory Domain Services (AD DS)**, accepted the required features, and hit Install.

<p align="center">
<img width="1031" height="600" alt="Screenshot 2026-06-09 103049" src="https://github.com/user-attachments/assets/7a2f0987-93d2-498e-ad06-71673154c484" />
</p>

5. Once the installation finished, I clicked the **Yellow Notification Flag** at the top right of the Server Manager screen and selected **Promote this server to a domain controller**.
6. Selected **Add a new forest**, configured my root domain name (such as `mydomain.com`), set a Directory Services Restore Mode (DSRM) password, and allowed the setup wizard to finish configuration, which automatically rebooted the **Server-VM**.

<p align="center">
<img width="1318" height="600" alt="Screenshot 2026-06-09 103932" src="https://github.com/user-attachments/assets/30e58e1b-4eba-4f5f-aa88-11bc6bc1a2d5" />
</p>

<br />

---

<h2>Step 2: Creating the Org Chart (Organizational Units)</h2>

**With the domain controller online, I re-established my RDP session to the Server-VM to build out the company's organizational chart using Organizational Units (OUs) to keep departments structured.**

1. On the **Server-VM**, navigated to **Server Manager** -> **Tools** -> **Active Directory Users and Computers**.
2. Right-clicked the domain name (`mydomain.com`), highlighted **New**, and selected **Organizational Unit**.

<p align="center">
<img width="941" height="500" alt="2A" src="https://github.com/user-attachments/assets/90e0d106-6f43-4769-a3de-0d68dacf4707" />
</p>

3. Created a primary parent organizational unit folder named **`_Employees`**.
4. Inside the `_Employees` folder, right-clicked again to create independent departmental sub-folders named **`_ADMINS`**, **`_ACCOUNTING`**, and **`_IT`**.

<p align="center">
<img width="952" height="500" alt="2B" src="https://github.com/user-attachments/assets/0f13a425-8c84-4e0f-a977-bd3b8b3d1669" />
</p>

<br />

---

<h2>Step 3: Mass-Creating Users with a PowerShell Script</h2>

**Instead of spending days manually typing in names and creating accounts one by one, I used automation inside the Server-VM to spin up thousands of dummy employee accounts in seconds.**

1. On the **Server-VM**, opened **PowerShell ISE** explicitly as an Administrator.
2. Opened the automated user-generation script block, which programmatically generates distinct user identities and points directly to the `_Employees` folder path.

#### **The Automation Script Used:**
```powershell
# ----- Edit these Variables for your own Use Case ----- #
$PASSWORD_FOR_USERS   = "Password1"
$NUMBER_OF_ACCOUNTS_TO_CREATE = 10000
# ------------------------------------------------------ #

Function generate-random-name() {
    $consonants = @('b','c','d','f','g','h','j','k','l','m','n','p','q','r','s','t','v','w','x','z')
    $vowels = @('a','e','i','o','u','y')
    $nameLength = Get-Random -Minimum 3 -Maximum 7
    $count = 0
    $name = ""

    while ($count -lt $nameLength) {
        if ($($count % 2) -eq 0) {
            $name += $consonants[$(Get-Random -Minimum 0 -Maximum $($consonants.Count - 1))]
        }
        else {
            $name += $vowels[$(Get-Random -Minimum 0 -Maximum $($vowels.Count - 1))]
        }
        $count++
    }

    return $name
}

$count = 1
while ($count -lt $NUMBER_OF_ACCOUNTS_TO_CREATE) {
    $fisrtName = generate-random-name
    $lastName = generate-random-name
    $username = $fisrtName + '.' + $lastName
    $password = ConvertTo-SecureString $PASSWORD_FOR_USERS -AsPlainText -Force

    Write-Host "Creating user: $($username)" -BackgroundColor Black -ForegroundColor Cyan
    
    New-AdUser -AccountPassword $password `
               -GivenName $fisrtName `
               -Surname $lastName `
               -DisplayName $username `
               -Name $username `
               -EmployeeID $username `
               -PasswordNeverExpires $true `
               -Path "ou=_EMPLOYEES,$(([ADSI]`"").distinguishedName)" `
               -Enabled $true$count++
}
```
3. Ran the execution block and observed the active host screen outputting the creation loop of the distinct usernames.
4. Navigated back to **Active Directory Users and Computers** on the **Server-VM** and refreshed the main **`_EMPLOYEES`** directory to verify that the target accounts populated successfully.

<p align="center">
<img width="982" height="500" alt="Screenshot 2026-06-10 115839" src="https://github.com/user-attachments/assets/a2095584-42dd-405b-b758-66da5f8c8948" />
</p>

<br />

---

<h2>Step 4: Connecting the Windows 11 Workstation to the Domain</h2>

**Next, I needed to configure the network dependency links so the separate Client-VM could recognize and join the active domain managed by the Server-VM.**

1. Checked the **Server-VM**'s internal networking properties to find its static Private IP address.
2. Logged into the external Azure Portal, navigated to the **Client-VM** properties page, and opened **Networking** -> **Network Interface** -> **DNS Servers**. Toggled the selection to **Custom** and input the **Server-VM**'s Private IP address so the workstation looks directly to the domain controller for name resolution.
3. Opened an RDP connection to log into the **Client-VM**. Opened the Windows start menu, searched for **About your PC**, and selected **Advanced system settings**.

<p align="center">
<img width="903" height="500" alt="Screenshot 2026-06-10 163233" src="https://github.com/user-attachments/assets/84e78148-ccee-4646-afb2-8881f647aa70" />
</p>

4. Navigated to the **Computer Name** properties tab, selected **Change...**, modified the member check box from Workgroup to **Domain**, typed in my root domain identity (`mydomain.com`), and selected OK.
5. Provided the secure **Server-VM** domain administrator credentials when prompted by the network challenge popup, received the official confirmation welcoming the machine to the domain, and authorized a system restart on the **Client-VM**.

<p align="center">
<img width="660" height="550" alt="Screenshot 2026-06-11 120848" src="https://github.com/user-attachments/assets/d00d803e-e24f-445a-b5e0-d1571428b7ee" />
</p>

<br />

---

<h2>Step 5: Testing the Employee Login</h2>

**The final verification step to confirm operational success involves establishing an enterprise network log-in using a generated account on the connected Client-VM workstation.**

1. Opened the **Remote Desktop Connection** program from my physical computer workstation and targeted the **Client-VM**'s Public IP address.
2. Switched the connection credentials options, typing in the explicit domain credentials of a single randomly generated script account (such as `mydomain\dogi.cug`) alongside the default set password.

<p align="center">
<img width="1077" height="697" alt="Screenshot 2026-06-15 120048" src="https://github.com/user-attachments/assets/fa5ad7fd-843a-42f6-8c91-c31f0257d04b" />
</p>

3. Once logged into the profile workspace on the **Client-VM**, accessed the Windows launcher, searched for **Command Prompt**, and booted the utility interface.
4. Input the terminal verification command `whoami` and hit enter. The screen successfully returned a response reading **`mydomain\dogi.cug`**, confirming that the client environment is talking to the cloud-hosted domain infrastructure.

<p align="center">
<img width="862" height="545" alt="Screenshot 2026-06-15 121130" src="https://github.com/user-attachments/assets/f94dc9e3-d50a-4039-ba68-b89532a86397" />
</p>



