| Lecture Number                         | Status             |
| -------------------------------------- | ------------------ |
| Lecture 2: History of malware          | :white_check_mark: |
| Lecture 3: Setting up a malware lab    | :white_check_mark: |
| Reading Article-1                      | :white_check_mark: |
| Lecture 4: Static malware analysis - 1 | :white_check_mark: |
| Lecture 5: PE + COFF                   | :white_check_mark: |
| Lecture 6: String Analysis             | :white_check_mark: |
| Lecture 7: YARA                        | :white_check_mark: |

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
	- **Stealth**
		- **Packer**: Techniques used to compress/encrypt malware code to evade detection by antivirus or other security measures
	- **Armoring**
		- **Payload**: Main component of malware
		- Mechanisms such as Obfuscation/Encryption to conceal the malware. Counts as stealth as well
	- **Persistence**
		- Mechanisms used by malware to maintain its presence on an infected system even after reboot/removal attempts
	- **Propagation**
		- Mechanisms used by the malware to spread to other systems/devices
	- **Communication**
		- Interactions b/w malware and C2 server
	- **Distribution Mechanisms**
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
- Obfuscation/Packing
	- Used to protect the inner workings of the malware from security researchers, malware analysts + RE
	- Make it difficult to analyze the binary
- String analysis
	- Process of extracting readable characters and words from the malware
	- Types of strings to look for (Only gives a hint to what the malware is capable of)
		- File names
		- URL
		- IP addresses
		- Commands i.e. attack commands
		- Registry keys
# Lecture 7: YARA

Why YARA and not AWKSCRIPT
- Yara is specifically tailored for string mathing
- AWK is tailored for log processing

```yara
to run a yara file use the following

$ yara32 -r yaraRule.yara fileToTestRule.exe
```


- Using hexadecimal strings
	- Good for using Jumps, Wildcards and alternatives.
		- Simple strings can also use wildcards but that involves regex
	- Wildcards = Use a "?" for each 4bits to guess
	- Jumps = Use when length of string is unknown. use \[3-5\] where 3 is minLen and 5 is maxLen
- Anonymous strings
	- Just use a \$. No need to name. Can only use the 'of them' condition for this though
- Global Rule
	- Impose restrictions on all rules within the file
- Private Rule
	- Disable the rule
- Iterative
	- same syntax as python.
	- example
	- for all i in (1,2,3):
		- (@a\[i\] + 10 == @b\[i\] )
	- This code checks if the first 3 letters of A are spaced 10 bytes apart from the first 3 letters of B and if they match or not

---
Copied from mattnotmax on github

## Basic Rule

Basic rule layout with suggested various meta descriptors.

```
rule specifc_name       // e.g. APT_CN_Winnti_exploit or crimeware_ZZ_RAT
{
    meta:               // suggested
        author = 
        date_created = 
        date_last_modified = 
        description = 
        filetype = 
        hash = 
        hash = 
        source = 
        TLP = 
        license = 
        min_yara_version = 
    
    strings:
        $a1 = "string type 1-1" ascii wide fullword nocase
        $a2 = "string type 1-2" 
        $a3 = "string type 1-3"

        $b1 = "string type 2-1"
        $b2 = "string type 2-2"
        $b3 = "string type 2-3"

        $c1 = "string type 3-1"
        $c2 = "string type 3-2"
        $c3 = "string type 3-3"
    
    condition:
        any of $a* or (2 of $b*) or (1 of $c*)
}
```

## Strings

- text strings are case sensitive.
- case insensitive can be used with `nocase` option.
- `wide` modifier can be used for UTF-16 formatting BUT not true UTF-16 support.
- `ascii` modifier can be used for ASCII encoding (default).
- `xor`  can be used to search for strings with a single byte xor applied to them.
- you can combine all types. E.g. `ascii wide nocase xor`.
- can write `xor (0x01-0xff)` for a specific range of xor bytes rather than all 255.
- `fullword` modifier guarantees that the string will match only if it appears in the file delimited by non-alphanumeric characters.
- use `fullword` keyword when string is short.

## Hexadecimal Strings

 - Hexadecimal strings allow three special constructions that make them more flexible: wild-cards, jumps, and alternatives.

### Wildcards
Wild-cards are just placeholders that you can put into the string indicating that some bytes are unknown and they should match anything.

The placeholder character is the question mark (?).

```
rule WildcardExample
{
    strings:
       $hex_string = { E2 34 ?? C8 A? FB }

    condition:
       $hex_string
}
```

### Jumps

Jumps can be used when the length of the content can vary or is unknown.

```
rule JumpExample
{
        strings:
           $hex_string = { F4 23 [4-6] 62 B4 }

        condition:
           $hex_string
}
```

### Alternatives

Alternatives can give a hex option similar to a regular expression.

```
rule AlternativesExample1
{
    strings:
       $hex_string = { F4 23 ( 62 B4 | 56 ) 45 }

    condition:
       $hex_string
}
```

## Regular Expressions

- They are defined in the same way as text strings, but enclosed in forward slashes instead of double-quotes.
- E.g. `/([Cc]at|[Dd]og)/`.
- can also be used in conjunction with `nocase`, `ascii`, `wide`, or `fullword`.
- Regular expression evaluation is inherently slower than plain string matching and consumes a significant amount of memory.

## Counting strings

The number of occurrences of each string is represented by a variable whose name is the string identifier but with a # character in place of the $ character.

```
rule CountExample
{
    strings:
        $a = "dummy1"
        $b = "dummy2"

    condition:
        #a == 6 and #b > 10
}
```
This rule matches any file or process containing the string $a exactly six times, and more than ten occurrences of string $b.

## File Size
- Can use bytes or append `KB` or `MB` as required.
- E.g. `filesize > 10KB`
- Don't use filesize modifier when scanning memory images.

## Offsets

The `at` modifier can be used to denote a decimal offset value (or vitual address for a running file).

The `in` modifier allows a range to be specified.

```
rule InExample_AtExample
{
    strings:
        $a = "dummy1"
        $b = "dummy2"
        $c = "dummy3"

    condition:
        $a in (0..100) and ($b in (100..filesize) or $c at 150)
}
```

## Conditions

Conditions are nothing more than Boolean expressions as those that can be found in all programming languages, for example in an if statement. They can contain the typical Boolean operators `and`, `or`, and `not`, and relational operators `>=`, `<=`, `<`, `>`, `==` and `!=`. Also, the arithmetic operators (`+`, `-`, `*`, `\`, `%`) and bitwise operators (`&`, `|`, `<<`, `>>`, `~`, `^`) can be used on numerical expressions.

## Checking File Headers
- if possible for speed and accuracy check the file headers.
- don't check file headers for memory images.

Examples:

PE Header
`uint16(0) == 0x5A4D`

ELF Header
`uint32(0) == 0x464c457f`

## Comments

```
/*
    This is a multi-line comment ...
*/
```

```
rule example { // this is a single line comment
```

## PE Module

The PE module allows you to create more fine-grained rules for PE files by using attributes and features of the PE file format.

Preface fule with `import "pe"`

see [PE Module](https://yara.readthedocs.io/en/stable/modules/pe.html#pe-module)


## Math Module

The Math module allows you to calculate certain values from portions of your file and create signatures based on those results.

Useful examples:

`math.entropy(0, filesize) >= 7`

## Rule Tips

- Don't use rules solely based on Windows APIs, this is prone to FPs.
- don't try to match on run-time generated strings (for disk files).
- don't put all criteria a necessary. Eg. not `all of them` but `five of them`.


### What to match

- Mutex
- Rare User Agents
- Registry Keys
- Typos
- PDB Paths
- GUIDs
- Internal module names
- Encoded or encrypted configuration strings


Use clusters of groups (See example at start). Eg:
- unique artifacts found in malware
- Win APIs
- File properties and structure (sections, entropy, timestamp, filesize etc.)

Then use these clusters to create the `condition`:
- `any of $a* or 5 of $b* or 2 of $c*`

## Random Tips

- Run command line with -p option to increase performance on SSDs.
- `pe.imphash() == "blah"` where `blah` needs to be lower case hex.
- loops vs strings: strings is faster.

## Random Rules from Kaspersky Webinar

Chinese language sameples, signed but not signed by MS, mimic legit Microsoft files by re-using their PE metainfo

```
condition:
    uint16(0) == 0x5A4D
    and filesize < 1000000
    and pe.version_info["Company Name"] contains "Microsoft" 
    and pe.number_of_signatures > 0
    and not forall i in (0..pe.number_of_signatures - 1):
        (pe.signatures[i].issuer contains "Microsoft" or pe.sigantures[i].issuer contains "Verisign")
    and pe.language(0x04 // LANG_CHINESE)
```

malware for AMD64 but compiled date before 64bit OS first released/created.

```
condition:
    uint16(0) == 0x5A4D
    and (pe.machine == pe.MACHINE_AMD64 or pe.machine == pe.MACHINE_IA64)
    and pe.timestamp > 631155661 // 1990-01-01
    and pe.timestamp < 1072915200 // 2004-01-01
    and filesize > 2000000
```

## Resouces

[Yara Binaries](https://github.com/VirusTotal/yara/releases)
[Yara Readthedocs](https://yara.readthedocs.io/en/stable/)
[Yara Git Repo](https://github.com/VirusTotal/yara)
[Kaspersky Yara Webinar](https://securelist.com/yara-webinar-follow-up/96505/)
[yaraPCAP](https://github.com/kevthehermit/YaraPcap)
[Kaspersky Klara](https://github.com/KasperskyLab/klara)
[YarGen](https://github.com/Neo23x0/yarGen)