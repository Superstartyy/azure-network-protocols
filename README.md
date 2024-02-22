# azure-network-protocols
<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

 1. File sharing with various permissions
 2. Acessing file shares as a normal user
 3. Security Group, assigning's & permissions




<h2>Actions and Observations</h2>


![image](https://github.com/Superstartyy/azure-network-protocols/assets/159973263/1f56b9a6-3a53-4a0f-a8cf-ced9c59de739)

Log into DC-1 using the domain admin account (mydomain.com\jane_admin) and log into Client-1 with a regular user account (mydomain<someuser>). On DC-1, navigate to the C:\ drive and establish four folders: "read-access," "write-access," "no-access," and "accounting." Assign specific permissions and share the folders accordingly to the "Domain Users" group: "read-access" grants the "Domain Users" group Read permissions, "write-access" provides Read/Write permissions, and "no-access" assigns Read/Write permissions to the "Domain Admins" group. 
</p>
<br />



![image](https://github.com/Superstartyy/azure-network-protocols/assets/159973263/fad521dd-8a10-4fbe-a046-3404690c299e)


Accessing the shared folder on Client-1 by navigating to \dc-1, I can access the "read-access" folder, view its contents, and create new items within it. However, I can't access the "write-access" folder, and the "no-access" folder doesn't appear to be listed. This aligns with the assigned permissions, as intended: "read-access" provides read-only access, "write-access" allows read and write actions, and "no-access" is restricted to the "Domain Admins" group.
</p>
<br />



![image](https://github.com/Superstartyy/azure-network-protocols/assets/159973263/5f75e529-ed54-4195-a530-af5fe42d778b)



<p>
Upon creating a security group named "ACCOUNTANTS" in Active Directory on DC-1, I assigned "Read/Write" permissions to the "accounting" folder for this group. When attempting to access the "accounting" folder on Client-1 as <someuser>, the access failed initially. After adding <someuser> as a member of the "ACCOUNTANTS" Security Group on DC-1, subsequent attempts to access the "accounting" share on \DC-1\ were successful.
<br />
