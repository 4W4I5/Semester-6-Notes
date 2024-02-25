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
			- Min Packet size
				- 20 bytes
			- Max Packet size
				- 60 Bytes
			- Row 1
			    - 16 bits for src port
			    - 16 bits for dest port
			- Row 2
			    - 32 bits for Sequence number
			- Row 3
				- 32 bits for Acknowledgement Number
			- Row 4
				- 4 bits for Header length
				- 6 bits are reserved
				- 6 bits for flags
					- PUSH: App informs that data should be pushed up the stack in the receiving app
			        - URGENT: Transmit everything right now, used for remote interrupts
			        - ACK: acknowledge
			        - RESET: Abort connection
			        - FIN: Close connection
			        - SYN: Sync
				- 16 bits for Window size i.e. number of bytes the receiver is willing to accept
			- Row 5
				- 16 bits for checksum
				- 16 bits for Urgent
			- Row 6
				- Variable length of bits for Options + Padding
			- Row 7
				- Payload
		- **UDP**
			- Min header size
				- 8 bytes
			- Max header size
				- theoretically 655355
			- Row 1
				- 16 bits for src port
				- 16 bits for dest port
			- Row 2
				- 16 bits for Header Length
				- 16 bits for checksum
			- Row 3
				- Payload
		- **ICMP**
			- Min Packet size
				- 8 bytes
			- Max Packet size
			    - 576 Bytes
			- Row 1
			    - 8 bits for Type
			    - 8 bits for Code
				- 16 bits for Checksum
			- Row 2
				- Variable length of bits for Data (depends on Type and Code)
		- **MAC Frame**
			- Min Packet size
				- 64 bytes
			- Max Packet size
		        - 1518 bytes (excluding preamble and frame check sequence)
		    - Row 1
		        - 48 bits for Destination MAC Address
		        - 48 bits for Source MAC Address
		    - Row 2
			    - 16 bits for EtherType or Length (depending on Ethernet version)
			    - For IPv4= 0x0800
			    - For IPv6= 0x86DD
		    - Row 3
			    - Variable length of bits for Payload (46-1500 bytes)
			- Row 4
				- 32 bits for Frame Check Sequence (FCS) / CRC (Cyclic Redundancy Check)
				- (Optional) FCS/Error Checking
			- The EtherType field is used to indicate the protocol type of the payload data. For example: