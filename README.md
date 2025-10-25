# Identity and Access Management in Active Directory – Home Lab Documentation

## 1. Introduction

This documentation outlines the process I followed to implement **Identity and Access Management (IAM)** using **Active Directory Domain Services (AD DS)** in a virtualized lab environment.  
The goal was to simulate a small organizational network where user identities, permissions, and policies could be centrally managed through a Domain Controller.

## 2. Objectives

The main objectives of this setup were:

- To understand how user and group management works within Active Directory.  
- To configure centralized authentication and access control.  
- To practice Group Policy management for enforcing system rules.  
- To simulate a basic domain environment similar to a workplace network.

## 3. Lab Environment Setup

**Virtualization Platform:** Oracle VirtualBox  
**Operating Systems Used:**  
- 1 × Windows Server (used as Domain Controller)  
- 2 × Windows 8 clients  

**Network Configuration:**  
All machines were connected using bridged network in VirtualBox.  
The server had a static IP address, which was later set as the DNS for the client machines.

## 4. Implementation Process

### Step 1: Installing Active Directory Domain Services (AD DS)

I started by installing the AD DS role on the Windows Server through the Server Manager. Once installed, I ran the configuration wizard to promote the server to a **Domain Controller**.

### Step 2: Promoting the Server to a Domain Controller

During promotion, I created a **new forest** and specified a custom domain name (`techouse.io`).  
The system automatically installed DNS Server services as part of the configuration.

### Step 3: Creating Organizational Units (OUs)

After logging into the new domain, I opened the **Active Directory Users and Computers (ADUC)** console and created an **Organizational Unit (OU)** which are branches of the organization in different locations to structure user and computer accounts.  
For example, I created an OU named `Lagos`, `UK` and another named `US`.

### Step 4: Creating Users and Groups

Within the `OUs`, I created several **user accounts** with varying roles to simulate different types of departments (e.g., IT, finance, marketing).  
I also created **security groups** (e.g., `ITAdmins`, `StandardUsers`) to manage permissions more efficiently.

### Step 5: Configuring Client Machines

On each Windows 8 client, I changed the **DNS settings** to point to the server’s IP address.  
Then, I joined both clients to the domain (`techouse.io`) using the “System Properties” > “Change Settings” option.  
After a restart, users could log in using their domain credentials.

### Step 6: Creating and Linking Group Policy Objects (GPOs)

To apply consistent rules, I created a **new Group Policy Object (GPO)** and linked it to the `OU`.  
Inside the GPO, I configured a few basic policies — such as restricting access to Control Panel, enforcing password complexity, and displaying a logon message.  
The policies were refreshed using the `gpupdate /force` command on client machines.

## 5. Testing and Validation

I tested the configuration by logging in with different domain accounts on the client PCs to confirm:

- Users could authenticate against the Domain Controller.  
- Group policies were applied correctly (e.g., restrictions and logon messages worked).  
- The domain DNS resolved properly.

## 6. Challenges and Troubleshooting

A few small issues came up:

- Initially, one client couldn’t join the domain due to incorrect DNS settings. Fixing the DNS to point to the server resolved it.  
- GPO changes didn’t apply immediately until I used `gpupdate /force` and restarted the clients.

## 7. Conclusion

This lab successfully demonstrated how Active Directory manages user identities and access controls within a network.  
Through this process, I gained a practical understanding of creating and organizing OUs, users, and groups, configuring DNS, joining clients to a domain, and applying group policies to enforce security standards.
