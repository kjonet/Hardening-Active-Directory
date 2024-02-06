![img](https://i.imgur.com/vrLa8Ma.png)

# Active Directory Hardening

Active Directory is a directory service from Microsoft that runs on Windows Server and connects users and devices on a centralized network. Because this is a powerful directory service, it's important to make sure the best hardening practices are implemented. That is what we'll do in this lab. 

# Objectives 

I will be hardening Active Director on a domain controller I have set up on a virtual machine. By the end of this lab, we will have covered the following: 

- Secure authentication methods
- Host security using group policy
- Implementing Least Privilege
- How To Prevent Unauthorized RDP Access
- Configuring a Microsoft compliance toolkit
- Recovery Plans

# LAN Manager Hash 

Since users within an organization are connected to a centralized network, it's imperative that we verify the users who are connected. This process is called <b>Authentication</b> Authentication helps verify the identity of the individual attempting to gain access to a system, application, or resource. Let us configure some security policies in the <b>Group Policy Managment</b> that will enable authentication. 

<b> Open Group Policy Management Editor > Computer Configuration > Policies > Windows Setting > Security Settings > Local Policies > Security Options > double-click Network security - Do not store LM hash value on next password change policy > click "Define policy setting" </b>  

<b> Why are we enabling this policy? </b>

This is considered a legacy authentication method that is now prone to brute-force attacks. Enabling the policy, <b>Network security - Do not store LM hash value on next password change policy prevents storing password's LM HASH.</b> 

# SMB Signing 

Server Message Block, or SMB, is a protocol used by Microsoft for file and print sharing. SMB is also a more secure way to transfer files over the network. SMB traffic could still fall prey to a man-in-the-middle attack so to help detect these attacks, SMB signaling will need to be configured through group policy. 

<b></b>Open Group Policy Management Editor > Computer Configuration > Policies > Windows Setting > Security Settings > Local Policies > Security Options > Double-click Microsoft network server: Digitally sign communication (always) > click Enable Digitally Sign Communications"</b>


![img](https://i.imgur.com/dFPizgF.png)
![img](https://i.imgur.com/wjuvD3f.png)

# LDAP Signing 

LDAP, or Light Weigh Directory Access Protocol is used to manage and authenticate directory resources. LDAP signing is useful in deterring replay or man-in-the-middle attacks, Simple Authentication and Security Layer (SASL) needs to be enabled so only signed LDAP requests are accepted. 

<b>Group Policy Management Editor > Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options > Domain controller: LDAP server signing requirements > select Require signing from the dropdown</b>

![img](https://i.imgur.com/pkf3fdM.png)

# Password Policy

It's important to implement strong password policies to uphold proper authentication and maintain authorization. Some of these policies include minimizing/maximizing the password age, enforcing password history, enabling password complexity, and enforcing a good password length. Enforcing a strong password policy helps deter password spraying, dictionary attacks, and brute force.

<b>Group Policy Management Editor > Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy</b>

![img](https://i.imgur.com/nLzOdZr.png)

<b>Multi-Factor Authentication</b>

Implementing multi-factor authentication is a great way to enable proper authentication and authorization of an organization's users. Multi-factor can come in all sorts of varieties as well. It can be location-based, meaning, users can only authenticate from a certain IP address. It can be based on a push notification sent by an authentication app in addition to having a username and password or it can be token-based, meaning every time a user signs it, it must use a one-time generated password. 

# Least Privilege 

When it comes to assigning roles within your organization, enforcing the principle of Least privilege is crucial to ensure only specific users have access to the appropriate resources needed to complete their tasks in their roles. This principle helps to reduce possible risks and improves an organization's security posture. 

<b>Examples: </b>

- File sharing: Katie, who works in marketing, needs to access a file from the accounting share, however, due to her role in the organization, she is unable to access the mapped drive that only users in the accounting department have access to.
- User Account Permissions: Tom is working on a proposal for his department's budget but wants to use a software called, Grammarly, to help him improve his sentence structure. When he goes to download it, he is unable to. He will need to reach out to certain users in his organization (most likely the sys admin or tier 1-3 help desk employees) who have authorization and can download the tool he needs.
- Database Access Control: Mary, who works in the creative department, is curious about learning SQL in her downtime and decides to open and play around with Microsoft Management Studio during her downtime. The software is already installed on her desktop but when she goes to look through the databases, she is not able to. Databases house sensitive information and because Mary's role does not require her to deal with sensitive information, her access to the company databases is restricted. 

As a systems administrator, the right accounts must be properly set up and given the appropriate permissions. Conducting an audit for accounts regularly is also crucial in making sure all accounts have the right access permissions. 

# Preventing Unauthorized RDP access

RDP is prone to brute-force attacks and without the proper security implementations, malicious attackers could remote into an organization's system leaving it prone to data loss and worse. 

Here are some recommendations that could help prevent this: 

- Whitelisting Source IP Addresses: This will allow authorized users to access the protocol if needed while preventing IP addresses that are not whitelisted, from gaining access.
- VPN Configuration: When using RDP, enforcing a virtual private network will provide a safe and encrypted tunnel for users to connect securely.
- Log Monitoring: Actively monitoring network logs will help to spot malicious attackers attempting to gain access before it escalates.
- Network Segmentation: Segmenting parts of your network can help minimize unauthorized access. 


# Microsoft Security Compliance Toolkit (MSCT)  

To help give organizations an idea of how their domain-level policies should look, Microsoft created a tool called Microsoft Security Compliance Toolkit (MSCT). The Microsoft Security Compliance Toolkit is there to help organizations provide recommended security configurations across their Microsoft-based systems by providing helpful resources to ensure a high standard when it comes to maintaining security posture. 

![img](https://i.imgur.com/Wz4mOq2.png)

# Conclusion

By implementing these various security measures, you can help mitigate unauthorized access to your domain. This can be done by ensuring secure authentication methods, such as multi-factor authentication, to bolster user verification. Also, incorporating secure group policies to enforce strict access controls and limit user privileges to the bare minimum is a simple yet effective way of maintaining a secure domain. To prevent unauthorized access via Remote Desktop Protocol (RDP), you can enforce the use of secure protocols and restrict RDP access to trusted IP addresses or VPN connections only. Finally, leveraging the Microsoft Security Compliance Toolkit (MSCT) is an excellent resource that can help organizations maintain compliance and protect against various cyber threats.








