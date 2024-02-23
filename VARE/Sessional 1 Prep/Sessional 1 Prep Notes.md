| Lecture Number                         | Status             |
| -------------------------------------- | ------------------ |
| Lecture 2: History of malware          | :white_check_mark: |
| Lecture 3: Setting up a malware lab    | :white_check_mark: |
| Reading Article-1                      | :white_check_mark: |
| Lecture 4: Static malware analysis - 1 | :white_check_mark: |
| Lecture 5: PE + COFF                   | :white_check_mark: |
| Lecture 6: String Analysis             | :warning           |
| Lecture 7: YARA                        | :warning:          |

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
	- Virtualization software must be kept UpToDate
	- Fresh copy of Guest OS
	- No sensitive information within the guest OS
	- Host-Only network config
	- No removeable media must be connected
	- Different Host OS to Guest OS
# Reading Article till page 14
Skipped taxonomy of malware. Added some extra types though
- Scareware
	- Designed to trick a user into buying and downloading unnecessary and potentially dangerous software
- Bots
	- Controlled by a C2 server, allows remote control of the infected system
- Rootkits
	- Hide processes/programs that enable continued privileged access to computers. They can instrument API calls in user-mode or tamper with OS structures as a device driver or a kernel module
- Hybrid malware
	- A malware that can belong to two or multiple types simultaneously. Such as spamware, adware and the like

### Development of the malware industry
-  Malware originated to expose security flaws or showcase technical prowess.
- Tactics like encryption, packing, obfuscation, polymorphism, and metamorphism are used to evade detection.
- Initially driven by curiosity, malware development shifted to profit-driven motives, exploiting the booming e-commerce sector.
- Trojans surged, constituting 73% of malware, forming a lucrative underground industry.
- Despite increased complexity, the barrier to entry for creating malware has lowered due to user-friendly toolkits like Zeus and SpyEye.
- This led to a flood of variants that mutate rapidly, overwhelming anti-malware systems.
- The exponential growth of malware is evident, posing a persistent threat to cybersecurity.

### Progress in malware detection
- **Signature-based Malware Detection**:
  - Anti-malware products like Comodo, Kaspersky, and others use signature-based methods to detect known threats.
  - Signatures are unique sequences of bytes specific to each malware, allowing for accurate identification.
  - The process involves manual generation, updating, and dissemination of signatures, leading to delays in detecting new threats.
- **Heuristic-based Malware Detection**:
  - This method relies on rules or patterns to discern malware from benign files, but it's prone to errors and time-consuming.
  - Automated malware development toolkits enable the creation of thousands of new malicious codes daily, evading traditional detection methods.
  - Manual analysis becomes a bottleneck, demanding intelligent techniques for automatic sample analysis.
- **Cloud-based Malware Detection**:
  - Many anti-malware vendors use cloud-based detection to overcome challenges and improve effectiveness.
  - The workflow involves scanning files locally, sending information about unknown files to the cloud server, classification by classifiers, and sending verdicts back to clients.
  - This approach ensures up-to-date security solutions and addresses the increasing number of unknown files.

### Malware detection by applying datamining techniques
- **Data Mining Techniques for Malware Detection**:
  - These techniques classify unseen malware samples, identify malware families, or infer signatures.
  - Detection involves feature extraction and classification/clustering.
  - Techniques vary in feature representation and data mining methods.
- **Classification**:
  - Model construction involves training samples, feature extraction, and classification algorithms like ANN, DT, or SVM.
  - Model usage classifies new samples based on their extracted feature vectors.
- **Clustering**:
  - Clustering groups malware samples with similar behaviors into different clusters.
  - It enables automatic malware categorization and signature generation for detection.
- **Evaluation Measures**:
  - True Positive Rate (TPR): Rate of correctly classified malware samples.
  - False Positive Rate (FPR): Rate of benign files misclassified as malware.
  - Accuracy (ACY): Rate of correctly classified instances (both positive and negative).
  - Evaluation can be instance-level (cumulative approach) or transaction-level (interactive-based approach).
  - Clustering-based methods are evaluated using Macro-F1 and Micro-F1 measures, emphasizing performance on rare and common categories, respectively.


### Feature Extraction
- **Feature Extraction Methods**:
	- **Static Analysis**:
	  - Analyzes PE files without execution.
	  - Includes decompression, disassembly, and extraction of patterns.
	  - Extracts features like API calls, byte n-grams, strings, opcodes, and control flow graphs.
	  - Advantages: exhaustive detection, no malware interaction.
	  - Disadvantages: undecidability in certain cases, limited support for runtime packing, complex obfuscation.
	- **Dynamic Analysis**:
	  - Observes execution to derive features.
	  - Techniques include debugging, profiling, and monitoring actions.
	  - Tools like debuggers, simulators, emulators, and virtual machines are used.
	  - Advantages: resolves environment-dependent information, useful for packed malware.
	  - Disadvantages: limited coverage, time-consuming, resource-intensive.
- **Hybrid Analysis**:
  - Integrates advantages of both static and dynamic analysis.
  - Addresses limitations of each approach.
  - Example: PolyUnpack combines dynamic and static analysis for packed malware.
- **Other Novel Features**:
  - Semantics-aware matching algorithms.
  - Analysis of file relationships and interdependence.
  - Example features: instruction sequences, file-to-machine relations, file placements.



# Lecture 4: Static malware analysis - 1
- Initial analysis method that involves
	- Extraction of useful information
	- Classification via informed decisions
	- Base for subsequent analysis
- Basic Static Analysis
	- Identifying a file
		- Analyze extension, magic byte, PE type,
	- Fingerprinting
		- Calculating SHA1, SHA256 & MD5 hashes.
		- Filenames not part of this, only the content is used
	- Extracting strings, function + metadata
	- Unpacking
	- Classifying and Comparing

# Lecture 5: PE + COFF
- PE aka COFF (Common Object File format)
- PE files do not contain PIE
- PE contains
	- Specifices where the exe needs to be loaded in memory
	- Reference for linking DLLs
	- Import/Export tables
	- Thread-Local Storage + Resource management data
- Components
	- Header
		- Structure
			- MZDOS > DOS STUB > PE FileHeader > Optional > Section Tables > Section
		- Metadata
			- Date, time, versions
			- Points + Offsets(RVAs) into sections where code and data are located
	- Sections
		- Stores data, code resources, directories + debug info
		- Important sections to note
			- DATA
				- .bss: Uninitialized global/static data
				- .rdata: ReadOnly data i.e. constants
				- .data: Stack data
			- RESOURCE
				- .rsrc: Images, icons, thumbnails, payload etc
			- EXE
				- .text: code i.e machine instructions
			- EXPORT
				- .edata: Exported symbols/functions
			- IMPORT
				- .idata: Imported symbols/functions
			- DEBUG
				- .debug: Debugging information such as symbol tables, line numbers
			- RELOCATE
				- .reloc: Holds information on how to relocate the exe in memory to a different address from the time it was linked

# Lecture 6: String Analysis
# Lecture 7: YARA

1. **Rule Structure**:
   - YARA rules start with the `rule` keyword followed by the rule name.
   - Curly braces `{}` enclose the rule body, which contains one or more conditions and an optional meta section.
   - Each condition consists of a boolean expression that defines characteristics of the malware or file being matched.

2. **Rule Naming**:
   - Choose descriptive names for your rules that reflect the malware or behavior they detect.
   - Avoid spaces or special characters in rule names.

3. **Metadata**:
   - The `meta` section allows you to add metadata to your rule, such as author, description, reference, etc.
   - Metadata is optional but can be helpful for documentation and categorization.

4. **Conditions**:
   - Conditions are comprised of strings, hex strings, or other YARA rules.
   - Strings are enclosed in double quotes `" "` and can use wildcards (`*`) and regular expressions (`/pattern/`).
   - Hex strings are enclosed in curly braces `{}` and start with the `$` sign followed by the hexadecimal representation of the bytes.
   - Conditions can be combined using boolean operators (`and`, `or`, `not`) and parentheses for precedence.

5. **String Matching**:
   - Be specific when writing string matches to avoid false positives.
   - Use the `nocase` modifier for case-insensitive matching when appropriate.
   - Utilize the `wide` modifier for wide character (UTF-16) string matching.

6. **Regular Expressions**:
   - Regular expressions (`/pattern/`) can be used for more complex string matching.
   - Keep regular expressions simple and efficient to avoid performance issues.

7. **Modifiers**:
   - Modifiers such as `nocase`, `ascii`, `wide`, etc., can be applied to strings to modify their behavior.
   - Choose modifiers wisely based on the nature of the data being matched.

8. **Comments**:
   - Use comments (`//` for single-line comments, `/* */` for multi-line comments) to document your rules and explain their purpose or logic.
   - Comments improve the readability and maintainability of your YARA rules.

Here's a basic example of a YARA rule:

```yara
rule ExampleRule {
    meta:
        description = "Detects example malware"
        author = "Your Name"
        date = "2024-02-24"
    
    strings:
        $str1 = "malicious_string" nocase
        $str2 = { DE AD BE EF }
        $regex1 = /malware\d{3}/

    condition:
        $str1 or $str2 or $regex1
}
```