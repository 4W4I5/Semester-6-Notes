| Chapter                                                           | Status             |
| ----------------------------------------------------------------- | ------------------ |
| Lecture 0 - Introduction to Ethical Hacking                       | :warning:          |
| Lecture 1 - Reconnaissance-1                                      |                    |
| Lecture 2 - Reconnaissance-2 (Social Sources)                     |                    |
| Lecture 3 - Reconnaissance-3 (Countermeasures)                    |                    |
| Lecture 4 - Network Scanning-1                                    |                    |
| Lecture 5 - Network Scanning-2 (Types of scanning)                |                    |
| Lecture 6 - Network Scanning-3 (Fingerprinting & Banner Grabbing) |                    |
| Lecture 7 - Enumeration                                           |                    |
| Lecture 8 - Scapy                                                 | :white_check_mark: |


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
			- Min Packet size
				- 21 bytes (20 for header and 1 for TCP data)
			- Max Packet size
				- 65535 Bytes
			- Header (20 Bytes of overhead for TCP header and then another 20 for IP overhead)
				- Row 1
					- 4 bits for version
					- 4 for header len
					- 8 for service
					- 16 for packet length
				- Row 2
					- 16 for identifier
					- 3 for flags
					- 13 for frag offset
				- Row 3
					- 8 for TTL
					- 8 for upper layer protocol
					- 16 for checksum
				- Row 4
					- 32 for src IP
				- Row 5
					- 32 for dest IP
				- Row 6
					- Variable length of bits for Options + Padding
				- Row 7
					- TCP/UDP payload
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
		- **TCP**
			- Row 1
			    - 16 bits for src port
			    - 16 bits for dest port
			- Row 2
			    - 32 bits for Sequence number
			- Row 3
				- 32 bits for Acknowledgement Number
			- Row 4
		    - len (8 BITS)
		    - UNUSED SECTION (8 BITS)
		    - recieve windows (32 BITS)
		        - num of bytes receiver is willing to accept
		    - chksum (32 BITS)
		    - flags = SYN, ACK, RESET, PUSH, URGENT, FIN (16 BITS)
		        - PUSH: App informs that data should be pushed up the stack in the receiving app
		        - URGENT: Transmit everything right now, used for remote interrupts
		        - ACK: acknowledge
		        - RESET: Abort connection
		        - FIN: Close connection
		        - SYN: Sync
		    - app data, can be variable length
		    - urgent data pointer (32 BITS)
		    - TOTAL SIZE = 20 BYTES