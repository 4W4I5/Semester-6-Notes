| Topic Title                                     | Status             |
| ----------------------------------------------- | ------------------ |
| Lecture 16: Sniffing                            | :white_check_mark: |
| Lecture 17: Social Engineering                  | :warning:          |
| Lecture 21: DoS & DDoS                          | :warning:          |
| Lecture 22: IDS, IPS, Firewall Evasion          | :warning:          |
| Assignment 3: Host Discovery                    | :warning:          |
| Assignment 4: Port Discovery                    | :warning:          |
| Assignment 5: Post Exploitation (RIA Hijacking) | :warning:          |

# Lecture 16: Sniffing
- **Concept of Sniffing**
    - Sniffing involves scanning and monitoring data packets passing through a network using sniffers with interfaces that have the following capabilities.
	    - **Promiscuous Mode**: Enables capturing all traffic on the network interface, not just traffic intended for the sniffer.
	    - **Packet Inspection**: Once captured, packets can be inspected for sensitive information.
- **Types of Sniffing**
    - **Passive Sniffing**:
        - Occurs on hubs where traffic is broadcasted to all ports.
        - No additional packets are sent; the attacker just listens.
    - **Active Sniffing**:
        - Used on switches where traffic is sent to specific ports via unicast packets.
        - Involves sending packets to manipulate network devices via the following
	        - MAC flooding
	        - DHCP attacks
	        - DNS poisoning
	        - ARP poisoning
- **Data Captured by Sniffing**
    - Types of traffic captured:
	    - SYSLOG
	    - DNS
	    - Web
	    - Email, etc.
    - Sensitive information like usernames and passwords from protocols
	    - HTTP
	    - POP
	    - IMAP
	    - FTP
	    - Telnet, etc.
- **Working of Sniffers**
	- For Networks connected via a Hub it is easy to listen in on traffic as all packets are multicast by the hub
	- However for Switches maintain a mac table linking each mac address to a specific port on the switch so therefore techniques like port mirroring or SPAN are used (NOTE:: Both are the same thing)
	    - **Port Mirroring**: Similar to port forwarding, the difference here is that packets are simply duplicated for debugging purposes i.e. the original flow of traffic is not affected
- **Hardware Protocol Analyzers**
    - Used to capture and analyze network traffic without interference.
    - Advantages include mobility, flexibility, and high throughput.
    - Examples: Products from Keysight Technologies, RADCOM, Fluke.
	- **SPAN Port**
	    - Used for network performance monitoring.
	    - Allows capturing traffic from one port on a switch to another port using tools like Wireshark.
	    - In essence it follows the logic of a wiretap where you are tapped into the flow of communication
- **Wiretapping**
    - **Active Wiretapping**: Monitors and alters communications. Example can be port forwarding
    - **Passive Wiretapping**: Monitors and records without alteration. Example is SPAN
    - **Lawful Interception**: Legal wiretapping by law enforcement agencies.
- **PRISM**
    - **Planning Tool for Resource Integration (PRISM)**: Monitors internet traffic through US servers.
    - A program by NSA for monitoring communications passing through or stored on US servers that collects data to identify and monitor suspicious activities.
- **MAC Attacks**
    - **MAC Address and CAM Table**:
        - **MAC address**: 48-bit unique identifier for network devices. Comprised of OUI-NIC
	        - **Offsets**
		        - 24-bit Object Unique Identifier (OUI)
		        - 24-bit Network-Interface Controller (NIC)
		    - **Notable things**
			    - First Octet -> 7th Bit is for Globally Unique/Locally administered. 8th Bit is for Unicast/Multicast
        - **CAM table**: Used in switches to map MAC addresses to interface ports for packet forwarding.
		    - **Content Addressable Memory (CAM)** -> Works by recording MAC addresses and their associated ports.
			    - To prevent a reuse however, every MAC entry is set to age after a set period of time. Default is 300 seconds
    - **MAC Flooding**:
        - Overloads CAM table with fake MAC addresses to fake IP Addresses causing the switch to broadcast packets as there is no direct route to the target device anymore.
        - Tool -> MACOF
    - **Switch Port Stealing (MITM Impersonation)**:
        - Involves sending bogus ARP packets to update CAM table, redirecting traffic to the attacker.
        - Attacker sends a packet
	        - Source 
- **Defending Against MAC Attacks**
    - **Port Security**: Limits the number of MAC addresses per port and sets violation actions.
    - **Dynamic Port Security**: Configures allowed number of MAC addresses dynamically.
- **DHCP Attacks**
    - **DHCP Starvation**:
        - Attacker sends spoofed requests to exhaust IP addresses in the DHCP pool.
    - **Rogue DHCP Server**:
        - Attacker sets up a fake DHCP server to direct traffic through it after starving the legitimate server.
- **Defending Against DHCP Attacks**
    - **DHCP Snooping**: Filters untrusted DHCP messages and maintains a binding database of legitimate DHCP transactions.
    - **Port Security**: Limits the number of MAC addresses to mitigate attacks.
- **ARP Poisoning** -> Uses MAC flooding to turn a switch into a hub, enabling packet sniffing.
    - **ARP Spoofing**:
        - Sends forged ARP packets to associate attacker's MAC address with the IP of a legitimate user to intercept traffic intended for them.
    - **Consequences**: Enables session hijacking, data interception, man-in-the-middle attacks, and more.
- **Defending Against ARP Poisoning**
    - **Dynamic ARP Inspection (DAI)**: Validates ARP packets against trusted IP-to-MAC bindings.
- **Spoofing Attacks**
    - **MAC Spoofing**: Manipulates MAC addresses to impersonate legitimate users.
    - **Tools**: Technetium MAC Address Changer, SMAC.
- **Defending Against Spoofing Attacks**
    - **DHCP Snooping and DAI**: Protect against MAC spoofing.
    - **Source Guard**: Restricts traffic to assigned IP addresses on client-facing switch ports.
---

# Lecture 17: Social Engineering

---

# Lecture 21: DoS & DDoS

---

# Lecture 22: IDS, IPS, Firewall Evasion


---

# Assignment 3: Host Discovery

---

# Assignment 4: Port Discovery

---

# Assignment 5: Post Exploitation (RIA Hijacking)

---