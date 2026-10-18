# NETWORKWALKS-B083-WK4-MEDIROZA

# Mediroza General Hospital – Penetration Testing Lab

## 1. Project Overview

This project is part of my cybersecurity learning. In this lab, I explored common web application security vulnerabilities and learned how security misconfigurations can expose sensitive information.

I used Kali Linux to follow the steps in the provided lab solution and studied the findings and their possible security impacts.

**Target:** Mediroza General Hospital training environment  
**Operating System:** Kali Linux  
**Project Type:** Educational Penetration Testing Lab

## 2. Objectives

The main objectives of this project were:

- To understand the reconnaissance process.
- To learn about username enumeration and SQL injection.
- To understand password-protected PDF files and password testing.
- To examine PDF metadata.
- To identify risks caused by exposed directories and database backups.
- To understand how vulnerabilities can be fixed.
- To document the findings in a clear and organized way.

## 3. Tools Used

- **Kali Linux:** Operating system used for the lab.
- **Firefox:** Used to access the training website.
- **curl:** Used to retrieve the `robots.txt` file.
- **Networkwalks Hash Calculator:** Used to extract PDF password hashes.
- **Networkwalks Password Cracker:** Used to test PDF passwords against a wordlist.
- **ExifTool:** Used to inspect file metadata.
- **wget:** Used to download the SQL backup in the lab.
- **qpdf:** Used to create an unlocked copy of a PDF when the correct password was available.
- **Terminal:** Used to execute commands and inspect files.

## 4. Milestone 1 – Initial Access

### 4.1 Reconnaissance

I started by checking the website's `robots.txt` file. This file contained references to directories such as `/patient/`, `/staff/`, and `/old/`.

This helped me understand how reconnaissance can reveal useful information about a web application.

**Screenshot M1-01: robots.txt**

<img width="1920" height="923" alt="VirtualBox_kali-linux-2026 2-virtualbox-amd64_18_10_2026_19_21_29" src="https://github.com/user-attachments/assets/694d1acb-403e-4c38-a9bb-fda21b169ce0" />


### 4.2 Username Enumeration

I learned that different error messages can reveal whether a username exists.

For example, the training application returned different messages for an unknown username and an incorrect password.

This is a security weakness because it helps someone identify valid usernames.

<img width="1920" height="923" alt="VirtualBox_kali-linux-2026 2-virtualbox-amd64_18_10_2026_19_29_42" src="https://github.com/user-attachments/assets/b23a7596-2ae0-491c-9bcf-faaa0c0fa028" />

<img width="1920" height="923" alt="VirtualBox_kali-linux-2026 2-virtualbox-amd64_18_10_2026_19_25_45" src="https://github.com/user-attachments/assets/f74eb3ba-b467-488f-8cb1-44f9a07fabde" />

<img width="1920" height="923" alt="VirtualBox_kali-linux-2026 2-virtualbox-amd64_18_10_2026_19_24_20" src="https://github.com/user-attachments/assets/ba1f6be3-b5d5-447d-b6c2-dc9102d31271" />

### 4.3 SQL Injection

The lab demonstrated that unsafe handling of user input could cause a database query error. The login application was also vulnerable to a SQL injection login bypass in the authorized training environment.

This showed why user input must be handled securely.

<img width="1920" height="923" alt="VirtualBox_kali-linux-2026 2-virtualbox-amd64_18_10_2026_19_34_31" src="https://github.com/user-attachments/assets/b7c0b58f-2ed4-46b7-8002-d16a9d2dbe17" />


### 4.4 Patient Reports

After accessing the training portal, I located the three password-protected PDF reports.

This demonstrated the importance of enforcing proper access controls on sensitive files.

**Screenshot M1-04: Report Listing**

<img width="1920" height="923" alt="VirtualBox_kali-linux-2026 2-virtualbox-amd64_18_10_2026_19_33_55" src="https://github.com/user-attachments/assets/6163e02b-33c0-4679-b928-a5c667d4ab0d" />


## 5. Milestone 2 – Crack the Encryption

### 5.1 PDF Hash Extraction

I learned that password-protected PDF files can use encryption and that a suitable hash can be extracted for password testing.

The hash calculator was used to obtain the PDF password hashes.

**Screenshot M2-01: PDF Hash Extraction**

<img width="802" height="217" alt="Screenshot 2026-10-18 194202" src="https://github.com/user-attachments/assets/5de9554f-f91f-493e-93cb-a8697acd9a0c" />

<img width="722" height="227" alt="Screenshot 2026-10-18 194319" src="https://github.com/user-attachments/assets/1528942b-be2f-4903-b08c-e630eded3723" />

<img width="746" height="227" alt="Screenshot 2026-10-18 194309" src="https://github.com/user-attachments/assets/09bddf2a-3472-4e04-a603-09d6f2e2563a" />

### 5.2 Learning Outcome

This milestone helped me understand why weak passwords are easier to guess and why organizations should use strong, unique passwords.

## 6. Milestone 3 – Deep Reconnaissance

### 6.1 PDF Metadata

I learned that PDF files may contain metadata, such as author information and comments, that is not immediately visible when reading the document.

ExifTool can be used to inspect this information. The lab solution connected the PDF metadata to a note about an old backup directory.

**Screenshot M3-01: PDF Metadata**

<img width="857" height="410" alt="Screenshot 2026-10-18 202631" src="https://github.com/user-attachments/assets/c91a7368-c6f0-47b7-a9ae-f0c35fee5d43" />


### 6.2 Exposed Directory

I visited the `/old/` directory identified during reconnaissance. The training website displayed a SQL backup file named `mediroza_db_backup_2019.sql`.

This demonstrated the risk of leaving old backup files in a publicly accessible web directory.

**Screenshot M3-02: Old Directory Listing**

<img width="1920" height="923" alt="VirtualBox_kali-linux-2026 2-virtualbox-amd64_18_10_2026_20_32_18" src="https://github.com/user-attachments/assets/9369222a-f79e-4f4a-9bcb-e2345f247d38" />


### 6.3 Connecting the Findings

This milestone helped me understand how different clues can be connected during a security assessment.

The metadata pointed towards an old directory, and the directory listing exposed a database backup. This demonstrated how one weakness can lead to further information exposure.

## 7. Milestone 4 – Penetration Testing Report

### 7.1 Findings Summary

The following table summarizes the findings described in the lab solution.

| No. | Finding | Location | Risk |
|---|---|---|---|
| 1 | Username enumeration | `patient/login.php` | Medium |
| 2 | SQL injection login bypass | `patient/login.php` | Critical |
| 3 | Encrypted PDFs accessible after login bypass | `patient/reports/` | High |
| 4 | Weak PDF passwords | Patient report PDFs | High |
| 5 | Sensitive metadata in a PDF | `patient_report_3.pdf` | Medium |
| 6 | Exposed old directory with directory listing | `old/` | Critical |
| 7 | Confidential database backup exposed | `old/mediroza_db_backup_2019.sql` | Critical |

*Note: These risk ratings are taken from the provided lab solution.*

## 8. What I Learned

Through this project, I learned:

- How to perform basic reconnaissance.
- How username enumeration can expose valid accounts.
- Why SQL injection is a serious security risk.
- How PDF password testing works.
- Why metadata should be checked before files are shared.
- How exposed backups can lead to confidential information being revealed.
- How to document findings and recommend security improvements.

I also learned that cybersecurity is not only about finding vulnerabilities. It is important to explain their impact and recommend ways to prevent them.

## 9. Conclusion

This lab helped me understand several common web application security issues and how they can be connected. It also improved my familiarity with Kali Linux, command-line tools, file metadata, and basic penetration testing documentation.

I will continue improving my cybersecurity knowledge through authorized training labs and practical exercises.

## 10. Disclaimer

This project is documented for educational purposes. Testing should only be performed on systems for which explicit permission has been granted.

No confidential database records, patient information, passwords, secret hashes, or other sensitive information should be included in this public repository.
