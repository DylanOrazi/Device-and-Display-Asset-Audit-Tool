PROJECT NAME: Device Display Asset Audit Tool 

MAIN FEATURES

- Local Windows computer scanning
- No domain connection required
- No remote computer access required
- No administrative rights check required
- Detailed console output
- Automated hardware and inventory warnings
- Overall audit status calculation
- Timestamped TXT report generation
- Automatic report folder creation
- Safe handling of missing hardware information
- Previous reports are preserved instead of overwritten

DEVICE IDENTIFICATION

The tool collects:

- Computer name
- Logged-in user
- Manufacturer
- Model
- System SKU or model number
- Serial number
- Chassis type
- Domain or workgroup information

PROCESSOR INFORMATION

The tool collects:

- Processor name
- Manufacturer
- Processor description
- Maximum clock speed
- Number of cores
- Number of logical processors
- Socket designation
- Processor architecture
- 64-bit processor support
- Number of installed processors

MEMORY INFORMATION

The tool collects:

- Total installed memory
- Total memory in gigabytes
- Number of memory modules
- Memory slot information
- Module manufacturer
- Module capacity
- Memory speed
- Configured clock speed
- Memory type
- Part number
- Serial number

LOGICAL DRIVE INFORMATION

The tool collects:

- Drive letter
- Drive type
- Volume name
- File system
- Total capacity
- Used space
- Free space
- Free-space percentage

PHYSICAL DRIVE INFORMATION

The tool collects:

- Physical drive model
- Friendly name
- Serial number
- Media type
- Bus type
- Drive capacity
- Health status
- Operational status

BIOS INFORMATION

The tool collects:

- BIOS manufacturer
- BIOS name
- BIOS version
- SMBIOS version
- BIOS serial number
- Release date
- BIOS status

DISPLAY INFORMATION

The tool uses Windows Management Instrumentation and EDID data to detect available displays.

The tool collects:

- Display number
- Display manufacturer
- Display model
- Display serial number
- Manufacturing week
- Manufacturing year
- Approximate display size
- Active status
- Connection information
- Internal or external display information when available

Some built-in laptop displays may not provide a readable model or serial number. These unavailable values do not necessarily indicate a hardware failure.

WINDOWS INFORMATION

The tool collects:

- Windows edition
- Windows version
- Windows build number
- Operating system architecture
- Installation date
- Last boot time
- System uptime

BATTERY INFORMATION

The tool collects battery information when a battery is detected.

Collected information may include:

- Battery name
- Battery manufacturer
- Device ID
- Estimated charge percentage
- Battery status
- Design capacity
- Full-charge capacity
- Battery health percentage
- Battery health rating
- Battery cycle count

Some computers do not expose detailed battery information through Windows Management Instrumentation. In these cases, certain fields may display as Not available.

A BatteryStaticData warning may appear on computers whose hardware or firmware does not expose that WMI class. This warning does not necessarily indicate a battery problem.

NETWORK INFORMATION

The tool collects information from active IP-enabled network adapters.

Collected information includes:

- Adapter name
- Adapter description
- Connection status
- IPv4 address
- IPv6 address
- MAC address
- Default gateway
- DNS servers
- DHCP status
- Connected Wi-Fi SSID when available

AUTOMATED AUDIT WARNINGS

The tool automatically reviews the collected information and generates warnings for conditions such as:

- Missing device serial number
- Missing device manufacturer
- Missing device model
- Low logical-drive free space
- Physical-drive health concerns
- Low battery health
- Missing display model information
- Missing display serial number
- No detected display EDID information

Missing information does not always indicate defective hardware. Some manufacturers do not expose every inventory field through Windows.

OVERALL AUDIT STATUS

The tool calculates an overall audit status based on the number of generated warnings.

Passed: No automated warnings were found
Review Recommended: One or two warnings were found
Attention Required: Three or more warnings were found

The status is intended as an inventory review indicator. It is not a hardware diagnostic result by itself.

For example, missing model and serial information from a built-in laptop display may increase the warning count even when the display is functioning normally.

TXT REPORT GENERATION

After the scan completes, the tool creates a timestamped TXT report.

The report includes:

- Basic audit summary
- Device identification
- Windows information
- BIOS information
- Processor information
- Memory information
- Logical-drive information
- Physical-drive information
- Display information
- Battery information
- Network information
- Automated audit warnings
- Final audit status

Reports are stored in:

Reports\TXT

Example report filename:

COMPUTERNAME_DeviceAudit_2026-06-19_153000.txt

The timestamp prevents previous reports from being overwritten.

PROJECT FOLDER STRUCTURE

Device and Display Asset Audit Tool

DeviceDisplayAssetAudit.ps1
README.txt
Reports
TXT

REQUIREMENTS

- Windows 10 or Windows 11
- Windows PowerShell 5.1 or later
- Visual Studio Code or another text editor
- PowerShell execution permissions
- Local access to the computer being scanned

The tool does not require:

- A Windows domain
- Active Directory
- Remote PowerShell
- A database
- Microsoft Excel
- Power BI
- Internet access

HOW TO RUN

- Extract and Open the Device and Display Asset Audit Tool folder.
- Click the File Explorer address bar and type PowerShell
- Open the integrated PowerShell terminal.
- If script execution is blocked, run:

Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass

Run the script:

.\DeviceDisplayAssetAudit.ps1

Review the scan results in the PowerShell terminal.
Open the Reports\TXT folder to view the generated report.

EXECUTION POLICY NOTE

The Process execution-policy setting applies only to the current PowerShell session.

Closing the terminal returns the execution policy to its previous configuration.

ERROR HANDLING

The script uses safe data-collection methods to prevent unavailable WMI or CIM information from stopping the entire scan.

When information cannot be collected:

- The script continues running
- The affected field may display Not available
- A warning may be shown
- Other hardware sections are still collected
- The TXT report is still generated when possible

KNOWN LIMITATIONS

- The tool scans only the local Windows computer
- Remote scanning is not included
- Domain-based inventory collection is not included
- Some laptop displays do not expose model or serial information
- Some battery manufacturers do not expose capacity or cycle data
- Wi-Fi information depends on the availability of the Windows netsh command
- Hardware information depends on what the system manufacturer exposes through Windows
- The overall audit status is based on warning count rather than warning severity
- Missing inventory information may affect the status even when the hardware is functioning correctly

