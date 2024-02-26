| Chapter                                                 | Status   |
| ------------------------------------------------------- | -------- |
| 1 - Understanding Forensics Profession & Investigations | bruh.    |
| 2 - Investigators Office                                | bruh.    |
| 3 - Data Acquisition                                    | bruh.    |
| 5 - Working with Windows & CLI systems                  | :warning | 

---

# Chapter 1 is insanely boring. Here's the summary
## Q/A
1. Digital forensics and data recovery refer to the same activities. False.
2. Police in the United States must use procedures that adhere to which of the following? b. Fourth Amendment
3. The triad of computing security includes which of the following? c. Vulnerability/threat assessment and risk management, network intrusion detection and incident response, and digital investigation
4. What’s the purpose of maintaining a network of digital forensics specialists? The purpose of maintaining a network of digital forensics specialists is to ensure timely and effective response to digital incidents, such as cyber attacks or data breaches, and to provide expertise in investigating and analyzing digital evidence.
5. Policies can address rules for which of the following? d. Any of the above
6. What are two items that should appear on a warning banner?
- A warning banner should typically include a notice that the system is for authorized users only and a warning that unauthorized access is prohibited.
7. Under normal circumstances, is a private-sector investigator considered an agent of law enforcement? False.
- A private-sector investigator is not typically considered an agent of law enforcement under normal circumstances.
8. Name two types of digital investigations typically conducted in a business environment.
- Two types of digital investigations commonly conducted in a business environment are internal investigations for employee misconduct or policy violations and forensic investigations for incidents such as data breaches or cyber attacks.
9. Define professional conduct and explain its importance.
- Professional conduct refers to the ethical behavior, integrity, and adherence to standards expected in a particular profession. It's important because it builds trust with clients, maintains the reputation of the investigator and their organization, and ensures fairness and legality in investigations.
10. What is the purpose of an affidavit?
- The purpose of an affidavit is to provide evidence or support for a legal proceeding or to establish facts in a case by presenting a sworn statement of facts written by an individual under oath.
11. What are the necessary components of a search warrant?
- The necessary components of a search warrant typically include the specific location to be searched, the items or evidence to be seized, probable cause for the search, the signature of a judge or magistrate, and the date issued.
12. How can you determine the resources needed for an investigation?
- Determining the resources needed for an investigation involves assessing factors such as the scope and complexity of the case, the expertise required, available budget and personnel, technological tools needed, and legal considerations.
13. What are three items that should be on an evidence custody form?
- Three items that should be on an evidence custody form are a description of the evidence, the date and time it was collected, and the signature of the person collecting and transferring the evidence.
14. Why should you do a standard risk assessment to prepare for an investigation?
- Conducting a standard risk assessment before an investigation helps identify potential risks, threats, and challenges that could impact the investigation's success. It allows investigators to prepare mitigation strategies and allocate resources effectively.
15. Should you always prove the allegations made by the person who hired you? False.
- It's not necessary to prove the allegations made by the person who hired you. Instead, investigators should focus on gathering objective evidence and reaching impartial conclusions based on facts.
16. For digital evidence, is an evidence bag typically made of antistatic material? True.
- True. An evidence bag for digital evidence is typically made of antistatic material to prevent static electricity from damaging the electronic components.
17. Why should evidence media be write-protected?
- Evidence media should be write-protected to prevent any unauthorized alteration, deletion, or addition of data, preserving the integrity and admissibility of the evidence in legal proceedings.
18. What are three items that should be in your case report?
- Three items that should be in a case report are a detailed description of the investigation process, findings of the investigation supported by evidence, and conclusions or recommendations based on the findings.

## Summary
- Digital forensics involves applying forensic procedures to digital evidence for use in legal cases. It differs from network forensics and data recovery.
- Laws governing digital evidence were established in the 1970s.
- Successful digital forensics investigators need familiarity with multiple computing platforms and networking professionals.
- Specialized workstations with additional drive bays, forensics software, and write blockers are essential for investigators.
- Public-sector investigations require a search warrant, while private-sector cases focus on policy violations and asset abuse.
- Warning banners remind employees of company policies on computer and internet use.
- Companies should limit authorized requesters for investigations.
- Professional conduct is crucial for digital forensics investigators.
- Systematic approaches and checklists guide investigations.
- Planning involves considering case nature, requester instructions, necessary tools, and evidence acquisition.
- Both criminal cases and policy violations require similar handling for presenting quality evidence in court.
- Contingency planning is vital for addressing unexpected challenges in investigations.
- Standard evidence custody forms track evidence chain of custody.
- Internet abuse investigations involve analyzing server log data.
- Attorney-client privilege cases require labeling written communication appropriately.
- Bit-stream copies, duplicates of original disks, are preferred for analysis.
- Maintaining a journal helps track evidence handling.
- Self-critique improves investigation methods for future cases.

# 2 - Investigators Office

How is this so boring, same scene as Chapter 1

1. An employer can be held liable for e-mail harassment. True.
2. Building a business case can involve which of the following? d. All of the above
3. The ANAB mandates the procedures established for a digital forensics lab. False.
4. The manager of a digital forensics lab is responsible for which of the following? a. Making necessary changes in lab procedures and software, b. Ensuring that staff members have enough training to do the job, c. Knowing the lab objectives
5. To determine the types of operating systems needed in your lab, list two sources of information you could use. Manufacturers' specifications and industry standards.
6. What items should your business plan include? Your business plan should include details such as the mission and objectives of the lab, target market, marketing strategies, financial projections, and operational plans.
7. List two popular certification programs for digital forensics. Certified Information Systems Security Professional (CISSP) and Certified Computer Examiner (CCE).
8. Why is physical security so critical for digital forensics labs? Physical security is critical for digital forensics labs to prevent unauthorized access, tampering, or theft of sensitive equipment and evidence, ensuring the integrity and reliability of forensic processes and findings.
9. If a visitor to your digital forensics lab is a personal friend, it’s not necessary to have him or her sign the visitor’s log. False.
10. What three items should you research before enlisting in a certification program? You should research the certification program's accreditation, reputation, and alignment with your career goals.
11. Large digital forensics labs should have at least two exits.
12. Typically, a(n) ________ lab has a separate storage area or room for evidence. Digital forensics lab.
13. Digital forensics facilities always have windows. False.
14. Evidence storage containers should have several master keys. False.
15. A forensic workstation should always have a direct broadband connection to the Internet. False.
16. Which organization provides good information on safe storage containers? National Institute of Standards and Technology (NIST).
17. Which organization has guidelines on how to operate a digital forensics lab? National Institute of Justice (NIJ).
18. What term refers to labs constructed to shield EMR emissions? Faraday cages.


# 3 - Data Acquisition

<!--
## Storage formats for Evidence
## Determine the best acquisition method
## Contingency planning for images
## Using tools
## Validating acquisitions
## Using remote acquisitions
## Using other acquisitions tools
-->
- Forensics data acquisitions are stored in three different formats: raw, proprietary, and AFF. Most proprietary formats and AFF store metadata about the acquired data in the image file.
- The four methods of acquiring data for forensics analysis are disk-to-image file, disk-to-disk copy, logical disk-to-disk or disk-to-data file, and sparse data copy of a folder or file.
- Lossless compression for forensics acquisitions doesn’t alter the data when it’s restored, unlike lossy compression. Lossless compression can compress up to 50% for most data. If data is already compressed on a drive, lossless compression might not save much more space.
- If there are time restrictions or too much data to acquire from large drives or RAID drives, a logical or sparse acquisition might be necessary. Consult with your lead attorney or supervisor first to let them know that collecting all the data might not be possible.
- You should have a contingency plan to ensure that you have forensically sound acquisition and make two acquisitions if you have enough data storage. The first acquisition should be compressed, and the second should be uncompressed. If one acquisition becomes corrupt, the other one is available for analysis.
- Write-blocking devices or utilities must be used with GUI acquisition tools in both Windows and Linux. Practice with a test drive rather than suspect drive, and use a hashing tool on the test drive to verify that no data was altered.
- Always validate your acquisition with built-in tools from a forensics acquisition program, a hexadecimal editor with MD5 or SHA-1 hashing functions, or the Linux md5sum or sha1sum commands.
- A Linux Live CD, such as Ubuntu, openSUSE, Arch Linux, Fedora, or Slackware provides many useful tools for digital forensics acquisitions.
- The preferred Linux acquisition tool is dcfldd instead of dd because it was designed for forensics acquisition. The dcfldd tool is also available for Windows. Always validate the acquisition with the hashing features of dcfldd and md5sum or sha1sum.
- When using the Linux dd or dcfldd commands, remember that reversing the output field (of=) and input field (if=) of suspect and target drives could write data to the wrong drive, thus destroying your evidence. If available, you should always use a physical write-blocker device for acquisitions.
- To acquire RAID disks, you need to determine the type of RAID and which acquisition tool to use. With a firmware- hardware RAID, acquiring data directly from the RAID server might be necessary.
- Remote network acquisition tools require installing a remote agent on the suspect computer. The remote agent can be detected if suspects install their own security programs, such as a firewall.

### Q/A
1. What’s the main goal of a static acquisition?
   - Answer: The main goal of a static acquisition is to create a bit-for-bit copy of the digital evidence in its original state without altering the original data.

2. Name the three formats for digital forensics data acquisitions.
   - Answer: The three formats for digital forensics data acquisitions are raw format, proprietary format, and logical format.

3. What are two advantages and disadvantages of the raw format?
   - Answer: Advantages:
     - Raw format preserves all data including deleted files and unallocated space.
     - It is universally compatible with forensic tools.
   - Disadvantages:
     - Large file size.
     - Does not include metadata, making analysis more challenging.

4. List two features common with proprietary format acquisition files.
   - Answer: Two common features with proprietary format acquisition files are compression to reduce file size and inclusion of metadata for better organization and analysis.

5. Of all the proprietary formats, which one is the unofficial standard?
   - Answer: The EnCase proprietary format is considered the unofficial standard in digital forensics.

6. Name two commercial tools that can make a forensic sector-by-sector copy of a drive to a larger drive.
   - Answer: Two commercial tools capable of making a forensic sector-by-sector copy are EnCase and FTK (Forensic Toolkit).

7. What does a logical acquisition collect for an investigation?
   - Answer: A logical acquisition collects only specific files and data relevant to the investigation, such as documents, emails, and user-generated content.

8. What does a sparse acquisition collect for an investigation?
   - Answer: A sparse acquisition collects only allocated data, ignoring unallocated space and deleted files.

9. What should you consider when determining which data acquisition method to use?
   - Answer: Factors to consider include the type of investigation, the nature of the digital evidence, legal requirements, available resources, and the capabilities of forensic tools.

10. Why is it a good practice to make two images of a suspect drive in a critical investigation?
    - Answer: Making two images provides redundancy and ensures data integrity. If one image becomes corrupted or compromised, the second one serves as a backup.

11. When you perform an acquisition at a remote location, what should you consider to prepare for this task?
    - Answer: Considerations include network stability, bandwidth availability, legal permissions, security protocols, and ensuring the remote system is not tampered with during acquisition.

12. With newer Linux kernel distributions, what happens if you connect a hot-swappable device, such a USB drive, containing evidence?
    - Answer: The device may be automatically mounted, potentially altering metadata and timestamps. It's crucial to disable auto-mounting or use write-blocking hardware.

13. In Linux, the fdisk -l command lists the suspect drive as /dev/hda1. Is the following dcfldd command correct? dcfldd if=image_file.img of=/dev/hda1
    - Answer: No, the command is incorrect. It should specify a partition (e.g., /dev/hda1) rather than the entire disk (/dev/hda) to avoid overwriting partition tables.

14. What’s the most critical aspect of digital evidence?
    - Answer: The most critical aspect of digital evidence is ensuring its integrity throughout the entire forensic process, from acquisition to analysis and presentation in court.

15. What’s a hashing algorithm?
    - Answer: A hashing algorithm is a cryptographic function that converts input data into a fixed-size string of characters, called a hash value or digest. It's used to verify data integrity and authenticity.

16. In the Linux dcfldd command, which three options are used for validating data?
    - Answer: The three options used for validating data in the dcfldd command are hash (hashing), hof (hash output file), and verify (verification).

17. What’s the maximum file size when writing data to a FAT32 drive?
    - Answer: The maximum file size when writing data to a FAT32 drive is 4 GB minus 1 byte.

18. What are two concerns when acquiring data from a RAID server?
    - Answer: Two concerns when acquiring data from a RAID server are ensuring proper handling of RAID configurations and dealing with data striping and redundancy across multiple disks.

19. With remote acquisitions, what problems should you be aware of? (Choose all that apply.)
    - Answer: Problems to be aware of include:
      - a. Data transfer speeds
      - b. Access permissions over the network
      - c. Antivirus, antispyware, and firewall programs

20. Which forensics tools can connect to a suspect’s remote computer and run surreptitiously?
    - Answer: Remote access tools like Netcat and Meterpreter can connect to a suspect's remote computer and execute commands or gather information without detection.

21. EnCase, FTK, SMART, and ILookIX treat an image file as though it were the original disk. True or False?
    - Answer: True. EnCase, FTK, SMART, and ILookIX treat an image file as though it were the original disk, allowing investigators to analyze the data without altering the original evidence.

22. FTK Imager can acquire data in a drive’s host protected area. True or False?
    - Answer: True. FTK Imager can acquire data from a drive's host protected area, which contains system files and configurations not accessible through traditional file system methods.

# 5 - Working with Windows & CLI systems
## Understanding Filesystems
- Boot sequence
	- BIOS/EFI at the hardware level
		- BIOS is for x86, typically used with MBR configured drives
		- EFI is for x64, typically used with GPT configured drives
- Understanding drives at the hardware level
	- Head - Two per platter, perform r/w operations
	- Tracks - Concentric circles holding sectors. Index from 0
	- Cylinder - Column of tracks i.e. 5th track on the top and bottom face of a platter is the 5th cylinder
	- Sector - Section on a track, min size of 512 bytes
- CHS (Cylinder, Head, Sector) calculations
	- Determine total number of addressable bytes
		- numOfCylinders \* numOfHeads(Tracks) \* numOfSectors => Total number of sectors available
		- For example: Drive has 1024 cylinders, 32 heads and 63 sectors
			- 1024 \* 32 \* 63 = 2,064,384 sectors
			- Total number of sectors \* 512 bytes per sector = 1.056 GB
- Wear-Levelling
	- SSDs cells are designed to handle 10k to 100k r/w operations
	- Wear levelling shifts data to less used cells to improve drive health
	- Bad for forensics as it modifies data that would've stayed in a HDD
## Exploring Microsoft file structures
- Clusters, logically grouped sectors, can range from 512bytes to 32kbytes in size
	- Numbered sequentially in LBA
		- 0 in NTFS
		- 2 in FAT
- Partition Table is in MBR
	- Located at sector 0
- Examining FAT
	- FAT12, floppy disk version, max size = 16mb
	- FAT16, Used till win95, max size = 4gb
	- FAT32, used for drives bigger than 2gb, max size = 2tb
	- exFAT
- Deleting FAT
	- Insert 0xE5 at the start of the filename
	- Set FAT chain of file to 0
- Drive slack
	- unused space in a cluster at the end of an active file and the end of the cluster
	- inlcudes Ram Slack and File Slack
## NTFS
- Everything is a file
	- Sector 0 is now the Partition Boot Sector, can expand to 16 sectors
	- MFT is next
	- Cluster size min is 4kb
-
## Whole disk encryption
## Windows Registry
## Startup Tasks

## Q/A

1. On a Windows system, sectors typically contain how many bytes?
   - Answer: b. 512 bytes

2. What does CHS stand for?
   - Answer: CHS stands for Cylinder-Head-Sector, a method used to address individual sectors on a disk drive.

3. Zone bit recording is how disk manufacturers ensure that a platter’s outer tracks store as much data as possible. True or False?
   - Answer: True.

4. Areal density refers to which of the following?
   - Answer: c. Number of bits per square inch of a disk platter

5. Clusters in Windows always begin numbering at what number?
   - Answer: Clusters in Windows always begin numbering at cluster number 2.

6. How many sectors are typically in a cluster on a disk drive?
   - Answer: c. 4 or more sectors.

7. List three items stored in the FAT database.
   - Answer: Three items stored in the FAT database are:
     - File allocation table entries
     - Cluster status (such as free or allocated)
     - Volume label

8. What does the Ntuser.dat file contain?
   - Answer: The Ntuser.dat file contains the user's specific configuration settings and preferences for their user profile in Windows.

9. In FAT32, a 123 KB file uses how many sectors?
   - Answer: In FAT32, a 123 KB file typically uses 4 sectors.

10. What is the space on a drive called when a file is deleted? (Choose all that apply.)
    - Answer: b. Unallocated space

11. List two features NTFS has that FAT does not.
    - Answer: Two features NTFS has that FAT does not are:
      - Support for file permissions and access control lists (ACLs)
      - Journaling for improved file system consistency and crash recovery.

12. What does MFT stand for?
    - Answer: MFT stands for Master File Table, a database in NTFS that stores information about all files and directories on a volume.

13. In NTFS, files smaller than 512 bytes are stored in the MFT. True or False?
    - Answer: False. In NTFS, files smaller than or equal to 512 bytes are stored within the MFT itself, not in separate clusters.

14. In Windows 7 and later, how much data from RAM is loaded into RAM slack on a disk drive?
    - Answer: In Windows 7 and later, 64 KB of data from RAM is loaded into RAM slack on a disk drive.

15. What’s a virtual cluster number?
    - Answer: A virtual cluster number is a logical cluster number that represents the location of a file or folder within the file system, independent of the physical layout of the disk.

16. Why was EFI boot firmware developed?
    - Answer: EFI (Extensible Firmware Interface) boot firmware was developed to replace the legacy BIOS (Basic Input/Output System) firmware, providing support for modern hardware features, larger disk sizes, and faster boot times.

17. Device drivers contain what kind of information?
    - Answer: Device drivers contain information required for the operating system to communicate with and control hardware devices.

18. Which of the following Windows 8 files contains user-specific information?
    - Answer: b. Ntuser.dat

19. Virtual machines have which of the following limitations when running on a host computer?
    - Answer: c. Virtual machines are limited to the host computer’s peripheral configurations, such as mouse, keyboard, CD/DVD drives, and other devices.

20. An image of a suspect drive can be loaded on a virtual machine. True or False?
    - Answer: True.

21. EFS can encrypt which of the following?
    - Answer: a. Files, folders, and volumes

22. What happens when you copy an encrypted file from an EFS-enabled NTFS disk to a non-EFS disk or folder?
    - Answer: b. EFS protection is maintained on the file.