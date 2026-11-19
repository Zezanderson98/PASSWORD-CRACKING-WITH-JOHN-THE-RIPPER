[johnny_2.2_win.zip](https://github.com/user-attachments/files/35099350/johnny_2.2_win.zip)
# NETWORKWALKS-B084-WK3-PM1-PASSWORD-CRACKING-WITH-JTR



<div align="center">

# 🔐 Penetration Testing Lab : Password Cracking with JTR

**Extracting Cryptographic PDF Hashes & Auditing Password Strength with John the Ripper and Johnny GUI**
</div>

<p align="center">
<img width="118" height="20" alt="image" src="https://github.com/user-attachments/assets/c7f8b072-f2a5-445f-b741-8e9b5ae3d638" />
<img width="99" height="20" alt="image" src="https://github.com/user-attachments/assets/b2ad8ab5-760b-4c0e-904f-6325e0ad06fd" />
<img width="141" height="20" alt="image" src="https://github.com/user-attachments/assets/1632e17a-962d-49e7-8280-0eccf09403b1" />
<img width="71" height="20" alt="image" src="https://github.com/user-attachments/assets/ba32250a-4556-4c8a-ba4e-76547de2b868" />
<img width="119" height="20" alt="image" src="https://github.com/user-attachments/assets/b1ee05d4-585b-4232-bc86-4e86c2a0e487" />
<img width="206" height="20" alt="image" src="https://github.com/user-attachments/assets/8ab5649f-5bd5-4218-b7b6-e291ca97bfb4" />
<img width="154" height="20" alt="image" src="https://github.com/user-attachments/assets/70a0d8e7-a2be-44e9-b27e-416da91c97d3" />
<img width="171" height="20" alt="image" src="https://github.com/user-attachments/assets/6bb56a6b-63b0-42a8-b92e-2d554e4044d7" />






## 📌 Project Overview
This project demonstrates how to audit and recover lost or weak passwords from encrypted PDF documents using **John the Ripper (JTR)** and its graphical user interface, **Johnny**. Originally developed for Unix systems, John the Ripper is a widely used open-source password security auditing and recovery tool capable of cracking various hash formats and password-protected files such as PDFs, ZIP archives, and Office documents on Windows, Linux, and macOS.

---

## 🎯 Purpose of the Lab
The purpose of this laboratory exercise is to simulate real-world password auditing in a controlled environment. By extracting cryptographic hashes from a locked PDF file and running automated dictionary/rule-based attacks, this lab demonstrates how weak passwords expose sensitive files to unauthorized access and reinforces the need for strong authentication controls.

---

## 🚀 Objectives
* **Understand Password Auditing:** Learn how security professionals evaluate password strength and recover access to protected files.
* **Differentiate Encryption vs. Hashing:** Distinguish between reversible two-way encryption and irreversible one-way cryptographic hashing.
* **Hash Extraction:** Extract cryptographic password hashes (`$pdf$...`) from an encrypted PDF file (`My Locked PDF1.pdf`).
* **GUI-Assisted Cracking:** Configure and execute a password cracking attack using Johnny GUI linked to the core `john.exe` binary.
* **Security Awareness:** Identify vulnerabilities caused by low-entropy passwords and implement effective defensive mitigations.

---

## 🏗️ Lab Architecture & Environment
* **Operating System:** Windows PC (or Kali Linux workstation with pre-installed JTR)
* **Core Cracking Engine:** John the Ripper (`v1.9.0-jumbo-1` Windows binaries)
* **Graphical Interface:** Johnny GUI (`v2.2`)
* **Hash Extraction Utility:** Online Hash Crack PDF Hash Extractor (`pdf2john` web utility)
* **Target Asset:** `My Locked PDF1.pdf` (Password-protected PDF document)

```mermaid
flowchart LR
    A[Encrypted PDF<br/>My Locked PDF1.pdf] -->|Upload File| B[PDF Hash Extractor<br/>pdf2john]
    B -->|Extract pdf Hash| C[Hash File<br/>hash1.txt]
    C -->|Load Target Hash| D[Johnny GUI v2.2]
    E[John the Ripper CLI<br/>john.exe] <-->|Backend Engine| D
    D -->|Dictionary / Rule Attack| F[Recovered Plaintext Password<br/>password1]
    F -->|Unlock Document| G[Access Granted / Flag Captured]
```

---

## 🛠️ Step-by-Step Lab Tasks

### 1. Download John the Ripper (CLI)
* Download the Windows binaries for **John the Ripper** from the official Openwall website <https://www.openwall.com/john/> or the Openwall distribution archive.
* Extract the downloaded archive to a local folder on your PC.




<img width="1366" height="768" alt="1_John the Ripper Download" src="https://github.com/user-attachments/assets/75052598-2fe2-4b08-a521-c18080a90e26" />







<img width="1366" height="768" alt="11_Extract John jumbo" src="https://github.com/user-attachments/assets/afe6abc5-8e15-4889-9f8d-02ac184ef4d7" />








### 2. Download and Install Johnny (GUI)
* Download the **Johnny GUI** installer (`johnny_2.2_win.zip` / `johnnyInstaller.exe`) from the Openwall wiki <https://openwall.info/wiki/john/johnny>.
* Run `johnnyInstaller.exe` and complete the installation wizard.





<img width="1360" height="765" alt="2_Jonny GUI Download" src="https://github.com/user-attachments/assets/2e1127d2-2e09-4b37-9f00-5af907efc170" />




<img width="1366" height="736" alt="3_Jonny Setup" src="https://github.com/user-attachments/assets/f5b63f94-0a84-4512-833e-59291070e222" />


<img width="1365" height="768" alt="4_Johnny_Installation" src="https://github.com/user-attachments/assets/2d649cc1-a95b-4d61-9dfb-aeec92c9c429" />




<img width="1366" height="768" alt="5_Johnny components" src="https://github.com/user-attachments/assets/cbaa3eec-5159-4d20-945b-6c86a1bc263a" />





<img width="1366" height="768" alt="6_Johnny Start menu shortcut" src="https://github.com/user-attachments/assets/2beee7aa-21a5-4d2d-b960-9148daca741c" />






<img width="1366" height="767" alt="7_Jonny Ready to  install" src="https://github.com/user-attachments/assets/d7d6bc3c-299c-411d-8cb2-c22c39835686" />




<img width="1366" height="768" alt="8_Johnny installation finish" src="https://github.com/user-attachments/assets/36d805e4-c76b-4390-b741-e20aef45c882" />










### 3. Link Johnny GUI to `john.exe`
* Launch **Johnny** from your desktop or Start menu.
* Navigate to the **Settings** tab on the left panel.
* Click **Browse** next to the *John the Ripper executable* field.
* Locate and select `john.exe` inside the extracted JTR `run` folder (e.g., `.../john-1.9.0-jumbo-1-win64/run/john.exe`).
* Verify that Johnny displays the detected JTR version.



<img width="1366" height="768" alt="9_Johnny open" src="https://github.com/user-attachments/assets/cde24c14-0c92-423f-bf4a-da83b0de1999" />



<img width="1366" height="768" alt="13_Select john exe" src="https://github.com/user-attachments/assets/5d438abd-c881-42f4-b7f7-b1fc355f3417" />


<img width="1366" height="768" alt="14_john exe in the executable john the ripper fieled" src="https://github.com/user-attachments/assets/c8b851f5-9afb-4863-9643-b2dcfdc99fc7" />



### 4. Extract the Hash from the Protected PDF
* Open your browser and navigate to the <https://onlinehashcrack.com>
* Click **Browse**, select the target encrypted file (`My Locked PDF1.pdf`), and click **Upload**.
* Copy the generated hash output string starting with `$pdf$...`.
  > **Note:** Ensure no extra characters (such as `b'` at the beginning or trailing quotes) are copied.

<img width="1366" height="762" alt="15_open hash website upload pdf file" src="https://github.com/user-attachments/assets/394a3f5e-b9ee-4d86-9afd-007f71fbf31d" />

<img width="1365" height="768" alt="16_selecting pdf1 file" src="https://github.com/user-attachments/assets/10228d53-fe2c-482d-b50b-e7c9f3917e3e" />


<img width="1366" height="768" alt="17_sucessful pdf1 upload on hash website" src="https://github.com/user-attachments/assets/c869571a-e1ad-4abd-9877-7368b4dbf472" />

<img width="1363" height="768" alt="18_pdf output" src="https://github.com/user-attachments/assets/ac902741-9a01-4ba0-8c62-0d031cb66422" />


<img width="1365" height="768" alt="19_pdf1 output copy" src="https://github.com/user-attachments/assets/2206a57c-0c05-4da2-907e-fa5ab421f680" />





### 5. Save the Hash to a Text File
* Open **Notepad** on your Windows PC.
* Paste the copied `$pdf$...` hash string into the blank document.
* Go to **File > Save As** and save the file as `hash1.txt`.



<img width="1366" height="768" alt="20_open notepad" src="https://github.com/user-attachments/assets/5bb791bb-87af-42fc-bd30-a4c5db5822b3" />




<img width="1366" height="761" alt="21_paste pdf1 output on notepad" src="https://github.com/user-attachments/assets/5b483ac0-46fe-423b-8bc5-28ef0cd2f13d" />



<img width="1366" height="741" alt="22_pdf1 output pasted on notepad" src="https://github.com/user-attachments/assets/983ce671-047b-410a-8fa4-d61d07aa0b08" />





<img width="1360" height="758" alt="23_save pdf1 output" src="https://github.com/user-attachments/assets/a1cc74ad-58fc-4484-a437-2337d8b31fa6" />



<img width="1366" height="768" alt="24_save as hash1 txt" src="https://github.com/user-attachments/assets/ebf098f6-59e9-47ce-ba14-afb195f021b8" />








### 6. Load the Hash File into Johnny
* Return to the **Johnny** application.
* Click **Open password file** on the top toolbar.
* Browse to your saved `hash1.txt` file and click **Open**.







<img width="1366" height="767" alt="25_open johnny again" src="https://github.com/user-attachments/assets/3c273468-4987-43c1-9c1e-f6fda37dfa7f" />


<img width="1360" height="767" alt="26_click on open password file" src="https://github.com/user-attachments/assets/f1d199a6-53a6-4669-a6f5-39002fa5d782" />







<img width="1366" height="768" alt="27_browse to hash1 file click open" src="https://github.com/user-attachments/assets/a798b436-33e3-4127-a2c4-adaefbb96e07" />










### 7. Execute the Password Cracking Attack
* Click **Start new attack** on the top toolbar.
* Wait for JTR to process the hash against its built-in wordlist and mangling rules.
* Once completed (`100%`), the recovered plaintext password (`good-luck`) will appear in the **Password** column.





<img width="1366" height="767" alt="28_click on start new attack" src="https://github.com/user-attachments/assets/7fedea51-7080-4a01-bf0d-153c8c4dd91a" />






<img width="1364" height="768" alt="29_pdf1 cracked sucessful" src="https://github.com/user-attachments/assets/7e44a17c-003d-4c61-bd7e-d8691825207b" />



### 8. Verify Access to the Encrypted PDF
* Double-click `My Locked PDF1.pdf` to open it in your PDF reader.
* Enter the cracked password (`good-luck`) when prompted.
* Confirm the document unlocks and displays the flag/contents.







<img width="1360" height="699" alt="30_open encrypted pdf file" src="https://github.com/user-attachments/assets/b166540c-2ac2-4048-b1b3-c9bf83a5e95a" />



<img width="1366" height="768" alt="31_enter good-luck" src="https://github.com/user-attachments/assets/0eeb7b76-0bfa-4cec-bd30-e3ac109b9bcb" />








<img width="1312" height="728" alt="32_flag captured sucessfully" src="https://github.com/user-attachments/assets/e41174d0-2c52-4d5c-87b4-5b5bc392aa63" />






---


## 📂 Repository Structure

```text
Password-Cracking-With-JTR/
├── README.md                                              # Project documentation, Mermaid architecture & step-by-step walkthrough
├── hashes/
│   └── hash1.txt                                          # Extracted cryptographic PDF hash (\(pdf\)...)
├── target/
│   └── My Locked PDF1.pdf                                 # Encrypted PDF file audited in the lab
└── screenshots/
    ├── task-01-download-jtr/
    │   ├── 01_john_the_ripper_download.png                # Downloading JTR Windows binaries from Openwall
    │   └── 02_extract_john_jumbo.png                      # Extracting john-1.9.0-jumbo-1-win64 archive
    ├── task-02-install-johnny-gui/
    │   ├── 03_johnny_gui_download.png                     # Downloading Johnny v2.2 Windows installer
    │   ├── 04_johnny_setup_welcome.png                    # Launching Johnny setup wizard
    │   ├── 05_johnny_installation_license.png             # Accepting installation terms
    │   ├── 06_johnny_components.png                       # Selecting Johnny installation components
    │   ├── 07_johnny_start_menu_shortcut.png              # Configuring Start Menu shortcut
    │   ├── 08_johnny_ready_to_install.png                 # Confirming installation settings
    │   └── 09_johnny_installation_finish.png              # Completing Johnny GUI installation
    ├── task-03-link-john-executable/
    │   ├── 10_johnny_open.png                             # Opening Johnny GUI interface
    │   ├── 11_select_john_exe.png                         # Browsing to john.exe inside JTR run folder
    │   └── 12_john_exe_linked_in_settings.png             # Verifying detected JTR version in Settings
    ├── task-04-extract-pdf-hash/
    │   ├── 13_open_hash_website_upload_pdf.png            # Navigating to Online Hash Crack PDF extractor
    │   ├── 14_selecting_pdf1_file.png                     # Selecting My Locked PDF1.pdf for upload
    │   ├── 15_successful_pdf1_upload.png                  # Uploading encrypted PDF to hash extractor
    │   ├── 16_pdf_hash_output.png                         # Generating cryptographic \(pdf\) hash string
    │   └── 17_pdf1_hash_output_copy.png                   # Copying clean \(pdf\) hash string
    ├── task-05-save-hash-to-file/
    │   ├── 18_open_notepad.png                            # Opening Windows Notepad
    │   ├── 19_paste_pdf1_output_notepad.png               # Pasting extracted hash into Notepad
    │   ├── 20_pdf1_output_pasted_verified.png             # Verifying no extra characters exist
    │   ├── 21_save_pdf1_output_dialog.png                 # Opening Save As dialog
    │   └── 22_save_as_hash1_txt.png                       # Saving hash file as hash1.txt
    ├── task-06-load-hash-in-johnny/
    │   ├── 23_open_johnny_again.png                       # Returning to Johnny GUI
    │   ├── 24_click_open_password_file.png                # Clicking Open password file on toolbar
    │   └── 25_browse_to_hash1_txt_open.png                # Loading hash1.txt into Johnny session
    ├── task-07-execute-cracking-attack/
    │   ├── 26_click_start_new_attack.png                  # Starting JTR dictionary/rule attack
    │   └── 27_pdf1_cracked_successful.png                 # Password cracked (good-luck) at 100%
    └── task-08-verify-pdf-access/
        ├── 28_open_encrypted_pdf_file.png                 # Opening My Locked PDF1.pdf in PDF reader
        ├── 29_enter_cracked_password_good_luck.png        # Entering recovered password (good-luck)
        └── 30_flag_captured_successfully.png              # PDF unlocked and flag captured
```
















## 🧠 Key Takeaways & Defensive Mitigations
* **Encryption vs. Hashing:** Encryption is a reversible two-way function requiring a decryption key, whereas hashing is a one-way mathematical function producing a unique message digest.
* **Vulnerability of Weak Passwords:** Simple dictionary words or predictable patterns (like `password1`) can be cracked within seconds once a file's hash is extracted.
* **Strong Password Policies:** Enforce high-entropy passwords (14+ characters combining uppercase, lowercase, numbers, and special symbols) to resist dictionary and brute-force attacks.
* **Modern Encryption Standards:** Protect sensitive documents using strong encryption algorithms (such as AES-256) and avoid uploading confidential files to third-party online hash extractors in real-world scenarios—prefer local utilities like `pdf2john.pl` or `pdf2john.py`.

---

## 🔐 Security & Ethical Use
This laboratory and repository are intended strictly for educational and authorized research purposes only. All password auditing activities were conducted within the authorized <https://networkwalks.com> lab scope. Unauthorized cracking or exploitation of external files and systems is illegal.

## 🔗 Tools & Resources
* **Primary Environment:** Windows PC / Kali Linux Workstation <https://networkwalks.com> Week 3 | Project Module 1)
* **Cracking & Extraction Suite:** `John the Ripper (JTR)`, `Johnny GUI`, `pdf2john`
* **Official Documentation:** [Openwall John the Ripper](https://openwall.com) | [Kali Linux Tools Reference](https://kali.org)

## 👤 Author
**Anderson Edaiyo Uzezi**  
Cybersecurity Professional B084  
LinkedIn: https://linkedin.com

