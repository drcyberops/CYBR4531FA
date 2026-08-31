# CYBR4531FA/6531

# CYBR 4531 FA - Malware Analysis Repository

Welcome to the course repository for CYBR 4531 FA. This repository serves as the distribution hub for students to access malware samples required for laboratory assignments, reverse engineering tasks, and behavioral analysis.

⚠️ **WARNING:** This repository contains live, dangerous malware samples. These files are intended strictly for educational and research purposes within a controlled environment. 

---

## 🔒 Important Security Notice & Password

To prevent accidental execution and block automated security software from removing the files, all malware samples are compressed inside password-protected ZIP archives.

* **ZIP Password:** `infected`
* **Handling Instructions:**
  * **Never** extract these files on your host operating system.
  * **Only** unzip and analyze these samples inside your designated, isolated virtual machine (VM) lab environment.
  * Ensure your VM network adapter is set to **Host-Only** or disconnected from the internet before extracting.

---

## 📂 Repository Contents

This repository hosts the following resources:

* **`/samples`**: Directories organized by lab assignment containing the password-protected `.zip` malware binaries.
* **`hashes.txt`**: A text file containing the SHA-256 and MD5 cryptographic hashes of all original samples to verify file integrity before analysis.

---

## 🚀 Student Quick Start

1. **Clone this repository** inside your secure analysis virtual machine:
   ```bash
   git clone https://github.com
   ```
2. **Navigate to the target lab folder**:
   ```bash
   cd CYBR4531FA/samples
   ```
3. **Extract the sample** using the password `infected`:
   ```bash
   unzip -P infected sample.zip
   ```

---

## 📋 Course Information

* **Course:** CYBR 4531 FA
* **Instructor:** Dr. Tony Rizi
