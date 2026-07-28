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
Proceed by selecting option 2, **Add roles and features**, then select **Next** until you reach **Server Roles**. In Server roles, select **Active Directory Domain Services (AD DS)** under **Server Roles**. Upon selection, I was prompted to add the required features, including Group Policy Management and Remote Server Administration Tools. I clicked **Add Features** and ensured that management tools were included to enable full administrative functionality.
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
