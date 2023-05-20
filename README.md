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

<h4>Logging into our Virutal Machine</h4>

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

<strong>What is IIS?</strong>

<p>IIS (Internet Information Services) is a web server software developed by Microsoft for Windows operating systems. It allows you to host and serve websites, web applications, and other web services on your Windows-based computer. IIS provides the infrastructure and tools necessary to handle HTTP requests, manage web content, and support various web technologies, making it easier to publish and manage websites on Windows servers. We need to set up IIS because osTicket runs out of a website and thus requires extra support.</p>






















