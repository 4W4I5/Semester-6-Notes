| Lecture Title                | Status             |
| ---------------------------- | ------------------ |
| Lecture 5 - GPT              | :white_check_mark: |
| Lecture 6 - MFT              | :warning:          |
| Lecture 7 - Registry         | :warning:          |
| Lecture 10 - Email Forensics | :warning:          |

<!--
:x:
:warning:
:white_check_mark:
-->

# Lecture 5 - GPT
- Addresses Security and Storage requirements not met by MBR

## Comparison of MBR and GPT
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
		- Data can still be hidden in
			- MS reserved partition (sizes range from 32mb to 128mb)
			- Partition Gap (sizes range from 47KB to 1MB)
			- Unused Sector 0, 1 + Unused partitions can be used to hide data
			- Start sector. Size = 17KB

## Comparison Table of MBR and GPT (Repeated data i know)

| Feature                               | MBR     | GPT                       |
| ------------------------------------- | ------- | ------------------------- |
| Backup Partition Table                | No      | Yes                       |
| Integrity Protection                  | No      | Yes                       |
| \# of Primary Partitions              | 4       | 128                       |
| Partition Gap                         | No      | Yes                       |
| Max Size                              | 2TB     | 8ZiB                      |
| Legacy Boot                           | Yes     | Need to enable UEFI       |
| Tampering resistance                  | No      | One table can be tampered |
| Hidden Sectors                        | Allowed | Not Allowed               |
| MS Reserved?                          | No      | Yes                       |
| Minimum Size                          | 3MB     | 128MB                     |
| CHS Addressing?                       | Yes     | No                        |
| Compatibility With Forensic software? | Yes     | Limited                   |

## GPT Layout
- **LBA 0**
	- Protective MBR -> Legacy systems see that the disk has a MBR partition in use and therefore do not attempt to overwrite
	- Type i.e 0x4 offset is set to 0xEEh if Protective MBR
- **LBA 1**
	- Header
		- 0x00 -> 8Bytes Length, Signature, "EFI PART"
		- 0x08 -> 4Bytes Length, Revision Number
		- 0x0C -> 4Bytes Length, Header Size in LE
		- 0x10 -> 4Bytes Length, Header CRC
		- 0x14 -> 4Bytes Length, Reserved, Set to 0
		- 0x18 -> 8Bytes Length, Current LBA where Header is placed
		- 0x20 -> 8Bytes Length, Backup LBA of other Header
		- 0x28 -> 8Bytes Length, First Useable LBA for Partition
		- 0x30 -> 8Bytes Length, Last Useable LBA for Partition
		- 0x38 -> 16Bytes Length, Disk GUID
		- 0x48 -> 8Bytes Length, Starting LBA of array of partition entries
		- 0x50 -> 4Bytes Length, Number of partition entries
		- 0x54 -> 4Bytes Length, Size of single partition entry
		- 0x58 -> 4Bytes Length, CRC of partition entries
		- 0x5C -> \* Bytes Length, Starting LBA of array of partition entries
- **LBA 2 to 33**
	- Partition entries
		- 0x00 -> 16Bytes Length, Partition Type GUID
		- 0x10 -> 16Bytes Length, Unique Partition GUID
		- 0x20 -> 8Bytes Length, First LBA in LE
		- 0x28 -> 8Bytes Length, Last LBA
		- 0x30 -> 8Bytes Length, Attribute Flags
			- Bit 0 -> OEM Partition
			- Bit 1 -> Ignore bit, DO NOT READ
			- Bit 2 -> Legacy BIOS Bootable
			- Bits 3-47 -> Reserved
			- Bits 48-63 -> Used by partition
		- 0x38 -> 72Bytes Length, Partition Name in unicode
- **LBA 34 to -34**
	- Holds Partitions i.e the data
- **LBA -33 to -2**
	- Backup of Partition Entries
- **LBA -1**
	- Other GPT Header (Secondary)

# Lecture 6 - MFT
### Understanding File Slack
- Consists of Drive and RAM slack
	- **Drive Slack**
		- Result of Windows allocating space in clusters. Leaves unused space from EOF active file to end of cluster
		- Cluster size for e.g. is generally 4KB so a file that uses a single sector leaves 7 sectors unused
	- **Ram Slack**
		- For last sector the OS includes random data from the ram to fill the slack
		- Now its just 0's

### Files in FAT
- Starting Cluster position assigned to file
	- First sector written here
- Next available cluster used when first is filled
	- If not contiguous, then file becomes fragmented
- Deletions
	- First letter of filename is replaced with 0xE5
		- For both RecycleBin and PermaDelete
	- File space used now becomes unallocated and is overwritable

### NTFS
- Journaling FS
- PBS (Partition Boot Sector) is set first and then the MFT (Master File Table)
- Use of Unicode as well as Smaller cluster sizes for small disk drives

#### MFT
- Contains info on all files on disk, essentially a metadata file
	- First 15 records reserved for system files
- All files are contained in 1KB records
	- A record can be resident or non-resident
- Files larger than 512 bytes are stored outside of the MFT
	- It becomes nonresident and now contains data runs

| Filename   | SystemFile            | Record Pos | Description                                                                                |
| ---------- | --------------------- | ---------- | ------------------------------------------------------------------------------------------ |
| \$\MFT     | MFT                   | 0          | Base file record for each folder on NTFS                                                   |
| \$\MFTMirr | MFT2                  | 1          | First four records of MFT saved here, Used to restore MFT as well if a single sector fails |
| \$\LogFile | LogFile               | 2          | Previous transactions are stored here for recovery after volume failure                    |
| \$Volume   | Volume                | 3          | Label, version of volume is stored here                                                    |
| \$AttrDef  | Attribute Definitions | 4          | Table listing attribute names, numbers and definitions                                     |
| \$         | RootFilename Index    | 5          | Root folder on the volume                                                                  |
| \$Bitmap   | Boot Sector           | 6          | Map of the partition shows which clusters are used/available                               |
| \$Boot     | Boot Sector           | 7          | Additional code for bootstrapping, identifies partition as boot as well                    |
| \$BadClus  | Bad Cluster file      | 8          | Bad clusters are noted here                                                                |
| \$Secure   | Security File         | 9          | ACL maintained here                                                                        |


#### How to read a MFT
-
# Lecture 7 - Registry

> [!WARNING]
> Converted slides directly using GPT

## NTFS Features

- **Encrypting File System (EFS):**
    - **Introduction:**
	    - EFS was introduced with Windows 2000, providing a method for encrypting files, folders, or disk volumes.
  - **Functionality:**
    - EFS implements a public key and private key method for encryption.
    - Users can apply EFS to files stored on local workstations or remote servers.
    - A recovery certificate is generated and sent to the local Windows administrator account.
  - **Recovery Key Agent:**
    - This component implements the recovery certificate stored in the Windows administrator account.
    - Windows administrators can recover keys through Windows or from a command prompt.
  - **EFS Keys:**
    - EFS utilizes the Data Decryption Field (DDF), which consists of the File Encryption Key (FEK) and File Encryption Key Information (FEKI).
    - The FEK encrypts file data using the user's public key, while Feki stores information about FEK.
    - When accessing an EFS-encrypted file, the OS retrieves the FEK and decrypts it using the user's private key.
- **NTFS File Deletion:**
    - When a file is deleted in Windows NT and later, the OS renames it and moves it to the Recycle Bin.
- **Resilient File System (ReFS):**
    - ReFS is designed to address large data storage needs, especially in cloud environments.
    - Features include maximized data availability, improved integrity, and scalability.
    - ReFS utilizes disk structures similar to the Master File Table (MFT) in NTFS.

## Windows Registry

- **Registry Structure:**
    - Key components of the Windows Registry structure include:
	    - HKEY_LOCAL_MACHINE (HKLM)
		- HKEY_CURRENT_CONFIG (HKCC)
		- HKEY_CLASSES_ROOT (HKCR)
		- HKEY_CURRENT_USER (HKCU)
		- HKEY_USERS (HKU)
		- HKEY_PERFORMANCE_DATA (visible in NT-based Windows)
		- HKEY_DYN_DATA (visible in Windows 9x/ME)
- **BitLocker Encryption:**
	- BitLocker encryption is available on various Windows versions, including Vista Enterprise/Ultimate, Windows 7/8/10 Professional/Enterprise, and Server 2008 and later.
	- It requires specific hardware and software configurations, including TPM microchip, compliant BIOS, and NTFS partitions.
- **Third-Party Disk Encryption Tools:**
	- Examples of third-party disk encryption tools include Endpoint Encryption, Voltage SecureFile, and Jetico BestCrypt Volume Encryption.


# Lecture 10 - Email Forensics

> [!WARNING]
> Converted slides directly using GPT

## Introduction
- **Role of Email in Crimes:**
	- Email serves as a primary mode of communication in various aspects of life, from personal to professional interactions.
	- Given its pervasive use, it becomes crucial to delve into its role in criminal activities, as it often leaves traces of illicit behavior within communication records.

## Terminology
- **Mail User Agent (MUA):**
    - Also referred to as an email client, MUA is the software interface utilized by end-users to compose, send, receive, and manage emails.
- **Mail Submission Agent (MSA):**
    - MSA is responsible for accepting outgoing emails from users, preparing them for transmission, and then submitting them to the Mail Transfer Agent (MTA) for onward delivery.
- **Mail Transfer Agent (MTA):**
    - MTA is a software component that facilitates the transfer of electronic mail messages from one computer to another using a client-server application architecture.
- **Mail Exchange (MX):**
    - MX records designate the mail server responsible for receiving email on behalf of a domain name.
- **Mail Delivery Agent (MDA):**
    - MDA is tasked with delivering incoming email messages to the respective recipient's local mailbox.

## Email Delivery
- **Corporate Mail vs. Web Mail:**
    - Corporate email services provided by organizations to their employees entail certain risks, especially concerning data security and potential unauthorized data transfer.
    - Web-based email services, like Yahoo or Gmail, pose even greater risks due to their accessibility and lack of stringent monitoring.
- **Email Transaction Analysis:**
    - While email transactions are not typically scrutinized in real-time, they play a significant role in forensic investigations, particularly when suspicions arise regarding illicit activities.

## How Email Works
- **Mail Servers:**
    - These servers act as intermediaries in the transmission of email messages, facilitating their routing from sender to recipient.
- **SMTP Servers:**
    - SMTP servers handle the outgoing email flow, processing messages and forwarding them to the intended recipients.
- **POP3 and IMAP Servers:**
    - POP3 and IMAP servers manage incoming email retrieval, with POP3 typically downloading messages to local storage and IMAP allowing access to messages stored on the server.

## Email Lifecycle
- **Steps in Email Transmission:**
    - The process encompasses composing the message, communication with SMTP servers, DNS resolution to locate recipient servers, routing between SMTP servers, recipient server processing, and final delivery to the recipient's inbox.

## Email Header Examination
- **Header Information:**
    - Email headers contain vital metadata such as IP addresses, sender and recipient details, timestamps, and protocol specifics.
- **Key Header Fields:**
    - These include From, Subject, Date, To, Return-Path, Delivery Date, Received, Message-ID, Mime-Version, Content-Type, DKIM-Signature, Domainkey-Signature, SPF, and DMARC.
- **Verification Techniques:**
    - Examining SPF, DKIM, DMARC fields, Return Paths, and Received fields aids in verifying the legitimacy of email communications.

## Email Examination Tools
- **Data Recovery Tools:**
    - Specialized software tools are available to facilitate the extraction and analysis of data from email servers and clients.
- **Examples:**
    - DataNumen, FINALeMAIL, MailXaminer, Paraben E-Mail Examiner, among others, offer functionalities tailored for email forensics purposes.

## Social Media Forensics
- **Role in Investigations:**
    - Social media platforms serve as significant repositories of digital evidence, providing insights into various aspects of individuals' activities, including criminal behavior.
- **Challenges:**
    - Jurisdictional complexities, legal constraints, and tool limitations pose challenges in conducting thorough social media forensic examinations.

## Mobile Devices and Social Media
- **Evidence Artifacts:**
    - The nature and availability of evidence artifacts vary across different social media channels and mobile device platforms.
- **Tool Development:**
    - While efforts are underway to develop specialized tools for social media forensics, the field currently faces limitations in terms of tool availability and legal considerations regarding the admissibility of obtained evidence in legal proceedings.