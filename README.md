<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>Overview</h2>

- Step 1: Create Resource Group inside Azure, Windows Virtual Machine, & Log into VM
- Step 2: Install Prerequisites [8 Items]
- Step 3: Install osTicket

<h2>List of Prerequisites</h2>

- Item 1: Install & Enable IIS in Windows with CGI
- Item 2: Install PHP Manager for IIS
- Item 3: Download & Install Rewrite Module
- Item 4: Create Directory in PHP on local hard drive
- Item 5: Download PHP 7.3.8 & Unzip Contents into C:\PHP
- Item 6: Download & Install C++ Redistributable
- Item 7: Install MySQL Server
- Item 8: Configure inside of IIS: Register PHP
 
<h2>Installation Steps</h2>

<h3>Step 1: Create Resource Group, Windows Virtual Machine, & Log into VM</h3>

<p>In order to download osTicket, we first will create a Virtual Machine that osTicket will run off of. The purpose of the Virtual Machine is to test/experiment softwares and services without tampering with our physical computer.</p>

<h4>Creating the Resource Group and Microsoft VM</h4>

1. Navigate to Microsoft Azure > Navigate to 'Resource Groups' via the quick access icon or search bar > select 'Create Resource Group'
2. We'll name our Resource Group: "RG-osTicket". There is nothing left for us to alter so select 'Review + Create'


<img src="https://i.imgur.com/a5aZTph.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

3. Navigate to 'Virtual Machines' within Azure via quick access icon or search bar > select 'Create Virtual Machine'
4. Within the Virtual Machine portal, we will make the following changes:

- Pick the resource group we just created: RG-osTicket
- Name of Virtual Machine: VM-osTicket
- Image: Windows 10 Pro, version 22H2 - x64 Gen2
- Size: 2-4 vcpus (4vcpu is okay since we’re only using 1 virtual machine and thus is free to utilize all power)
- Username/password of choice: Example username: darinstathos (Remember this username/password for later when logging into VM)
- Check Licensing Box: [X] ‘I confirm I have an eligible Windows 10/11 license with multi-tenant hosting rights.’
- Select 'Next: Disks >', 'Next: Networking >': Beside Virtual Network: We don't have a virtual network yet so Azure automatically created on for us 
- Select 'Review + Create'

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br>

<h4>Logging into our Virtual Machine</h4>

<p>We want to access the virtual machine we just created so we can install osTicket onto our virtual machine.</p>

1. We need to copy the Public IP Address of VM-osTicket: Navigate to Azure > ‘Virtual Machines’ > VM-osTicket > Overview: Copy Public IP address to clipboard
2. WindowsOS vs MacOS:

- If you’re using Windows, click the ‘Start’ menu (Windows Icon) on desktop > search bar > Remote Desktop Connection
- This is done from the perspective of MacOS, so open/download application: Microsoft Remote Desktop > Add PC > paste Public IP Address > input ‘username/password’ from when we created the VM. (example: darinstathos)
 
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br> 

<h3>Step 2: Install Prerequisites [8 Items]</h3>  

<h4>Item 1: Install & Enable IIS in Windows with CGI</h4>

<strong>What is IIS (Internet Information Services)?</strong>

<p>IIS (Internet Information Services) is a web server software developed by Microsoft for Windows operating systems. It allows you to host and serve websites, web applications, and other web services on your Windows-based computer. IIS provides the infrastructure and tools necessary to handle HTTP requests, manage web content, and support various web technologies, making it easier to publish and manage websites on Windows servers. We need to set up IIS because osTicket runs out of a website and thus requires extra support.</p>

1. Within our Windows Virtual Machinne, right-click the 'Start Menu" (Windows icon on desktop) > select 'Run' > type 'Control' for Control Panel
2. Select 'Programs' > Select 'Turn Windows Features On & Off' > Enable [X] Internet Information Services
3. Expand [+] for 'World Wide Web Services' > Expand [+] for 'Application Developer' > [X] check 'CGI' 

<Strong>Why do we need CGI and what is PHP?</strong>

<p>This is because CGI allows us to install PHP Manager later and PHP is needed for osTicket. CGI (Common Gateway Interface) needs to be enabled on IIS (Internet Information Services) in order to install osTicket because osTicket relies on CGI scripts to process and handle certain web requests. CGI is a standard protocol that allows web servers like IIS to interact with external programs or scripts to generate dynamic content. PHP is a server-side scripting language that is widely used for web development. It is needed to run osTicket because osTicket is written in PHP and relies on PHP for its functionality. PHP allows osTicket to dynamically generate web pages, process form submissions, interact with databases, and perform various other tasks necessary for its ticketing system. It provides the underlying scripting capabilities that osTicket relies on to handle user interactions, store ticket data, and generate the appropriate responses.</p>

4. We can check that everything is working correctly by typing '127.0.0.1' into the search bar on Microsoft Edge within the VM. We can see that the default Internet Information Services webpage loads. 

<strong>Why type 127.0.0.1?</Strong>
<p>Typing '127.0.0.1' allows us to access the loopback address on our local machine. The loopback address refers to the computer itself, allowing you to access the web server or any other services running on your own machine.</p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br>

<h4>Item 2: Install PHP Manager for IIS</h4>

[LINK XXX -- MAKE OWN FILE WITH DOWNLOADS]

<Strong>What is PHP Manager and why is it needed for IIS/Installing osTicket later?</strong>

<p>PHP Manager is an IIS (Internet Information Services) extension for managing PHP installations on Windows servers. It is needed for installing osTicket because osTicket is written in PHP and requires a properly configured PHP environment to run.</p>

1. Use the link provided: click and download PHP manager
2. Navigate to Windows File Explorer > Downloads: it should appear there 
3. Open and install PHP manager with all default settings. Select: ‘I Agree’

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br>

<h4>Item 3: Download & Install Rewrite Module</h4>

[LINK XXX -- MAKE OWN FILE WITH DOWNLOADS]

<Strong>What is a Rewrite Module and why is it needed for osTicket?</strong>

<p>osTicket requires the Rewrite Module to be installed in order to utilize URL rewriting capabilities provided by the web server. URL rewriting is a technique that allows the modification of incoming request URLs, which can be helpful for creating user-friendly and search engine optimized URLs.

The Rewrite Module, typically used with IIS (Internet Information Services), enables osTicket to transform complex or dynamic URLs into more concise and meaningful ones. This enhances the usability and aesthetics of the URLs while ensuring proper navigation and linking within the osTicket system.

By leveraging the Rewrite Module, osTicket can achieve URL structures that are easier to read, remember, and share. It improves the user experience, search engine visibility, and overall accessibility of osTicket's support ticketing system.</p>

1. Use the link provided: click and download the Rewrite Module
2. Navigate to Windows File Explorer > Downloads: it should appear there
3. Open the Application > Agree to it > Install & Close

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br>

<h4>Item 4: Create Directory for PHP on the local hard drive</h4>

We want to create a PHP folder on the root of the C: Drive. This is because later we will download PHP and extract the contents into this folder. 

1. Open 'File Explorer' > select 'My PC' > Click 'C: Drive'
2. Right click inside of the C:Drive > 'New' > 'Folder' > name the folder 'PHP'

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br> 

<h4>Item 5: Download PHP 7.3.8 and Unzip Contents into C:\PHP</h4> 

[LINK XXX -- MAKE OWN FILE WITH DOWNLOADS]
 
 <Strong>Why is PHP needed for osTicket again?</strong>
 
 <p>PHP is needed for osTicket because it is the programming language in which osTicket is built. It enables osTicket to dynamically generate web pages, process form submissions, interact with databases, and provide the necessary functionality for a support ticketing system. Without PHP, osTicket would not be able to operate and deliver its ticket management capabilities to users.</p>
 
 1. Use the link provided: click and download the PHP 7.3.8 [Leave all the files as they are, just download it straight away]
 
 **Side note: If this comes up when downloading, select 'Keep' and 'Keep All'
 
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
 
 2. Naviagte to 'Downloads' in File Explorer > Right-click: 'Extract All'
 3. When it wants a destination to extract the contents in, we want to unzip into C:PHP folder: Click 'Browse' > 
 4. This PC > C: Drive > select 'PHP folder > 'Extract"

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br>

 <h4>Item 6: Download & Install C++ Restributable</h4>
 
 [LINK XXX -- MAKE OWN FILE WITH DOWNLOADS]
 
 <Strong>Why do we need to install Microsoft C++ Restributable in order to use osTicket?</strong>
 
<p>Microsoft C++ Redistributable software is required for installing osTicket because osTicket is built using the C++ programming language and relies on specific components provided by the Microsoft Visual C++ Redistributable packages. These packages contain essential runtime components and libraries necessary for osTicket to run smoothly and without compatibility issues. Installing the appropriate Redistributable software ensures that the required C++ dependencies are available on the system, enabling osTicket to function properly.</p>
 
1. Use the link provided: click and download VC Redist
2. Open ‘File Explorer’ > Downloads > double click to open > Agree & Install

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br>

<h4>Item 7: Install MySQL Server</h4>

 [LINK XXX -- MAKE OWN FILE WITH DOWNLOADS]
 
 <strong>What is MySQL and why is it needed to install osTicket?</strong>
 
 <p>MySQL is an open-source relational database management system (RDBMS) that is used to store and manage data. It is needed to install osTicket because osTicket requires a database to store ticket information, user data, and other related data. MySQL provides the backend storage and retrieval capabilities necessary for osTicket's ticketing system to function effectively and securely.</p>
 
 1. Use the link provided: click and download MySQL
 2. Follow the installation process. The things to take note of are:
 
 - Select 'Typical Install'
 - When the Config Wizard pops up: select 'Standard Configuration'
 - For credentials, the username is: 'root' and create a password. Password will be used later when registering/signing up for osTicket: Example password: 'Password1'
 - Select 'Execute' & 'Finish'

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br> 

<h4>Item 8: Configure IIS as Admin & Register PHP</h4>

<Strong>Why do we need to register PHP?</strong>

<p>We have downloaded PHP onto our machine, but it's not in a position to where it can be recognized by osTicket yet. Registering PHP on PHP Manager before installing osTicket is necessary to ensure that the correct PHP version and configuration are set up for osTicket. By registering PHP, PHP Manager can identify and manage the installed PHP version, extensions, and settings specific to osTicket's requirements. This ensures compatibility, performance, and proper functioning of osTicket within the IIS (Internet Information Services) environment, allowing the ticketing system to operate smoothly.</p>

1. Navigate to search bar on Windows desktop > Type 'IIS' > Right-click to 'Run As Administrator'
2. Double-click PHP manager > select 'Register New PHP Version'
3. Click the three dots icon to browse > click 'PHP' folder > PHP-CGI > select 'OK'
4. Select the VM were using within IIS > click 'Restart' (This is so the system can restart and reset with PHP now added. It is good practice to do so)

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br>

<h3>Step 3: Install osTicket</h3>

[LINK XXX -- MAKE OWN FILE WITH DOWNLOADS]

<Strong>What is osTicket and why is it useful?</strong>
osTicket is a popular open-source ticketing system that helps organizations efficiently manage customer support and inquiries. It provides a centralized platform for capturing, tracking, and resolving customer tickets, ensuring timely and effective communication. osTicket offers features such as ticket assignment, email integration, knowledge base, customizable forms, and reporting, making it useful for streamlining support processes, improving customer satisfaction, and maintaining organized customer interactions.

<h4>Downloading osTicket and Setting up IIS</h4>

1. Use the Download Link provided > Download osTicket 
2. Open 'File Explorer' > Open two Windows of File Explorer. Our goal is to Extract and Copy “Upload” folder to c:\inetpub\wwwroot:

- File Explorer 1: Navigate to 'Downloads' > osTicket > Double-click to unzip contents > You’ll see ‘Upload Folder’
- File Explorer 2: My PC > C: Drive > Inetpub > wwwroot

3. Drag and drop 'Upload' folder in wwwroot
4. Rename ‘Upload’ folder to ‘osTicket’: Right-click ‘Upload’ Folder > Rename > Rename to “osTicket”
5. Go back to IIS to now load osTicket website: search 'IIS' on Windows search bar > Right-click to 'Run as Administrator' > click 'VM-osTicket' > select 'Restart'
6. Inside of IIS: Navigate to 'VM-osTicket' > Expand [+] Sites > Expand [+] Default Web Site > Select "osTicket" > Select “Browse *:80” on the right

<p> We can see that the osTicket website has loaded! However, there are some items signaled by red X's. We're going to enable some extensions.</p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br>

<h4>Enabling IIS Extensions</h4>

1. Navigate back to 'IIS' > Select "VM-osTicket" > Expand [+] 'Sites' > Expand [+] 'Default Web Site' > Select 'osTicket' > select 'PHP Manager' 
2. Select 'Enable or disable an extension'
3. Enable the following extensions:

- Enable: php_imap.dll
- Enable: php_intl.dll
- Enable: php_opcache.dll

4. Go back to osTicket in browser > Refresh > notice how some of the red X’s turned green

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
 
<br>

<h4>Rename: ost-config.php & Changing Access Permissions</h4>

<p>Our goal is to change "C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php" into "C:\inetpub\wwwroot\osTicket\include\ost-config.php", essentially taking out the word "Sample"</p>

1. Navigate to 'File Explorer' > 'This PC' > C:Drive > 'inetpub' > 'wwwroot' > osTicket > 'include' folder
2. Scroll down within the 'include' folder until you find “ost-sampleconfig.php”
3. Rename to ost-config (erasing the word “sample”): Right-click the file name > Rename 

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br>

<p>osTicket needs to interact with this file in order to run. We don’t know what user its going to use, so we’re going to set the file permissions so anyone can access it so that there are no issues in trying to deploy/use osTicket due to user authentication and permissions:</p>

4. Right-click 'ost-config' file > Select 'Properties' > 'Security' > 'Advanced'
5. Select 'Disable inheritance' (so it stops inheriting permissions from the parent) > Select 'Remove all permissions'
6. To add permissions: select 'Add' > 'Select a principal' > type 'Everyone' & 'Check Names'> select 'Full Control' > 'Apply' & 'OK'

<p>Now everyone has permissions to ost-config</p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


<h4>Continue Setting Up osTicket in the Browser</h4>

1. In the browser, select "Continue" 
2. Fill out the fields: Examples below: (darin@helper.com is a fake email)
3. Install Heidi SQL: [LINKKKKKKK]

<strong>What is Heidi SQL?</strong>
<p>HeidiSQL is a user-friendly program that helps you manage and work with databases. It provides a graphical interface where you can connect to your databases, view and edit data, and perform various tasks without writing complex commands. It's a useful tool for developers and database administrators who want to interact with databases easily and efficiently. It allows us to communicate with the database we installed earlier: MySQL so that we can easily set up a database that osTicket can use.</p>

- Download Heidi SQL using the link above > Open in 'Downloads' within File Explorer
- Select 'Next' on everything > 'Install' > 'Finish'
- Another window of ‘Launch Heidi’ will open: Click ‘New’ cause were going to create a new connection to Database
- The username: 'root', password: 'Password1' (We created these when we downloaded mySQL server) > select 'Open'
- Now we have our connection to mySQL server: > Create a new database called “osTicket”

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

4. We can now finish setting up osTicket in the browser:

- Username: root, Password: 'Password1' (for example purposes)
- Database name: 'osTicket' (This was just created in HeidiSQL)
- Select 'Install Now"

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br>

<h4>Clean Up</h4>

1. We need to delete the 'Set Up' folder in C:\inetpub\wwwroot\osTicket\setup

- Navigate to 'File Explorer' > 'My PC' > C: Drive > 'inetpub' > 'wwwroot' > 'osTicket' > 'Set Up' folder > Right-click to Delete 

2. Set Permissions to “Read Only" within C:\inetpub\wwwroot\osTicket\include\ost-config.php

- Navigate to 'File Explorer' > 'My PC' > C: Drive > 'inetpub' > 'wwwroot' > 'osTicket' > 'Include' folder > Select 'ost-config'
- Right-click 'ost-config' > select 'Properties'
- select 'Security' at the top > select 'Advanced'
- select 'Everyone' > select 'Edit'
- Uncheck [ ] 'Full Control', 'Modify', 'Read & Execute' so that we only have 'Read' remains

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<br>

<h4>Testing Log In</h4>

There are two URL's:

- Admin Login: http://localhost/osTicket/scp/login.php
- End-User Login (where people can create tickets): http://localhost/osTicket/

1. Click the Admin Login link
2. Input the username/email & password created when signing up for osTicket earlier:

- Example: username: darin_admin

Congrats! We've successfully installed osTicket!

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>







