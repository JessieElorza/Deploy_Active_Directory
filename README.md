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

- Windows Server 2022
- Windows 10 (21H2)

<h2>Key Actions </h2> 

- Create Organizational Units for Employees and Admins
- Create Domain Admin account
- Join the client VM to the domain
- Configure Remote Desktop access for domain users
- Automate bulk user creation with PowerShell

> [!NOTE] 
>This project builds upon a prior lab where the Azure environment, virtual machines, Active Directory Domain Services, and DNS configuration were initially deployed. <br /> [Step 1: Active Directory: Preparing AD Infrastructure in Azure](https://github.com/Ernanm280/preparing-ad-inf-azure)


<h2>Deployment and Configuration Steps</h2>

**1. Create a Domain Admin User**
---
