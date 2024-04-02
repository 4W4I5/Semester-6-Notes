| Lecture Number                                      | Status                                                            |
| --------------------------------------------------- | ----------------------------------------------------------------- |
| Lecture 8 & 9: Reverse Engineering                  | :warning:                                                         |
| Lecture 10 & 11: Windows Internal - DLLs & Registry | :warning:                                                         |
| Lecture 12: IDA                                     | :x: Would be Regurgitating Info, Go through the slides (42 Pages) | 
| Lecture 13: Basic Dynamic Analysis                  | :white_check_mark:                                                |

<!--
:x:
:warning:
:white_check_mark:
-->


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
#### Operand Types + Addressing Mode
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

#### Registers
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

#### Important x86 Instructions
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
	- Identify Code segement
		- Generally Code and Data segments are mixed
			- Observe PE/ELF format to understand both segments
			- These generally have mechanisms to identify code and entrypoint
	-

## Disassembly Algo (Linear sweep vs Recursive Descent)

# Lecture 10: Windows Internal - DLLs- 2
# Lecture 11: Windows Internal - Registry- 3
# Lecture 12: IDA
# Lecture 13: Basic Dynamic Analysis
### Basics
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