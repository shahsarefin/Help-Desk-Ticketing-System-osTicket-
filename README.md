<h1>Help Desk Ticketing System (osTicket)</h1>
In this project, we configure a help desk ticketing system using osTicket on Azure Virtual Machines. This setup helps streamline support and ticket management, simulating real-world help desk environments.

<h2>Environments and Technologies Used</h2>
<ul>
  <li>Azure Virtual Machines</li>
  <li>osTicket</li>
  <li>Internet Information Services (IIS)</li>
</ul>

<h2>Operating Systems Used</h2>
<ul>
  <li>Windows 10</li>
</ul>

<h2>High-Level Steps</h2>
<ol>
  <li>osTicket Setup on Azure VM</li>
  <li>Post Installation Configuration of osTicket</li>
  <li>Tickets and Tickets Lifecycle Management</li>
</ol>

<h2>Actions and Observations</h2>

<!-- Step 1: osTicket Setup -->
<h3>Part 1: osTicket Setup</h3>
<p>We begin by setting up osTicket on a Windows 10 VM in Azure, installing necessary dependencies, configuring IIS, and completing the osTicket installation.</p>

<h4>Step-by-Step Instructions:</h4>
<ol>
  <li>Create an Azure Virtual Machine:
    <ul>
      <li>Go to the Azure Portal (<a href="https://portal.azure.com">portal.azure.com</a>).</li>
      <li>Click "Virtual Machines" > "Create" > "Azure Virtual Machine."</li>
      <li>Name the VM `osticket-vm`, choose the Windows 10 image, and select a size with at least 4 vCPUs.</li>
      <li>Set the authentication method to password, using Username: `labuser` and Password: `osTicketPassword1!`.</li>
      <li>Place the VM in an appropriate resource group and Virtual Network.</li>
      <li>Click "Review + Create" and then "Create."</li>
    </ul>
  </li>

  <li>Log into the VM with Remote Desktop:
    <ul>
      <li>Use the IP address provided by Azure and the credentials `labuser / osTicketPassword1!`.</li>
    </ul>
  </li>

  <li>Download and Unzip osTicket Installation Files:
    <ul>
      <li>Download the osTicket installation package (`osTicket-Installation-Files.zip`) to the VM.</li>
      <li>Unzip the file onto your desktop; the folder should be named `osTicket-Installation-Files`.</li>
    </ul>
  </li>

  <li>Install Internet Information Services (IIS) with CGI:
    <ul>
      <li>Open Control Panel > Programs > Turn Windows features on or off.</li>
      <li>Expand "Internet Information Services" > "World Wide Web Services" > "Application Development Features".</li>
      <li>Check the box for `[X] CGI` and click "OK" to install.</li>
    </ul>
  </li>

  <li>Install PHP Manager for IIS:
    <ul>
      <li>From the `osTicket-Installation-Files` folder, run `PHPManagerForIIS_V1.5.0.msi` to install PHP Manager.</li>
    </ul>
  </li>

  <li>Install Rewrite Module:
    <ul>
      <li>From the `osTicket-Installation-Files` folder, run `rewrite_amd64_en-US.msi` to install the Rewrite Module.</li>
    </ul>
  </li>

  <li>Set Up PHP Environment:
    <ul>
      <li>Create a directory `C:\PHP` on your VM.</li>
      <li>Unzip `php-7.3.8-nts-Win32-VC15-x86.zip` from the `osTicket-Installation-Files` into the `C:\PHP` folder.</li>
    </ul>
  </li>

  <li>Install VC Redist:
    <ul>
      <li>From the `osTicket-Installation-Files` folder, run `VC_redist.x86.exe` to install Visual C++ Redistributable.</li>
    </ul>
  </li>

  <li>Install MySQL 5.5.62:
    <ul>
      <li>Run `mysql-5.5.62-win32.msi` from the `osTicket-Installation-Files` folder.</li>
      <li>Follow the Typical Setup path and launch the Configuration Wizard.</li>
      <li>Choose Standard Configuration, set the username to `root`, and password to `root`.</li>
    </ul>
  </li>

  <li>Configure IIS for PHP:
    <ul>
      <li>Open IIS Manager as Administrator.</li>
      <li>In IIS, click on the server name, then open "PHP Manager" and register PHP by selecting `C:\PHP\php-cgi.exe`.</li>
      <li>Reload IIS by stopping and starting the server.</li>
    </ul>
  </li>

  <li>Install osTicket:
    <ul>
      <li>Unzip `osTicket-v1.15.8.zip` from the `osTicket-Installation-Files` folder.</li>
      <li>Copy the `upload` folder to `C:\inetpub\wwwroot` and rename it to `osTicket`.</li>
      <li>Reload IIS and browse to the osTicket site via IIS Manager (Sites -> Default -> osTicket -> Browse *:80).</li>
    </ul>
  </li>

  <li>Enable PHP Extensions:
    <ul>
      <li>In IIS Manager, go to Sites -> Default -> osTicket and open PHP Manager.</li>
      <li>Click “Enable or disable an extension” and enable the following:
        <ul>
          <li>`php_imap.dll`</li>
          <li>`php_intl.dll`</li>
          <li>`php_opcache.dll`</li>
        </ul>
      </li>
      <li>Refresh the osTicket page in your browser to observe the changes.</li>
    </ul>
  </li>

  <li>Configure `ost-config.php`:
    <ul>
      <li>Rename `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php` to `ost-config.php`.</li>
      <li>Disable inheritance on the file by removing all permissions and setting new permissions for "Everyone" with full access.</li>
    </ul>
  </li>

  <li>Finish osTicket Setup:
    <ul>
      <li>Continue setting up osTicket in the browser by following the on-screen prompts.</li>
      <li>Set the Helpdesk name and default email to receive customer emails.</li>
    </ul>
  </li>

  <li>Install HeidiSQL:
    <ul>
      <li>From the `osTicket-Installation-Files` folder, install HeidiSQL.</li>
      <li>Open HeidiSQL, create a new session using `root/root`, and connect.</li>
      <li>Create a database named `osTicket`.</li>
    </ul>
  </li>

  <li>Finalize osTicket Installation:
    <ul>
      <li>In the osTicket setup page, enter MySQL Database: `osTicket`, Username: `root`, Password: `root`.</li>
      <li>Click "Install Now!" and complete the installation process.</li>
    </ul>
  </li>

  <li>Post-Installation Cleanup:
    <ul>
      <li>Delete the setup folder at `C:\inetpub\wwwroot\osTicket\setup`.</li>
      <li>Set `C:\inetpub\wwwroot\osTicket\include\ost-config.php` permissions to “Read-only.”</li>
    </ul>
  </li>
</ol>

---

<h3>Part 2: Post Installation Configuration</h3>
<p>We configure osTicket settings, including user roles, departments, SLAs, and help topics, to simulate real-world help desk environments.</p>

<h4>Step-by-Step Instructions:</h4>
<ol>
  <li>Log in to the Admin/Analyst Panel:
    <ul>
      <li>Admin/Analyst Login Page: <a href="http://localhost/osTicket/scp/login.php">http://localhost/osTicket/scp/login.php</a></li>
      <li>End Users URL: <a href="http://localhost/osTicket">http://localhost/osTicket</a></li>
    </ul>
  </li>

  <li>Configure Roles:
    <ul>
      <li>Go to Admin Panel -> Agents -> Roles.</li>
      <li>Create a new role named “Supreme Admin” with full permissions.</li>
    </ul>
  </li>

  <li>Configure Departments:
    <ul>
      <li>Go to Admin Panel -> Agents -> Departments.</li>
      <li>Create departments such as “SysAdmins” for grouping tickets based on different help desk roles.</li>
    </ul>
  </li>

  <li>Configure Teams:
    <ul>
      <li>Go to Admin Panel -> Agents -> Teams and create teams by pulling agents from various departments (e.g., "Online Banking").</li>
    </ul>
  </li>

  <li>Configure Ticket Settings:
    <ul>
      <li>Allow anyone to create tickets by going to Admin Panel -> Settings -> User Settings and unchecking “Require registration and login to create tickets.”</li>
    </ul>
  </li>

  <li>Configure Agents and Users:
    <ul>
      <li>Add new agents and assign them to specific departments (e.g., Jane in SysAdmins, John in Support).</li>
      <li>Add new users (customers) like Karen and Ken in the Agent Panel -> Users -> Add New.</li>
    </ul>
  </li>

  <li>Configure SLA Policies:
    <ul>
      <li>Go to Admin Panel -> Manage -> SLA and configure policies like Sev-A (1 hour, 24/7), Sev-B (4 hours, 24/7), and Sev-C (8 hours, Business Hours).</li>
    </ul>
  </li>

  <li>Configure Help Topics:
    <ul>
      <li>In Admin Panel -> Manage -> Help Topics, set up topics like “Business Critical Outage,” “Personal Computer Issues,” and “Password Reset” for when users create tickets.</li>
    </ul>
  </li>
</ol>

---

<h3>Part 3: Tickets and Ticket Lifecycle Management</h3>
<p>This section involves creating, assigning, and resolving tickets to simulate the complete help desk ticket lifecycle.</p>

<h4>Step-by-Step Instructions:</h4>
<ol>
  <li>Create and Manage Tickets:
    <ul>
      <li>Log in as an end-user and create tickets with varying issues (e.g., “Entire mobile/online banking system is down”).</li>
      <li>As a Help Desk Agent (e.g., John), observe and modify ticket properties like Priority, Department, and SLA.</li>
      <li>Work on the tickets and resolve them based on assigned SLAs and department workflows.</li>
    </ul>
  </li>

  <li>Change Department Settings:
    <ul>
      <li>Reconfigure departments, such as changing SysAdmins to a top-level department or deleting unnecessary ones like Maintenance.</li>
    </ul>
  </li>

  <li>Observe Ticket Permissions:
    <ul>
      <li>Work on the tickets and observe how permissions affect the visibility and accessibility of ticket details.</li>
      <li>Switch to the admin panel to modify access if needed and ensure proper assignment.</li>
    </ul>
  </li>

  <li>Complete the Lab:
    <ul>
      <li>Resolve all the tickets, taking note of how osTicket notifies users via email updates.</li>
      <li>Discuss real-life ticket intake methods (phone, email, chat, etc.) and the importance of tracking all issues with tickets for metrics and accountability.</li>
    </ul>
  </li>
</ol>
---
### Purpose of the Lab

The purpose of this lab is to provide hands-on experience in setting up and managing a help desk ticketing system using osTicket on Azure Virtual Machines. The lab demonstrates the configuration of a ticketing system to streamline support operations, manage user roles, set up departments, define SLAs, and handle ticket lifecycle management. This exercise simulates real-world help desk scenarios, enhancing skills in IT support, user management, and service delivery.

### Key Learnings

- **osTicket Installation and Configuration:**  
  Learn how to install and configure osTicket, including setting up dependencies like IIS, PHP, and MySQL to run the help desk system efficiently.

- **User Roles and Permissions Management:**  
  Understand how to configure roles, departments, and teams within osTicket to manage permissions and define responsibilities among support staff.

- **SLA Management:**  
  Gain experience in setting up Service Level Agreements (SLAs) to prioritize ticket response times based on severity, ensuring timely support.

- **Ticket Lifecycle Management:**  
  Learn the full cycle of ticket management, from creation by end-users to resolution by support agents, including setting ticket properties and responding to user issues.

- **Troubleshooting and Real-World Application:**  
  Develop troubleshooting skills by working through common help desk scenarios, such as reassigning tickets, managing access, and configuring system settings to meet operational needs.

### Concepts Taught by This Lab

- **Help Desk Operations:**  
  Understand the fundamentals of a help desk ticketing system and how it helps streamline IT support workflows by tracking and managing customer issues.

- **Web Server and Application Configuration:**  
  Learn to configure IIS and PHP settings on Windows, crucial for hosting web applications like osTicket and similar systems.

- **Database Management:**  
  Set up and manage MySQL databases for application backends, including database creation, user access, and connection settings.

- **User and Access Control:**  
  Explore the importance of properly assigning roles, setting permissions, and creating departmental structures to manage support staff efficiently.

- **SLA Policy Implementation:**  
  Understand how to define and apply SLAs within a ticketing system to enforce response times and prioritize critical issues.

- **Ticket Lifecycle and Reporting:**  
  Grasp the complete ticket lifecycle and the importance of tracking each step for metrics, accountability, and improving customer satisfaction.
