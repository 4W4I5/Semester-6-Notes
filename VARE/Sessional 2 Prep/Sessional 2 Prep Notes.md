| Lecture Number                                      | Status                                                            |
| --------------------------------------------------- | ----------------------------------------------------------------- |
| Lecture 8 & 9: Reverse Engineering                  | :white_check_mark:                                                |
| Lecture 10 & 11: Windows Internal - DLLs & Registry | :white_check_mark:                                                |
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
