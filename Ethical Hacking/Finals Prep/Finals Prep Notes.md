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
#### Introduction to Social Engineering
- **Definition**: The art of convincing people to reveal confidential information.
- **Common Targets**:
    - Help desk personnel
    - Support executives
    - System administrators
    - Receptionists
    - Technical support executives
    - Users
    - Clients
    - Vendors
    - Senior executives

#### Impact of Social Engineering
- **Economic Losses**: Direct financial damage.
- **Damage to Goodwill**: Harm to reputation and trust.
- **Loss of Privacy**: Compromised personal and organizational information.
- **Dangers of Terrorism**: Potential misuse of information for terrorist activities.
- **Lawsuits and Arbitration**: Legal consequences and disputes.
- **Temporary or Permanent Closure**: Operational shutdowns.

#### Vulnerable Behaviors
- **Authority**: Trusting figures of authority without verification.
- **Intimidation**: Succumbing to threats or coercion.
- **Consensus/Social Proof**: Following the crowd without critical thinking.
- **Scarcity**: Acting out of fear of missing out.
- **Urgency**: Responding quickly due to a sense of urgency.
- **Familiarity/Liking**: Trusting individuals based on perceived friendliness.
- **Trust**: Misplaced trust in unverified entities.
- **Greed**: Falling for offers that seem too good to be true.

#### Factors Making Companies Vulnerable
- **Insufficient Security Training**: Lack of awareness and skills.
- **Unregulated Access to Information**: No strict control over sensitive data.
- **Multiple Organizational Units**: Complexity and lack of cohesive security measures.
- **Lack of Security Policies**: Absence of formal guidelines and procedures.

#### Effectiveness of Social Engineering
- **Human Susceptibility**: Humans are the weakest link in security.
- **Detection Challenges**: Difficult to identify and prevent.
- **Low Cost and Ease of Implementation**: Simple and inexpensive for attackers.

#### Phases of Social Engineering Attack
1. **Research the Target Company**: Gathering information.
2. **Select a Target**: Identifying a specific victim.
3. **Develop a Relationship**: Establishing trust.
4. **Exploit the Relationship**: Using trust to extract information.

#### Types of Social Engineering Attacks
- **Human-Based**: Direct interactions such as:
    - **Impersonation**: Pretending to be someone else to gain information.
    - **Eavesdropping**: Listening to private conversations to gather information.
    - **Shoulder Surfing**: Observing someone entering confidential information.
    - **Dumpster Diving**: Searching through trash for sensitive information.
    - **Piggybacking/Tailgating**: Gaining unauthorized access by following someone into a secure area.
- **Computer-Based**: Techniques such as:
    - **Phishing**: Deceptive emails or websites to steal information.
    - **Spam**: Unsolicited emails often containing malicious links or attachments.
    - **Pop-up Attacks**: Malicious pop-ups that trick users into revealing information.
    - **Spear Phishing**: Targeted phishing attacks on specific individuals.
    - **Vishing**: Voice phishing using phone calls to extract information.
    - **Whaling**: Phishing attacks targeting senior executives.
- **Mobile-Based**: Techniques such as:
    - **Malicious Apps**: Applications designed to steal information.
    - **Fake Security Applications**: Apps pretending to be security tools but are malicious.
    - **SMiShing**: Phishing attacks via SMS.

#### Phishing Tools
- **ShellPhish**
- **BLACKEYE**
- **Phishx**
- **Modlishka**
- **Trape**
- **Evilginx**

#### Insider Threats
- **Definition**: Attacks by trusted individuals with privileged access.
- **Common Perpetrators**:
    - Privileged users
    - Disgruntled employees
    - Terminated employees
    - Accident-prone employees
    - Third parties
    - Undertrained staff
- **Motivations**:
    - Financial gain
    - Data theft
    - Revenge
    - Competition
    - Public announcements

#### Types of Insider Threats
1. **Malicious Insider**: Intentional harm.
2. **Negligent Insider**: Unintentional harm due to carelessness.
3. **Professional Insider**: Selling information to competitors.
4. **Compromised Insider**: External manipulation of an insider.

#### Social Networking Threats
- **Data Theft**
- **Involuntary Data Leakage**
- **Targeted Attacks**
- **Network Vulnerability**
- **Spam and Phishing**
- **Content Modification**
- **Malware Propagation**
- **Business Reputation Damage**
- **Infrastructure and Maintenance Costs**
- **Loss of Productivity**

#### Identity Theft
- **Definition**: Stealing personal information for fraudulent purposes.
- **Commonly Stolen Information**:
    - Name
    - Address
    - SSN
    - Phone number
    - DOB
    - Bank account numbers
    - Credit card info
    - Usernames and passwords
- **Uses**:
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

#### Countermeasures
- **Awareness and Training**: Educate employees.
- **Effective Policies**: Develop and enforce security policies.
- **Background Checks**: Thorough vetting of employees.
- **Two-Factor Authentication**: Enhanced security measures.
- **Regular Software Updates**: Ensure systems are up-to-date.
- **Monitoring and Auditing**: Continuous oversight of activities.
- **Physical Security**: Secure access to physical facilities.
- **Data Loss Prevention (DLP)**: Tools to monitor and protect data.
- **Identity and Access Management (IAM)**: Control user access.

#### Detecting Insider Threats
- **Deterrence Controls**:
    - Separation of duties
    - Assigning privileges
    - Recommended actions
- **Detection Controls**:
    - IDS/IPS
    - Log management
    - SIEM tools
- **Insider Risk Controls**:
    - Monitor permissions
    - Access controls
    - User actions

#### Identity Theft Prevention
- **Document Security**: Shred sensitive documents.
- **Personal Information Protection**: Secure personal data.
- **Credit Monitoring**: Regularly review credit reports.
- **Safe Communication**: Verify requests for personal data.
- **Secure Online Practices**: Avoid sharing sensitive information on public Wi-Fi, enable two-factor authentication, use host security tools.

#### Examples of Social Engineering Attacks
1. **Phishing**: Deceptive emails or websites to steal information.
2. **Pretexting**: Creating a fabricated scenario to obtain information.
3. **Baiting**: Offering something enticing to get information or infect a system.
4. **Quid Pro Quo**: Offering a service in exchange for information.
5. **Tailgating**: Following someone into a restricted area.

### Additional Information (Not in PPT)
- **Social Engineering in Cybersecurity Context**:
    - Often the first step in larger cyber attacks.
    - Can lead to more significant breaches like malware deployment, ransomware attacks, and data exfiltration.
- **Psychological Manipulation Techniques**:
    - **Reciprocity**: People tend to return favors.
    - **Commitment**: Once a person commits to something, they are more likely to follow through.
    - **Consistency**: Aligning new requests with previous actions or beliefs.
- **Recent Trends**:
    - Increasing sophistication of attacks.
    - Use of AI and deepfakes to enhance credibility.
    - Targeted attacks on remote workers due to the rise of telecommuting.
---

# Lecture 21: DoS & DDoS
#### Overview of DoS/DDoS
- **Denial of Service (DoS) Attack**
    - Definition: An attack on a computer or network that reduces, restricts, or prevents access to system resources for legitimate users.
    - Goal: To make a system or network resource unavailable to its intended users.
    - Methods: Flooding the victim’s system with non-legitimate service requests or traffic.
- **Distributed Denial of Service (DDoS) Attack**
    - Definition: A coordinated attack that involves multiple compromised systems (botnet) attacking a single target, denying service to users of the targeted system.
    - Mechanism: Utilizes a botnet to launch attacks from numerous sources.

#### Types of DoS Attacks
- **Flooding Attacks**
    - Overloading a system with more traffic than it can handle.
- **Service Flooding**
    - Overloading a service (e.g., IRC) with more events than it can handle.
- **Corrupt Packet Attacks**
    - Crashing a TCP/IP stack by sending corrupt packets.
- **Unexpected Interactions**
    - Crashing a service by interacting with it in unexpected ways.
- **Infinite Loops**
    - Hanging a system by causing it to enter an infinite loop.

#### Impact of DoS Attacks
- Consumption of resources (bandwidth, disk space, CPU time).
- Physical destruction or alteration of network components.
- Destruction of programs and files in a computer system.

#### Categories of DoS/DDoS Attack Vectors
- **Volumetric Attacks**
    - **Definition**: Exhaust bandwidth either within the target network or between the target and the rest of the Internet.
    - **Magnitude**: Measured in bits per second (bps).
    - **Techniques**:
        - **Flood Attack**: Zombies send large volumes of traffic to exhaust the target’s bandwidth.
        - **Amplification Attack**: Attacker sends messages to a broadcast IP address to amplify malicious traffic.
        - **Examples**:
            - UDP flood attack
            - ICMP flood attack
            - Ping of Death (PoD) attack
            - Smurf attack
            - Pulse wave attack
            - Zero-day attack
            - Malformed IP packet flood attack
            - Spoofed IP packet flood attack
- **Protocol Attacks**
    - **Definition**: Consume resources other than bandwidth, such as connection state tables.
    - **Magnitude**: Measured in packets per second (pps) or connections per second (cps).
    - **Techniques**:
        - SYN flood attack
        - Fragmentation attack
        - Spoofed session flood attack
        - ACK flood attack
        - TCP state exhaustion attack
        - RST attack
- **Application Layer Attacks**
    - **Definition**: Exploit vulnerabilities in the application layer protocol or application itself.
    - **Magnitude**: Measured in requests per second (rps).
    - **Techniques**:
        - HTTP flood attack
        - Slowloris attack
        - UDP application layer flood attack
        - HTTPS GET/POST attack
        - Multi-vector attack
        - Peer-to-peer attack
        - Permanent DoS (PDoS) attack
        - Distributed reflection DoS (DRDoS) attack

#### Botnets in DDoS Attacks
- **Botnets**: Networks of compromised systems used to perform various malicious activities including DDoS attacks, spamming, keylogging, and more.
- **Typical Botnet Setup**:
    - Scanning for vulnerable machines.
    - Propagation of malicious code.
    - Use of mobile devices for launching attacks.

#### Case Studies
- **DDoS Attack on GitHub**
    - Demonstrates the impact of DDoS attacks and response strategies.

#### DoS/DDoS Attack Techniques
- **UDP Flooding Attack**: Overwhelming a target with UDP packets.
- **ICMP Flooding Attack**: Overloading a target with ICMP packets.
- **Ping of Death**: Sending oversized packets causing buffer overflow.
- **Smurf Attack**: Using IP broadcast with ICMP requests to flood a target.
- **Pulse Wave Attack**: Alternating high-volume attacks to bypass mitigation strategies.
- **Zero-Day Attack**: Exploiting unknown vulnerabilities.
- **SYN Flood Attack**: Exploiting TCP connection sequence by sending SYN requests and not responding to SYN-ACK.

#### Countermeasures for SYN Flood Attacks
- Decrease the time-out period for pending connections.
- Use SYN cookies and SynAttackProtect.

#### Detection and Countermeasures
- **Detection Techniques**: Identify unusual traffic patterns, implement rate-limiting, and use anomaly detection systems.
- **Countermeasure Strategies**:
    - Protect secondary victims.
    - Neutralize handlers.
    - Prevent potential attacks.
    - Deflect attacks.
    - Mitigate ongoing attacks.
    - Perform post-attack forensics.

#### ISP Level Protection
- **Collaboration**: Work with ISPs to implement large-scale defenses.

#### Protection Tools and Techniques
- **Tools**: Firewalls, intrusion detection systems (IDS), honeypots (e.g., SSHHiPot, Artillery).
- **Techniques**: Rate limiting, IP blacklisting, traffic analysis, and behavior-based detection.
---

# Lecture 22: IDS, IPS, Firewall Evasion
#### **Difference between IDS, IPS, FW, NGFW:**
- **NGFW Capabilities**:
    - Application awareness and control.
    - Web content filtering.
    - SSL inspection.
    - User identity awareness.
- **IPS Capabilities**:
    - Signature-based intrusion detection and prevention.
    - Network-based anomaly detection.
    - Network-based vulnerability assessment.

#### **Intrusion Detection System (IDS):**
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

#### **Intrusion Prevention System (IPS):**
- An Intrusion Prevention System (IPS) is a proactive security measure that not only detects but also prevents malicious activities on a network.
**How IPS Works:**
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
**Response Actions:**
- **Blocking:**
    - The IPS can block malicious traffic immediately, preventing it from reaching its intended target.
- **Dropping:**
    - Malicious packets are discarded by the IPS to prevent them from causing harm.
- **Quarantining:**
    - Infected devices or suspicious traffic can be isolated to prevent the spread of malware.
- **Alerting:**
    - When a threat is detected, the IPS sends alerts to network administrators for further investigation.
**Types of IPS:**
1. **Network-based IPS (NIPS):**
    - Deployed at critical points in the network to inspect traffic across multiple segments.
    - Protects the network perimeter and internal network segments from a variety of threats.
2. **Host-based IPS (HIPS):**
    - Installed on individual hosts (e.g., servers, workstations).
    - Monitors and protects individual devices from both external and internal threats.
    - Provides granular control and protection for specific high-value assets.
**Advantages of IPS:**
- **Proactive Defense:**
    - An IPS actively blocks threats, providing a proactive layer of defense.
- **Comprehensive Protection:**
    - Protects against a wide range of attacks, including known and emerging threats.
- **Policy Enforcement:**
    - Ensures adherence to security policies and compliance requirements.
- **Integration:**
    - Can be integrated with other security solutions, such as firewalls and SIEM systems, for a comprehensive security posture.
**Challenges and Limitations of IPS:**
- **False Positives:**
    - Incorrectly identifying legitimate traffic as malicious can disrupt business operations.
- **Performance Impact:**
    - The inspection of large volumes of traffic can introduce latency and affect network performance.
- **Complex Configuration:**
    - Requires skilled personnel to configure, manage, and fine-tune the system.
- **Evasion Techniques:**
    - Sophisticated attackers may employ techniques to bypass IPS detection, necessitating constant updates and vigilance.
**IPS Deployment Best Practices:**
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
**IPS vs. IDS:**
- **Intrusion Detection System (IDS):**
    - Detects and alerts on potential threats but does not take action to prevent them.
    - Functions as a passive monitoring tool.
- **Intrusion Prevention System (IPS):**
    - Actively blocks or mitigates detected threats, providing a proactive defense.
    - Functions as an active security measure.
**Examples of IPS:**
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

#### **Intrusion Detection Tools:**
- **Snort**:
    - Rule-based intrusion detection system.
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
- **Insertion and Evasion**:
    - Techniques to bypass IDS/IPS detection.
- **Denial-of-Service Attack (DoS)**:
    - Overload the system to disrupt service.
- **Obfuscating**:
    - Hiding attack details to avoid detection.
- **False Positive Generation**:
    - Create noise to cause false alarms.
- **Session Splicing**:
    - Split attack data into smaller packets.
- **Unicode Evasion Technique**:
    - Use unicode characters to bypass detection.
- **Fragmentation Attack**:
    - Split malicious payload into fragments.
- **Time-To-Live Attack**:
    - Manipulate TTL to bypass network security.
- **Invalid RST Packets**:
    - Send invalid reset packets to disrupt connections.
- **Urgency Flag**:
    - Use urgent flags in TCP packets for evasion.
- **Polymorphic Shellcode**:
    - Modify shellcode to avoid signature detection.
- **Application-Layer Attacks**:
    - Exploit application vulnerabilities.
- **Desynchronization**:
    - Desynchronize IDS/IPS and target communications.
- **Other Types of Evasion**:
    - Various advanced techniques to avoid detection.

### Tools for IDS/IPS and Honeypots:
- **HoneyBOT**
- **MongoDB-HoneyProxy**
- **Modern Honey Network**
- **Honeyd**

---

# Assignment 3 + 4: Host + Port Discovery
### Host Discovery
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

### Port Discovery
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