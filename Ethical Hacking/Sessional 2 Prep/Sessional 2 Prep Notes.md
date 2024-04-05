| Lecture Title                       | Status             |
| ----------------------------------- | ------------------ |
| Lecture 7 - Enumeration             | :white_check_mark: |
| Lecture 9 - Vulnerability Analysis  | :white_check_mark: |
| Lecture 10, 11, 12 - System Hacking | :warning:          |
| Lecture 14, 15 - Malware Threats    | :white_check_mark: |

<!--
:x:
:warning:
:white_check_mark:
-->


# Lecture 7 - Enumeration
## What is Enumeration
- Internally Conducted, attacker/scanner has to be part of the network i.e. the environment is an intranet.
	- Discover hosts and services available on the network
	- Create NULL Sessions where a connection is established but not authenticated to extract info. For example, SV scans from nmap to get OS info
- Involves the attacker creating active connections and performing directed queries to gain more info on the target
- Looking for
	- Usernames
	- Groups
	- Machine Names
	- Network Resources
	- Services Running
	- Routing Tables
	- Auditing Services
	- Applications
	- DNS & SNMP info
## Techniques of enumeration
- Email/Business Cards
	- Getting an email ID can reveal the username and the domain name of the target
- Windows Groups
	- Interal domains and groups
- Default Passwords
	- Known default passwords or a policy stating a default password that needs to be changed
		- Use art of misdirection here
- SNMP
	- Extract usernames via the API
- Brute Force AD
	- Can enumerate throughout the AD to get users when "Logon Hours" is enabled
	- Tells the attacker if a username exists or does not. Design flaw of AD.
- DNS Zone transfers
	- Used to replicate DNS Data across several DNS servers or backups. Successful Auth of a Zone transfer request dumps all IP and DNS of the server into an ascii file
	- If proper auth is not setup, anyone can init a Zone Transfer and get all hosts within that domain. Can be performed using NSLOOKUP and DIG commands
- WindowsSysInternals
	- Shows who has what access to directories, files and registry keys

## Services and Ports to Enumerate
- TCP/UDP 53 -> DNS Zone Transfer
	- DNS servers commonly communicate over UDP, but if the request URL exceeds 512 octets, it's invalid, prompting a TCP request. This mechanism serves as a failsafe for larger queries.
- TCP/UDP 135 -> RPC Endpoint Mapper
	- Authentication is not typically required, making it susceptible to multiple types of attacks.
- TCP/UDP 389 -> LDAP
	- Exploiting misconfigurations can lead to username enumeration, revealing sensitive information.
- TCP/UDP 3268 -> Global Catalog Server
	- Acts as a distributed data storage in a domain controller, enabling searches across all domains in an Active Directory network.
- TCP/UDP 445 -> SMB over TCP
	- Provides file and printer sharing services among networked computers, commonly exploited for unauthorized access.
- UDP 161 -> SNMP
	- Requests can be sent to SNMP agents for network management purposes.
- TCP/UDP 162 -> SNMP Trap
	- Receives responses for SNMP requests (port 161) and is used for system uptime notifications and time synchronization.
- UDP 137 -> NetBIOS Name Service
	- Provides name resolution for devices on the same local network.
- TCP 139 -> SMB over NetBIOS
	- Primarily used for file sharing and printing services. Vulnerable to NULL session enumeration, exposing system information.
- TCP 25 -> SMTP
	- SMTP commands like VRFY and EXPN can be exploited to confirm valid usernames and reveal aliases or mailing lists, respectively.
- UDP 500 -> ISAKMP
	- Facilitates the negotiation of cryptographic keys for IPsec VPN connections.
- TCP 22 -> SSH
	- Secure Shell protocol for secure remote access to systems, typically used for administration purposes.
- TCP 2049 -> NFS
	- Network File System used for sharing files between networked devices. Exploitable for unauthorized remote and privileged access.

## Microsoft tools to enumerate with (PsTools Suite)
- PsExec -> Executes processes remotely
- PsFile -> Shows files opened remotely
- PsGetSID -> Displays the SID of a computer/user
- PsKill -> Kills processes by name/process ID
- PsInfo -> List info about a system
- PsList -> Lists detailed info on processes
- PsLoggedOn -> Shows who is logged on locally/via resource sharing
- PsLogList -> Dumps event log records
- PsPasswd -> Change account password
- PsShutdown -> Shutdown/reboot a computer

## Enumeration Countermeasures

| Protocol | Countermeasure                                                                                                                       |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| SNMP     | Remove the SNMP agent or turn off the SNMP service                                                                                   |
| \*       | If shutting off SNMP is not an option, then change the default community string names                                                |
| \*       | Upgrade to SNMP3, which encrypts passwords and messages                                                                              |
| \*       | Implement the Group Policy security option called "Additional restrictions for anonymous connections"                                |
| \*       | Ensure that the access to null session pipes, null session shares, and IPSec filtering is restricted                                 |
| \*       | Do not misconfigure SNMP service with read-write authorization                                                                       |
| DNS      | Disable Zone-Transfers to untrusted hosts                                                                                            |
| \*       | Ensure that the private hosts and their IP addresses are not published in DNS zone files of public DNS servers                       |
| \*       | Use premium DNS registration services that hide sensitive information, such as host information (HINFO) from the public              |
| \*       | Use standard network admin contacts for DNS registrations to avoid social engineering attacks                                        |
| SMTP     | Ignore email messages to unknown recipients                                                                                          |
| \*       | Exclude sensitive mail server and local host information in mail responses                                                           |
| \*       | Disable open relay feature                                                                                                           |
| \*       | Limit the number of accepted connections from a source to prevent brute-force attacks                                                |
| LDAP     | By default, LDAP traffic is transmitted unsecured; use SSL or STARTTLS technology to encrypt the traffic                             |
| \*       | Select a username different from your email address and enable account lockout                                                       |
| \*       | Use NTLM or any basic authentication mechanism to limit access to legitimate users only                                              |
| SMB      | Disable SMB protocol on Web, DNS and any Internet-Facing Servers                                                                     |
| \*       | Disable ports TCP 139 and TCP 445 used by the SMB protocol                                                                           |
| \*       | Restrict anonymous access through RestrictNullSessAccess parameter from the Windows Registry                                         |
| NFS      | Implement proper permissions (read/write must be restricted to specific users) on exported file systems                              |
| \*       | Implement firewall rules to block NFS port 2049                                                                                      |
| \*       | Ensure proper configuration of files, such as /etc/smb.conf, /etc/exports and ete/hosts.allow, to protect the data stored in servers |
| \*       | Log requests to access system files on the NFS server                                                                                |
| \*       | Keep the root_squash option in /etc/exports file turned ON, so that no requests made as root on the client are trusted               |
| FTP      | Implement secure FTP (SFTP, which uses SSH) or FTP secure (FTPS, which uses SSL) to encrypt the FTP traffic over the network         |
| \*       | Implement strong passwords or a certification-based authentication policy                                                            |
| \*       | Ensure that unrestricted uploading of files on the FTP server is not allowed                                                         |
| \*       | Disable anonymous FTP accounts; if not feasible, regularly monitor anonymous FTP accounts                                            |
| \*       | Restrict access by IP or domain name to the FTP server                                                                               |

# Lecture 9 - Vulnerability Analysis
## Concept
- Discover weaknesses/designFlaws in an environment that can cause the OS, Application and/or Website to be misused
- **Causes**
	- Misconfigs
	- default configs
	- buffer overflows
	- OS flaws
	- Open services
## Types of VA
- **Active Assessments**:
	- Process of VA which includes actively sending requests to the live target and examining responses
- **Passive Assessments**:
	- Use of packet sniffing, monitoring directory changes, Seeing what services are available and running
- **External Assessments**:
	- Conduct VA on Systems from the outside
- **Internal Assessments**:
	- Scanning the internal network
- **Tree-Based Assessments**:
	- Use of multiple approaches to conduct the assessments for e.g. the auditor might use a technique for windows that might not be the same for ubuntu
- **Inference-Based Assessments**:
	- An initial result is used to conduct a deep audit of the result
### Approaches to VA
- **Product-based solutions**:
	- Deployed within a small private network
	- Usually dedicated for such networks
- **Service-based solutions**:
	- 3rd party solutions that offer security and auditing services to a network. Can be external/internal.
	- Being internal makes it a risk to security

## VA Lifecycle
- **Creating a Baseline**
	- Pre-Assessment. Creates inventory of all resources and assets which helps to manage & prioritize the assessment
	- Maps infrastructure, learn security controls, policies and standards followed by the org
	- Helps to plan the process effectively, schedule tasks, manage them with respect to priority
- **VA**
	- Includes examination and inspection of security faults, and other vulns either by individual probing or assessment tools
	- Once scanning is complete, findings are ranked in terms of priorities
	- Result: Report with all detected vulns, their scope and priorities
- **Risk Assessment**
	- Scoping the identified Vulns and their impact on the corporate/org network
- **Remediation**
	- Remedial actions for these detected vulns. High priority/High impact ones are addressed first
- **Verification**
	- Ensures that all vulns are eliminated
- **Monitor**
	- Monitor Network traffic + System behavior for any further intrusions
## Best practices and Vuln Scoring
- **Best practices**
	- Auditor must fully understand the assessment tool before using it
	- Ensure that the tool used will not cause any damage/changes to the existing infrastructure
	- Ensure to focus on the scan on only the suspect parts of the infrastructure
	- Run scan frequently
- **Vuln Scoring**
	- Common Vulnerability Scoring Systems (CVSS)
		- Gives a number from 0 to 10.0
			- 0 -> None
			- 0.1-3.9 -> Low
			- 4.0-6.9 -> Medium
			- 7.0-8.9 -> High
			- 9.0-10.0 -> Critical
	- Common Vulnerability and Exposure (CVE)
		- Maintains a list (NVD) + description of known vulns under a CVE identifier
			- Provides fix info severity scores and impact ratings
		- Launched by NIST
		- CVE data is fed into the NVD

## Vuln scanning tools
- Performs deep inspection of scripts, open ports, banners, running services, config errors
	- Nessus
	- OpenVAS
	- Nexpose
	- Retina
	- GFI LanGuard
	- Qualys Freescan
# Lecture 10, 11, 12 - System Hacking
## Goals
- Part of VA
	- Includes
		- Cracking Passwords
		- Executing Apps
		- Escalating Privs
		- Hiding Files
		- Covering tracks
- Approach to System Hacking
	- Bypass ACL via Password cracking/Social Engineering to gain system OS access
	- Exploit OS vulns to escalate privs
	- Execute malware as root/system to create a backdoor
	- Steal info
	- Cover up using rootkits to persist backdoor or stegno to hide logs
	- Clear all logs or hide them
## Password Cracking
### Non-Electronic Attacks
- No technical knowledge required
- Done via
	- Shoulder surfing i.e. standing behind the target to observe input
	- Social engineering
	- Dumpster diving
### Active Online Attacks
- Active i.e. direct. Online i.e host is up
- Attacks
	- Dictionary -> Use of wordlists to bruteforce
	- BruteForce -> Use of every possible charecter
	- Hash Injection -> Extract LOGON HASH from SAM file via SE or some sort of technique to compromise the machine. Use hashes of other users/admins to login
### Passive Online Attacks
- Packet capture, inspect for data from telnet, ftp, smtp, rlogin proto to get passwords
- MITM, Use of replay attacks, setup attacker as CA and distribute SSL certs in the network. All traffic goes through attacker, can easily decode and inspect packets. Use SSLStrip, BurpSuite and BEEF. Can count as Active as well
### Default Password
- DeviceIDs can be used to get service manuals or quick start guides that contain default passwords. People do not often change these
### Offline Attack
- Use of precomputed hashes and a rainbow table
	- Rainbow table: Hash dictionary of all possible password combinations
	- Precomputed Hashes: Hash the pw and now compare with rainbow table
	- Takes a while to compute the rainbow table
- Distributed Network Attack
	- Similar to a botnet use multiple computers to decrypt the hash
	- DNA manager: Manages clients centrally. Allocates small part of the computation to each client
	- DNA client: obvs what it dose
- Password Guessing
	- Trial and error
- USB Drive
	- Load usb with passview and an autorun script
	- Itll attempt to decrypt any stored passwords on the connected host
### Password cracking flowchart
- Start
- Check pw policy
- SE attack
	- Shoulder surfing
	- Dumpster diving
- Default password
- Dictionary Attack
- Bruteforce
- Guess pw
- Keylogger
- Spyware
- Hash injection
- Wire sniffing
- MITM Attack
- Replay attack
- Rainbow table
- DNA

## Microsoft Authentication
#### General Knowledge
- Windows stores pw in SAM file
- Windows DC stores in NTDS.dit file
- Linux stores in Shadow
### SAM
- DB that stores creds
	- Location: C:/windows/system32/config/sam
- Passwords are hashed
	- NTLM hashing format
	- XP Onwards the Lan Manager (LM) hash stopped being stored and if it exceed 14 charecters blank or dummy values were added
- Locked to be accessed from other services when OS is running
### NTLM
- Login authn by a domain controller
- DC sends a nonce (16byte random number) challenge that has to be encrypted with the password hash
- DC permits or denys based on its own calculated response
- Two versions
	- NTLM1
	- NTLM2: Combined with SSP (Security Support provider)
### Kerberos
- Clients receive ticket from Kerberos Key Distribution Center (KDC)
	- Depends on Authn Server + Ticket-Granting Server
- Steps
	- Once per login
		- Client sends TGT request
		- Authn Server sends TGT + Session key
	- Once per type of service
		- Client sends Service Ticket request
		- Ticket-Granting Server sends TGT + Session key
	- Once per service session
		- Client sends Service Request
		- Service Server sends Service Response 

## Password salting
- Hashes are seeded with data of the file. Salting is where a random string like the current time is added to increase uniqueness of the hash
- Harder to reverse therefore harder to brute force using a dictionary or a rainbow table

## Priv escalation
- **Introduction:**
    - After gaining access to the target system, privilege escalation is necessary for complete high-level access with no or limited restrictions.
- **Types of Privilege Escalation:**
    1. **Horizontal Privileges Escalation:**
        - Involves an attacker attempting to take command over the privileges of another user with the same set of privileges.
        - Occurs when accessing the same set of resources allowed for a particular user.
    2. **Vertical Privileges Escalation:**
        - Involves an attacker attempting to escalate privileges to a higher level, typically to the administrator account.
        - Higher privileges allow access to sensitive information, installation, modification, and deletion of files and programs.

### Privilege Escalation using DLL Hijacking:
- **Overview:**
    - Applications in Windows OS search for Dynamic Link Libraries (DLL) in directories instead of using fully qualified paths.
- **Exploitation:**
    - Malicious DLLs are renamed with the same name as legitimate DLLs and replaced in the directory.
    - When an application runs, it loads the malicious DLL from the application directory instead of the real DLL.
- **Tools:**
    - DLL hijacking tools like Metasploit can generate DLLs that return with a session with privileges.
    - These DLLs are renamed and placed in the directory, leading to the opening of a session with system privileges.
- **Registry Key:**
    - Known DLLs are specified in the registry key:
	- `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\`


### Executing Applications:

- **Introduction:**
    - After gaining unauthorized access and escalating privileges, attackers execute malicious applications on the target system.
    - The intention is to gain unauthorized access to system resources, crack passwords, set up backdoors, etc.
- **Tools:**
    - RemoteExec: Allows remote installation, execution of code and scripts, updating files, and remote configuration management.
    - PDQ Deploy: Installs and sends updates silently to remote systems, facilitating the deployment of applications and software.

### Keyloggers:

- **Overview:**
    - Keyloggers monitor or record user actions, such as keystrokes, without the user's knowledge.
    - They can be software-based or hardware-based.
- **Software Keyloggers:**
    - Remotely installed or executed by the user, includes application, kernel, and form-grabbing keyloggers.
- **Hardware Keyloggers:**
    - Physically installed on hardware, including PC/Bios embedded, keyboard, and external keyloggers.
- **Anti-Keyloggers:**
    - Application software that protects against keylogging by providing SSL protection, clipboard logging protection, etc.

### Spyware:

- **Overview:**
    - Spyware gathers user interaction information without informing the user, typically used for tracking internet interactions.
- **Types of Spyware:**
    - Includes adware, system monitors, tracking cookies, and Trojans.
- **Features:**
    - Tracks users, records conversations, blocks applications/services, delivers logs remotely, etc.

### Rootkits:

- **Overview:**
    - Rootkits provide privileged access to a remote user over the target system, often installed after an attack for maintaining access.
- **Types of Rootkits:**
    - Application level, kernel-level, hardware/firmware level, and hypervisor level.
- **Countermeasures:**
    - Detection methods include integrity-based, difference-based, and behavioral detection, along with tools like Rootkitrevealer and anti-rootkit software.

### NTFS Data Stream:

- **Overview:**
    - NTFS (New Technology File System) is a proprietary file system by Microsoft.
- **Alternate Data Stream (ADS):**
    - A file attribute in NTFS used for hiding data within an existing file without noticeable changes.
    - Can be exploited for hiding malicious data.

### Countermeasures:
- Moving files to FAT partition or using third-party tools like ADS Spy, LADS, and Stream Armor for detection and removal.


# Lecture 14, 15 - Malware Threats
## Malware
- Designed for gaining access, stealing info and harming the target system
- **Modes of propagation**
	- Freeware
		- Cracked software contains patched malicious DLLs
	- File sharing services
		- Freeware usually downloaded via P2P clients, can sneak a malware in the download
	- Removeable media
		- Many malware are configured to store a copy into a newly mounted Filesystem to enhance propagation chances
	- Email Comms
		- Sent via attachments, if bad AV then download will proceed as planned
	- Inadequate Firewall and AV protection
		- Some people disable AV and firewall, common sense as to what'll happen here
## Trojans
- Insert story of Troy and the wooden horse
- Trojans mislead the user to thinking the program has functionality that might be productive to them, at the backend they can
	- Create backdoors/Gain Unauthorized access
	- Steal Info, Download other software, Disable firewalls
	- Infect connected devices
	- Use victim device as a botnet/spamming net

### Trojan Lifecycle
- Creation using Trojan construction Kit
	- Pandora's Box, Senna SpyGen, DarkHorse, etc
- Create a Dropper
	- Payload delivery without detection
	- ROTBROWA, MEREDROP, DESTOVER-C, etc
- Create a Wrapper
	- Packing trojan inside a non-malicious file
- Crypter
	- Encrypt, obfuscate and manipulate the malware to hide it
	- Avoids AV Sig Detection
	- CRYOGENIC, HEAVEN, SWAYZ
- Propagation
	- Can be via the email, net, removable devices
- Execute Dropper
	- Run unpacker during non-malicious file execution and execute dropper to install required files for the trojan

### Trojan Deployment (Social Engineering)
- Upload dropper to a download server
- Dropper link attached to a email and sent to target user
- User clicks on link and file is downloaded to PC instantly
- Download file is executed and unpacks after which the exe starts a dropper to download the trojan
- Trojan connects to attacker with privileged access/Steal info and secretly send it back to the attacker
	- C2 approach

### Trojan Types & Countermeasures
- **Types**
	- Command Shell -> CLI Reverse Shell, Use of NETCAT
	- Defacement -> View, edit and extract info from any windows program, Attacker leaves their mark on every file. Website defacement is a good example.
	- HTTP/S -> HTTP/S Reverse Shell created after bypassing firewall
	- Botnet -> C2 server control, Used for DDOS, Spamming, Mining, etc
	- Proxy Server -> Turn host system into a proxy server, Used to launch DDOS and/or mask and spoof attacker's IP to a real device
	- RAT (Remote Access Trojans) -> Backdoor to maintain admin access and control over victim, provide GUI Access to target
	- Others
		- FTP, VNC, Mobile, ICMP, Covert, Notification, Data Hiding
- **CounterMeasures (Social Engineering based)**
	- Avoid suspected links/attachments/downloads
	- Block unused ports
	- Configure host-based firewall/IDS
	- Scan removeable media

## Viruses
- Self replicating program, Execute on download, Can sleep and remain undetected by AV
- **Features**
	- Infect other files
	- Alter files, Transformation, Corruption, Encryption, Self-replication
- **Types**
	- Ransomware -> Deploys via Trojans, Encrypts User + System Files, Demands ransom from user to be granted the decryption key
	- System/Boot sector -> Replaces MBR with its own copy, virus gets executed before the OS is loaded. Can either boot into OS as system or outright prevent the PC from booting
	- File/Multipartite -> FILE: Infect BAT/EXE files | MULTIPARTITE: Infects BootSector and Files simultaneously
	- Macro -> Specializes in Microsoft Office Suite. Macro is a feature provided in the suite. Abuses privileges provided to the suite
	- Cluster -> Specialized to attack Location/Directory Table. Modifies the entries so the virus is executed whenever the user attempts to open a file
	- Stealth/Tunneling -> Avoids AV detection. Memory-Resident/Serves a safe copy of the file it has infected for AV to scan.
	- Logic Bombs -> Stays in Sleep state until a trigger event occurs. Can be timebased. Effect same as regular virus afterwards.
	- Encryption -> Not ransomware, Virus encrypts and decrypts itself to avoid detection while replicating
### Virus/Anti-Virus Development lifecycle
- **Design** -> Use construction kits or DIY
- **Replication** -> Virus replicates for a set period of time, usually short and done before spreading to other files
- **Launch** -> File clicked on, interacted with in some way to trigger virus execution
- **Detection** -> Behavioral analysis to observe signatures and IOCs
- **Incorporation** -> Update sig database/create method to detect and then include the new virus, update AV to load new database/methods
- **Elimination** -> AV takes appropriate action

#### Virus Development Example
- Create a folder with BAT and TXT file
- Add code to TXT file
- Save as .BAT
- Convert to executable using BAT2COM or BAT2EXE
- Now it will execute on click

### Virus attack modes
- **Infection** -> Plant Virus, Enforce methods of propagation such as Email attachments, File infection, transfer to external media
- **Attack** -> Triggered when the file is interacted with, however some might wait for further conditions to be fulfilled

## Worms
- Need a trigger to be executed
- Self-replicate over the network instead of local PC
	- Uses File transport protocols

## Virus Detection & Analysis
- **Scanning** -> Scan suspected file for signatures
- **Detection** -> Check entire disk for integrity via checksum
- **Interception** -> Behavioral analysis within the system, virus tends to access and create files for self-replication so such behavior should be flagged. NOTE:: ONLY A WARNING IS GIVEN. NO ACTION TAKEN.
- **Code Emulation & Heuristic Analysis aka SheepDipping** -> Kind of same as interception but run it in a dynamic analysis environment to gather and store IOCs for sig analysis in file header or behaviors

### Goals of analysis
- Understand threat severity
- Classify malware
- Scope the attack
- Build defenses
- Find root cause
- Build IR Actions
- Add sig to AV or develop custom anti-malware