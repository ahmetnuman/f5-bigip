## WAF Security Models

#### Policy Building By Whitelisting Entities

- File types (object extensions like .png , .jpg etc.)
- URLs (directory + object name which is the web file)
- Parameters (these are the names we stored value)
- Cookies 
- Redirection Domains

#### Policy Building By False Positive Elimination

- Attack signature and other triggered violations

#### Positive Security Model

- Firewalls : Permit what is necessary and deny everthing else
- WAF : Permit Entities such as File Types, URLs, Parameters, Cookies , Redirection Domains

#### Negative Security Model

- IPS : deny what is unnecessary and permit everthing else 
- WAF : uses complieance, evasion detection , blacklist and attack signature
- WAF : Considered the default policy. Faster and easier

Waf can use both Positive and Negative Security Model

#### Key Questions in Relation to which Security Models to use

- Do apps change frequently ?
- Are apps complex ?
- How many apps ?
- What protections are most important ?
- How many security policy ?
- How much time do we have ?

