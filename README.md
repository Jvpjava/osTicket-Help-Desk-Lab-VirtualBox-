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
- Create a **domain admin user** in Active Directory Users and Computers
<p align="center">
  <img src="img/3. Signin to Desktop1 with user Credentials.png" width="900">
</p>
- Create a virtual machine named **Desktop1** and join it to the domain (**GetHired.com**)
<p align="center">
  <img src="img/5. Domain Joined Computer GETHIRED.COM.png" width="900">
</p>
<p align="center">
  <img src="img/4. Desktop1 Computer has to be domain joined computer.png" width="900">
</p>
- Configure Desktop1’s IPv4 settings to use the **Domain Controller (DC-2019) as the DNS server**
<p align="center">
  <img src="img/2. Domain Joined Computer point to DC Server.png" width="900">
</p>

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
  <img src="img/ 12. Creating an Agent.png" width="900">
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
- Karen  
  
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

## 🎯 Skills Demonstrated

- Active Directory (Domain Services)
- DNS Resolution
- IIS Web Server Configuration
- Virtualization (VirtualBox)
- Help Desk Ticketing Systems
- Role-Based Access Control (RBAC)
- SLA Management

---

## 📊 Key Takeaway

This lab demonstrates how enterprise environments operate:
- DNS resolves hostnames to IP addresses  
- Web traffic flows over HTTP (Port 80)  
- IIS hosts internal applications  
- Domain-joined machines trust the Domain Controller  

---

## 🚀 Why This Project Matters

This project reflects a real IT help desk workflow:
- Users submit tickets  
- Tickets are categorized and prioritized  
- Agents resolve issues based on SLAs  
- The system enforces structured IT support operations  

---

## 📂 Documentation

Full lab documentation included in this repository:
- `Lab 3 Checklist - osTicket Post-Installation Setup.pdf`

---

## 🔧 Future Improvements

- Configure email ticketing (SMTP)
- Integrate Active Directory (LDAP authentication)
- Enable HTTPS (SSL/TLS)
- Deploy in cloud environment (Azure/AWS)
```
