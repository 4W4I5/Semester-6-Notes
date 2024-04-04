| Lecture Title                      | Status             |
| ---------------------------------- | ------------------ |
| Lecture 7 - Enumeration            | :white_check_mark: |
| Lecture 9 - Vulnerability Analysis | :warning:          |
| Lecture 10 - System Hacking Pt1    | :warning:          |
| Lecture 11 - System Hacking Pt2    | :warning:          |
| Lecture 12 - System Hacking Pt3    | :warning:          |
| Lecture 14 - Malware Threats Pt1   | :warning:          |
| Lecture 15 - Malware Threats Pt2   | :warning:          |
<!--
:x:
:warning:
:white_check_mark:
-->


# Lecture 7 - Enumeration
### What is Enumeration
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
### Techniques of enumeration
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

### Services and ports to Enumerate
- TCP/UDP 53 -> DNS Zone Transfer
- TCP/UDP 135 -> RPC Endpoint Mapper
- TCP/UDP 389 -> LDAP
- TCP/UDP 445 -> SMB over TCP
- TCP/UDP 162 -> SNMP Trap
- UDP 137 -> NetBIOS name service
- TCP 25 -> SMTP
	- VRFY: Confirm name of valid user
	- EXPN: Reveal actual address of user aliases and mailing list
- UDP 500 -> ISAKMP
- TCP 22 -> SSH
- UDP 161 -> SNMP

### Microsoft tools to enumerate with (PsTools Suite)
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

### Enumeration Countermeasures
| Protocol | Countermeasure                                                                                                                       |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| SNMP     | Remove the SNMP agent or turn off the SNMP service                                                                                   |
|          | If shutting off SNMP is not an option, then change the default community string names                                                |
|          | Upgrade to SNMP3, which encrypts passwords and messages                                                                              |
|          | Implement the Group Policy security option called "Additional restrictions for anonymous connections"                                |
|          | Ensure that the access to null session pipes, null session shares, and IPSec filtering is restricted                                 |
|          | Do not misconfigure SNMP service with read-write authorization                                                                       |
| DNS      | Disable Zone-Transfers to untrusted hosts                                                                                            |
|          | Ensure that the private hosts and their IP addresses are not published in DNS zone files of public DNS servers                       |
|          | Use premium DNS registration services that hide sensitive information, such as host information (HINFO) from the public              |
|          | Use standard network admin contacts for DNS registrations to avoid social engineering attacks                                        |
| SMTP     | Ignore email messages to unknown recipients                                                                                          |
|          | Exclude sensitive mail server and local host information in mail responses                                                           |
|          | Disable open relay feature                                                                                                           |
|          | Limit the number of accepted connections from a source to prevent brute-force attacks                                                |
| LDAP     | By default, LDAP traffic is transmitted unsecured; use SSL or STARTTLS technology to encrypt the traffic                             |
|          | Select a username different from your email address and enable account lockout                                                       |
|          | Use NTLM or any basic authentication mechanism to limit access to legitimate users only                                              |
| SMB      | Disable SMB protocol on Web, DNS and any Internet-Facing Servers                                                                     |
|          | Disable ports TCP 139 and TCP 445 used by the SMB protocol                                                                           |
|          | Restrict anonymous access through RestrictNullSessAccess parameter from the Windows Registry                                         |
| NFS      | Implement proper permissions (read/write must be restricted to specific users) on exported file systems                              |
|          | Implement firewall rules to block NFS port 2049                                                                                      |
|          | Ensure proper configuration of files, such as /etc/smb.conf, /etc/exports and ete/hosts.allow, to protect the data stored in servers |
|          | Log requests to access system files on the NFS server                                                                                |
|          | Keep the root_squash option in /etc/exports file turned ON, so that no requests made as root on the client are trusted               |
| FTP      | Implement secure FTP (SFTP, which uses SSH) or FTP secure (FTPS, which uses SSL) to encrypt the FTP traffic over the network         |
|          | Implement strong passwords or a certification-based authentication policy                                                            |
|          | Ensure that unrestricted uploading of files on the FTP server is not allowed                                                         |
|          | Disable anonymous FTP accounts; if not feasible, regularly monitor anonymous FTP accounts                                            |
|          | Restrict access by IP or domain name to the FTP server                                                                               |

### !What can we learn from enumeration
### !Technologies we can enumerate
# Lecture 9 - Vulnerability Analysis

# Lecture 10 - System Hacking Pt1
# Lecture 11 - System Hacking Pt2
# Lecture 12 - System Hacking Pt3
# Lecture 14 - Malware Threats Pt1
# Lecture 15 - Malware Threats Pt2