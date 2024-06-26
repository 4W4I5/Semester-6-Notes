| Topic Title                                     | Status             |
| ----------------------------------------------- | ------------------ |
| Lecture 16: Sniffing                            | :white_check_mark: |
| Lecture 17: Social Engineering                  | :white_check_mark: |
| Lecture 21: DoS & DDoS                          | :white_check_mark: |
| Lecture 22: IDS, IPS, Firewall Evasion          | :white_check_mark: |
| Assignment 3 & 4: Host + Port Discovery         | :white_check_mark: |
| Assignment 5: Post Exploitation (RID Hijacking) | :white_check_mark: |

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
	    - LAN-Only
        - Involves sending bogus ARP packets to update CAM table, redirecting traffic to the attacker.
        - Attacker sends a packet
	        - Source ->Stolen Host MAC
	        - Destination -> Target MAC for another device
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
- **Social Engineering**
    - Definition: Art of convincing people to reveal confidential information.
    - Common Targets:
        - Help desk personnel
        - Support executives
        - System administrators
        - Receptionists
        - Technical support executives
        - Users & Clients
        - Vendors
        - Senior executives
- **Impact of Social Engineering**
    - Economic Losses: Direct financial damage.
    - Damage to Goodwill: Harm to reputation and trust.
    - Loss of Privacy: Compromised personal and organizational information.
    - Dangers of Terrorism: Potential misuse of information for terrorist activities.
    - Lawsuits and Arbitration: Legal consequences and disputes.
    - Temporary or Permanent Closure: Operational shutdowns.
- **Vulnerable Behaviors**
    - Authority: Trusting figures of authority without verification.
    - Intimidation: Succumbing to threats or coercion.
    - Consensus/Social Proof: Following the crowd without critical thinking.
    - Scarcity: Acting out of fear of missing out.
    - Urgency: Responding quickly due to a sense of urgency.
    - Familiarity/Liking: Trusting individuals based on perceived friendliness.
    - Trust: Misplaced trust in unverified entities.
    - Greed: Falling for offers that seem too good to be true.
- **Factors Making Companies Vulnerable**
    - Insufficient Security Training: Lack of awareness and skills.
    - Unregulated Access to Information: No strict control over sensitive data.
    - Multiple Organizational Units: Complexity and lack of cohesive security measures.
    - Lack of Security Policies: Absence of formal guidelines and procedures.
- **Effectiveness of Social Engineering**
    - Human Susceptibility: Humans are the weakest link in security.
    - Detection Challenges: Difficult to identify and prevent.
    - Low Cost and Ease of Implementation: Simple and inexpensive for attackers.
- **Phases of Social Engineering Attack**
    - Research the Target Company: Gathering information.
    - Select a Target: Identifying a specific victim.
    - Develop a Relationship: Establishing trust.
    - Exploit the Relationship: Using trust to extract information.
- **Types of Social Engineering Attacks**
    - Human-Based:
        - Impersonation/Reverse Social Engineering: Pretending to be someone else to gain information.
	        - Honey Traps
		    - Baiting: Offering something enticing to get information or infect a system.
		    - Quid Pro Quo: Offering a service in exchange for information.
	        - Elicitation
        - Eavesdropping: Listening to private conversations to gather information.
        - Shoulder Surfing: Observing someone entering confidential information.
        - Dumpster Diving: Searching through trash for sensitive information.
        - Piggybacking/Tailgating: Gaining unauthorized access by following someone into a secure area.
    - Computer-Based:
        - Phishing: Deceptive emails or websites to steal information.
        - Spam: Unsolicited emails often containing malicious links or attachments.
        - Pop-up Attacks: Malicious pop-ups that trick users into revealing information.
        - Spear Phishing: Targeted phishing attacks on specific individuals.
        - Vishing: Voice phishing using phone calls to extract information.
        - Whaling: Phishing attacks targeting senior executives.
    - Mobile-Based:
        - Malicious Apps: Applications designed to steal information.
        - Fake Security Applications: Apps pretending to be security tools but are malicious.
        - SMiShing: Phishing attacks via SMS.
- **Phishing Tools**
    - ShellPhish
    - BLACKEYE
    - Phishx
    - Modlishka
    - Trape
    - Evilginx
- **Insider Threats**
    - Definition: Attacks by trusted individuals with privileged access.
    - Common Perpetrators:
        - Privileged users
        - Disgruntled employees
        - Terminated employees
        - Accident-prone employees
        - Third parties
        - Undertrained staff
    - Motivations:
        - Financial gain
        - Data theft
        - Revenge
        - Competition
        - Public announcements
- **Types of Insider Threats**
    - Malicious Insider: Intentional harm.
    - Negligent Insider: Unintentional harm due to carelessness.
    - Professional Insider: Selling information to competitors.
    - Compromised Insider: External manipulation of an insider.
- **Social Networking Threats**
    - Data Theft
    - Involuntary Data Leakage
    - Targeted Attacks
    - Network Vulnerability
    - Spam and Phishing
    - Content Modification
    - Malware Propagation
    - Business Reputation Damage
    - Infrastructure and Maintenance Costs
    - Loss of Productivity
- **Identity Theft**
    - Definition: Stealing personal information for fraudulent purposes.
    - Commonly Stolen Information:
        - Name
        - Address
        - SSN
        - Phone number
        - DOB
        - Bank account numbers
        - Credit card info
        - Usernames and passwords
    - Uses:
        - Fraudulent credit card accounts
        - Phone services
        - Utility services
        - Bank accounts
        - ATM withdrawals
        - Loans
        - Government benefits
        - Impersonation
        - Insurance claims
        - Selling information
        - Online orders
        - Email hijacking
        - Health services
        - Tax fraud
- **Countermeasures**
    - Awareness and Training: Educate employees.
    - Effective Policies: Develop and enforce security policies.
    - Background Checks: Thorough vetting of employees.
    - Two-Factor Authentication: Enhanced security measures.
    - Regular Software Updates: Ensure systems are up-to-date.
    - Monitoring and Auditing: Continuous oversight of activities.
    - Physical Security: Secure access to physical facilities.
    - Data Loss Prevention (DLP): Tools to monitor and protect data.
    - Identity and Access Management (IAM): Control user access.
- **Detecting Insider Threats**
    - Deterrence Controls:
        - Separation of duties
        - Assigning privileges
        - Recommended actions
    - Detection Controls:
        - IDS/IPS
        - Log management
        - SIEM tools
    - Insider Risk Controls:
        - Monitor permissions
        - Access controls
        - User actions
- **Identity Theft Prevention**
    - Document Security: Shred sensitive documents.
    - Personal Information Protection: Secure personal data.
    - Credit Monitoring: Regularly review credit reports.
    - Safe Communication: Verify requests for personal data.
    - Secure Online Practices: Avoid sharing sensitive information on public Wi-Fi, enable two-factor authentication, use host security tools.
- **Examples of Social Engineering Attacks**
    - Phishing: Deceptive emails or websites to steal information.
    - Pretexting: Creating a fabricated scenario to obtain information.
    - Tailgating: Following someone into a restricted area.
- **Additional Information (Not in PPT)**
    - Social Engineering in Cybersecurity Context:
        - Often the first step in larger cyber attacks.
        - Can lead to more significant breaches like malware deployment, ransomware attacks, and data exfiltration.
    - Psychological Manipulation Techniques:
        - Reciprocity: People tend to return favors.
        - Commitment: Once a person commits to something, they are more likely to follow through.
        - Consistency: Aligning new requests with previous actions or beliefs.
    - Recent Trends:
        - Increasing sophistication of attacks.
        - Use of AI and deepfakes to enhance credibility.
        - Targeted attacks on remote workers due to the rise of telecommuting.
---

# Lecture 21: DoS & DDoS
#### DoS/DDoS
- **Denial of Service (DoS) Attack**
    - Definition: An attack designed to make a machine or network resource unavailable to its intended users by temporarily or indefinitely disrupting services of a host connected to the Internet.
    - Goal: To deny legitimate users access to services or resources.
    - Methods: Overloading the system with non-legitimate requests, making it unable to respond to legitimate traffic.
- **Distributed Denial of Service (DDoS) Attack**
    - Definition: An attack where multiple compromised systems attack a single target, causing a Denial of Service (DoS) for users of the targeted system.
    - Mechanism: Uses a botnet to generate overwhelming traffic from numerous sources.

#### Types of DoS Attacks
- **Flooding Attacks**
    - Overwhelming a system with excessive traffic.
    - UDP flood, ICMP flood.
- **Service Flooding**
    - Overloading a service with more events than it can handle.
    - Overloading an IRC server with excessive connections.
- **Corrupt Packet Attacks**
    - Crashing a TCP/IP stack by sending corrupt packets.
- **Unexpected Interactions**
    - Crashing a service by interacting with it in unexpected ways.
    - Sending unexpected inputs to a service causing it to fail.
- **Infinite Loops**
    - Causing a system to hang by making it enter an infinite loop.
    - Sending a specific sequence of packets that trigger an infinite loop in the service.

#### Impact of DoS Attacks
- **Resource Consumption**
    - Bandwidth, disk space, CPU time.
- **Physical Damage**
    - Destruction or alteration of network components.
- **Data Damage**
    - Destruction of programs and files in a computer system.

#### Categories of DoS/DDoS Attack Vectors
- **Volumetric Attacks**
    - **Definition**: Exhaust bandwidth either within the target network or between the target and the rest of the Internet.
    - **Magnitude**: Measured in bits per second (bps).
    - **Techniques**:
        - **UDP Flood Attack**: Overwhelming a target with UDP packets.
        - **ICMP Flood Attack**: Overloading a target with ICMP packets.
        - **Ping of Death (PoD) Attack**: Sending oversized packets causing buffer overflow.
        - **Smurf Attack**: Using IP broadcast with ICMP requests to flood a target.
        - **Pulse Wave Attack**: Alternating high-volume attacks to bypass mitigation strategies.
        - **Zero-Day Attack**: Exploiting unknown vulnerabilities.
        - **Malformed IP Packet Flood Attack**: Sending malformed packets to exhaust resources.
        - **Spoofed IP Packet Flood Attack**: Sending packets with a forged sender address.
- **Protocol Attacks**
    - **Definition**: Consume resources other than bandwidth, such as connection state tables.
    - **Magnitude**: Measured in packets per second (pps) or connections per second (cps).
    - **Techniques**:
        - **SYN Flood Attack**: Exploiting TCP connection sequence by sending SYN requests and not responding to SYN-ACK.
        - **Fragmentation Attack**: Sending fragmented packets to exhaust resources.
        - **Spoofed Session Flood Attack**: Overloading with spoofed session requests.
        - **ACK Flood Attack**: Sending numerous ACK packets to exhaust resources.
        - **TCP State Exhaustion Attack**: Exploiting TCP state handling to exhaust resources.
        - **RST Attack**: Sending RST packets to tear down legitimate connections.
- **Application Layer Attacks**
    - **Definition**: Exploit vulnerabilities in the application layer protocol or application itself.
    - **Magnitude**: Measured in requests per second (rps).
    - **Techniques**:
        - **HTTP Flood Attack**: Overloading with HTTP requests.
        - **Slowloris Attack**: Keeping connections open to exhaust server resources.
        - **UDP Application Layer Flood Attack**: Overwhelming with UDP application-layer requests.
        - **HTTPS GET/POST Attack**: Overloading with HTTPS requests.
        - **Multi-Vector Attack**: Combining multiple attack vectors.
        - **Peer-to-Peer Attack**: Exploiting P2P networks to flood a target.
        - **Permanent DoS (PDoS) Attack**: Permanently disabling hardware or software.
        - **Distributed Reflection DoS (DRDoS) Attack**: Using amplification techniques to reflect attacks.

#### Botnets in DDoS Attacks
- **Botnets**: Networks of compromised systems used to perform various malicious activities including DDoS attacks, spamming, keylogging, and more.
- **Typical Botnet Setup**:
    - **Scanning for Vulnerable Machines**: Identifying and compromising vulnerable systems.
	    - Scanning Types
		    - Random
		    - Hit-List
		    - Topological
		    - Local Subnet
		    - Permutation
    - **Setup Handler:** C2 for zombies
    - **Propagation of Malicious Code**: Distributing malware to establish control over compromised systems.
	    - Types
		    - Central Source -> Setup a deployment server outside of attacker system
		    - Back-Chaining -> Use attacker system as deployment server
		    - Autonomous -> Send toolkit as soon as target is infected
    - **Recruit Zombies:** Self explanatory
    - **Start Attack:** Send commands to the C2 handler for disrupting services on a target

#### Case Studies
- **DDoS Attack on GitHub**
    - **Details**: Demonstrates the impact of DDoS attacks and response strategies.

#### DoS/DDoS Attack Techniques
- **UDP Flooding Attack**: Overwhelming a target with UDP packets.
- **ICMP Flooding Attack**: Overloading a target with ICMP packets.
- **Ping of Death**: Sending oversized packets causing buffer overflow.
- **Smurf Attack**: Using IP broadcast with ICMP requests to flood a target.
- **Pulse Wave Attack**: Alternating high-volume attacks to bypass mitigation strategies.
- **Zero-Day Attack**: Exploiting unknown vulnerabilities.
- **SYN Flood Attack**: Exploiting TCP connection sequence by sending SYN requests and not responding to SYN-ACK.

#### Countermeasures for SYN Flood Attacks
- **Decrease Time-Out Period**: Reducing the time connections remain in the half-open state.
- **SYN Cookies**: Using cryptographic techniques to handle SYN requests without allocating resources until the connection is completed.
- **SynAttackProtect**: Enabling built-in protection mechanisms in network devices and operating systems.

#### DDOS Detection and Countermeasures
- **Detection Techniques**:
	- Identify unusual traffic patterns.
	- Implement rate-limiting to control traffic flow.
	- Use anomaly detection systems to detect deviations from normal behavior.
	- Deploy network traffic analysis tools to monitor real-time traffic.
	- Utilize signature-based detection for known attack patterns.
	- Implement behavioral analysis to detect abnormal user and network behavior.
	- Conduct regular vulnerability assessments and penetration testing.
- **Countermeasure Strategies**:
	- **Absorb the attack:**
		- Requires preplanning + Additional Resources
	- **Degrading Services:**
		- Only keep critical functions running until attack has subsided
	- **Shutting down**
		- While mentioned in the slides, this is stupid as this is exactly what the attacker intends for
	- **Protect Secondary Victims**:
	    - Implement network segmentation to isolate critical systems.
	    - Use access control lists (ACLs) to restrict traffic to and from vulnerable areas.
	    - Ensure robust backup systems to protect data integrity.
	    - Educate secondary victims on security best practices.
	- **Neutralize Handlers**:
	    - Identify and disable command and control (C&C) servers used by attackers.
	    - Use threat intelligence to update blacklists of known malicious IP addresses.
	    - Deploy honeypots to attract and neutralize malicious traffic.
	    - Engage with ISPs to take down malicious domains and servers.
	- **Prevent Potential Attacks**:
	    - Apply patches and updates to all systems and applications promptly.
	    - Implement strong authentication and authorization mechanisms.
	    - Use encryption to protect data in transit and at rest.
	    - Employ proactive threat hunting to identify and mitigate threats before they materialize.
	    - Enforce strict password policies and use multi-factor authentication (MFA).
	- **Deflect Attacks**:
	    - Use deception technologies such as honeypots and honeynets to divert attackers.
	    - Implement load balancers to distribute traffic and reduce the impact of attacks.
	    - Deploy cloud-based DDoS protection services.
	    - Use network address translation (NAT) to obscure internal network structure.
	- **Mitigate Ongoing Attacks**:
	    - Deploy an incident response team to manage and mitigate the attack.
	    - Use firewall rules to block malicious IP addresses and domains.
	    - Implement rate limiting and traffic shaping to control traffic flow.
	    - Engage with law enforcement and security vendors for assistance.
	    - Isolate affected systems to prevent the spread of the attack.
	- **Perform Post-Attack Forensics**:
	    - Collect and analyze logs from all relevant systems.
	    - Preserve evidence for potential legal action.
	    - Conduct a root cause analysis to determine how the attack occurred.
	    - Review and update security policies and procedures based on findings.
	    - Communicate findings and lessons learned to stakeholders and improve defenses.
	- **Incident Response Planning**:
	    - Develop and maintain an incident response plan (IRP).
	    - Conduct regular training and simulation exercises for the incident response team.
	    - Establish clear communication channels for incident reporting and response.
	- **Continuous Monitoring and Improvement**:
	    - Implement continuous monitoring of networks and systems for real-time threat detection.
	    - Use security information and event management (SIEM) systems to aggregate and analyze security data.
	    - Regularly review and update detection and countermeasure strategies based on emerging threats and vulnerabilities.
	    - Perform regular security audits and compliance checks.
	    -
#### ISP Level Protection
- **Collaboration**: Working with ISPs to implement large-scale defenses.

#### Protection Tools and Techniques
- **Firewalls**: Configuring rules to block malicious traffic.
- **Intrusion Detection Systems (IDS)**: Monitoring network traffic for suspicious activity.
- **Honeypots**: Deploying decoy systems to attract and analyze attacks (e.g., SSHHiPot, Artillery).
- **Rate Limiting**: Controlling the rate of incoming traffic to prevent overload.
- **IP Blacklisting**: Blocking traffic from known malicious IP addresses.
- **Traffic Analysis**: Analyzing traffic patterns to identify and block attacks.
- **Behavior-Based Detection**: Identifying attacks based on anomalous behavior patterns.

#### Additional Information (Added)
- **Advanced Mitigation Techniques**: Use of AI and machine learning to predict and mitigate attacks.
- **Cloud-Based DDoS Protection**: Leveraging cloud services for scalable DDoS protection.
- **Legal and Ethical Considerations**: Understanding the legal implications and ethical considerations of implementing certain countermeasures.
---

# Lecture 22: IDS, IPS, Firewall Evasion
## Difference between IDS, IPS, FW, NGFW
- **IDS (Intrusion Detection System):**
	- **Function:**
	    - Monitors network traffic for suspicious activity and potential threats.
	    - Generates alerts when potential intrusions are detected.
	- **Deployment:**
	    - Can be network-based (NIDS) or host-based (HIDS).
	- **Response:**
	    - Passive: Alerts administrators but does not take action to block threats.
	- **Advantages:**
	    - Good for detecting a wide range of threats.
	    - Provides detailed information on potential security incidents.
	- **Limitations:**
	    - Cannot prevent or block attacks.
	    - Requires manual intervention to respond to threats.
- **IPS (Intrusion Prevention System):**
	- **Function:**
	    - Monitors network traffic for suspicious activity and potential threats.
	    - Takes action to block or prevent identified threats in real-time.
	- **Deployment:**
	    - Can be network-based (NIPS) or host-based (HIPS).
	- **Response:**
	    - Active: Automatically blocks or mitigates detected threats.
	- **Advantages:**
	    - Proactively prevents attacks from causing harm.
	    - Provides real-time threat mitigation.
	- **Limitations:**
	    - Can cause false positives, blocking legitimate traffic.
	    - May impact network performance due to real-time traffic inspection.
	- **Capabilities:**
		- **Signature-based Intrusion Detection and Prevention:**
		    - Uses predefined signatures to identify known threats.
		    - Effective at detecting well-known attacks quickly.
		- **Network-based Anomaly Detection:**
		    - Monitors network traffic patterns to identify deviations from normal behavior.
		    - Detects unknown or new threats by identifying anomalous activity.
		- **Network-based Vulnerability Assessment:**
		    - Scans the network for vulnerabilities that could be exploited by attackers.
		    - Helps in proactively identifying and addressing security weaknesses before they can be exploited.
- **FW (Firewall):**
	- **Function:**
	    - Controls incoming and outgoing network traffic based on predetermined security rules.
	    - Acts as a barrier between a trusted internal network and untrusted external networks.
	- **Deployment:**
	    - Typically placed at the network perimeter or between network segments.
	- **Response:**
	    - Static: Filters traffic based on rules set by administrators.
	- **Advantages:**
	    - Provides a first line of defense against external threats.
	    - Can block known malicious IP addresses and ports.
	- **Limitations:**
	    - Does not inspect the contents of traffic beyond basic header information.
    - Cannot detect or prevent sophisticated attacks that bypass basic filtering.
- **NGFW (Next-Generation Firewall):**
	- **Function:**
	    - Combines traditional firewall capabilities with advanced security features.
	    - Inspects traffic at a deeper level, including application layer.
	- **Deployment:**
	    - Placed at the network perimeter, similar to traditional firewalls.
	- **Response:**
	    - Dynamic: Uses advanced techniques to detect and block threats in real-time.
	- **Advantages:**
	    - Provides comprehensive security by combining multiple functions.
	    - Can inspect encrypted traffic and user-specific activity.
	- **Limitations:**
	    - More complex to configure and manage compared to traditional firewalls.
	    - Higher cost due to advanced capabilities and features.
	- **Capabilities:**
		- **Application Awareness and Control:**
		    - Identifies and controls applications regardless of port, protocol, or IP address used.
		    - Enables granular policy enforcement based on application and user.
		- **Web Content Filtering:**
		    - Filters web traffic to block access to malicious or inappropriate websites.
		    - Protects against web-based threats like malware and phishing.
		- **SSL Inspection:**
		    - Inspects encrypted traffic (SSL/TLS) to detect and block threats hidden within encrypted sessions.
		    - Ensures security policies are enforced even on encrypted traffic.
		- **User Identity Awareness:**
		    - Associates network traffic with specific users, enabling user-based policies.
		    - Enhances visibility and control over user activity on the network.

### **Intrusion Detection System (IDS):**
- **How an IDS Detects an Intrusion**:
    - Monitors network traffic.
    - Identifies suspicious activities based on signatures and behavior.
- **General Indications of Intrusions**:
    - Unusual login attempts.
    - Unauthorized file access.
    - Suspicious network traffic patterns.
- **Types of Intrusion Detection Systems**:
    - Network-based IDS (NIDS).
    - Host-based IDS (HIDS).
- **Types of IDS Alerts**:
    - True Positive.
    - False Positive.
    - True Negative.
    - False Negative.

### **Intrusion Prevention System (IPS):**
- An Intrusion Prevention System (IPS) is a proactive security measure that not only detects but also prevents malicious activities on a network.

#### How IPS Works:
- **Traffic Monitoring:**
    - The IPS continuously monitors all network traffic, inspecting packet headers and payloads to identify potential threats.
- **Detection Methods:**
    - **Signature-based Detection:**
        - Relies on a database of known threat signatures to identify and block malicious activity. This method is highly effective against known attacks but can struggle with zero-day threats.
    - **Anomaly-based Detection:**
        - Establishes a baseline of normal network behavior and flags deviations from this norm. This method can detect novel attacks but may produce false positives if normal behavior changes.
    - **Policy-based Detection:**
        - Uses predefined security policies to detect and respond to malicious activities. Policies can be based on organizational rules and compliance requirements.
    - **Heuristic-based Detection:**
        - Uses algorithms and heuristics to detect suspicious activities by identifying patterns that may indicate an attack.

#### **Response Actions:**
- **Blocking:**
    - The IPS can block malicious traffic immediately, preventing it from reaching its intended target.
- **Dropping:**
    - Malicious packets are discarded by the IPS to prevent them from causing harm.
- **Quarantining:**
    - Infected devices or suspicious traffic can be isolated to prevent the spread of malware.
- **Alerting:**
    - When a threat is detected, the IPS sends alerts to network administrators for further investigation.

#### **Types of IPS:**
1. **Network-based IPS (NIPS):**
    - Deployed at critical points in the network to inspect traffic across multiple segments.
    - Protects the network perimeter and internal network segments from a variety of threats.
2. **Host-based IPS (HIPS):**
    - Installed on individual hosts (e.g., servers, workstations).
    - Monitors and protects individual devices from both external and internal threats.
    - Provides granular control and protection for specific high-value assets.

#### **Advantages of IPS:**
- **Proactive Defense:**
    - An IPS actively blocks threats, providing a proactive layer of defense.
- **Comprehensive Protection:**
    - Protects against a wide range of attacks, including known and emerging threats.
- **Policy Enforcement:**
    - Ensures adherence to security policies and compliance requirements.
- **Integration:**
    - Can be integrated with other security solutions, such as firewalls and SIEM systems, for a comprehensive security posture.

#### **Challenges and Limitations of IPS:**
- **False Positives:**
    - Incorrectly identifying legitimate traffic as malicious can disrupt business operations.
- **Performance Impact:**
    - The inspection of large volumes of traffic can introduce latency and affect network performance.
- **Complex Configuration:**
    - Requires skilled personnel to configure, manage, and fine-tune the system.
- **Evasion Techniques:**
    - Sophisticated attackers may employ techniques to bypass IPS detection, necessitating constant updates and vigilance.

#### **IPS Deployment Best Practices:**
- **Proper Placement:**
    - Position IPS devices strategically within the network to maximize coverage and effectiveness.
- **Regular Updates:**
    - Keep signatures and detection rules up-to-date to defend against the latest threats.
- **Baseline Normal Traffic:**
    - Establish a baseline of normal network behavior to improve the accuracy of anomaly detection.
- **Monitor and Tune:**
    - Continuously monitor IPS alerts and adjust settings to minimize false positives and negatives.
- **Integration:**
    - Integrate IPS with other security systems for a layered defense strategy.
- **Testing:**
    - Regularly test the IPS to ensure it functions as expected and provides adequate protection.

#### **IPS vs. IDS:**
- **Intrusion Detection System (IDS):**
    - Detects and alerts on potential threats but does not take action to prevent them.
    - Functions as a passive monitoring tool.
- **Intrusion Prevention System (IPS):**
    - Actively blocks or mitigates detected threats, providing a proactive defense.
    - Functions as an active security measure.

#### **Examples of IPS:**
1. **Snort:**
    - An open-source network IPS and IDS.
    - Uses a rule-based language to detect and prevent network intrusions.
2. **Suricata:**
    - An open-source IDS, IPS, and network security monitoring engine.
    - Capable of real-time intrusion detection and prevention.
3. **Cisco Firepower:**
    - A commercial IPS solution by Cisco.
    - Integrates with Cisco’s security ecosystem for comprehensive threat protection.
4. **Palo Alto Networks:**
    - Next-generation firewalls with integrated IPS functionality.
    - Provides advanced threat prevention and real-time protection.

#### **Firewalls:**
- **Firewall Architecture**:
    - Packet filtering.
    - Stateful inspection.
    - Application-layer proxies.
    - NAT (Network Address Translation).
- **Types of Firewalls**:
    - Packet Filtering Firewalls.
    - Circuit-Level Gateways.
    - Application-Level Firewalls.
    - Stateful Multilayer Inspection Firewalls.
    - Application Proxy.
    - Network Address Translation (NAT).
- **Firewall Technologies by OSI Layer**:
    - Application: VPN, Application Proxies.
    - Presentation: VPN.
    - Session: VPN, Circuit-Level Gateways.
    - Transport: VPN, Packet Filtering.
    - Network: VPN, NAT, Packet Filtering, Stateful Multilayer Inspection.
    - Data Link: VPN, Packet Filtering.

#### **Honeypots:**
- **Types of Honeypots by Deployment Strategy**:
    - **Production Honeypots**:
        - Deployed inside production networks.
        - Capture limited adversary information.
        - Help find internal flaws and attackers.
    - **Research Honeypots**:
        - Deployed by research institutes and governments.
        - High interaction to gain detailed adversary knowledge.
- **Types of Honeypots by Deception Technology**:
    - **Malware Honeypots**:
        - Trap malware campaigns.
        - Emulate vulnerabilities to lure attackers.
    - **Database Honeypots**:
        - Fake databases for SQL injection and enumeration attacks.
    - **Spam Honeypots**:
        - Target spammers abusing open mail relays.
    - **Email Honeypots**:
        - Fake email addresses to attract malicious emails.
    - **Spider Honeypots**:
        - Trap web crawlers extracting sensitive information.
    - **Honeynets**:
        - Networks of honeypots to determine adversaries' capabilities.
- **Detecting Honeypots**
	- **Probe services on system**
		- Craft malicious HTTPS, SMTPS or IMAPS packets
		- Deny the 3-way handshake to confirm if service is running
		- Can extend this by using TOR for multiprobes
	- **Detect Layer 7 TarPits**
		- Observe Latency Response
	- **Detect Layer 4 TarPits**
		- Observe TCP window Size, could constantly ACK packets even if it is 0
	- **Detect Layer 2 TarPits**
		- Observe MAC address **0:0:f:ff:ff:ff**
			- Acts as a black hole
	- **Detect Honeypots running on VMWare**
		- Observe IEEE standards for current range of MAC addresses assigned to VMWare inc
	- **Detect presence of HoneyD Honeypot**
		- Observe time-based TCP Fingerprinting behavior (SYN-Proxy)
	- **Detect presence of User-Mode Linux Honeypot**
		- Observe mount, interrupts and cmdline files in /proc
		- These contain UML info
	- **Detect presence of Sebek-based Honeypot**
		- Observe congestion in Network Layer
	- **Detect presence of Snort_inline Honeypot**
		- Observe outgoing packets through another host and look for modifications
	- **Detect presence of Fake AP**
		- Only beacon frames sent by FakeAP
		- Can notice this during monitoring
	- **Detect presence of Bait&Switch Honeypot**
		- Observe TCP/IP attributes such as RTT, TTL, TCP Timestamp

#### **Intrusion Detection Tools:**
- **Snort**:
    - Rule-based intrusion detection system.
	    - Example Rule
		    - `log tcp any any -> 192.168.1.0/24 !6000:6010`
			    - RuleAction ProtocolType src dest
    - Capabilities include rule actions, IP protocols, direction operator, IP addresses, and port numbers.
- **Suricata and AlienVault OSSIM**:
    - Alternative IDS tools with various detection capabilities.

#### **Intrusion Detection Tools for Mobile Devices:**
- **Zimperium’s zIPS**:
    - Mobile intrusion prevention system for iOS and Android.
    - Detects known and unknown threats by analyzing device behavior.
- **Wifi Inspector**:
    - Identifies devices connected to the network.
    - Provides IP addresses, device names, and MAC addresses.
- **Wifi Intruder Detect**:
    - Detects intruders accessing the network without consent.

#### **Evasion Techniques:**
- **Insertion and Evasion**
    - **Insertion**:
        - Force IDS/IPS to read invalid packets:
            - Malformed length
            - Varied TTL
        - IDS gets way more packets than the destination in an attempt to sneak more through
    - **Evasion**:
        - Send a bytestream where half is rejected by IDS
        - The malicious section is not rejected and passed onto the end system
        - IDS gets fewer packets than the destination
- **Denial-of-Service Attack (DoS)**
    - Overload the system to disrupt service.
    - Target the centralized logging/monitoring server, overload so that:
        - IDS/IPS is locked up
        - Support cannot observe logs, as none are recorded
        - DoS the IDS/IPS + Logging server
- **Obfuscating**
    - Hiding attack details to avoid detection.
    - Use of polymorphic code, bypasses signature-based IDS/IPS
- **False Positive Generation**
    - Create noise to cause false alarms.
    - Hide real attack traffic, IDS cannot differentiate true from false
- **Session Splicing**
    - Split attack data into smaller packets.
    - Useful for IDS that do not reconstruct packets after intrusion signatures
        - Even if they do, they have a time limit via a delay, bypassing that limit allows for splicing
    - Attack is not logged after a successful splice
- **Unicode Evasion Technique**
    - Use Unicode characters to bypass detection.
    - Multiple representations of the same character
    - Convert attack strings to Unicode to avoid pattern and signature matching
- **Fragmentation Attack**
	- Both the victim and IDS receive fragments 2 and 4 (out of 4) with a false payload.
	- The victim drops these fragments after 30 seconds without sending an ICMP message, as fragment 1 was never received.
	- Both the victim and IDS receive fragments 1 and 3 (out of 4).
	- The IDS attempts to reassemble the four received fragments but drops the packet due to an invalid checksum.
	- Both the victim and IDS receive the real fragments 2 and 4 (out of 4).
	- The victim reassembles the four fragments and is successfully attacked, while the IDS times out and drops fragments 2 and 4.
- **Time-To-Live Attack**
    - Manipulate TTL to bypass network security.
    - Set the TTL value of packets to expire before reaching the IDS. Frag malicious packet into 3 frags
	    - Send Frag1-HighTTL + Frag2-LowTTL
	    - IDS checks both, Target only gets the 1st frag
	    - Send Frag3-HighTTL, target receives 3rd frag
	    - IDS drop malformed packet after reassembly
	    - Send Frag2-NormalTTL
	    - No log created for attack
    - Ensure that the IDS does not see the packet while the target does.
- **Invalid RST Packets**
    - Send invalid reset packets to disrupt connections.
    - Send reset (RST) packets with invalid checksum
    - IDS does not process as it assumes connection is closed but the data is still sent
    - Target drops the packet but now IDS will not check for further packets sent to the Target
- **Urgency Flag**
    - Use urgent flags in TCP packets for evasion.
    - Set the URG flag in TCP packets.
    - Bypass IDS filters that do not properly handle or inspect urgent data.
- **Polymorphic Shellcode**
    - Modify shellcode to avoid signature detection.
	    - Combine multiple sigs to avoid matches
    - Change the appearance of the shellcode each time it is sent.
	    - Encode/Encrypt the payload
    - Evade signature-based IDS by ensuring the shellcode does not match known patterns.
- **Application-Layer Attacks**
    - Exploit application vulnerabilities that can cause an overflow.
    - Target weaknesses in the application layer (e.g., SQL injection, XSS).
	    - Compress the files to bypass sig verification
    - Bypass lower-layer IDS/IPS that focus on network or transport layer attacks.
- **Desynchronization**
	- **Pre-Connection SYN**
		- **Mechanism**: Send an initial SYN with an invalid TCP checksum before the real connection.
		- **Impact on IDS**: If the IDS sees this SYN after opening the TCP control block, it resets the sequence number to match the fake SYN.
		- **Objective**: Attackers use invalid sequence numbers to desynchronize the IDS, preventing it from monitoring legitimate and attack traffic.
	- **Post-Connection SYN**
		- **Mechanism**: Send a SYN packet within an established connection, causing divergent sequence numbers.
		- **Impact on Target Host**: Ignores the SYN as the connection is already established.
		- **Impact on IDS**: Resynchronizes to the new SYN packet's sequence numbers, ignoring legitimate data from the original stream.
		- **Follow-Up**: Attackers send an RST packet with the new sequence number to close the IDS's notion of the connection, fully desynchronizing it.
- **Other Types of Evasion**
    - Various advanced techniques to avoid detection.
    - **Examples**:
        - **Encrypted Traffic**: Use encryption to hide payload content.
        - **Tunneling**: Encapsulate malicious traffic in legitimate protocols (e.g., HTTP, DNS).
        - **Traffic Morphing**: Alter traffic patterns to mimic benign activity.
        - **Behavioral Evasion**: Change attack behavior dynamically to avoid behavioral detection systems.

### Defend against IDS/FW Evasion
- **IDS Best Practices:**
	- Normalize fragmented packets for proper reassembly.
	- Define DNS server with client resolver for routers and network devices.
	- Enhance security of modems, routers, and switches.
	- Disable switch ports associated with known attack hosts.
	- Conduct in-depth analysis of ambiguous network traffic.
	- Use TCP FIN or reset (RST) packets to terminate malicious TCP sessions.
	- Detect non-standard nop opcodes to defend against polymorphic shellcode.
	- Train users to recognize attack patterns and update systems regularly.
	- Deploy IDS after analyzing network topology, traffic nature, and host count.
	- Use traffic normalizers to remove ambiguity before packets reach IDS.
	- Block ICMP TTL expired packets at external interfaces and set large TTL values.
	- Regularly update antivirus signature databases.
	- Store attack information (IP addresses, timestamps) for future analysis.
- **Firewall Best Practices:**
	- Run regular risk queries to identify vulnerable firewall rules.
	- Filter out intruder IP addresses in firewall configuration.
	- Set ruleset to deny all traffic by default, enabling only required services.
	- Monitor and restrict user access to firewall configurations.
	- Notify and document firewall changes to the security policy administrator.
	- Use unique user IDs for firewall services instead of administrator/root IDs.
	- Configure and protect a remote syslog server from malicious users.
	- Regularly monitor firewall logs and investigate suspicious entries.
	- Specify source and destination IP addresses and ports.
	- Control physical access to the firewall.
	- Disable all FTP connections by default.
	- Take regular backups of firewall ruleset and configuration files.
	- Review all inbound and outbound traffic allowed through the firewall.
	- Schedule regular firewall security audits.

### Tools for IDS/IPS and Honeypots:
- **HoneyBOT**
- **MongoDB-HoneyProxy**
- **Modern Honey Network**
- **Honeyd**

---

# Assignment 3 + 4: Host + Port Discovery
## Host Discovery

``` python
def scan(nm, target, arguments=None):
    # Perform the scan
    nm.scan(
        hosts=target, arguments=f"{arguments} --min-rate=5000 -T5 -reason", sudo=True
    )

    # Loop through the scan results and get the status and state of each host
    hosts_list = [(x, nm[x]["status"]["state"]) for x in nm.all_hosts()]

    # if hosts_list is emptu, then no hosts were discovered
    if len(hosts_list) == 0:
        print(
            f"\t[!] No hosts discovered."
        )
    else:
        print(
            f"\t[!] Hosts discovered:"
        )
        for host, status in hosts_list:
            # If host is X.X.X.1 or X.X.X.254, then it is a router
            if host.split(".")[-1] == "1" or host.split(".")[-1] == "254":
                print(
                    f"\t\t[+] {host} is a router."
                )
            else:
                # If host is up, then get the reason
                if nm[host]["status"]["state"] == "up":
                    # If host is up, then get the reason
                    reason = nm[host]["status"]["reason"]

    print("\n")

    # List of scan names
    scanName = [
        "ARP ping (-PR)",
        "ICMP Echo ping (-PE)",
        "ICMP Echo ping sweep (-PS)",
        "ICMP timestamp ping (-PP)",
        "ICMP Address Mask ping (-PM)",
        "UDP Ping (-PU)",
        "TCP SYN (-PS)",
        "TCP ACK (-PA)",
        "TCP NULL (-PN)",
        "TCP FIN (-sF)",
        "TCP XMAS (-sX)",
        "IP Protocol ping (-PO)",
    ]
```

## Port Discovery

``` python
def scan(nm, target, argument=None):
    # Perform the scan
    nm.scan(
        hosts=target,
        arguments=f"{argument} -F --min-rate=5000 -T5 --reason",
        sudo=True,
    )

    # Loop through the scan results and get the status and state of each host
    hosts_list = [(x, nm[x]["status"]["state"]) for x in nm.all_hosts()]

    # if hosts_list is emptu, then no hosts were discovered
    if len(hosts_list) == 0:
    else:
        downHosts = 0
        for host, status in hosts_list:
            # If host is X.X.X.1 or X.X.X.254, then it is a router
            if host.split(".")[-1] == "1":
                continue
                # print(
                #     f"\t\t[+] {host} is default gateway."
                # )
            elif host.split(".")[-1] == "254":
                continue
                # print(
                #     f"\t\t[+] {host} is a broadcast address."
                # )
            else:
                # If host is up, then get the reason
                if nm[host]["status"]["state"] == "up":
                    # If host is up, then get the reason
                    reason = nm[host]["status"]["reason"]
                    if reason == "localhost-response":
                        continue

                    # Get port status of the host as well
                    for proto in nm[host].all_protocols():
                        lport = list(nm[host][proto].keys())
                        lport.sort()
                        print(lport)
                        for port in lport:
                            state = nm[host][proto][port]["state"]

    print("\n")
        scanName = [
            "ICMP Ping (-PE)",
            "UDP Ping (-sU)",
            "TCP SYN (-sT)",
            "TCP SYN Silent|Half-Open (-sS)",
            "Inverse TCP NULL (-sN)",
            "Inverse TCP XMAS (-sX)",
            "Inverse TCP Maimon (-sM)",
            "ACK TTL-Based (-sA)",
            "ACK Window (-sW)",
        ]

```

---

# Assignment 5: Post Exploitation (RID Hijacking)
- **Registry Entry**
	- HKEY_LOCAL_MACHINE\\SAM\\SAM\\Domains\\Accounts\\\\Users\\selectedUser\\
	- Access by using PsExec to run regedit (Access SAM entries as SYSTEM)
	- Key value determines account access level (RID)
		- Admins have 0x1f4h -> 500
		- Guests have 0x1f5h -> 501
	- Can be validated using wmic (Use sql style commands to query data)
- **Reading Security Identifiers (SID)**
	- Length -> 256 char
	- Format
		- `S-1-5-21-3623811015-3361044348-30300820-1013`
			- S -> SID is a string
			- 1 -> Version level of SID
			- 5 -> Identifier Authority Value
			- 21-3623811015-3361044348-30300820 -> Subauthority value
			- 1013 -> RID.
				- In this case it is not a default account hence the >1000 RID
	- **HEX info. Note that these are reversed**
		- Offset 30 stores RID
		- Offset 38 stores account enable state
			- 1502 -> Disabled, 1402 -> Enabled

---