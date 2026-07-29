<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployment on Azure </h1>
This repository contains instructions and configurations for deploying an on-premises Active Directory environment on Azure Virtual Machines. The steps outlined in this repository demonstrate the setup and management of Active Directory Domain Services within a cloud-based environment.<br />


<h2>Environments and Technologies Used</h2>

<img src="https://skillicons.dev/icons?i=azure,windows,powershell" />

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell
- RDP

<h2>Operating Systems Used </h2>

- Windows Server 2025 (x64 Gen2)
- Windows 11 pro Virtual Machine(25H2)(x64 Gen2)(2 vCPUs)

<h2>Key Actions </h2> 

- Install Active Directory
- Create Organizational Units for Employees and Admins
- Create Domain Admin account
- Join the client VM to the domain
- Configure Remote Desktop access for domain users
- Automate bulk user creation with PowerShell

> [!NOTE] 
>This project builds upon a prior lab where the Azure environment, virtual machines, Active Directory Domain Services, and DNS configuration were initially deployed. <br /> [Step 1: Active Directory: Preparing AD Infrastructure in Azure](https://github.com/Ernanm280/preparing-ad-inf-azure)


<h2>Deployment and Configuration Steps</h2>

**1. Install Active Directory**
---

<p>
To install Active Directory on the domain controller, I returned to the **dc-1** VM and navigated to the **Server Manager** dashboard.
</p>
<p>
<img width="473" height="583" alt="Screenshot 2026-07-25 091327" src="https://github.com/user-attachments/assets/ffae5af8-e1bc-47ba-868f-5050a5d1444c" />
</p>
<br />

<h2></h2>

<p>
<img width="952" height="510" alt="Screenshot 2026-07-25 091415" src="https://github.com/user-attachments/assets/6788fe48-c83e-40ba-80ca-55a9c3183faf" />
</p>
<p>
Proceed by selecting option 2, **Add roles and features**. Select **Next** until you reach **Server Roles**. In Server roles, select **Active Directory Domain Services (AD DS)** under **Server Roles**. Upon selection, I was prompted to add the required features, including Group Policy Management and Remote Server Administration Tools. I clicked **Add Features** and ensured that management tools were included to enable full administrative functionality.
</p>
<br />

<h2></h2>

<p>
<img width="587" height="415" alt="Screenshot 2026-07-25 091438" src="https://github.com/user-attachments/assets/be99694d-9187-44fb-b1c1-755322ca335d" />
</p>
<p>
Select **Next** until you reach **Server Roles**. In Server roles, select **Active Directory Domain Services (AD DS)** under **Server Roles**. Upon selection, I was prompted to add the required features, including Group Policy Management and Remote Server Administration Tools. Click **Add Features** and ensure that management tools were included to enable full administrative functionality.
</p>
<br />

<h2></h2>

<p>
<img width="587" height="418" alt="Screenshot 2026-07-25 091517" src="https://github.com/user-attachments/assets/c3663eda-e7c3-4e05-a53d-5a7d39cdcfe9" />
</p>
<p>
I proceeded through the Features and AD DS informational pages by selecting **Next**. On the Confirmation screen, I enabled “Restart the destination server automatically if required” to ensure a smooth installation process, then clicked **Install** to begin deploying Active Directory Domain Services.
</p>
<br />

<h2></h2>

<p>
<img width="397" height="202" alt="Screenshot 2026-07-25 091705" src="https://github.com/user-attachments/assets/47bb9a31-1248-4f68-b420-61d4e833c37d" />
</p>
<p>
After the installation was completed, a notification appeared in Server Manager indicating that additional configuration was required. I selected **“Promote this server to a domain controller”** to begin setting up Active Directory and converting the server into a Domain Controller.
</p>
<br />

<h2></h2>

<p>
<img width="571" height="426" alt="Screenshot 2026-07-25 091742" src="https://github.com/user-attachments/assets/afd6ba3b-4046-4b9a-83a2-f7e77dfe0417" />
</p>
<p>
From Server Manager, select **“Promote this server to a domain controller.”** In the Deployment Configuration screen, choose **“Add a new forest”** and enter **“mydomain.com”** as the root domain name (the forest name can be customized as needed). Click **Next**.
</p>
<br />

<h2></h2>

<p>
<img width="568" height="434" alt="Screenshot 2026-07-25 091852" src="https://github.com/user-attachments/assets/ff8fdc2b-e00d-44b3-b89c-f93583c452f0" />
</p>
<p>
In the Domain Controller Options, create and confirm the **DSRM password**. Proceed by clicking **Next**. Ensure the **DNS Delegation** option is unchecked.
</p>
<br />

<h2></h2>

<p>
<img width="569" height="419" alt="Screenshot 2026-07-25 092049" src="https://github.com/user-attachments/assets/9030d422-59ee-4831-8fbe-759afad0fcce" />
</p>
<p>
Continue selecting **Next** through the remaining steps, then click **Install**. The virtual machine will complete the forest installation and automatically restart/sign out.
</p>
<br />

<h2></h2>

<p>
<img width="454" height="151" alt="Screenshot 2026-07-25 092309" src="https://github.com/user-attachments/assets/d7ed7f23-c2a4-4b7e-bb88-488255590ef1" />
</p>
<p>
The **dc-1** VM will restart.
</p>
<br />

<h2></h2>

<p>
<img width="287" height="110" alt="Screenshot 2026-07-25 092832" src="https://github.com/user-attachments/assets/57de8627-1e67-4290-882a-83c461f07fdf" />
</p>
<p>
<img width="556" height="591" alt="Screenshot 2026-07-25 092920" src="https://github.com/user-attachments/assets/06256b70-ffca-422e-af67-dd0301ca9fcf" />
</p>
<p>
Before remotely logging back in, in **Remote Desktop Client**, select **More options**. Under the username field, I specified the domain user in the format `mydomain.com\<yourcreatedcredentials>`, then selected **Connect**. I was prompted to enter the credentials, allowing me to log into the domain-joined machine successfully.
</p>
<br />

<h2></h2>

<p>
<img width="602" height="174" alt="Screenshot 2026-07-25 091415" src="https://github.com/user-attachments/assets/d1581840-0857-4bbb-a1e3-ab74c13130c2" />
</p>
<p>
After logging back into the Domain Controller, I reviewed the Server Manager Dashboard to confirm that both Active Directory Domain Services (AD DS) and DNS roles were successfully installed and are running properly.
</p>
<br />

<h2></h2>

**1. Create a Domain Admin User**
---

<p>
<img width="580" height="590" alt="Screenshot 2026-07-25 093532" src="https://github.com/user-attachments/assets/8f96da93-edcc-42ca-a636-7902d79093f3" />
</p>
<p>
In **dc-1** VM using the original admin user created in Azure, but with domain credentials `mydomain.com\<yourcreatedcredentials>` and password. I ran **Active Directory Users and Computers (ADUC)** as an administrator.
</p>
<br />

<h2></h2>

<p>
<img width="561" height="394" alt="Screenshot 2026-07-25 093638" src="https://github.com/user-attachments/assets/a19f2b87-1340-433a-9c19-e4989a7b636c" />
</p>
<p>
<img width="326" height="279" alt="Screenshot 2026-07-25 093735" src="https://github.com/user-attachments/assets/0a4c74dd-408f-436d-94a5-5d7ecae19e90" />
</p>
<p>
<img width="326" height="279" alt="Screenshot 2026-07-25 093801" src="https://github.com/user-attachments/assets/d38a9bc9-a6f5-4df1-b50c-9c6de676c359" />
</p>
<p>
Within **Active Directory Users and Computers**, I right-clicked the domain (mydomain.com), selected **New** → **Organizational Unit**, and created two Organizational Units (OUs) named _EMPLOYEES and _ADMINS. These (OUs) will be used to logically separate standard user accounts from administrative accounts, allowing for better organization and easier management of permissions and Group Policy.
</p>
<br />

<h2></h2>

<p>
<img width="561" height="423" alt="Screenshot 2026-07-25 093953" src="https://github.com/user-attachments/assets/9153ab1d-c283-4a86-b5d8-ae2fff258d27" />
</p>
<p>
Once created, I navigated to the **_ADMINS** Organizational Unit, right-clicked, and selected **New** → **User** to create a new administrative account. I entered the user’s details, including the name **Jane Doe**, and assigned the username jane_admin in the **mydomain.com** domain. After completing the required fields, on the password screen, I unchecked “User must change password at next logon”, enabled “Password never expires”, and then set a password for the account.

This account will be used as an administrative account, separate from standard user accounts, to follow best practices for privilege management.
</p>
<br />

<h2></h2>

<p>
<img width="327" height="281" alt="Screenshot 2026-07-25 094036" src="https://github.com/user-attachments/assets/d85dbb15-23c3-4425-a0c3-e7d87a08693c" />
</p>
<p>
I entered the user’s details, including the name **Jane Doe**, and assigned the username jane_admin in the **mydomain.com** domain.
</p>
<br />

<h2></h2>

<p>
<img width="562" height="395" alt="Screenshot 2026-07-25 094226" src="https://github.com/user-attachments/assets/78b4fa67-450f-4436-b0d5-d63ecd0683c1" />
</p>
<p>
On the password screen, uncheck “User must change password at next logon”, enable “Password never expires”, and then set a password for the account.

This account will be used as an administrative account, separate from standard user accounts, to follow best practices for privilege management.
</p>
<br />

<h2></h2>

<p>
<img width="327" height="280" alt="Screenshot 2026-07-25 094241" src="https://github.com/user-attachments/assets/e6eda1e8-c5a2-4370-be4a-bc190a8d4e7c" />
</p>
<p>
Verify that Jane Admin is in the designated group, the _ADMINS (OU). 
</p>
<br />

<h2></h2>

<p>
<img width="561" height="395" alt="Screenshot 2026-07-25 094315" src="https://github.com/user-attachments/assets/138e8a76-d641-4801-aeeb-24ab1bc13da1" />
</p>
<p>
Right-click **Jane Doe** (administrative account), select the user’s **Properties**. 
</p>
<br />

<h2></h2>

<p>
<img width="562" height="446" alt="Screenshot 2026-07-25 094422" src="https://github.com/user-attachments/assets/d93cc024-3963-47c9-b68e-12710f467654" />
</p>
<p>
Under the **Member Of** tab, I selected **Add**, entered "Domain Admins", and clicked **Check Names** to validate the group. After confirming, I clicked **OK** to add the user to the Domain Admins group, granting administrative privileges.
Adding the user to the Domain Admins group provides full administrative control over the domain, following the practice of using dedicated admin accounts instead of default ones.
</p>
<br />

<h2></h2>

<p>
<img width="333" height="196" alt="Screenshot 2026-07-25 094800" src="https://github.com/user-attachments/assets/35e3b443-747f-43b6-94cb-fab5736ee5bb" />
</p>
<p>
<img width="330" height="628" alt="Screenshot 2026-07-25 095055" src="https://github.com/user-attachments/assets/f6d7acab-ab9a-465b-933d-f59924518baf" />
</p>
<p>
Logged out of DC-1 and logged back in using the domain credentials `mydomain.com\jane_admin` as the username and password. For the remaining steps, we will keep **Remote Desktop** open to use **jane_admin** as the admin account for the rest of the lab.
</p>
<br />

<h2></h2>

**2. Join client-1 to the Domain**
---

<p>
<img width="301" height="488" alt="Screenshot 2026-07-25 095352" src="https://github.com/user-attachments/assets/38780a1d-d027-4281-b420-86b162a352c6" />
</p>
<p>
Navigated to the Azure Virtual Machines list and selected the client-1 VM. Initiated a Remote Desktop connection using the public IP address (172.200.210.160), authenticating with domain credentials in the format `mydomain.com\<yourcreatedcredentials>` and the associated password.
</p>
<br />

<h2></h2>

<p>
<img width="152" height="453" alt="Screenshot 2026-07-25 095652" src="https://github.com/user-attachments/assets/8bd067c3-7d7b-41b5-ad21-323c6cfe94fe" />
</p>
<p>
Once logged in to **client-1**, I right-clicked the Start menu and opened **System** to access the computer’s settings and configuration details.
</p>
<br />

<h2></h2>

<p>
<img width="1123" height="433" alt="Screenshot 2026-07-25 095750" src="https://github.com/user-attachments/assets/57c59af5-87fa-4eda-834c-45261f40c138" />
</p>
<p>
On the right-hand side, I navigated to **client-1 (Advanced system settings).
</p>
<br />

<h2></h2>

<p>
<img width="689" height="477" alt="Screenshot 2026-07-25 095947" src="https://github.com/user-attachments/assets/5a32cddc-07bb-4bf8-854f-9b89ab6c5b8c" />
</p>
<p>
Under the **Computer Name** tab, I clicked **Change** to modify the computer’s domain membership. Next, I selected the **Domain** option, entered **"mydomain.com"**, and clicked **OK** to join **client-1** to the domain.
</p>
<br />

<h2></h2>

<p>
<img width="652" height="439" alt="Screenshot 2026-07-25 100128" src="https://github.com/user-attachments/assets/297c9ff5-38f1-4837-8624-2c9bf324bffc" />
</p>
<p>
<img width="264" height="143" alt="Screenshot 2026-07-25 100157" src="https://github.com/user-attachments/assets/a87c7b5e-f5b4-4134-ba2a-11d20ce0ed29" />
</p>
<p>
After entering valid domain credentials, the computer was successfully joined to the domain and required a restart to apply the changes. Joining the computer to the domain allows centralized management of users, security policies, and resources through Active Directory, making administration more efficient and scalable.
</p>
<br />

<h2></h2>

### Verify in Active Directory

<p>
<img width="577" height="588" alt="Screenshot 2026-07-25 100519" src="https://github.com/user-attachments/assets/07cdb8a2-fbad-42be-b5da-c3a8e61cf11a" />
</p>
<p>
I went back to the Domain Controller VM (dc-1), opened **Active Directory Users and Computers**.
</p>
<br />

<h2></h2>

<p>
<img width="561" height="395" alt="Screenshot 2026-07-25 100641" src="https://github.com/user-attachments/assets/f0f4fc8b-77ab-4dfb-8e6c-01c267060508" />
</p>
<p>
Verify that (client-1) appears in the Computers folder under the domain (mydomain.com), confirm it was successfully added to the domain.
</p>
<br />

<h2></h2>

<p>
<img width="561" height="392" alt="Screenshot 2026-07-25 100810" src="https://github.com/user-attachments/assets/ef20b928-fd61-4888-bc66-5d97ac44efd0" />
</p>
<p>
<img width="327" height="280" alt="Screenshot 2026-07-25 100841" src="https://github.com/user-attachments/assets/e48465ed-2b1a-428e-a700-87ce3df9de5e" />
</p>
<p>
<img width="562" height="394" alt="Screenshot 2026-07-25 101241" src="https://github.com/user-attachments/assets/d6f068e6-3ffa-4354-b9ed-c574cb2456c0" />
</p>
<p>
Separate administrators, employees, and client systems into distinct containers for improved organization and management, Create a new Organizational Unit named "_CLIENTS" and move client-1 into it.
</p>
<br />

<h2></h2>

**3. Set up Remote Desktop for Non-Administrative Users**
---
<p>

</p>
<p>
Logged in to the **client-1** VM using the domain admin username `mydomain.com\jane_admin`, and password. Once logged in, I right-clicked the Start menu and selected **System** to open Remote Desktop Settings, then enabled Remote Desktop by selecting “Select users that can remotely access this PC”. In the Object names field, I typed "Domain User" and selected **Check Names** to validate. After confirming, I clicked **OK** to grant all domain users remote access.

This configuration allows authorized domain users to remotely connect to the client machine using Remote Desktop Protocol (RDP), enabling centralized and flexible access to the system.
</p>
<br />

<h2></h2>
