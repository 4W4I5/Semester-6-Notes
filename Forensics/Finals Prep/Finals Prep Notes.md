| Chapter                                                                     | Status             |
| --------------------------------------------------------------------------- | ------------------ |
| Smart Watch Forensics - Lec 20                                              | :white_check_mark: |
| Mobile Forensics  - Lec 16                                                  | :white_check_mark: |
| Cloud Forensics - Lec 13                                                    | :warning:          |
| Digital Forensics Analysis & Validation (Anti-Forensics Techniques) - Lec 9 | :warning:          |
| Report Writing - Lec 14                                                     | :warning:          |
| Assignment 1: Laws + Policies                                               | :white_check_mark:          |
| Assignment 2: Android Forensics                                             | Skipped :x:        |
| Assignment 3: MFT + NTFS + ADS                                              | :white_check_mark: |
| Assignment 4: Dark Web Forensics                                            | Skipped :x:        |
| Assignment 5: Python code to read MBR                                       | :white_check_mark: |
| Assignment 6: Timeline Analysis using TSK                                   | :white_check_mark: |

# Smart Watch Forensics (Lec 20)
## Android & Apple Forensics Artifacts
- Device Info
- User ID
- Comms Data
- App Data
- Sync Data
- Location Info
- Health & Fitness Data
- Multimedia Files
- Apple Only
	- Calendar & Reminders
	- Sensor Data
	- Payment & Transaction Data
	- System Logs & Diagnostics
	- Voice Assistant Data (Siri)
	- Workout & Exercise Data
	- Fall Detection & Emergency SOS Data
## Challenges in Smartwatch Forensics
- Compact Size
- Proprietary OS
- Intricacies of Data sync
- Small storage capacity
- Encryption & Security measures
- Compatibility with DF tools
- Fragmentation across models
- Limited DF standards + Guidelines
## Tools & Techniques
- Data Extraction
	- Perform acquisition via the cloud, mobile app or direct hardware.
	- Gather health metric, GPS records, notification history and communication records
- Data Analysis
	- Correlate and compose a result based on data extracted
- Cloud Integration
	- Gaining access to synced data on the cloud
	- More comprehensive insight into user's data footprint
	- Use OxygenForensics toolkit to
		- Extract data from the cloud
		- Extract data from smartmobile devices
		- Direct Watch Extraction -> Possible but not much data as storage is limited on smartwatches
			- Done via mobiledit smartwatch kit that has interfaces for most smartwatches that have a debug port
---
# Mobile Forensics (Lec 16)
## Android
- **Levels of security**
	- SELinux-based OS level controls
		- Ensures every app is sandboxed via user-based protection model
	- Google Safety checks, updates, play protect
	- OEM based security and patches
- **Data storage location**
	- Internal/External storage
		- External i.e. a mounted sdcard or these days in modern phones its a virtual card thats symlinked
		- Internal i.e. /data
	- Shared preferences
	- SQLite Database
	- Network(Cloud)
- **Filesystem partitions**
	- Logical, some phones support failover partitions such as A/B slots
	- Types
		- /boot -> Boot partition, holds boot image as well as ramdisk if supported
		- /recovery -> Alternate (Not Failover) boot partition should regular boot sequence fail, allows for factory reset or cache clearing.
			- Further functionality such as System-wide Root and Flashing a new rom/sideloading via adb requires a custom recovery such as TWRP or orangefox
		- /system -> Android OS, does not include Google GMS/GSF
		- /data -> aka userdata
			- Includes contacts, messages, settings and installed apps
			- Wiped during Factory reset, great source of forensic data
		- /metadata -> used when device is encrypted
		- /cache -> Self-explanatory, good source of forensic data provided it is wiped
		- /misc -> Boolean switches for a lot of settings on the phone, device features may not function correctly if missing/corrupted
		- /sdcard -> All data seen in the file manager app on android is stored here, symlinked to /storage/emulated/0
		- /sd-ext -> Used widely in custom ROMs, used to simulate an sdcard to offload apps
		- /product -> Vendor/Carriers customizations to the OS
		- /vendor -> Vendor specific binary i.e. tmobile custom binary, can also contain firmware specific to a SOC
- **Forensic Acquisitions**
	- Physical
		- Read the chip itself to gather Files bit by bit, Hidden files and deleted data
	- Logical
		- Dump the data via ADB or if root is available create a raw image using dd
			- `adb shell` -> Get a shell in the system, if root needed use su but need rooted OS
			- `adb push apkName.apk` -> Copy file to the device, use pull to get files off the device
			- `adb backup -apk -shared -all -f <PATH>`-> Copy all directories and apps off of the device
		- Use an app to gather appdata, userdata and system settings available to the user
		- Custom recoveries such as TWRP allow for dd backup and restores from within the recovery
	- Approaches
		- Manual Extraction -> Invasive, requires human intervention to copy data
		- Logical Extraction -> Non-Invasive, copies userdata and sdcard data. Cannot access System unless root
		- HexDump/JTAG -> Hijack debug port/UART port on the memory. Get bit by bit image directly with the chip intact
		- ChipOff -> Remove memory from SOC and plug into a reader, iterate through addresses and create a dd image
		- MicroRead -> Destroy chip, use electron microscope to create a bitmap of the silicon to read data
- **Tools for Android**
	- CLI-Based
		- Andriller, by images it seems like it uses adb
		- Foroboto, similar to andriller
		- AFLogicial OSE
		- Dazai, extracts dd images
	- GUI-Based
		- XRY, Does both physical and logical analysis. If device is not supported then root access is required
		- Autopsy, Generates dd image
- **Challenges/Future research for Forensics**
	- Social networking apps
	- Evaluation of existing tools for extracting e-evidence from mobile
	- Automated Data collection + reporting
	- Interpretation of timestamps
	- Preservation of digital evidence
	- Efficient Generalized Forensics Framework for Mobile Devices (No clue what this is)
---
# Cloud Forensics (Lec 13)
- **Types of Cloud Deployment**
	- Public -> Accessible to the public internet, Best for ease of use
	- Private -> Internal Cloud deployment, used by orgs
	- Community -> Purpose based sponsored by big orgs that want to fulfil a purpose via a business license
	- Hybrid -> Mix of Private + Public Glass
- **Cloud Forensics Essentials**
	- Organizational -> Structure of the cloud i.e. data storage location and administration of services
	- Legal -> 
	- Technical
- **Requirements of a Cloud Forensics Tool?**
	- Data Collection
	- Elastic, Static and Live forensics
	- Evidence Segregation
	- Investigations in Virtualized Enviros
- **Legal Challenges**
	- Service Level Agreements (SLAs)
	- Jurisdiction
	- Evidence Access
- **Technical Challenges**
	- Architecture
	- Data Collection
	- Anti-Forensics
	- Incident First-Responders
	- Role Management
	- Standards + Training
	- Encryption in the cloud
- **Methods of data acquisition**
	- Evidence Collection Methods
	- Enumeration + File Recovery
	- Remote Acquisition
	- Snapshots in VE
	- Complexity of cloud systems
	- Encryption in the cloud
	- Handling Encrypted data
	- Encryption in the Cloud
	- Handling Encrypted Data
	- Encryption Tools and Vendors
	- Advanced Encryption Techniques
---
# Digital Forensics Analysis & Validation (Anti-Forensics Techniques) (Lec 9)
- **Data to collect/analyze during an investigation**
	- Investigation Types
		- Criminal
			- Tailored via warrants that specify what data to grab and from what media
		- Civil
			- Limited by court orders, only data relevant to the case is gathered
			- Tailored via warrants that specify what data to grab and from what media
		- Private-Sector
			- Involves internal Policy violations and/or litigations
			- Broad scope involving internal company comms channels such as email, company provided phones and laptops, company emails and etc.
			- Tailor the investigation by ensuring it is comprehensive but focused i.e. the scope is fine-tuned
	- Outlining an Investigation
		- Handling Scope Creep
		- Investigation Plan
	- Procedure
		- Prepare Target Drives
		- Inventory hardware
		- Static Acquisitions
		- Data Acquisitions
		- Examine Data methodically
		- File analysis
		- Password-Protected Files
		- Executable Files
		- Control and Documentation
- **Validation of Forensic Data**
	- Use of Hex Editors
	- Hashing specific data in a file
	- Use of Forensic Tools
- **Data Hiding Techniques**
	- Changing File Extensions
	- Setting Hidden attribute
		- .nomedia in android and hidden attribute flag on windows
	- Hiding Partitions
		- Taking advantage of file slack
	- Marking Bad clusters
	- Bit-Shifting
	- Steganalysis Methods
	- Steganalysis Attacks
	- Examining Encrypted Files
	- Recovering Passwords
---
# Report Writing (Lec 14)
- Report Types
	- Formal Report
	- Examination Plan
	- Verbal Report
	- Preliminary Written Report
	- Written Report
- Guidelines to writing a report
	- Expressing an Opinion
	- Preliminary Reports
	- Report Structure
	- Writing Reports Clearly
	- Layout & Presentation
	- Examination & Data Collection Methods
	- Results & Conclusions
	- References & Appendixes
	- Writing Style
---
# Assignments
## Assignment 1: Laws + Policies
- **Scope of Digital Forensics in Pakistan**
    - **Cybercrime Investigation**
        - Investigates cybercrimes like hacking, phishing, malware attacks, and identity theft.
        - Analyzes digital evidence to trace attacks and identify perpetrators.
    - **Data Breach Response**
        - Determines extent of breaches, identifies compromised data, and mitigates impact.
        - Preserves evidence and implements security measures.
    - **Legal Proceedings**
        - Digital evidence is admissible in court for criminal prosecutions, civil litigation, and regulatory investigations.
        - Ensures evidence integrity and authenticity.
    - **Incident Response Planning**
        - Develops response plans, conducts assessments, and establishes incident handling protocols.
    - **Cybersecurity Compliance**
        - Supports compliance with laws like the Prevention of Electronic Crimes Act (2016) and standards like ISO/IEC 27001.
- **General Cases**
    - **Corporate Sector**
        - **Employee Misconduct**
            - Investigates unauthorized data access and misuse of resources.
        - **Intellectual Property Theft**
            - Tracks theft, identifies culprits, and traces stolen data.
        - **Data Breaches**
            - Determines breach cause and extent, identifies compromised data, and helps compliance and mitigation.
    - **Public Sector**
        - **Cybercrime Investigations**
            - Assists law enforcement in investigating hacking, fraud, and child exploitation.
        - **Financial Fraud**
            - Uncovers activities like embezzlement and money laundering.
        - **Public Safety Incidents**
            - Identifies the source and impact of cyberattacks on critical infrastructure.
- **Policies, Laws, and Regulations of Pakistan**
    - **Prevention of Electronic Crimes Act (PECA) 2016**
        - Addresses various cybercrimes, legal mechanisms for investigation, and digital evidence collection.
        - Federal Investigation Agency (FIA) as the primary enforcing agency.
    - **National Cyber Security Policy (NCSP) 2021**
        - Outlines objectives for cybersecurity and protection of critical infrastructure.
        - Promotes collaboration between government, private sector, and international partners.
    - **Telecommunication (Re-organization) Act 1996**
        - Regulatory oversight of telecommunications services.
        - Pakistan Telecommunication Authority (PTA) regulates and monitors compliance.
    - **Digital Forensic Science Lab (DFSL) Rules 2018**
        - Guidelines for digital evidence examination and reporting.
    - **Payment Systems and Electronic Fund Transfers Act (PEFTA) 2007**
        - Regulates electronic transactions and investigates financial crimes using digital forensics.
- **Comparative Analysis**
    - **General Data Protection Regulation (GDPR)**
        - Pakistan lacks specific GDPR-like law; PECA addresses data protection.
        - UK has GDPR via Data Protection Act 2018.
    - **Computer Misuse Act**
        - PECA criminalizes unauthorized access and data interference.
        - UK has the Computer Misuse Act 1990.
    - **Freedom of Information Act**
        - Pakistan lacks an equivalent law.
        - UK has the Freedom of Information Act 2000.
    - **Prevention of Electronic Crimes Act (PECA)**
        - Comprehensive legislation against cybercrimes in Pakistan.
- **Limitations**
    - **Enforcement Challenges**
        - Limited resources and expertise hinder effective implementation.
    - **Lack of Coordination**
        - Fragmentation among agencies impedes information exchange.
    - **Legal Gaps**
        - Rapid technological advancements expose gaps in laws.
    - **Privacy Concerns**
        - Digital surveillance raises privacy concerns.
    - **International Cooperation**
        - Limited frameworks hinder cross-border investigations.


## Assignment 3: MFT + NTFS + ADS
- **ADS**
	- Commands
		- Create ADS on text.txt -> `echo hidden > text.txt:ads.txt`
		- Read ADS on text.txt -> `more < text.txt:ads.txt`
		- Executing DLL via ADS -> `rundll32 test.txt:malicious.dll,EntryPoint`
			- To view contents -> `more < test.txt:malicious.dll`

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
		- Data can still be hidden in
			- MS reserved partition (sizes range from 32mb to 128mb)
			- Partition Gap (sizes range from 47KB to 1MB)
			- Unused Sector 0, 1 + Unused partitions can be used to hide data
			- Start sector. Size = 17KB

#### Comparison Table of MBR and GPT (Repeated data i know)

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

#### GPT Layout
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

#### Understanding File Slack
- Consists of Drive and RAM slack
	- **Drive Slack**
		- Result of Windows allocating space in clusters. Leaves unused space from EOF active file to end of cluster
		- Cluster size for e.g. is generally 4KB so a file that uses a single sector leaves 7 sectors unused
	- **Ram Slack**
		- For last sector the OS includes random data from the ram to fill the slack
		- Now its just 0's

#### Files in FAT
- Starting Cluster position assigned to file
	- First sector written here
- Next available cluster used when first is filled
	- If not contiguous, then file becomes fragmented
- Deletions
	- First letter of filename is replaced with 0xE5
		- For both RecycleBin and PermaDelete
	- File space used now becomes unallocated and is overwritable

#### NTFS
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
- Identify FILE (46 49 4C 45)
- Offsets from start of FILE
	- 0x14 -> Length of MFT Header. Should point to start of StandardInformation Attribute 0x10 (Generally it is at 0x38)
	- **StandardInformation Attribute 0x10**
		- 0x04 to 0x05 -> Length of attribute
		- Timestamps at:
			- 0x18 to 0x1F -> Last Creation Time Time/Date
			- 0x20 to 0x27 -> Last Modified Time Time/Date
			- 0x28 to 0x2F -> Last Accessed Time Time/Date
			- 0x30 to 0x37 -> Last Updated Time/Date
	- **Filename Attribute 0x30**
		- 0x04 to 0x05 -> Length of attribute
		- Timestamps at:
			- 0x20 to 0x27 -> Last Creation Time Time/Date
			- 0x28 to 0x2F  -> Last Modified Time Time/Date
			- 0x30 to 0x37 -> Last Accessed Time Time/Date
			- 0x38 to 0x3F -> Last Updated Time/Date
		- 0x5A to Length of Attribute -> ShortFilename in Unicode (Should Notice ASCII with 00 gaps. For e.g. 'A' would be 41 00)
	- **ObjectID Attribute 0x40**
		- 0x04 to 0x05 -> Length of attribute
		- 0x14 -> Offset for GUID
			- Whatever value 0x14 points to is where the GUID starts. Length of GUID is 16 bytes
	- **Data Attribute 0x80**
		- 0x04 to 0x05 -> Length of attribute
		- 0x08 -> Resident/Non-Resident Flag set to 1 or 0 respectively
			- Understanding DataRuns
				- For `0x32`, 3 means \# of Bytes to store starting LCN and 2 is \# of Bytes to store Clusters assigned to this data run
				- IF NumOfClusters = 1 then VCN == LCN
					- Otherwise if First byte of VCN is 0x80 or greater then the VCN is a negative number. Use 2's complement to calculate
			- If resident
				- 0x10 -> Length of Resident Data run
				- 0x18 -> Start of Data run
			- If NonResident
				- 0x40 -> Start of Data Run. First Logical Cluster Number (Logical Cluster Number)
	- **DDF Attribute 0x0100 (LECTURE 7 EFS CONTENT)**
		- Contains FEK and FEKI
			- FEK is a symmetric encryption key, FEKI contains info on FEK that is the version num, algo used and length of FEK
		- 0x20 -> FEK
		- 0x20 + FEK Len(normally 32bytes) -> FEKI
	- **Checksum**
		- 0x01FE and 0x01FF -> Sector checksum value
	- **End of Sector**
		- Identified by `FF FF FF FF`
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


## Assignment 5: Python Code to read MBR
- Essentially read the first 446 bytes of the first sector and hash
- Compared hash later on using winhex


## Assignment 6: Timeline Analysis using TSK
- **After creating an image via an imaging tool such as FTKImager**
- **Creating a filesystem log with MAC times**
    - `fls -rpl -m /IMG_NAME.img > txtfile.txt`
    - Can try tsk custom scripts too, the output is similar
        - `tsk_gettimes /IMG_NAME.img > txtfile.txt`
- **Using mactime.pl to create a timeline. Note that we can feed the output from other files into this timeline and it will enrich the timeline**
    - `mactime.pl -b txtfile.txt > output`
- **Extra commands to use that might be helpful**
	- TSK Automated Tools
	    - `tsk_comparedir`: compare localdir with contents of image/raw device
	    - `tsk_recover`: Recover file using the ils inodes
	- File System Layer tools
	    - `fsstat`: Show FS system details and statistics including layout, sizes and labels
	- File Name Layer Tools
	    - `ffind`: Find allocated/unallocated file names in given metadata structure
	    - `fls`: List allocated/unallocated filenames in a directory. Use switches -rpl to list long names recursively
	- Data Unit Layer Tools
	    - `blkcat`: Display contents of a data unit
	    - `blkls`: List data units in a disk image
	    - `blkstat`: Display details about a specific data unit
	    - `blkcalc`: Calculate which data unit contains a specific byte
	- Filesystem Journal Tools
	    - `jcat`: Display the contents of a journal data unit
	    - `jls`: List the contents of a file system journal
	- Volume System Tools
	    - `mmls`: Display partition layout of a volume system
	    - `mmstat`: Display volume system statistics
	    - `mmcat`: Extract data from a specific volume system
	- Image File Tools
	    - `img_stat`: Display details about an image file
	    - `img_cat`: Extract data from an image file
	- Disk Tools
	    - `disk_sreset`: Reset disk to a known state
	    - `disk_stat`: Display disk statistics
	- Other Tools
	    - `hfind`: Find hash values in a hash database
	    - `mactime`: Create a timeline from a body file
	    - `sorter`: Sort file system data into categories
	    - `sigfind`: Find a signature in a file or data stream
- **Windows Artifacts to recover**
	- LNK files -> Shortcut file, stored in appdata/roaming/microsoft/windows/recentitems
	- Thumbnails -> .db extension. stored in /appdata/local/microsoft/windows/explorer
	- JumpLists
		- Can be OS generated or Custom, Uses MRU values
		- Stored in /appdata/roaming/microsoft/windows/recent/automaticdestinations or customdestinations
	- Libraries
		- Folder libs not code libs, stored in /appdata/roaming/microsoft/windows/libraries
	- Windows Search History
		- /appdata/local/microsoft/windows/connectedsearch/history
	- Recycle Bin
		- Renames files to `<SID>/RandomFilename.png`
		- if $i then it has the metadata
		- if $r then it has the actual file
	- VSS
		- Holds restore points
		- c/SystemVolumeInformation
	- Prefetch
		- Holds files required to boot application up faster
		- c/windows/prefetch
	- ShellBags
		- Windows registries NTuser.dat
		- If it exists i.e. it has been accessed before, used to track user behaviour
	- ShimCache
		- Provides compatibility to old windows apps
		- HKLM\\SYSTEM\\CurrentControlSet\\Control\\SessionManager\\AppCompatCache\\AppCompatCache
		- Use amcacheparser
	- USBForensics
		- Registry
			- HKLM\\SYSTEM\\ControlSet\\ENUM\\USBSTOR
			- Get usb name>serial number>properties
		- System Log
			- c/windows/inf
				- setup.offline.log
				- setupapi.dev\/upgrade\/setup.log (dev setup and upgrade are diff options)
			- c/windows
				- setupact.log
				- setup.err.log
	- Registry
		- Timezone ->HKLM\\SYSTEM\\ControlSet\\Control\\TimeZoneInformation
		- Windows product info ->HKLM\\SOFTWARE\\Microsoft\\WindowsNT\\CurrentVersion
		- Windows Computer Name -> HKLM\\SYSTEM\\ControlSet\\Control\\ComputerName\\ComputerName
		- Windows Services ->HKLM\\SYSTEM\\ControlSet\\Service
			- Start key with values 0,1,2,3,4
				- 0:boot
				- 1:system
				- 2:auto
				- 3:manual
				- 4:disabled
		- DHCP Config ->HKLM\\SYSTEM\\ControlSet00#\\Services\\Tcpip\\Parameters\\Interfaces\\{GUID}\\DhcpIPAddress
		- Legal Notice & Text
		    - Notice which appears to the user at logon screen (Legalnoticetext, Legalnoticecaption)
		    - `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\`
		- NTFS Last Accessed
		    - Last access time in registry is updated or not
		    - `HKLM\SYSTEM\ControlSet###\Control\FileSystem\NTFSDisableLastAccess` → (0: not updated, 1: updated)
		- Autoruns
		    - Places where startup apps are running found
		    - `HKLM\Software\Microsoft\Windows\CurrentVersion\Run`
		    - `HKLM\Software\Microsoft\Windows\CurrentVersion\RunOnce`
		    - Note that we can use AutoRuns tool
		- Installed Applications
		    - Helps us when installed application does not appear on desktop or has been uninstalled
		    - `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall`
		    - `HKLM\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall`
		- Windows Firewall
		    - Firewall is on state by default and we can look for its state in some registry keys:
		        - Private environment: `HKLM\SYSTEM\ControlSet###\Services\SharedAccess\Parameters\Firewallpolicy\StandardProfile\EnableFirewall`
		        - Public environment: `HKLM\SYSTEM\ControlSet###\Services\SharedAccess\Parameters\Firewallpolicy\PublicProfile\EnableFirewall`
		        - Domain environment: `HKLM\SYSTEM\ControlSet###\Services\SharedAccess\Parameters\Firewallpolicy\DomainProfile\EnableFirewall`
		    - `EnableFirewall` → (0: off, 1: on)
		- Remote Desktop
		    - `HKLM\SYSTEM\ControlSet###\Control\TerminalServer\fDenyTSConnections`
		    - `fDenyTSConnections` → (0: off, 1: on)
		- Network Profiles
		    - Include network and connection type
		    - `HKLM\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\NetworkList\profiles`
		    - We can find keys under profiles which are network profiles and each one of renamed with its GUID.
		- Network History
		    - Network history cache: `HKLM\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\NetworkList\Nla\Cache`
		    - Place tells me that networks not part of domain: `HKLM\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\NetworkList\Nla\Signatures\Unmanaged\`
		    - Place tells me that networks part of domain: `HKLM\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\NetworkList\Nla\Signatures\managed\`
		- Network Interfaces and Past Networks
		    - Network interfaces and their info such as IP address, subnets, Domain, DHCP, etc.
		    - `HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces`
		- Shutdown details
		    - `HKLM\SYSTEM\Controlset001\control\windows`
		- AppInit_DLLs
		    - Includes list of DLLs which is called automatically when app is run
		    - `HKLM\Software\Microsoft\WindowsNT\CurrentVersion\Windows\Applnit_DLLs`
		- Windows Recycle Bin
		    - We can find that if file has been bypassed recycle bin or just moved to
		    - `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\BitBucket\Volume\{GUID}\NukeOnDelete`
		    - `NukeOnDelete` → (0: move to Recycle Bin, 1: bypass Recycle Bin)
		- Last User Logged In
		    - We can know when was the last time a logging in was occurred and who was the user
		    - `SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\LogonUI\LastLoggedOnUser`
		- User Sessions
		    - During a live Windows session, the logged on user are recorded in this volatile path
		    - `SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\LogonUI\SessionData\<session number>\LastLoggedOnSamUser`
		- Local Users
		    - Where we can find name, login date\time, passwords hints, etc
		    - `HKLM\SAM\Domains\Account\Users`
		- User Account Control (UAC)
		    - Enable Users to perform common tasks as non-admins, it is on state by default and we can check that at:
		    - `HKLM\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\Policies\System\EnableLUA`
		    - `EnableLUA` → (0: disabled, 1: enabled)
		- User Assist Keys
		    - Registry value which tracks user’s interactions via Windows Explorer
		    - `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist`
		- What key last viewed
		    - Last registry key opened by user
		    - `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Applets\Regedit\LastKey`
		- Hidden file setting and extension
		    - (Show\Hide) files and extensions are options for user customization in file explorer
		    - `NTUSER.DAT\Software\Microsoft\Windows\Currentversion\Explorer\Advances\(Hidden or HidefileExt)`
		- Most recently used and opened
		    - OS keeps track for MRU (Most Recently Used) files and apps which are stored in NTUSER.DAT
		        - `CIDSizeMRU`: Tracks size, position of file explorer screen
		        - `Start menu run MRUs`: Tracks list of apps which ran before
		            - `HKU\{SID}\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU`
		        - `RecentDocs MRUs`: Includes no of recently opened files and extension
		            - `HKU\{SID}\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`
		        - `Remote Desktop MRUs`: Recent connection history and configuration data for RDP
		            - `HKEY_USERS\{SID}\Software\Microsoft\Terminal Server\Client\(Default or Servers)\`
		- Most recently opened
		    - Applications and files that have been opened
		    - `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32`
		        - `LastVisitedPidlMRU`: Applications
		        - `OpenSavePidlMRU`: Files
		- IE typed URLs and Setting
		    - Typed URLs by user in Internet Explorer
		    - `NTUSER.DAT\Software\Microsoft\Internet Explorer\Main\TypedURLs`
		    - Internet explorer settings such as (local page, start page, tabs, etc)
		    - `NTUSER.DAT\Software\Microsoft\Internet Explorer\Main`