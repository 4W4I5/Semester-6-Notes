| Chapter                                                                     | Status    |
| --------------------------------------------------------------------------- | --------- |
| Smart Watch Forensics - Lec 20                                              | :warning: |
| Mobile Forensics  - Lec 16                                                  | :warning: |
| Cloud Forensics - Lec 13                                                    | :warning: |
| Digital Forensics Analysis & Validation (Anti-Forensics Techniques) - Lec 9 | :warning: |
| Report Writing - Lec 16                                                     | :warning: |
| Assignment 1: Laws + Policies                                               | :warning: |
| Assignment 2: Android Forensics                                             | :warning: |
| Assignment 3: MFT + NTFS + ADS                                              | :warning: |
| Assignment 4: Dark Web Forensics                                            | :warning: |
| Assignment 5: Python code to read MBR                                       | :warning: |
| Assignment 6: Timeline Analysis using TSK                                   | :warning: |

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

---
# Cloud Forensics (Lec 13)
---
# Digital Forensics Analysis & Validation (Anti-Forensics Techniques) (Lec 9)
---
# Report Writing (Lec 14)
---
# Assignments
## Assignment 1: Laws + Policies
## Assignment 2: Android Forensics
## Assignment 3: MFT + NTFS + ADS
- **ADS**
	- Commands
		- Create ADS on text.txt -> `echo hidden > text.txt:ads.txt`
		- Read ADS on text.txt -> `more < text.txt:ads.txt`
		- Executing DLL via ADS -> `rundll32 test.txt:malicious.dll,EntryPoint`
			- To view contents -> `more < test.txt:malicious.dll`
## Assignment 4: Dark Web Forensics
## Assignment 5: Python Code to read MBR
## Assignment 6: Timeline Analysis using TSK