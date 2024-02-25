| Chapter                                                           | Status    |
| ----------------------------------------------------------------- | --------- |
| Lecture 0 - Introduction to Ethical Hacking                       | :warning: |
| Lecture 1 - Reconnaissance-1                                      |           |
| Lecture 2 - Reconnaissance-2 (Social Sources)                     |           |
| Lecture 3 - Reconnaissance-3 (Countermeasures)                    |           |
| Lecture 4 - Network Scanning-1                                    |           |
| Lecture 5 - Network Scanning-2 (Types of scanning)                |           |
| Lecture 6 - Network Scanning-3 (Fingerprinting & Banner Grabbing) |           |
| Lecture 7 - Enumeration                                           |           |
| Lecture 8 - Scapy                                                 |           |


<!--
:white_check_mark:
:x:
-->

# Lecture 0 - Introduction to EHCP
# Lecture 1 - Reconnaissance-1
# Lecture 2 - Reconnaissance-2 (Social Sources)
# Lecture 3 - Reconnaissance-3 (Countermeasures)
# Lecture 4 - Network Scanning-1
# Lecture 5 - Network Scanning-2 (Types of scanning)
# Lecture 6 - Network Scanning-3 (Fingerprinting & Banner Grabbing)
# Lecture 7 - Enumeration
# Lecture 8 - Scapy
- Scapy
	- **Definition**
		- Interactive packet manipulation python program
	- **Capabilities**
		- Forge/Decode packets from a wide number of protocols
		- Send crafted packets, Layering, Capture, Match requests and replies
		- Can easily handle scanning, tracerouting, probing, unit tests and attacks
	- **Protocols**
		- Defined via RFC(Request for Comments)
		- Includes TCP/UDP, IP, FTP, HTTP, SMTP, etc
	- **IP**
		- Header
			- 4 bits for version
			- 4 for header len
			- 8 for service
			- 16 for packet length
			- 16 for identifier
			- 3 for flags and 13 for frag offset
			- 8 for TTL
			- 8 for upper layer protocol
			- 16 for checksum
			- 32 for src and dest IP
			- payload
			- 20 Bytes of overhead for TCP header and then another 20 for IP overhead
		- Max Transmission Unit
			- Length of largest frame sent over a link
			- if larger than MTU
				- Packet is fragmented
		- IPv4 Fragmentation
			- Components
				- ID, random for each og full size packet. kept the same for fragmented packets from original
				- Flags, first bit is reserved. other two are Dont Frag and More Frag flags
					- DF = 1, packet will be dropped if over MTU
					- MF = 1, more fragments, 0 if not
						- Last frag MF is set to 0 others are 1
				- Frag Offset
					- work in octets (base 8)
		- IPv6 doesn't have fragmentation
			- Causes complexity at the router
			- can also be used to DOS
		- CIDR
			- fixed bits denoted by /x
			- 192.168.1.1/24 means there are 24 fixed bits
				- it also means this is a class C network
		- Address class
			- OLD WAY had either 0, 10, or 110 at the start of an IP address to determine its class respectively from A to C
			- also these classes have ranges
				- CLASS A = 1 - 126
				- CLASS B = 128 - 191
				- CLASS C = 192 - 223