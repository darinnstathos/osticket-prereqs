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
3. We'll name our Resource Group: "RG-osTicket". There is nothing left for us to alter so select 'Review + Create'
4. Navigate to 'Virtual Machines' within Azure via quick access icon or search bar > select 'Create Virtual Machine'
5. Within the Virtual Machine portal, we will make the following changes:

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
 
 <Strong>Why do we need to install Microsoft C++ Restributable in order to use osTicket?</strong>
 
<p>Microsoft C++ Redistributable software is required for installing osTicket because osTicket is built using the C++ programming language and relies on specific components provided by the Microsoft Visual C++ Redistributable packages. These packages contain essential runtime components and libraries necessary for osTicket to run smoothly and without compatibility issues. Installing the appropriate Redistributable software ensures that the required C++ dependencies are available on the system, enabling osTicket to function properly.</p>
 
 














