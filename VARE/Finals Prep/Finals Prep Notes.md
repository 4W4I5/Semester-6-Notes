NOTE:: Skipped introduction

| Lecture Number                                               | Status                                                            |
| ------------------------------------------------------------ | ----------------------------------------------------------------- |
| Lecture 2: History of malware                                | :white_check_mark:                                                |
| Lecture 3: Setting up a malware lab                          | :white_check_mark:                                                |
| Reading Article-1                                            | :white_check_mark:                                                |
| Lecture 4: Static malware analysis - 1                       | :white_check_mark:                                                |
| Lecture 5: PE + COFF + Windows Internal - 1                  | :white_check_mark:                                                |
| Lecture 6: String Analysis - 1                               | :white_check_mark:                                                |
| Lecture 7: String Analysis - 2 + YARA                        | :white_check_mark:                                                |
| Lecture 8 & 9: Reverse Engineering                           | :white_check_mark:                                                |
| Lecture 10 & 11: Windows Internal - 2/3 + DLLs & Registry    | :white_check_mark:                                                |
| Lecture 12: IDA                                              | :x: Would be Regurgitating Info, Go through the slides (42 Pages) |
| Lecture 13: Basic Dynamic Analysis                           | :white_check_mark:                                                |
| Lecture 14: Windows Internal - 4 + Advanced Dynamic Analysis | :white_check_mark:                                                |
| Lecture 15: Vulnerability Assessment                         | :white_check_mark:                                                |
| Lecture 16: Assessment Environment                           | :white_check_mark:                                                |

<!--
:x:
:warning:
:white_check_mark:
-->

# Lecture 2: History of malware
- Malware is a software that is written with the intention of disrupting networks, causing harm to user/computer
	- Without the knowledge of the user (Ransomware only reveals itself when the data is encrypted)
- **Taxonomy of malware**
	- Malicious programs aka malware
		- Needs a host
			- Trapdoors, basically backdoors, allow to bypass normal authentication means
			- Logic Bombs, wait for a condition before triggering
			- Trojans
			- Viruses
		- Independent
			- Worm
			- Zombie, basically bots
- **Goals of MA&RE**
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

- **Advanced Persistent Threat (APT)**
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
- **Components of Malware**
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
- **Exploits**
	- Small piece of code input into programs to target their vulns
	- **Patches**
		- Identify and fix vulns before they can be exploits
		- Done via updates by vendors
		- Zero-Day = Vuln is not patched
	- **Exploit Kit**
		- Baits and traps using malicious servers, observes connected hosts and deploys malware accordingly
		- Devised to attack computers that are hidden behind their home network
		- Automatically managing and deploying exploits against a target computer
		- Wait for users to contact these malicious server
- **Dimensions of infection vectors**
	- Speed
	- Stealth
	- Coverage
	- Shelf life
- **Malware Attack LifeCycle (Missed out in Sessional 1)**
	- Development
	- Distribution
	- Infection
	- Post-Infection


---

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

## Development of the malware industry
- **Origins and Evolution**
    - Malware originated to expose security flaws or showcase technical prowess.
    - Uses tactics like encryption, packing, obfuscation, polymorphism, and metamorphism to evade detection.
- **Shift to Profit-Driven Motives**
    - Shifted from curiosity-driven to profit-driven, exploiting the booming e-commerce sector.
    - Trojans now constitute 73% of malware, forming a lucrative underground industry.
- **Lowered Barrier to Entry**
    - Barrier to entry has lowered due to user-friendly toolkits like Zeus and SpyEye.
- **Proliferation of Variants**
    - Flood of rapidly mutating variants overwhelms anti-malware systems.
- **Persistent Threat**
    - Exponential growth of malware poses a persistent cybersecurity threat.

## Progress in malware detection
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

## Malware detection by applying datamining techniques
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

## Feature Extraction
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

---

# Lecture 4: Static malware analysis - 1
- **Initial analysis method that involves**
	- Extraction of useful information
	- Classification via informed decisions
	- Base for subsequent analysis
- **Basic Static Analysis (I.F.E.U.C2)**
	- Identifying a file
		- OS only checks the extension
		- Analyze extension, magic byte, PE type,
	- Fingerprinting
		- Calculating SHA1, SHA256 & MD5 hashes.
		- Filenames not part of this, only the content is used
	- Extracting strings, function + metadata
	- Unpacking
	- Classifying and Comparing

---

# Lecture 5: PE + COFF + Windows Internal - 1
## Portable Executables + COFF
- PE aka COFF (Common Object File format)
- PE files do not contain PIE
- **PE contains**
	- Specifices where the exe needs to be loaded in memory
	- Reference for linking DLLs
	- Import/Export tables
	- Thread-Local Storage + Resource management data
- **Components**
	- **Header**
		- **Structure**
			- MZDOS > DOS STUB > PE FileHeader > Optional > Section Tables > Section
		- **Metadata**
			- Date, time, versions
			- Points + Offsets(RVAs) into sections where code and data are located
	- **Sections**
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


## Windows Internals - 1
- Windows Architecture
	- Kernel
		- Monolithic in nature
		- Runs in Kernel/User Mode
	- Layered Design
- WinAPI
	- Expose Kernel functions to the OS
	- Provide
		- Base/Advanced Services -> Basic resource + Kernel resource access
		- GUI
		- Common Control/Dialog Box Library -> Basic GUI such as dialog boxes, progress bars, etc
		- Windows Shell
		- Network Services
- COM
	- DLL/EXE where COM classes are implemented
	- Language neutral
	- Loaded dynamically
	- Virtual Table Dispatch
		- Interface clients and objects via contracts
- WinRT (Windows RunTime)
	- Platform services for Windows Apps which can use both WinAPI and COM APIs
	- Sandboxed
	- Built on top of COM
- .NET framework
	- Provides Common Language Runtime
	- Interface WinAPI with .NET apps
- Services, Functions & Routines
	- WinAPI calls -> Documented + Callable subroutines
	- System calls -> Undocumented/Hidden function calls + Callable from usermode
	- Routines (Kernel Functions) -> Callable routines in kernel-mode
- Windows Services
	- Contains processes run by the service control manager
	- Provides kernel interface to such programs
- DLLs
	- PE files marked as DLLs
	- Used extensively by user-mode processes
	- .NET assemblies are also compiled as DLLs but without any unmanaged exported subroutines
- Processes
	- Static Sequence of instructions
	- Contains
		- Private address space
		- Security Context
		- ProcessID
		- At least one thread for execution
- Threads
	- Scheduled process entity
	- Contains
		- Register contents
		- Two Stacks, one each for operating mode of kernel
		- TLS i.e. thread level storage
		- ThreadID
	- Fiber: App-Specific threads
- Jobs
	- Group of processes managed in a unit
	- Allow management/manipulation + basic accounting i.e. MAC times
	- Provide control over certain attributes
	- Provide limits for process(es) associated with the jo
- Virtual Memory
	- SWAP space for processes suspended or requiring memory much larger than available physical memory
- Kernel Modes
	- User
		- Grants 4 process types
			- User processes -> Windows apps running on WinRT
			- Service processes -> Host windows services i.e. task scheduler
			- System processes -> Hardwired i.e. the logon process
			- Environment Subsystem Server process -> Presented to user/programmer + implement support for OS enviro
	- Kernel
		- Executive -> Contains all managers
		- Device Drivers -> Virtual and Hardware
		- Hardware Abstraction Layer (HAL) -> Isolate platform specific hardware
		- Windowing + graphic system -> Windows user + GDI functions
		- Hypervisor layer -> Passthru certain PCI-E devices for virtualization
- Windows Registry
	- Contains
		- Boot information
		- Configuration information
		- Security DB
		- Performance Counters
		- In-Memory Volatile data

---

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

---

# Lecture 7: YARA

Why YARA and not AWKSCRIPT

- Yara is specifically tailored for string matching
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
- Sets of strings
	- Can select strings from a set of strings
	- Example:
		- 2 of them or all of them or any of them
		- 2 of ($1, $2, $3, $4)
		- 2 of ($*)
- Counting Strings
	- Use # to specific counts
	- Example:
		- /#a == 6 and /#b < 10 -> A should be exactly 6 and B should be less than 10
- Offsets
	- Specify offset from entrypoint in bytes
	- Example:
		- $a at 100 and $b at 300
	- Can be ranged
	- Example:
		- $a in (0..100) or $b in (100..filesize)
- Anonymous strings
	- Just use a \$. No need to name. Can only use the 'of them' condition for this though
- Global Rule
	- Impose restrictions on all rules within the file
- Private Rule
	- Disable the rule
- Referencing other rules
	- Example:
		- $a and Rule1
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

<!--
:x:
:warning:
:white_check_mark:
-->

---

# Lecture 8 & 9: Reverse Engineering
## Why?
- Understand the internal workings of a malware binary
- Implement detection mechanism for a given sample
- Cure needed
- **Tools**
	- Disassembler
		- Convert machinecode -> asm file
	- Decompiler
		- Convert machinecode -> pseudo-code (HLL Type)
	- Debugger
		- Run machine code in a safe enviro to step through and observe program flow + registers state

## Understanding machine code
- **CPU specific code**
	- Wide variety of CPUs, generically based on their own ISA's (Instruction-Set Architectures)
		- x86-64
		- amd
	- Program execution viability is checked in the NT header
		- NT Header -> File Header

## Perspectives

|                         | High Level                                                                                                                                                                                                                                                                | Low Level                                                                                                                                                                                                           |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Program Structure       | Modules i.e. DLL and Static Libs                                                                                                                                                                                                                                          | ASM version                                                                                                                                                                                                         |
| Data Management         | Procedural/OOP                                                                                                                                                                                                                                                            | Registers, Stack, Heaps, Non-NX Data sections                                                                                                                                                                       |
| Example Language        | C, C++, C#, Java, Python                                                                                                                                                                                                                                                  | Assembly                                                                                                                                                                                                            |
| Compilation/ListingFile | Frontend parses source code after performing lexical analysis and converts it to an Intermediate Representation or Abstract Syntax Tree. Optimizer optimizes by deadcode elimination, loop optimization, register allocation, etc. Backend generates machinecode/bytecode | Compiler generated, Text file, IR of the code read by compiler frontend, Maps ASM code to the Machine code (1:1), Mapping to ASM->Source is (M:1) i.e. One line of source code can consist of multiple instructions |

## Execution Environments
- **Software Enviros**
	- Any type of VM
		- JVM, CLR that runs .NET, bytecodes
- **Hardware Execution in modern Processors**
	- Modern execution techniques such as spectre, NetBurst and microOps

## Assembly Language
### Operand Types + Addressing Mode
- **Immediate**
	- Fixed values
- **Indirect**
	- Essentially a pointer, refers to a memory location to fetch data from. Identify via use of \[ \]
- **Register**
	- Common Sense
- **Implicit VS Explicit**
	- Implicit
		- No explicit operand/addresses required
	- Explicit
		- Common Sense

### Registers
- **EAX**
	- Accumulator
- **EBX**
	- Base Register, used for indexing/address calculations
- **ECX**
	- Counter, used by loops
- **EDX**
	- Used for Data I/O
- **EIP**
	- Instruction pointer, points to the address of the next instruction to fetch
- **ESP**
	- Stack pointer, points to top of stack
- **EBP**
	- Base pointer, points to the base address of the currently executing function
- **ESI**
	- Stack Index, points to starting address to fetch
- **EDI**
	- Data index, points to last address to fetch to
- **Flags/Status**
	- OF -> Overflow Flag
	- DF -> Direction Flag
	- IF -> Interrupt Flag
	- TF -> Trap Flag(Single step mode)
	- SF -> Signed Flag
	- ZF -> Zero Flag
	- AF -> Auxiliary Flag (Half-Carry)
	- PF -> Parity Flag
	- CF -> Carry Flag
- **Debug**
	- DR0 thru DR3
		- Hold Breakpoint addresses
	- Debug control is in bits of DR7

### Important x86 Instructions
- **Stack**
	- PUSH, POP, CALL, RETURN, ENTER, LEAVE
- **Arithmetic**
	- ADD, SUB, MUL, DIV, INC, DEC
		- Sub modifies ZF and CF
		- MUL is single op, multiples AX with op
- **Logical**
	- AND, OR, XOR, CMP, TEST, SHL, SHR
		- AND, OR, and XOR Sets OF and CF to 0
		- ZF, SF, PF modified according to result
- **Control Flow**
	- CALL, JMP, RET
		- Unconditional^
	- JZ, JO, JS, JC, JP.
		- All have a NOT modifier version as well
	- LOOPs
- **Data movement**
	- MOV, XCHG
- **Address Loading**
	- LEA
		- Essentially use of indirect addressing
- **String Manipulation**
	- MOVS, SCAS, LODS
	- Need to point ESI/EDI to the correct location first
	- SCAS Modifies ZF if found
- **Interrupt**
	- INT
		- Generate a software level interrupt

## Disassembly Algo (Concept)
- Step 1
	- Identify Code segment
		- Generally Code and Data segments are mixed
			- Observe PE/ELF format to understand both segments
			- These generally have mechanisms to identify code and entrypoint
- Step 2
	- Given the initial address of an instruction
	- Read value contained at file offset and lookup from a table to convert from binary opcode to asm mnemonic
	- Additional bytes may need to be retrieved in cases where (Variable-Length Instructions) VLI are used
- Step 3
	- Format decoded mnemonics and output a formatted listing
	- Can chose x86 or AT&T as the formats
- Step 4
	- Advance to next instruction
	- Repeat

## Disassembly Algo (Linear sweep vs Recursive Descent)

| Aspect                   | Linear Sweep Disassembly                                      | Recursive Descent Disassembly                                 |
| ------------------------ | ------------------------------------------------------------- | ------------------------------------------------------------- |
| Approach                 | Straightforward, linear                                       | Focuses on control flow                                       |
| Starting point           | Begins at the first byte in a code section                    | Decides whether to disassemble based on references            |
| Handling of control flow | Does not recognize nonlinear instructions such as branches    | Focuses on understanding control flow                         |
| Method                   | Linear fashion through the section                            | Analyzes how instructions affect the CPU instruction pointer  |
| Maintaining pointers     | Maintains a pointer to mark the beginning of each instruction | Utilizes control flow to determine disassembly                |
| Instruction length       | Computes the length of each instruction to determine the next | Considers how instructions affect the CPU instruction pointer |
| Ease of disassembly      | Challenging for complex control flows                         | Better suited for understanding complex control flow          |

---

# Lecture 10 & 11: Windows Internal - DLLs & Registry
## Static VS Dynamic

| Aspect           | Static                                                 | Dynamic                                                 |
| ---------------- | ------------------------------------------------------ | ------------------------------------------------------- |
| Linking          | Linked directly into the exe                           | Loaded and linked at runtime                            |
| Runtime behavior | Self-Contained as code is directly included in the exe | Loaded into memory separately and linked during runtime |
| Reusability      | Not necessarily possible across multiple applications  | Can be shared among different programs                  |

## What is a DLL like
- Same structure as a PE exe file
	- PE Header Flags
		- Even has the EXE flag set
		- DLL flag is set
## Dependencies
- An imported DLL is known as a dependency
	- Can observe which DLLs are directly required by checking the import table
- DLLs can be chained
	- Runtime chaining can be observed using process hacker
- Exports
	- Both EXE and DLLs have exports
		- EXE generally export the main function for the LOADER process to load the process into memory
	- DLLs can export functions for other DLLS/EXE files to use
- Import Address Table (IAT)
	- Table that is filled in with external functions that are imported by LOADER as DLLs are loaded into memory

## Windows Application Programming Interface (Win32API)
- Software Interface
- Provides a layer of abstraction to the inner workings of a program that is offering a service to other software
- Win32API provides a set of DLLs, present under the system32 folder
- Consists of
	- NT version of API
	- Extended Versions
	- Undocumented API's
### Categories of Win32API

| Component                   | Description                                                                                       | DLL File                   |
|-----------------------------|---------------------------------------------------------------------------------------------------|----------------------------|
| Base Services               | Provides access to basic resources like file systems, devices, processes, threads, and error handling. | kernel32.dll, KernelBase.dll |
| Graphics Device Interface  | Outputs graphics content to monitors, printers, etc.                                             | gdi32.dll (user-mode), win32k.sys (kernel-mode) |
| User Interface             | Manages screen windows, basic controls, receives input, etc.                                      | user32.dll, comctl32.dll (basic controls since Windows XP) |
| Common Control Library     | Advanced controls such as status bars, progress bars, toolbars, etc.                              | comctl32.dll               |
| Common Dialog Box Library  | Provides standard dialog boxes for file operations, color and font selection, etc.                | comdlg32.dll               |
| Advanced Services          | Access functions beyond the kernel like Windows registry, system shutdown/restart, etc.            | advapi32.dll, advapires32.dll |
| Windows Shell              | Allows access to OS shell functions and customization.                                             | shell32.dll, shlwapi.dll (Shell Lightweight Utility Functions) |
| Network Services           | Provides access to networking abilities like NetBIOS, Winsock, RPC, etc.                          | netapi32.dll               |

### Behavior Identification with APIs
- Both clean and malware files use APIs and just behavior wont be enough
	- Context of API function, the parameters sent to the API, the sequence of APIs called matters as well

### Important DLLs

| DLL Name       | Description                                                                                                                      |
|----------------|----------------------------------------------------------------------------------------------------------------------------------|
| NTDLL.DLL      | Provides a collection of library functions for numerous system tasks, including system startup, system shutdown, and exception handling. |
| KERNEL32.DLL   | Contains core Windows functions such as memory management, input/output operations, and process/thread management.                   |
| KERNELBASE.DLL | A subset of functions in KERNEL32.DLL, containing essential functions for Windows applications.                                     |
| GDI32.DLL      | Manages graphical devices, allowing applications to display graphical content on monitors, printers, etc.                            |
| USER32.DLL     | Handles user interface functions, including window management, message processing, and input handling.                              |
| COMCTL32.DLL   | Provides advanced controls and common dialog boxes for Windows applications, enhancing user interface capabilities.                 |
| ADVAPI32.DLL   | Offers access to advanced services such as registry manipulation, system shutdown/restart, and user account management.              |
| OLE32.DLL      | Supports Object Linking and Embedding (OLE) technology, enabling compound documents and inter-process communication.                  |
| NETAPI32.DLL   | Facilitates network-related operations and services, allowing applications to interact with various networking protocols.             |
| COMDLG32.DLL   | Provides standard dialog boxes for common file operations, font selection, color selection, and other user interactions.           |
| WS2_32.DLL     | Offers functions for socket programming and network communication using the Winsock API.                                            |
| WININET.DLL    | Provides high-level functions for internet communication, including HTTP, FTP, and Gopher protocols.                                |
| MSVCRT.DLL     | Implements a large part of the C standard library, including input/output operations, string handling, and memory allocation.      |
| MSVCPxx.DLL    | Microsoft C++ runtime library, providing support for C++ applications compiled with Microsoft Visual Studio.                       |
| MSVBVM60.DLL   | Runtime library for Visual Basic 6.0 applications, providing necessary support for executing VB6 programs.                          |
| VCRUNTIMExx.DLL| Microsoft Visual C++ runtime library, version-specific, providing support for applications compiled with Visual C++.                  |

### Important APIs

| API Name                | Description                                                                                                             |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------|
| CreateFile              | Creates or opens a file or I/O device.                                                                                  |
| WriteFile               | Writes data to the specified file or I/O device.                                                                        |
| ReadFile                | Reads data from the specified file or I/O device.                                                                       |
| SetFilePointer          | Moves the file pointer of an open file.                                                                                 |
| DeleteFile              | Deletes an existing file.                                                                                               |
| CloseFile               | Closes an open file handle.                                                                                             |
| RegCreateKey            | Creates a new registry key or opens an existing one.                                                                    |
| RegDeleteKey            | Deletes a subkey and its values from the registry.                                                                      |
| RegSetValue             | Sets the data for the default or specified value in the specified registry key.                                          |
| VirtualAlloc            | Reserves or commits a region of pages in the virtual address space of the calling process.                                |
| VirtualProtect          | Changes the protection on a region of committed pages in the virtual address space of the calling process.               |
| NtCreateSection         | Creates a section object that represents a memory section that can be mapped into the address space of another process.  |
| WriteProcessMemory      | Writes data to an area of memory in a specified process.                                                                |
| NtMapViewOfSection      | Maps a view of a section of a file into the address space of a process.                                                  |
| CreateProcess           | Creates a new process and its primary thread.                                                                           |
| ExitProcess             | Terminates the calling process.                                                                                         |
| CreateRemoteThread      | Creates a thread that runs in the address space of another process.                                                      |
| CreateThread            | Creates a new thread for the specified process.                                                                         |
| GetThreadContext        | Retrieves the context of the specified thread.                                                                          |
| SetThreadContext        | Sets the context for the specified thread.                                                                              |
| TerminateProcess        | Terminates the specified process and all of its threads.                                                                 |
| CreateProcessInternalW  | Creates a new process and its primary thread with additional options specified in a STARTUPINFO structure.                |
| OpenSCManager           | Opens a connection to the service control manager on the specified computer.                                             |
| CreateService           | Creates a service object and adds it to the service control manager database on the local or specified computer.         |
| OpenService             | Opens an existing service.                                                                                              |
| ChangeServiceConfig2W   | Changes the configuration parameters of a service.                                                                      |

## Registry
- A Record/Database that holds information/settings
- OS component configs are stored and referred to from here
- Can be found on disk
	- `C:\Windows\System32\config\*`
- Some are created dynamically in memory after windows is booted
- Split in HIVES aka Root Directories
	- HKEY_CLASSES_ROOT (HKCR): stores information about installed programs like file associations and/or shortcuts for application
	- HKEY_LOCAL_MACHINE (HKLM): stores information that is common to all users on the system. HW and SW related settings
	- HKEY_USERS (HKU): contains Windows group policy settings.
	- HKEY_CURRENT_CONFIG (HKCC): contains the hardware profile that the system uses at startup
	- HKEY_CURRENT_USER (HKCU): contains the information of the currently logged-in user.
- Malware Use
	- Append their own data to achieve persistence or bypass AV
		- This is done via WinAPI calls for RegCreateKey, RegDeleteKey, RegSetValue

---

# Lecture 13: Basic Dynamic Analysis
## Basics
- Dynamic analysis involves
	- Analyzing a sample by executing it in an isolated environment and monitoring its
		- Activities
		- Interaction
		- Effect on the system
- Analyst extract information to explore the
	- Nature
	- Purpose
	- Functionality
- Dynamic analysis is also called **behavioral** **analysis**

## Steps
- **Clean Slate**
	- Revert to a snapshot with no malware loaded
- **Start up monitoring tools.** NOTE:: Run as Admin
	- Why?
		- Expected interactions
			- System
				- Child processes spawned
				- Files dropped
				- Registry keys modified
			- Network
				- Contact with C2
				- New files to be downloaded
	- Types
		- Process Monitoring
			- Process activity and properties of the running process following an execution
		- FileSystem Monitoring
			- Check for changes, files being deleted/added
		- Registry Monitoring
		- Network Monitoring
			- Inspect live traffic to/from malware during execution
	- Tools
		- Process monitor/Process Hacker
			- OpenSrc
			- Process inspection
				- Inspect process/thread attributes
				- Explore Disk activity, open network connections, etc
		- Noriben
			- Works alongside procmon
				- Collects, Analyzes and reports running IOCs of the malware
			- Stores results in .txt and .csv file
		- Wireshark
			- Network monitor, Logs all packet information from an interface
		- FakeNet-NG/INetSIM
			- Runs a server that returns a deadend page to any and all network traffic while generating a pcap file of all packets sent to the server
			- Simulates the network environment essentially
		- RegShot, Take a shot before running malware
- **Execute Malware for a set interval**
- **Stop monitoring tools, take another RegShot**
- **Analyze results from tools and compare RegShot shots**

---

# Lecture 14: Windows Internal - 4 + Advanced Dynamic Analysis

- **User Defined DLL**
	- Attackers implement malicious code as DLLs
	- Advantages:
		- Load into any process, including legitimate ones (e.g., Explorer.exe, winlogon.exe)
		- Persistence on the system
		- Manipulate process functionality
	- Challenges:
		- Analyzing DLLs is more complex than executables
- **Analyzing the DLL**
	- Understanding DLL execution is essential
	- Windows tool: `rundll32.exe` can launch DLLs and invoke exported functions
- **Launching a DLL with rundll32.exe**
	- Syntax: `rundll32.exe <full path to dll>,<export function> <optional arguments>`
	- Full path to DLL: No spaces or special characters
	- Export function: Function in the DLL to be called
	- Optional arguments: Passed to the export function
	- Comma: Separates the DLL path and export function
- **Debugging Malicious Binaries: Advanced Dynamic Analysis**
	- **What is Debugging?**
	- Controlled execution of malicious code
	- Benefits:
		- Inspect code at a granular level
		- Full control over runtime behavior
		- Execute single/multiple instructions or specific functions
	- Environment: Conduct in a malware lab or isolated environment
- **Popular Debuggers**
	- IDA Pro, X64dbg
	- Others: radare2, WinDbg, Ollydbg, Immunity Debugger, Hopper, Binary Ninja
- **Steps in Debugging**
	- Not standalone; involves multiple steps:
		1. **Launching and Attaching to Process**
			- Select the program to debug
			- Methods: Attach to a running process or launch a new one
		1. **Controlling Process Execution**
			- Modify behavior during execution
			- Capabilities:
				- Control execution: Continue (Run), Step into/over, Execute till Return, Run to cursor
				- Interrupt execution: Use breakpoints
		1. **Interrupting a Program with Breakpoints**
			- Breakpoint: Interrupts execution at specific locations
			- Uses:
				- Pause at a particular instruction
				- When a function/API is called
				- When memory is accessed
			- Types: Software, Hardware, Memory, Conditional
			- Monitoring/modifying aspects of the process upon reaching breakpoints
		1. **Tracing Program Execution**
			- Recording specific events during execution
			- Provides detailed information about the binary
- **Kernel-related Information**
	- Inquiry about methods to access kernel info
- **Debugging a Binary Using x64dbg**
	- Open-source debugger for 32-bit and 64-bit applications
- **x64dbg Debugger Interface**
	- Components:
		1. Disassembly Window (CPU Window)
		2. Registers Window
	    1. Stack Window
	    2. Dump Window
	    3. Memory Map Window
	    4. References Window
	    5. Handles Window
	    6. Threads Window
---

# Lecture 15: Vulnerability Assessment

- **Key Terms**
	- **Vulnerability**: A weakness exploitable by cybercriminals to gain unauthorized access to systems.
	- **Exploit**: Code that takes advantage of a software vulnerability or security flaw.
	- **Patch**: Software update that fixes vulnerabilities and security flaws.
	- **Threat**: Potential cause of an unwanted incident that may result in harm to a system or organization.
- **Types of Vulnerabilities**
	- Flaws in software or protocol design.
	- Weaknesses in how protocols and software are implemented.
	- Weaknesses in system and network configurations.
	- DOS (Denial of Service) vulnerabilities.
	- User information disclosure.
	- Insecure data storage.
	- Outdated or unpatched systems.
	- Man-in-the-Middle (MITM) and spoofing attacks.
	- Poor code quality.
	- Weak cryptography.
	- Flawed or insufficient authentication mechanisms.
- **Causes of Vulnerabilities**
	- **Complexity**: Increased complexity leads to more potential security gaps.
	- **Familiarity**: Widely used software can be more attractive targets.
	- **Connectivity**: Increased connections expand the attack surface.
	- **Poor Password Management**: Weak passwords create easy entry points.
	- **Operating System Flaws**: OS vulnerabilities provide entry points for attacks.
	- **Internet Usage**: Browsing and internet activity expose systems to risks.
	- **Software Bugs**: Coding errors can lead to security vulnerabilities.
	- **Unchecked User Input**: Lack of input validation can lead to code injection.
	- **Human Factors**: Users can be tricked or make mistakes that compromise security.
- **Locations of Vulnerabilities**
	- Found at various levels: application, user, network, OS, storage, device, client-server, code, and database.
	- Specific to system types such as IoT devices, Android applications, digital surveillance systems, and cloud-based systems.
- **Exploitation of Vulnerabilities**
	- Through writing exploits, programming, and using tools.
	- By targeting known vulnerabilities and security weaknesses in web applications.
- **Vulnerability Databases**
	- Platforms that collect, maintain, and share information on discovered vulnerabilities.
	- Examples include CVE (Common Vulnerabilities and Exposures), NVD (National Vulnerability Database), VulDB, and Snyk Security.
- **Categories of Vulnerabilities**
	- **Hardware**: Susceptibility to physical damage, poor encryption, or firmware issues.
	- **Network**: Unprotected communication lines, MITM attacks, insecure network architecture.
	- **Personnel**: Poor recruiting policies, lack of security awareness, poor password management.
	- **Physical Site**: Exposure to natural disasters, unreliable power sources, inadequate physical security.
	- **Software**: Insufficient testing, design flaws, memory safety violations, input validation errors, cross-site scripting, SQL injection.
	- **Organizational**: Lack of audit, continuity plans, and incident response plans.
- **Need for Security Assessment**
	- Deploying state-of-the-art security solutions and implementing strong security controls are not enough.
	- Regular security tests are required, similar to quality assurance in other fields.
- **Types of Security Tests**
	- **Security Testing**: Ensures security controls function properly through automated scans, pen-testing tools, and manual attempts.
		- Considerations: resources, protected applications, technical failure probability, impact on business, and testing difficulty.
	- **Security Assessment**: Detailed review of a system's security by a trained professional, including risk assessments and threat analysis.
		- Includes comprehensive reviews of threat environments, risks, and asset values.
	- **Security Audits**: Conducted by third parties for an unbiased review of security posture.
		- Types: internal audits and external audits.
- **Vulnerability Management**
	- Cyclical practice of identifying, classifying, remediating, and mitigating security vulnerabilities.
	- Essential elements include detection, assessment, and remediation.
	- Programs can be bottom-up or top-down.
- **Detection Methods**
	- **Vulnerability Scanning**: Software assessing computers, networks, or applications for known vulnerabilities.
	- **Authenticated Scans**: Direct access to networked assets using system credentials.
	- **Unauthenticated Scans**: External scans often used by attackers to gauge security posture.
- **Penetration Testing**: Also known as ethical hacking, it tests IT assets for exploitable vulnerabilities.
	- Can be automated or manual, testing security policies, compliance, and incident response.
- **Google Hacking**: Using search engines to find vulnerabilities due to misconfigurations or exposed information.
	- Common issues include software vulnerabilities and cloud service misconfigurations.
- **Common Vulnerabilities**
	- **Initial Deployment Failure**: Insufficient testing leading to exploitable flaws.
	- **SQL Injection**: Common database attack recorded in vulnerability databases.
	- **Misconfiguration**: Improperly configured services leading to vulnerabilities.
	- **Inadequate Auditing**: Lack of audit trails making it hard to detect data alterations or breaches.
- **Security Basics**
	- **CIA Triad**: Confidentiality, Integrity, Availability.
	- **Identification and Authentication**: Ensuring proper access controls.
	- **Authorization and Accountability**: Ensuring actions can be traced.
	- **Monitoring and Auditing**: Keeping track of security events and actions.
	- **Nonrepudiation**: Ensuring actions cannot be denied.
	- **Safeguards and Attack Vectors**: Implementing measures to protect against threats.

---

# Lecture 16: Assessment Environment
## Policy Template
- Company name
- Vulnerability Assessment Policy
	- Created by
	- Reviewed by
	- Approved by
- Overview
- Purpose
- Scope
- Policy
- Vulnerability assessment process
- Expectation
- Enforcement
- Related Documents
- Revision History
- Glossary

## Penetration Testing Lifecycle (Bold are main points)
- **Information Gathering**
	- NMAP, Shodan, Maltego, SPART
- **Enumeration**
	- NMAP, Unicornscan
- Vulnerability Assessment
	- OpenVAS, Nexpose, Nessus
- **Gaining Access**
	- Metasploit, John the ripper, Hydra
- **Privilege Escalation**
	- Metasploit
- **Maintaining Access**
- **Covering Tracks**
	- Metasploit
- WebApp Security Testing
	- w2af, Burpsuite, ZAP Proxy
- Reporting
	- Keepnote, Draidis

## Industry Standards
- **Open Web Application Security Project Testing Guide**
	- Provide specific instructions on how to identify, verify, and remediate each vulnerability in an application.
	- Community Project publishes top 10’s for awareness.
	- Integrate throughout all the phases of SDLC.
	- **Benefits**
		- Ensure minimum security requirements.
		- OWASP community has developed many security tools.
		- Provides testing guidelines (Technology/vendor).
		- Helps in designing and implementing security controls.
		- Industry-wise visibility and acceptance.
- **Penetration Testing Execution Standard (PTES)**
	- **Consists of seven stages:**
		- Pre-engagement Interactions
		- Intelligence Gathering
		- Threat Modeling
		- Vulnerability Analysis
		- Exploitation
		- Post Exploitation
		- Reporting
	- **Benefits**
		- Thorough pen-testing framework.
		- Detailed instructions to perform testing tasks.
		- Created by best testers who perform pen-testing on a daily basis.
		- Simple to understand and adaptable.
		- Industry-wise visibility and acceptance.


## Security Assessment Prerequisites
- **Planning & Target Scoping**
	- Deciding and Defining a Formal Scope
		- Precisely define what to test
		- Cannot test every aspect of the target i.e. the Network
	- Important factor that is often overlooked
	- State team plan, resources + timelines
	- Invalid scoping results
		- To scope creep
		- Customer Dissatisfaction + Legal Trouble
- **Gathering Requirements**
	- Clarity about customer requirements and expectations
	- Customer may be internal or external to the organization
	- Document customer requirements (checklists)
	    - Security compliance
	    - Requirements and code of conduct
	    - Network segment
	    - Security devices
	    - Assets to scan (list of assets exposed, list of business-critical assets)
	    - Tools (licensed, prohibited)
	    - Reporting mechanism (recent VA report if available)
	- Suitable time frame and testing hours
	- Identifying stakeholders
	    - Executives
	    - IT Security head
	    - VA Lead Tester (SPOC)
	    - VA Tester (PoC)
	    - Asset owner
	    - Third-party service provider
	    - End users
- **Decision on type of vulnerability assessment**
	- Based on location
	    - External
	    - Internal
	- Based on knowledge about environment/infrastructure
	    - Black box
	    - White box
	    - Gray box
	- Announced and unannounced
	- Automated testing
	    - Authenticated vs unauthenticated
	    - Agent-based vs agent-less
	- Manual testing
- **Estimating the resources & deliverables**
	- Success of vulnerability assessment depends on accurate estimation.
	- **Challenges**
	    - Network security devices blocking.
	    - Assets not responding.
	    - Scan impacting business-critical services.
	    - Blocking user IDs allocated for scanning.
	    - Slowing down of network.
	- Time padding should be considered (usually 20%).
		- If padding is not completely utilized, tester can use extra time for more in-depth findings.
- **Preparing Test plans & Test boundaries**
	- A comprehensive test plan is known as a Statement of Work (SoW)
		- Overview
		- Purpose
		- Applicable laws and regulations
		- Applicable standards and guidelines
		- Scope
		- Assumptions
		- Methodology
		- Test plans
		- Rules of engagement
		- Stakeholders communication
		- Liabilities
		- Authorized approval and signatures
- **Getting Approval & Signing NDA's**
	- Must be approved by senior management.
	- Preapproved support from senior management in case of disruptions.
	- Sign confidentiality and nondisclosure agreements.
	- Provide coverage for various areas such as negligence and liability in case of mishaps.
