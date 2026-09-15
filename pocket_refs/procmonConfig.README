# Procmon Configuration File Notes

## Procmon Filter for Manual Dynamic Malware Analysis

This Procmon filter provides a **general-purpose starting point for manual dynamic malware analysis**.

The purpose of the filter is to reduce some of the normal Windows activity visible in **Process Monitor (Procmon)** while highlighting system behavior commonly examined when investigating suspicious or malicious software.

> **Note:** This configuration is intended as a starting point for analysis. It is not designed to identify every possible malware behavior.

---

## Filter Coverage

### Process and Memory Activity

Highlights process creation and termination, thread activity, image/DLL loading, and selected memory-related operations.

This activity can help identify:

* Child processes
* Unexpected process execution
* Dynamically loaded DLLs
* Process and thread activity
* Potential code injection or unusual memory behavior

---

### File-System Activity

Monitors file creation, modification, deletion, renaming, mapping, and resizing.

Particular attention is given to executable and script file types commonly encountered during malware analysis, including:

```text
.exe
.dll
.bat
.cmd
.vbs
.vbe
.js
.jse
.wsf
.hta
.scr
.pif
```

These filters can help identify dropped payloads, scripts, configuration files, and other artifacts created during execution.

---

### Common Malware Drop Locations

Highlights activity in directories frequently used for temporary files, staging, or payload storage.

Examples include:

```text
\AppData\Local\Temp
\Windows\Temp
\ProgramData
\Users\Public
```

Files appearing in these locations are **not automatically malicious**, but unexpected activity in these directories may warrant additional investigation.

---

### Registry Persistence

Monitors several Windows Registry locations commonly associated with persistence and automatic execution.

Examples include:

```text
Run
RunOnce
RunOnceEx
Services
Winlogon
Active Setup
Shell Folders
User Shell Folders
Image File Execution Options (IFEO)
```

Monitoring these locations can help identify attempts to execute malware after reboot, user logon, or other system events.

---

### Security Evasion

Highlights registry activity involving Windows security configuration, including areas associated with:

* Microsoft Defender
* Windows security policies
* Local Security Authority (LSA)
* Security Providers
* Explorer policies
* System policies

Changes to these locations may indicate attempts to disable, weaken, or modify Windows security controls.

---

### COM Hijacking and File Associations

Monitors registry locations associated with Windows COM objects and file associations, including:

```text
CLSID
Interface
TypeLib
.exe
exefile
.dll
```

Malware may abuse these locations to redirect program execution, establish persistence, or cause malicious code to execute when legitimate applications are launched.

---

### Registry Modification

Captures important registry modification operations, including:

```text
RegCreateKey
RegSetValue
RegDeleteValue
RegDeleteKey
RegLoadKey
```

These operations provide visibility into configuration changes made by a sample during execution.

---

### Drivers and System Locations

Highlights activity involving important Windows system locations and artifacts, including:

```text
\System32\drivers
\SysWOW64\drivers
\Windows\System32\tasks
\Windows\System32\wbem
\drivers\etc\hosts
```

The filter also monitors `.lnk` shortcut files.

These locations may be relevant when investigating drivers, scheduled tasks, WMI-related activity, persistence, or modification of hostname resolution.

---

### Network Activity

Monitors selected network operations, including:

```text
TCP Connect
TCP Send
UDP Send
```

Additional filters highlight activity associated with common network ports:

|  Port | Protocol/Service |
| ----: | ---------------- |
|  `53` | DNS              |
|  `80` | HTTP             |
| `443` | HTTPS            |

This activity may help identify:

* DNS queries
* Command-and-control (C2) connections
* Payload downloads
* External communications
* Potential data exfiltration

Procmon should **not replace Wireshark or another network-analysis tool** when detailed packet-level analysis is required.

---

### Credential and Browser Data

Highlights access to potentially sensitive Windows and browser locations, including:

```text
\config\SAM
\config\SECURITY
\AppData\Local\Google\Chrome\User Data
\AppData\Roaming\Mozilla\Firefox\Profiles
```

Unexpected access to these locations may warrant further investigation for credential access, browser-data collection, or information-stealing behavior.

---

### Ransomware Indicators

Includes selected filters intended to highlight possible ransomware-related activity, such as:

* Ransom-note creation
* `.README` files
* Writes to `.txt` files
* `.crypto` files
* `.locked` files

These indicators alone **do not establish that ransomware is executing**. They should be correlated with broader file-system behavior, such as large numbers of file modifications or renames.

---

### System Anomalies

The configuration includes events returning:

```text
ACCESS DENIED
```

These events can sometimes reveal attempted access to protected:

* Files
* Directories
* Registry keys
* Processes
* System resources

`ACCESS DENIED` is common during normal Windows operation and should therefore be treated as investigative context rather than an indicator of compromise by itself.

---

## Important Limitations

This filter is **not a catch-all malware detection solution**.

It will not identify every technique used by malware, and legitimate Windows applications may generate many of the same events. The presence of an event in the filtered Procmon results **does not automatically mean the activity is malicious**.

The configuration should instead be treated as a **baseline for manual investigation**.

Analysts should correlate Procmon observations with evidence collected from other dynamic-analysis tools, such as:

* Process Explorer or Process Hacker
* Regshot
* Wireshark
* INetSim
* ProcDOT

Filters should also be **modified as necessary for the specific malware sample being investigated**.

---

## Recommended Workflow

A basic workflow for using this configuration is:

1. Start from a clean analysis VM or snapshot.
2. Load the Procmon filter configuration.
3. Clear existing Procmon events.
4. Begin capturing activity.
5. Execute or detonate the malware sample using the appropriate lab procedure.
6. Allow the sample sufficient time to exhibit behavior.
7. Stop the Procmon capture.
8. Review processes, files, registry activity, and network events.
9. Correlate Procmon findings with Regshot, Wireshark, Process Explorer/Process Hacker, INetSim, and other analysis evidence.
10. Add or modify Procmon filters when additional behavior requires investigation.

---

## Final Note

**A filter helps reduce noise; it does not replace analysis.**

Malware behavior varies considerably between samples. Use this Procmon configuration to identify areas that deserve closer investigation, then pivot into the relevant processes, files, registry keys, network connections, and other artifacts to determine what the sample actually did.
