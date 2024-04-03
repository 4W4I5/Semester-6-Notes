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
	- Storage Limit -> 8ZiB `2^64 * 512 = 9.44ZB`
	- Redundancy -> Backup of GPT headers and partition tables in last sectors of a disk. Fetched when main information is corrupted
	- Security -> CRC32 Checksum
	- Primary Partitions -> No extended partitions. All partitions are main partitions. Max 128 allowed by windows.
	- No hidden sectors -> First partition starts right after the partition table

## GPT Layout
- **LBA 0**
	- Protective MBR -> Legacy systems see that the disk has a MBR partition and therefore do not attempt to mount
- **LBA 1**
- **LBA 2**
- **LBA 33**
- **LBA 34**
- **LBA -34**
- **LBA -2**
- **LBA -1**

# Lecture 6 - MFT
# Lecture 7 - Registry
# Lecture 10 - Email Forensics