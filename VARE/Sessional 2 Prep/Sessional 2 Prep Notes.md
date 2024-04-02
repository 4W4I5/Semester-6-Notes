| Lecture Number                             | Status    |
| ------------------------------------------ | --------- |
| Lecture 8 & 9: Reverse Engineering         | :warning: |
| Lecture 10: Windows Internal - DLLs- 2     | :warning: |
| Lecture 11: Windows Internal - Registry- 3 | :warning: |
| Lecture 12: IDA                            | :warning: |
| Lecture 13: Basic Dynamic Analysis         | :warning: |

<!--
:x:
:warning:
:white_check_mark:
-->


# Lecture 8 & 9: Reverse Engineering

## Perspectives

|                   | High Level                                                                                                                                                                                                                                                                | Low Level                                     |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| Program Structure | Modules i.e. DLL and Static Libs                                                                                                                                                                                                                                          | ASM version                                   |
| Data Management   | Procedural/OOP                                                                                                                                                                                                                                                            | Registers, Stack, Heaps, Non-NX Data sections |
| Example Language  | C, C++, C#, Java, Python                                                                                                                                                                                                                                                  | Assembly                                      |
| Compilation       | Frontend parses source code after performing lexical analysis and converts it to an Intermediate Representation or Abstract Syntax Tree. Optimizer optimizes by deadcode elimination, loop optimization, register allocation, etc. Backend generates machinecode/bytecode | n/a                                              |

#### Listing File
- Compiler generated
- Text file
- IR of the code read by compiler frontend
- Maps ASM code to the Machine code (1:1)
	- Mapping to ASM->Source is (M:1) i.e. One line of source code can consist of multiple instructions

# Lecture 10: Windows Internal - DLLs- 2
# Lecture 11: Windows Internal - Registry- 3
# Lecture 12: IDA
# Lecture 13: Basic Dynamic Analysis

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
