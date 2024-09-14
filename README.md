# osTicket Installation and Configuration

In this project, we install osTicket on a Windows 10 Azure Virtual Machine, set up post-installation settings, and manage the ticket lifecycle.

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Web Browser
- osTicket

## Operating Systems Used

- Windows 10

## High-Level Steps

- Part 1: osTicket Installation
- Part 2: osTicket Post-Installation Setup
- Part 3: Ticket and Ticket Lifecycle Management

## Actions and Observations

### Part 1: osTicket Installation

In this part, we set up a Windows 10 Virtual Machine on Azure and install osTicket with all necessary dependencies.

#### Step-by-Step Actions

1. **Create Azure Virtual Machine (VM)**:
   - Name: `osticket-vm`
   - Username: `labuser`
   - Password: `osTicketPassword1!`
   - Size: 4 vCPUs
   - Region: Canada Central

2. **Install IIS with CGI Enabled**:
   - Enable IIS with Application Development Features -> [X] CGI.

3. **Install PHP and Modules**:
   - Install PHP Manager for IIS and the Rewrite Module.
   - Create a directory at `C:\PHP` and unzip PHP 7.3.8 into this directory.
   - Install required Visual C++ redistributables and MySQL 5.5.62.

4. **Configure IIS for PHP**:
   - Register PHP with IIS and restart the server.

5. **Install osTicket**:
   - Unzip osTicket v1.15.8 into `C:\inetpub\wwwroot` and rename the folder to `osTicket`.
   - Configure PHP extensions and set up the initial osTicket configuration in the browser.

6. **Set Up Database**:
   - Create a new database named `osTicket` using HeidiSQL and finalize the installation.

#### Observations

- Successfully installed and configured osTicket on the VM.
- Properly set permissions for configuration files.

### Part 2: osTicket Post-Installation Setup

After installing osTicket, this part covers configuring roles, departments, and teams, and setting up agents and users.

#### Step-by-Step Actions

1. **Configure Roles and Departments**:
   - Set up roles like Supreme Admin and departments like SysAdmins.

2. **Create Teams**:
   - Example: Online Banking team pulling agents from different departments.

3. **Configure Agents and Users**:
   - Add agents such as Jane (SysAdmins) and John (Support).
   - Add users such as Karen and Ken.

4. **Set Up SLAs and Help Topics**:
   - Create SLA plans such as Sev-A, Sev-B, and Sev-C with different response times.
   - Define help topics like Business Critical Outage and Password Reset.

#### Observations

- Configurations allow for efficient ticket handling and user management.
- Ensured only registered users can create tickets.

### Part 3: Ticket and Ticket Lifecycle Management

This part demonstrates creating and managing tickets, setting priorities, and resolving them.

#### Step-by-Step Actions

1. **Modify Department Structure**:
   - Change SysAdmins to a top-level department.
   - Delete the Maintenance Department.

2. **Create and Manage Tickets**:
   - As an end-user, create tickets for various issues like banking system outages and laptop problems.
   - As an agent, observe ticket properties, set priorities, and work the tickets to completion.

3. **Set Ticket Properties**:
   - Set tickets to appropriate SLAs and departments, such as Sev-A for high-priority issues.

4. **Resolve Tickets**:
   - Complete the ticket lifecycle from creation to resolution while adhering to SLAs.

#### Observations

- Ticket properties such as priority and SLA are crucial for managing workflows.
- Role permissions affect what agents can see and modify.

---
