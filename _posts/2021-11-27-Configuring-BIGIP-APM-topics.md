---
layout: post
tags: Configuring BIG-IP APM Access Policy Manager 
title: Configuring BIG-IP APM Access Policy Manager 
categories: f5-apm
---

>> Ahmet Numan Aytemiz , 27.11.2021 - Ankara, Turkey

---

#### 1. Lab Topology

![Image](/img/apm-lab.png)


#### 2. Setting Up the BIG-IP System

- [Lab 2.1 Provisionig the BIG-IP System and Confirm Network Configuration](https://ahmetnuman.github.io/f5-bigip/f5-apm/2022/05/18/provisioning-bigip.html)

---

#### 3. Configuring Web Application Access

**Concepts and Technologies**

- Virtual Servers
- Pools, Pool Members and Nodes
- Full Proxy Architecture
- Load Balancing and Health Monitoring
- Source Address Translation
- Client and Server SSL Profiles (SSL Termination)
- HTTP Profiles
- Access Profiles, Access Polices and Visual Policy Editor
- Active Directory Authentication adn BIG-IP APM AAA Servers 

**Task**

`A new application has been created in three linux servers that are to be load balanced. We need to put it on the Internet as soon as possibe. Because the content is restricted to employees and partners, use Active Directory to authenticate.`

  - [ Lab 3.1 Web Applcaiton Access 1](https://ahmetnuman.github.io/f5-bigip/f5-apm/2022/05/19/web-application-access-1.html)  
  - [ Lab 3.2 HTTP Load Balancing](https://ahmetnuman.github.io/f5-bigip/f5-apm/2022/05/22/http-load-balancing.html)  
  - [ Lab 3.3 HTTPS Load Balancing](https://ahmetnuman.github.io/f5-bigip/f5-apm/2022/05/22/https-load-balancing.html)
  - [ Lab 3.4 Web Applcaition Access 2](https://ahmetnuman.github.io/f5-bigip/f5-apm/2022/05/23/web-application-access-two.html)
  - [ Lab 3.5 - HTTP Web App Access](https://ahmetnuman.github.io/f5-bigip/f5-apm/2022/05/24/http-web-app-access.html)

---

#### 4. Exploring The Access Policy

**Concepts and Technologies**

- Import, Export and Copy Access Profiles
- Add, Delete and Move Agents in the Visual Policy
- Add, Delete, Edit and Re-order Branches within the Agent
- New Redirect Endings and Customized Deny Endings
- Client OS Checking Agent

**Task**

`The Helpdesk is complaining because Linux users are being allowed to log on and connect to the Wiki, but it has only been tested with Windows (7 and later), Mac, IOS and Android.`

`We need to prevent any unsupported devices from connecting and we need to do that ASAP!!`

  - [ Lab 4.1 - Access Policy](https://ahmetnuman.github.io/f5-bigip/f5-apm/2022/05/24/access-policy.html)
  - [ Lab 4.2 - Policy Import , Export , Copy and Delete](https://ahmetnuman.github.io/f5-bigip/f5-apm/2022/05/24/policy-import-export-copy-date.html)
  - **Lab 4.3 - Allow Only Supported Platforms**

---  

#### 5. Managing BIG-IP APM

**Concepts and Technologies**

  - User Sessions
  - Session Cookies
  - Session Variables
  - Session Count Limits
  - Logging
  - Message Box

**Task : You had a maintenance windows scheduled last nihgt, but the CEO was in the middle of the demo'ing the Wiki to our partners in Japan at that time. Dont ever let that happen again, or we'll both be looking for new jobs!!**  


  - **Lab 5.2 - Managing APM**    
  - **Lab 5.2 - Find and Delete Active Sessions**    
  - **Lab 5.3 - Use a Logging Agent**    
  - **Lab 5.4 - Instrument the Policy**    
  - **Lab 5.5 - Inspect Session Cookies**
#### 6. Using Authenticaiton
  - **Lab 6.1 - Testing Active Directory**      
  - **Lab 6.2 - Alternate Authenticaiton**      
  - **Lab 6.3 - One Time Password**      
  - **Lab 6.4 - Local User Database**
#### 7. Understanding Assignment Agents*
  - **Lab 7.1 Dynamic Pool Assignmet**
  - **Lab 7.2 Two Factor Authenticaition**
#### 8. Configuring Portal Access
  - **Lab 8.1 Portal Access for OWA**       
  - **Lab 8.2 Portal Access for Server 2**
#### 9. Configuring Network Access
  - **Lab 9.1 Network Access aka SSL VPN**
  - **Lab 9.2 Source Address Translation**
  - **Lab 9.3 Network Access DTLS**
#### 10. Deploying Macros
  - **Lab 10.1 Access Policy Macros**
  - **Lab 10.2 Looping Macros**
  - **Lab 10.3 Simplify Policy with Macros**
  - **Lab 10.4 Virtual Keyboard Agent**
#### 11. Exploring Client-Side Checks
  - **Lab 11.1 Firewall Check**
  - **Lab 11.2 Wİndows File Check**
  - **Lab 11.3 Windows Info Check**
  - **Lab 11.4 Windows Process Check**
  - **Lab 11.5 Windows Registry Check**
  - **Lab 11.6 Windows Cache and Session Control**
#### 12. Exploring Server-Side Checks
  - **Lab 12.1 Date and Time Check**
  - **Lab 12.2 License Check**
#### 13. Using Authoization
  - **Lab 13.1 Dynamic Resource Assignment**
  - **Lab 13.2 Dynamic VPN Assignment**
#### 14. Configuring App Tunnels
  - **Lab 14.1 App Tunnel Resource**
  - **Lab 14.2 Network Access Optimized Tunnel**
  - **Lab 14.3 Remote Desktop Certificate Prep**
  - **Lab 14.4 Remote Desktop**
  - **Lab 14.5 Webtop Links**
#### 15. Deploying Access Control Lists
  - **Lab 15.1 Layer 4 ACLs**
  - **Lab 15.2 Layer 7 ACLs**
  - **Lab 15.3 ACLs and Portal Access**
  - **Lab 15.4 Dynamic ACLs for VPN**
#### 16. Signing On with SSO
  - **Lab 16.1 Remote Desktop SSO**
  - **Lab 16.2 Form-Bases SSO for OWA**
#### 17. Using iRules
  - **Lab 17.1 Insert HTTP Header iRule**
  - **Lab 17.2 Predefind Redirect iRule**
  - **Lab 17.3 Custom TCL Branch Rule**
  - **Lab 17.4 Variable Assign Using Advanced TCL**
  - **Lab 17.5 Launch iRule from Access Policy**
#### 18. Customizing BIG-IP APM
  - **Lab 18.1 Customized Logon Page**
  - **Lab 18.2 Webtop Sections**   
#### 19. Deploying SAML
  - **Lab 19.1 - SAML IdP and SP Services**  
  - **Lab 19.2 - SAML Attribute**  
#### 20. Exploring Webtops and Wizards
  - **Lab 20.1 - VPN Webtop from Wizards**  
  - **Lab 20.2 - OWA Webtop from Wizard**
#### 21. Using BIG-IP Edge Client
  - **Lab 21.1 - Big-Ip Edge Client**    
  - **Lab 21.2 - Big-Ip Edge Client CLI**    
  - **Lab 21.3 - Client Troubleshooting Utility**
 
