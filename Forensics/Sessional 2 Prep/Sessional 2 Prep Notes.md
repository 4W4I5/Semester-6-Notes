| Lecture Title                | Status    |
| ---------------------------- | --------- |
| Lecture 5 - GPT              | :warning: |
| Lecture 6 - MFT              | :warning: |
| Lecture 7 - Registry         | :warning: |
| Lecture 10 - Email Forensics | :warning:  |
<!--
:x:
:warning:
:white_check_mark:
-->

# Lecture 5 - GPT
- Addresses Security and Storage requirements not met by MBR

### Comparison of MBR and GPT
- **MBR**
	- Resides in Sector 0
	- 446(01 BE) bytes long bootcode
	- 2 Byte signature
	- Limitations
		- Max space 2TB
		- Not tamper-proof
	- Example partition that is 16 bytes long will have
		- 1 Byte bootable flag
		- 3 bytes for CHS Starting address
		- 1 Byte for Filesystem
		- 3 Bytes for CHS Ending address
		- 4 Bytes LBA Starting address
		- 4 Bytes LBA Size of partition
- **GPT**
	-

# Lecture 6 - MFT
# Lecture 7 - Registry
# Lecture 10 - Email Forensics