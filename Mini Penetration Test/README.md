## Mini Penetration Test Report: Lab Environment

Target: Metasploitable 2 (10.0.2.3)
Attacker: Kali Linux (10.0.2.15)


## 1. Vulnerability Scanning (Nmap)
Command:nmap -sV -sC -O -p- 10.0.2.3 -oN full_scan.txt
![Description of screenshot](images/nmap_fullscan.png)

## Key Findings:
Service Detection: Identified multiple high-risk services including FTP (21), SSH (22), 
Telnet (23), HTTP (80), SMB (139/445), and MySQL (3306).
Critical Vulnerability Found: The scan identified vsFTPd 2.3.4. This specific version is famous for having a backdoor (CVE-2011-2523) that allows an attacker to gain a root shell by sending a specific sequence (a smiley face :) in the username).
Web Vulnerabilities: The script likely flagged several directories (like /phpMyAdmin/ or /twiki/) that are susceptible to cross-site scripting (XSS) or SQL injection.


## 2. Exploitation: FTP Service
Command:ftp 10.0.2.3 (User: anonymous)
![Description of screenshot](images/ftp_service.png)
![Description of screenshot](images/ftp_service2.png)
![Description of screenshot](images/ftp_service3.png)

## Findings:
Status:SUCCESSFUL ACCESS
Details: Anonymous login is enabled. While system-level directories like /etc/ were restricted (Permission Denied), the ability to log in indicates a configuration weakness.
Data Leakage: A .message file was visible in the root directory.
Risk: Even with restricted permissions, anonymous FTP can be used to host malicious files or leak internal documentation if not properly configured.

## 3. Enumeration: SMB Service

Command:smbclient -L //10.0.2.3
![Description of screenshot](images/smb_client.png)

## Findings:
Status:SUCCESSFUL ENUMERATION
Shared Folders Identified:
tmp: Often used for temporary file storage (highly vulnerable).
opt: May contain application data.
IPC$: Used for inter-process communication (standard but useful for further mapping).
Risk: The absence of a password requirement to list shares indicates a "Null Session" vulnerability. This allows attackers to map the internal file structure of the server without credentials.

## 4. Conclusion & Recommendations

## Summary:
The target machine is highly insecure. An attacker can easily gather information about the system (SMB) and gain a foothold (FTP). The presence of the vsFTPd 2.3.4 backdoor is a "Critical" finding that would allow full system takeover.

Remediation Steps:
Disable Anonymous FTP: Modify /etc/vsftpd.conf to set anonymous_enable=NO.
Patch/Update vsFTPd: Update the FTP service to a version later than 2.3.4 to remove 

the backdoor.
Secure SMB Shares: Require authentication for all SMB shares and disable Null Sessions.
Firewall Rules: Configure the OPNsense firewall to block these ports from the external WAN and only allow specific, monitored traffic.
