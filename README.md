# active-directory-lab

# 🏢 Active Directory Home Lab (Windows Server)

## 📌 Overview

I built a full Active Directory lab environment using Windows Server to simulate a real enterprise network.

The project includes domain setup, client integration, user management, Group Policy enforcement, DNS troubleshooting, and PowerShell automation.

---

## 🎯 Objectives

* Deploy Active Directory Domain Services (AD DS)
* Join client machines to the domain
* Organize users using Organizational Units (OUs)
* Implement Group Policies (GPOs)
* Manage users via PowerShell
* Troubleshoot DNS issues
* Monitor security events

---

## screenshots

https://www.notion.so/Active-Directory-Windows-Server-Project-2f02f9b6c93180dea935f81318d0a31a?source=copy_link

## 🧱 Environment Setup

### Domain

* Domain Name: **alusani.local**

### Server Roles

* Active Directory Domain Services (AD DS)
* DNS Server

### Client

* Windows 10 machine joined to domain

---

## 👥 Active Directory Management

I used **Active Directory Users and Computers (ADUC)** to manage:

* Users
* Computers
* Organizational Units (OUs)

Departments created:

* HR
* IT
* Finance

---

## 💻 Domain Join

A Windows 10 machine was successfully joined to the domain and is centrally managed through Active Directory.

---

## 🔐 Group Policy (GPO)

### Policies Implemented:

* Disabled Control Panel access for HR users
* Applied Account Lockout Policy

### Testing:

* Entered incorrect password 3 times
* Account locked successfully
* Verified via Event Viewer

---

## ⚙️ PowerShell Administration

### User Management:

* Created users using `New-ADUser`
* Reset passwords using `Set-ADAccountPassword`
* Enabled/Disabled accounts

### Example:

```powershell
New-ADUser -Name "Test User2" `
-SamAccountName testuser2 `
-UserPrincipalName testuser2@alusani.local `
-Path "OU=HR_Department,DC=alusani,DC=local" `
-AccountPassword (ConvertTo-SecureString "P@ssw0rd123" -AsPlainText -Force) `
-Enabled $true
```

---

## 📊 Bulk User Creation (CSV)

Created multiple users using CSV and PowerShell automation.

### Example:

```powershell
Import-Csv C:\lab\users.csv | ForEach-Object {
New-ADUser `
-Name "$($_.FirstName) $($_.LastName)" `
-SamAccountName $_.Username `
-UserPrincipalName "$($_.Username)@alusani.local" `
-Path "OU=$($_.OU),DC=alusani,DC=local" `
-AccountPassword (ConvertTo-SecureString "P@ssword123!" -AsPlainText -Force) `
-Enabled $true
}
```

---

## 🌐 DNS Troubleshooting (Break & Fix)

### Scenario:

Client could not log in due to DNS misconfiguration.

### Issue:

* DNS manually changed to **8.8.8.8**

### Troubleshooting Steps:

* Verified using `ipconfig /all`
* Tested with `nslookup alusani.local`
* Ran `dcdiag /test:dns` on server

### Resolution:

* Restored correct DNS settings
* Flushed DNS cache
* Forced policy update

```bash
ipconfig /flushdns
gpupdate /force
```

---

## 📊 Event Monitoring

Used Event Viewer to analyze:

* Failed logons → Event ID **4625**
* Account lockouts → Event ID **4740**

---

## 🧪 Testing & Validation

* Domain join successful
* GPO applied correctly
* Account lockout enforced
* DNS issue successfully resolved
* PowerShell automation working

---

## 🚧 Challenges & Solutions

| Issue                     | Solution                             |
| ------------------------- | ------------------------------------ |
| DNS misconfiguration      | Restored correct DNS settings        |
| Account lockouts          | Verified and unlocked via PowerShell |
| Bulk user creation errors | Fixed CSV formatting                 |

---

## 📈 Key Takeaways

* Hands-on Active Directory administration
* GPO configuration and enforcement
* PowerShell automation
* DNS troubleshooting
* Security event monitoring

---
