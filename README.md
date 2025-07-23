# Installing and Configuring osTicket on Windows Server (GCP)

## Overview

Set up a working osTicket helpdesk ticketing system hosted on a Windows Server virtual machine (VM) in Google Cloud Platform (GCP). This includes configuring IIS, PHP, MySQL, and related dependencies.

---

## Environments and Technologies

- Google Cloud Platform (GCP)
- Windows Server 2022
- Windows 10 Pro (RDP client)
- IIS (Internet Information Services)
- MySQL Database
- PHP
- osTicket v1.15.8
- Remote Desktop Protocol (RDP)

---

## Installation Files

Download required installation files:

- [Download Package](https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD)

---

## Part 1: VM Setup

1. **Create a Windows Server VM** in Google Cloud Platform (choose Windows Server 2022).
2. **Connect via RDP** using the Microsoft Remote Desktop Client from Windows or macOS.

---

## Part 2: Configure IIS and PHP

### Step 1: Install IIS & Enable CGI

1. Open **Server Manager**
2. Go to `Manage > Add Roles and Features`
3. Select:
   - **Web Server (IIS)**
   - Under **Application Development**, enable:
     - CGI

### Step 2: Install PHP

1. Extract and move the PHP folder to `C:\PHP`
2. Add `C:\PHP` to **System Environment Variables** > `Path`
3. Configure `php.ini` and enable:
   - `extension=mysqli`
   - `extension=gd`

---

## Part 3: Configure MySQL

1. Install MySQL
2. During setup, set a root password (save it securely)
3. Create a database named `osTicket` using MySQL Shell or Workbench

---

## Part 4: Install osTicket

### Step 1: Extract Files

- Extract `osTicket-v1.15.8.zip` into `C:\inetpub\wwwroot\osTicket`

### Step 2: Rename Configuration File

Rename:

```text
From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php  
To:   C:\inetpub\wwwroot\osTicket\include\ost-config.php
```

### Step 3: Set Permissions

Give full permissions to `IIS_IUSRS` for the following folders:

- `C:\inetpub\wwwroot\osTicket\include`
- `C:\inetpub\wwwroot\osTicket\include\ost-config.php`

---

## Part 5: Web-Based Setup

### Access Installation URL

```
http://<VM_Public_IP>/osTicket
```

### Fill in Required Fields

- **System Settings** – Fill in with your own entries
- **Admin User** – Fill in with your own credentials
- **Database Settings**:

  ```
  MySQL Database: osTicket
  MySQL Username: root
  MySQL Password: [your_root_password]
  ```

Click **Install Now**

---

## Post-Installation Setup

- Delete the `setup` folder at:  
  `C:\inetpub\wwwroot\osTicket\setup`

### Access URLs

- **Staff Panel**: `http://<VM_Public_IP>/osTicket/scp`
- **User Panel**: `http://<VM_Public_IP>/osTicket`

---

## Part 6: Ticket Management Practice

### As User

- Log in and create a ticket using any Help Topic.

### As Agent

- Triage, assign, and resolve tickets.
- Practice with different severity levels (e.g., Sev-A, Sev-B).

---

## Acknowledgments

This lab project was inspired by the Ticketing Systems lab concept from the Information Technology course by CourseCareers. The implementation is entirely my own, developed using freely available resources.
