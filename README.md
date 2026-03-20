# osTicket Help Desk Lab Post Installation (VirtualBox)

<p align="center">
  <img src="img/Osticket Project Cover.png" width="900">
</p>


## Project Overview
This project demonstrates the deployment and configuration of an **osTicket help desk system** in a virtualized lab environment using **VirtualBox**, **Windows Server 2019**, and a **Windows 10 client machine**.

The lab simulates a real-world IT support environment where users submit tickets and support agents manage, prioritize, and resolve them.

---

## Lab Environment

| Component        | Details                          |
|-----------------|----------------------------------|
| Host Machine     | Local Laptop (VirtualBox)        |
| Client Machine   | Windows 10 (Domain-Joined)       |
| Server           | Windows Server 2019              |
| Roles on Server  | Domain Controller + IIS + DNS    |
| Application      | osTicket                         |

---

## Network Architecture

<p align="center">
  <img src="img/1. Network Topology.png" width="900">
</p>

---

## Pre-Setup Steps (osTicket Lab - VirtualBox)

Follow these steps before using osTicket in your lab environment:

- Log into the Domain Controller and configure a **static IPv4 address**
<p align="center">
  <img src="img/1. Domain Controller Static Ip Address.png" width="900">
</p>

## Create 2 virtual machines named **Desktop1 & Desktop2** and join both machines to domain (**GetHired.com**). 

- I will show the example with Desktop2.

I then created a new Windows 10 virtual machine named **Desktop2** in VirtualBox with:
<p align="center"><img src="img/4. Create Windows VM.png" width="700"></p>

- **2 CPUs**
- **4 GB RAM**
<p align="center"><img src="img/4. Windows VM Ram-CPU.png" width="700"></p>
- **50 GB storage**
<p align="center"><img src="img/5. Windows VM Storage.png" width="700"></p>

Now Windows Installation
<p align="center"><img src="img/6. Start Your VM.png" width="700"></p>
<p align="center"><img src="img/6. OS Setup.png" width="700"></p>
<p align="center"><img src="img/6. OS Windows Pro.png" width="700"></p>
<p align="center"><img src="img/6. OS Custom Drive.png" width="700"></p>
<p align="center"><img src="img/6. OS Installation.png" width="700"></p>
<p align="center"><img src="img/6. Desktop2 PC Name.png" width="700"></p>
<p align="center"><img src="img/6. Windows Getting Ready.png" width="700"></p>


After installation, I configured the network, pointed IPv4 DNS toward the domain controller, renamed the machine, and joined it to the domain.  
This allowed the new workstation to authenticate against Active Directory and appear as a managed company device.

## Workstation Domain Configuration

Configured VirtualBox network adapter to use Host-Only Adapter for isolated lab communication
<p align="center"><img src="img/7. VB Network Settings.png" width="700"></p>
Renamed the virtual machine to Desktop2 for proper identification in the domain
<p align="center"><img src="img/7. Change Computer Name 2.png" width="700"></p>
Retrieved the Domain Controller’s IP address (DC-2019) using ipconfig /all
<p align="center"><img src="img/7. DC-2019 IPV4 Address.png" width="700"></p>
Set Desktop2 IPv4 DNS to point to the Domain Controller for domain resolution
<p align="center"><img src="img/7. Desktop Points DC-2019.png" width="700"></p>
Joined Desktop2 from a workgroup to the Active Directory domain
<p align="center"><img src="img/7. Desktop2 Workgroup to Domain.png" width="700"></p>
<p align="center"><img src="img/7. Domain Signin.png" width="700"></p>
<p align="center"><img src="img/7. Welcome to GetHired.com.png" width="700"></p>
<p align="center"><img src="img/7. Verification for Domain Network.png" width="700"></p>
Verified that Desktop2 successfully appears in Active Directory (ADUC) under domain computers
<p align="center"><img src="img/7. AD Service Computers - Desktop2.png" width="700"></p>
VM is running and operating
<p align="center"><img src="img/7. VM is running and operating.png" width="700"></p>

Your environment is now ready for osTicket setup.

---

## How It Works

1. User enters:
   
```

[http://DC-2019/osTicket](http://DC-2019/osTicket)

```

<p align="center">
  <img src="img/6. From Desktop1 Signin as JuniorP.png" width="900">
</p>

* Welcome to osTicket

<p align="center">
  <img src="img/7. Welcome to osTicket.png" width="900">
</p>

2. DNS resolves hostname → IP  
```

DC-2019 → 192.168.56.104

```
[Click Here to install IIS, PHP, MySQL, Etc.](https://github.com/Jvpjava/osTicket-Help-Desk-Deployment-and-Incident-Management-Lab)

  3. Client sends HTTP request (Port 80)
  
  4. IIS (Web Server) receives the request
  
  5. osTicket processes request using PHP + MySQL
  
  6. Web page is returned to the client

**Key Concept:**  
Even though a hostname is used, communication happens using the IP address after DNS resolution.

---

## 🔐 Access URLs

| Type        | URL |
|------------|-----|
| End User   | http://DC-2019/osTicket |
| Admin Panel| http://DC-2019/osTicket/scp/login.php |

<p align="center">
  <img src="img/8. Admin Panel.png" width="900">
</p>
Admin Panel Backend
<p align="center">
  <img src="img/8. Admin Panel 2.png" width="900">
</p>

---

## ⚙️ Post-Installation Configuration

### 🔹 Roles (Permissions)
<p align="center">
  <img src="img/9. Roles.png" width="900">
</p>
- Created role: **Supreme Admin**

<p align="center">
  <img src="img/9. Add new role.png" width="900">
</p>

- Permissions:
- Assign tickets
- Edit tickets
- Delete tickets
- Merge tickets
<p align="center">
  <img src="img/9. Full Control.png" width="900">
</p>
<p align="center">
  <img src="img/9. Supreme Admin Role Created.png" width="900">
</p>
---

### 🔹 Departments
Used to control ticket visibility:
- SysAdmins  
- Support  
- Maintenance  
<p align="center">
  <img src="img/10. Departments.png" width="900">
</p>
Creating System Administrator's Department
<p align="center">
  <img src="img/10. Creating new deparment.png" width="900">
</p>
Created System Administrator's Department
<p align="center">
  <img src="img/10. System Administration Created.png" width="900">
</p>
---

### 🔹 Teams
Cross-department collaboration:
- Online Banking  
- Level 1 Support  
<p align="center">
  <img src="img/11. Teams.png" width="900">
</p>
Creating System Online Banking Team
<p align="center">
  <img src="img/11. Creating Team.png" width="900">
</p>
Created Online Banking 
<p align="center">
  <img src="img/11. Team Created Online Banking.png" width="900">
</p>

---

### 🔹 Agents (Support Staff)
| Name | Department |
|------|------------|
| Jane | SysAdmins  |
| John | Support    |

Creating Jane Doe as an agent
<p align="center">
  <img src="img/12. Creating an Agent.png" width="900">
</p>
Creating Jane Doe's password
<p align="center">
  <img src="img/12. Agent Password.png" width="900">
</p>
Give Jane Doe Supreme admni rights
<p align="center">
  <img src="img/12. Jane Supreme Admini Access.png" width="900">
</p>
Adding Jane doe to the Online banking team
<p align="center">
  <img src="img/12. Jane Doe Teams.png" width="900">
</p>

Creating John Doe as an agent
<p align="center">
  <img src="img/13. Creating Agent.png" width="900">
</p>
Adding John Doe's to a Department
<p align="center">
  <img src="img/13. John Doe Department.png" width="900">
</p>
All osTicket Agents
<p align="center">
  <img src="img/13. osTicket Agents.png" width="900">
</p>
---

### 🔹 Users (Customers)
- Karen Valerio
  - Username: KarenV
  - Email: KarenValerio@GetHired.com
- Ken Valerio
  - Username: KenV
  - Email: KenValerio@GetHired.com
  
Switch to agent panel 
<p align="center">
  <img src="img/14. Agent Panel.png" width="900">
</p>
Create Karen
<p align="center">
  <img src="img/14. Create a User.png" width="900">
</p>
Created Karen
<p align="center">
  <img src="img/14. Created Karen User.png" width="900">
</p>
Created Ken
<p align="center">
  <img src="img/14. Created Ken User.png" width="900">
</p>

---

### 🔹 SLA (Service Level Agreements)

| SLA Level | Response Time | Schedule        |
|----------|--------------|-----------------|
| Sev-A    | 1 hour       | 24/7            |
| Sev-B    | 4 hours      | 24/7            |
| Sev-C    | 8 hours      | Business Hours  |

Go Back to Admin Panel and go to SLA
<p align="center">
  <img src="img/15. Admin Panel SLA.png" width="900">
</p>
Create SLA level Service A
<p align="center">
  <img src="img/15. Service A Created.png" width="900">
</p>
Create SLA level Service B
<p align="center">
  <img src="img/15. Service B Created.png" width="900">
</p>
Create SLA level Service C
<p align="center">
  <img src="img/15. Service C Created.png" width="900">
</p>
All Service plans
<p align="center">
  <img src="img/15. All Service Plans.png" width="900">
</p>

---
###  Issues, Request, Inquiry, and Outages
- Business Critical Outage  
- Personal Computer Issues  
- Equipment Request  
- Password Reset  
- General Inquiry

<p align="center">
  <img src="img/16. Help Topics.png" width="900">
</p>
<p align="center">
  <img src="img/16. All Help Topics Created.png" width="900">
</p>

---
###  Create end users and admin user in Active Directory
Login to DC-2019 Domain Controller
- Admin users will use Desktop1  computer and have more access such as admin in the domain.
    - Admin users like John Doe and Jane Doe will use Helpdesk1 domain account to help end users.
    - If you want you can create individual credentials in AD for John Doe and Jane Doe.
    - This is for lab puroses to make things run faster.
 
Go to Server Manager
<img src="img/17. Server Manager.png" width="700">

Go To Active Directory Users and Computers
<img src="img/17. Active Directory Users and Computers.png" width="700">

Go to Users List
<img src="img/17. AD List.png" width="700">

Create New User
<img src="img/17. New User.png" width="700">

Enter Credentials Username
<img src="img/18. Helpdesk1 Credentials Username.png" width="700">

Enter Credentials Password
<img src="img/18. Helpdesk1 Credentials Password.png" width="700">

Go to properties on the helpdesk1 user account
<img src="img/19. helpdesk1 Properties.png" width="700">

Go to Member of
<img src="img/19. helpdesk1 Member Of.png" width="700">

Add a group member
<img src="img/19. Helpdesk1 Add Member.png" width="700">

Add Domain Admin
<img src="img/19 Add Domain Admin.png" width="700">

Look at the group member list
<img src="img/19. Member of Groups .png" width="700">

- End users will use Desktop2 computer and have individual accounts in the domain.
  - You can use the same credentials we used in osTicket to create the users.
  - For Example like Karen Valerio and Ken Valerio like we did above.
  
Create a new user
<p align="center"><img src="img/8. New User KarenV.png" width="700"></p>
Karen Credentials: Username & same credentials in osTicket
<p align="center"><img src="img/8. KarenV Created.png" width="700"></p>
Karens Credentials: Password
<p align="center"><img src="img/8. KarenV Password.png" width="700"></p>
Check Active Directory Users List to see if the User is created
<p align="center"><img src="img/8. AD List .png" width="700"></p>
Same Process applies for Ken Valerio & same credentials in osTicket
<p align="center"><img src="img/8. New User KenV.png" width="700"></p>
Start Desktop2
<p align="center"><img src="img/9. Signin To Domain.png" width="700"></p>
Sign into the domain Ex: GetHired\KarenV
  - Samething applies to Ken: Gethired\KenV
<p align="center"><img src="img/9. Gethired-KarenV.png" width="700"></p>
Karen Should logged into the domain computer as a domain user.
<p align="center"><img src="img/9. KarenV in Windows Machine.png" width="700"></p>
---
## 🎯 Skills Demonstrated

- Active Directory (Domain Services)
- DNS Resolution
- IIS Web Server Configuration
- Virtualization (VirtualBox)
- Help Desk Ticketing Systems
- Role-Based Access Control (RBAC)
- SLA Management

---
