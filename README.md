<h1>Active Directory Home Lab (System Administration)</h1>

<img src="https://i.imgur.com/jy4tDFa.png" height="100%" width="100%" alt="Active Directory Homelab Cover"/> 

<h2>Description</h2>

This project serves as a demonstrative showcase of adept system administration skills, illustrating proficiency in constructing and managing complex network environments. By meticulously configuring a Microsoft Server to host Active Directory and deploying a Domain Controller, the undertaking underscores adeptness in system architecture and domain management.

The utilization of PowerShell scripting to automate user creation processes showcases a nuanced understanding of automation tools, streamlining administrative tasks and enhancing efficiency. Moreover, the successful integration of Windows 11 Enterprise and the Microsoft Server 2022 ISO within a VMWare virtualized environment underscores adaptability and proficiency in deploying contemporary technologies.

Through the seamless orchestration of these components, this project not only exemplifies technical expertise but also highlights the ability to navigate and optimize multifaceted IT landscapes, essential traits for effective system administration.

<br/>

<h2>Learning Objectives </h2>

- Understand the fundamental concepts of Active Directory and its role in network administration
- Develop skills in utilizing virtualization software (such as VMWare) to create and manage virtual machines
- Learn to set up and manage a Domain Controller within a network infrastructure
- Develop problem-solving skills through troubleshooting any issues encountered during the setup and configuration process
- Acquire proficiency in using PowerShell scripting to automate administrative tasks within a Windows environment
- Understand domain connectivity principles and authentication mechanisms, exemplified through logging into user accounts within a domain environment
  
<h2>Technologies + Requirements </h2>

- Virtualization Software: <a href="https://www.vmware.com/content/vmware/vmware-published-sites/us/products/workstation-pro/workstation-pro-evaluation.html.html"> VMware Workstation Player <a/> or <a href="https://www.virtualbox.org/wiki/Downloads"> Oracle Virtualbox </a>
- <a href="https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022"> Microsoft Windows Server 2022 <a/>
- <a href="https://www.microsoft.com/en-in/evalcenter/download-windows-11-enterprise"> Microsoft Windows 11 Enterprise <a/>
> You will need to download the files above beforehand
- Powershell
- Active Directory
- CMD

<h2>Lab Walk-Through</h2>

> <b>To accommodate my Domain Controller on the Virtual Machine, I require two network adapters. Firstly, a NAT adapter utilizing my home router's IP address to facilitate external connectivity, and secondly, an Internal Network Adapter (VMnet0) to enable communication with other Virtual Machines. Please consult the diagram provided earlier for reference</b>

<img height="100%" width="100%" alt="adhl_1 1" src="https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/809a2589-54f6-474c-bcef-8714e5ac431e">

<img height="100%" width="100%" alt="adhl_1 2" src="https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/8d42f7a6-55c3-40cb-9468-7ebe375725da">

> <b>Upon installing Windows Server 2022 on the Virtual Machine, my initial task involves configuring the two network adapters at my disposal: one designated for external connectivity and the other for internal network communication</b>

<img height="100%" width="100%" alt="adhl_1 3" src="https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/9b44d5c7-dcf0-44fc-9e76-8441cfe144ca">

> <b>Now, I need to determine which NIC serves as our NAT. Ethernet0 is identified as the NAT adapter since its DNS is assigned to "localdomain."</b> 

<img height="100%" width="100%" alt="adhl1 4" src="https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/248cd244-c363-43eb-ba45-e96493672bc8">

<img height="100%" width="100%" alt="adhl_1 5" src="https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/de70b3c2-7c58-42dd-8398-56d88869572c">

> <b>I proceed to rename the adapters for clarity, which will prove beneficial during the subsequent setup of the Domain Controller (DC) and DHCP</b>

![adhl1 6](https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/aa85bc5c-5f69-4baa-9a8e-8fddcc3d6511)

> <b>Next, I configure the Internal network adapter, assigning it the IP address depicted in the diagram (172.16.0.1). Omitting a default gateway is intentional since the Domain Controller serves as the gateway. For DNS server configuration, I allocate an IP address per the diagram, anticipating Active Directory installation, which automatically installs DNS. I designate it as a loopback address to enable self-pinging</b>

![adhl1 7_configntwk](https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/a0ae5578-0e7a-4c83-a486-b58d69645bd0)

> <b>Having identified the external and internal network adapters, I proceed to rename the PC from its current long and complex name to simply "DC" (Domain Controller). This action necessitates a restart, which is acceptable</b>

<img height="100%" width="100%" alt="adhl1 8" src="https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/00c53f49-b02a-4565-a9a1-2f1d08aa3162">

> <b>Upon rebooting, I initiate the download process for Active Directory</b>

https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/3fbb824a-b8af-4411-8853-8b89014ac68b

> <b>I've installed Active Directory Domain Services, but we haven't yet designated the server (or computer) as the domain. Now, I need to proceed with creating the domain</b>

https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/41cbb45f-4035-4857-b273-6c9e901d0449

> <b>Upon promoting the server to a domain, a restart is enforced. Upon logging back in, you'll notice that the domain has been successfully created as my admin account now displays "MYDOMAIN" prefixed to it</b>

<img height="100%" width="100%" alt="adhl_2 2" src="https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/38ff04b8-4ecf-4766-82a3-d5be190c5173">

> <b>Now, instead of relying on the built-in Admin account, I will establish a dedicated domain Admin account</b>

https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/7f7503e9-0482-41b5-9d2d-174b37473e90

> <b>I've created a domain-specific admin account, but it lacks administrative privileges. To rectify this, I navigate to Active Directory and elevate this new account to Administrator status. Once completed, I log out of the built-in Admin account and log in using my newly created Domain Admin account<b>

https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/242f1af5-dee4-4066-ba14-902c29b92200

> <b>Next, I must install and set up the RAS/NAT to enable my Windows 11 client computer to access the internet via the internal network routed through the Domain Controller<b/>

https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/adc8cf60-1c6c-46e7-ac9c-d459afc4f579

> <b>With the role successfully installed, the next step is to configure the Routing and Remote Access functionality</b>

https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/90498c51-c780-4776-a80e-3a97b725edc4

> <b>Excellent! With Remote Access installed and configured, it's time to proceed with installing a DHCP Server. This step will facilitate the assignment of IP addresses to our Windows 10 clients, enabling them to browse the internet seamlessly</b>

![adhl_2 6_dhcp_install](https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/283d6b8b-2ffd-4116-b743-27d4794e7407)

> <b>Now, let's configure the DHCP and establish a scope. DHCP's primary function is to automatically assign IP addresses to computers on the network. The scope I'm creating will allocate IP addresses within the range of 192.168.1.100 to 192.168.1.200, providing DHCP the capability to assign 100 IP addresses effectively. Additionally, I've set the lease duration to 8 days. This lease ensures that once an IP address is assigned, it remains reserved for that device for a specified period. Without it, new devices couldn't obtain IP addresses, hindering their ability to connect to the internet.

> To illustrate, consider a scenario like a library offering Wi-Fi access. If patrons typically spend around 2 hours inside, it wouldn't be practical to lease an IP address for 8 days. This would tie up the IP address unnecessarily. In such a case, it's advisable to set the lease duration to under 4 hours and allocate a broader range. However, for a virtual environment like ours, where usage is temporary, the lease duration isn't crucial</b>

https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/2dbc7973-868f-4e64-b29c-d68acf537345

> <b>In order to retrieve my PowerShell script from the internet, I must enable web browsing capabilities. This involves temporarily disabling security features on the Domain Controller. It's crucial to note that in a real production environment, such actions would never be taken due to the inherent security risks. However, since this setup is solely for personal lab experimentation, security concerns are less of an issue. While technically possible to browse the internet without this step, it would result in a barrage of warnings for every webpage visited, which can be quite bothersome</b>

![adhl_2 8_toggleoff_ie_security](https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/8cada394-b44d-4926-9fce-8d77258583a3)

> <b>With Active Directory and my Domain Controller properly configured, I utilize a PowerShell script to generate more than 1000 user accounts. Below is a video showcasing the script in action!</b>

https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/def52115-f57e-4330-be61-7812c973580e

> <b>The script has executed without any issues, and the visual confirmation of the created user accounts is quite impressive. While there were some duplicates that were not created, resolving this is straightforward by enhancing the PowerShell script with additional lines of code to handle duplicates. For instance, we can instruct the script to append a "1" to the end of the account name if a duplicate is encountered. If you're interested in reviewing the complete code utilized, please refer to the top of this repository. The script can be found under the name "CREATE_USERS.ps1."</b>

<img height="100%" width="100%" alt="adhl_3 1" src="https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/0a7f43a7-6a33-4399-8e1a-00dba0679aec">

> <b>The next step is to establish a new Virtual Machine, which will function as a user within the domain. I designate this machine with the name "CLIENT1."</b>
<img height="100%" width="100%" alt="adhl_3 2" src="https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/5a04a9a0-1d1b-4cd8-81ae-b382c9f72470">

> <b>I adjust the network adapter settings to disable NAT and restrict internet access within my local network. The sole means for this Virtual Machine to connect to the internet is by obtaining an IP address from the Domain Controller on the Server VM. To accomplish this, I configure the network adapter to operate within the same internal network as the Domain Controller, utilizing VMnet0, as indicated in the initial diagram</b>

<img height="100%" width="100%" alt="adhl_3 3" src="https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/80b2f053-2f9a-4134-ac02-b615051f2240">

> <b>Following the setup of a distinct virtual machine to simulate an employee logging into the domain, I streamline the process by renaming the computer to CLIENT1 and selecting the option to join the mydomain.com domain. As part of this step, I'm prompted to provide login credentials, and I opt to utilize the Administrator account that I established previously</b>

<img height="100%" width="100%" alt="adhl_3 4" src="https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/82d04817-ddaf-4503-8616-80e680410418">

> <b>I have successfully become a member of the domain!</b>

<img height="100%" width="100%" alt="adhl_3 5" src="https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/476ad0bb-f4f7-491d-8c67-454a10c62514">

> <b>I log into a user account generated from the PowerShell script to verify the correctness of the configurations. Rather than accessing the user account created during the virtual machine setup, I attempt to log into a user account established within MYDOMAIN</b>

![adhl_3 6](https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/15098e55-a8c4-4c2c-925a-0ab60a7f4644)

> <b>I'm running Command Prompt to verify if the client VM is correctly receiving the assigned IP address from the DC. As shown by the purple circle, it confirms that I have been successfully leased an IP address by the domain controller. Additionally, the green circle highlights successful pinging of the domain, indicating proper connectivity</b>

<img height="100%" width="100%" alt="adhl_3 7" src="https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/4d2fe7d3-0d5d-4173-a4c1-64b5e555e573">

> <b>A conclusive test to ensure the functionality of the work environment and the bulk users I've created</b>

<img height="100%" width="100%" alt="adhl_3 71" src="https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/11ec8839-e505-4c93-96ff-d5389c517cbc">

> <b>Returning to my server VM, I review the DHCP to assess the number of leased addresses. As highlighted in red, it's evident that my CLIENT1 Virtual Machine has been assigned an address. In a real corporate setting, this folder would likely contain hundreds, if not thousands, of leased addresses, depending on the lease duration. Of course, the number varies depending on the specific environment; in this instance, I've set the lease duration to 8 days</b>

<img height="100%" width="100%" alt="adhl_3 72" src="https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/0a5e4ee2-5c61-41f8-a638-12deefdf764c">

> <b>Here's an alternative method to monitor the current connected devices within the domain. It's evident from Active Directory that my CLIENT1 computer is being accurately recognized. In a genuine corporate setting, this folder would likely contain a multitude of devices, potentially numbering in the thousands</b>

<img width="957" alt="adhl_3 73" src="https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/b84ffe5d-35c9-4b8c-8d1e-c8d7e173d9e2">

> <b>Here, I'm scrolling through the User accounts generated using PowerShell. Remarkably, over 1000 accounts have been successfully created!</b>

![adhl_3 8](https://github.com/portfoleyo/ActiveDirectoryHomeLab/assets/50858187/8792e616-d3e3-4e44-bdbd-a5ba3a22157d)
