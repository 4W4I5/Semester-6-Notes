| Lecture Number    | Status             |
| ----------------- | ------------------ |
| 2.pdf             | :white_check_mark: |
| 3.pdf             | :white_check_mark: |
| Reading Article-1 | :x:                |
| 4.pdf             | :warning:          |
| 5.pdf             | :warning:          |
| 6.pdf             | :warning           |
| 7.pdf             | :warning:          |
|                   |                    |

<!--
:x:
:warning:
:white_check_mark:
-->

NOTE:: Skipped introduction
# Lecture 2: History of malware
- Malware is a software that is written with the intention of disrupting networks, causing harm to user/computer
	- Without the knowledge of the user (Ransomware only reveals itself when the data is encrypted)
- Taxonomy
	- Malicious programs
		- Needs a host
			- Trapdoors
			- Logic Bombs
			- Trojans
			- Viruses
		- Independent
			- Worm
			- Zombie
- Goals of MA&RE
	- Determine capability of Malware
	- Detect
	- Contain
	- Cure and prevent future infections

| Aspect             | Static Analysis                                          | Dynamic Analysis                                                |
| ------------------ | -------------------------------------------------------- | --------------------------------------------------------------- |
| Timing of Analysis | Performed without executing the program                  | Performed while the program is executing                        |
| Scope of Analysis  | Focuses on the source code or static representations     | Focuses on the runtime behavior of the software                 |
| Type of Issues     | Syntactic and semantic issues, potential vulnerabilities | Runtime errors, memory leaks, buffer overflows                  |
| Automation         | Can be highly automated                                  | May require manual intervention, but can be automated           |
| Coverage           | Provides comprehensive coverage of the codebase          | Coverage depends on the executed test cases                     |
| Resource           | Requires fewer resources                                 | Can be more resource-intensive, especially for complex programs |

- Advanced Persistent Threat (APT)
	- Malware created to infect a particular individual, company or organization
	- Targeted campaigns against
		- Platforms
		- Devices
		- Network
		- Stay undetected for a long time (STUXNET for e.g.)
	- Cyber killchain
		- Reconnaissance
		- Weaponization
		- Delivery
		- Exploitation
		- Installation
		- C2
		- Action on Objectives
- Components of Malware
	- Stealth
		- Packer: Techniques used to compress/encrypt malware code to evade detection by antivirus or other security measures
	- Armoring
		- Payload: Main component of malware
		- Mechanisms such as Obfuscation/Encryption to conceal the malware. Counts as stealth as well
	- Persistence
		- Mechanisms used by malware to maintain its presence on an infected system even after reboot/removal attempts
	- Propagation
		- Mechanisms used by the malware to spread to other systems/devices
	- Communication
		- Interactions b/w malware and C2 server
- Distribution Mechanisms
	- Heavily dependent on social engineering
		- Email
		- Clicking on links
		- Drive-by Downloads
- Exploits
	- Small piece of code input into programs to target their vulns
	- Patches
		- Identify and fix vulns before they can be exploits
		- Done via updates by vendors
		- Zero-Day = Vuln is not patched
	- Exploit Kit
		- Devised to attack computers that are hidden behind their home network
		- Automatically managing and deploying exploits against a target computer
		- Baits and traps using malicious servers
		- Wait for users to contact these malicious server
- Dimensions of infection vectors
	- Speed
	- Stealth
	- Coverage
	- Shelf life

# Lecture 3: Setting up a malware lab
- Precautions
	- Virtualization software must be kept uptodate
	- Fresh copy of Guest OS
	- No sensitive information within the guest OS
	- Host-Only network config
	- No removeable media must be connected
	- Different Host OS to Guest OS