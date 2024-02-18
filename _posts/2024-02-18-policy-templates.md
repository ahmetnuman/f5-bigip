## Policy Deployment Workflow 

#### Main Components 

- Virtual Server 
- Security Policy aka Policy

#### Security Policy Basic Settings

- Policy Name 
- Policy Type - Standart or Parent
- Policy Template (Rapid Deployment , Comprehensive, Vulnerability Scanner etc.)
- Select Virtual Server 

#### How Will the Policy be applied ?

- Stand alone Policy 
- Parent Policy 

#### Rapid Deployment / Application-Ready / Vulnerability Scanner Output (Tier 1)

- Full HTTP RFC Compliance
- Attack Signature 
- Application-specific objects
- Scan results

#### Fundamental (Tier 2)

- Attack Signatures
- More app component protection

#### Comprehensive Passive (Tier 3)

- Some HTTP RFC Compliance
- Attack Signatures
- Full app component protection

Note : Rapid Deployment Poicy uses maneal policy building, Fundamental and Comprehensive polices are usinf automatic policy deployment (by default)

#### Assigning Security Policy to Virtual Server

- Create Virtual Server
- HTTP or HTTPS
- Host address and port
- assign pool
- Enable HTTP Profile
- Enable ASM 
- Assign a security policy

#### Policy Building 

- Manual 
- Automatic

#### Rapid Deployment

- Manual 
- Admin interprets events and learinig suggestions and takes action

#### Fundamental and Comprehensive (Passive)

- Automatic 
- ASM interprets events and learingn suugestions and takes action 
- Passive = ASM takes no action / impact on traffic

#### Disabling Case Sensitivity in Policies

By default, the BIG-IP ASM system is case-sensitive; however, to reduce the chance of false positives, F5 recommends that you create policies with case sensitivity disabled.

While most web applications do not treat URIs with case sensitivity, some do. In such applications, example.html and Example.html may access different web pages, each with their own associated content, parameters and security access controls. In such cases, enabling case sensitivity is required.




