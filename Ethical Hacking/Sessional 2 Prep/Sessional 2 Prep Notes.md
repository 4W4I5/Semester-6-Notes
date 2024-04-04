| Lecture Title                      | Status    |
| ---------------------------------- | --------- |
| Lecture 7 - Enumeration            | :warning: |
| Lecture 9 - Vulnerability Analysis | :warning: |
| Lecture 10 - System Hacking Pt1    | :warning: |
| Lecture 11 - System Hacking Pt2    | :warning: |
| Lecture 12 - System Hacking Pt3    | :warning: |
| Lecture 14 - Malware Threats Pt1   | :warning: |
| Lecture 15 - Malware Threats Pt2   | :warning: |
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
| Protocol | Countermeasure |
| -------- | -------------- |
| SNMP     | Point 1        |
|          | Point 2        |
|          | Point 3        |
|          | Point 4        |
|          | Point 5        |
|          | Point 6        |
| DNS      | Point 1        |
|          | Point 2        |
|          | Point 3        |
|          | Point 4        |
| SMTP     | Point 1        |
|          | Point 2        |
|          | Point 3        |
|          | Point 4        |
| LDAP     | Point 1        |
|          | Point 2        |
|          | Point 3        |
| SMB      | Point 1        |
|          | Point 2        |
|          | Point 3        |
|          | Point 4        |
| NFS      | Point 1        |
|          | Point 2        |
|          | Point 3        |
|          | Point 4        |
|          | Point 5        |
| FTP      | Point 1        |
|          | Point 2        |
|          | Point 3        |
|          | Point 4        |
|          | Point 5        |

### !What can we learn from enumeration
### !Technologies we can enumerate
# Lecture 9 - Vulnerability Analysis
# Lecture 10 - System Hacking Pt1
# Lecture 11 - System Hacking Pt2
# Lecture 12 - System Hacking Pt3
# Lecture 14 - Malware Threats Pt1
# Lecture 15 - Malware Threats Pt2