# 🔐 TryHackMe - Blue Room

## 📌 Overview
The Blue Room focuses on exploiting a vulnerable Windows machine using the MS17-010 (EternalBlue) vulnerability. It covers the full attack lifecycle: reconnaissance, exploitation, privilege access, and post-exploitation.

## 🎯 Objectives
- Perform enumeration on the target machine  
- Identify vulnerabilities  
- Exploit the system using Metasploit  
- Gain a shell and escalate access  
- Dump and crack password hashes  
- Retrieve flags from the system  

## 🔍 Reconnaissance
Started with an Nmap scan using `nmap -sV -vv --script vuln <target-ip>` to identify open ports and services. The scan revealed multiple open ports under 1000 and an SMB service vulnerable to MS17-010 (EternalBlue).

## 💥 Exploitation
Launched Metasploit (`msfconsole`), searched for the vulnerability using `search ms17-010`, and selected the module `exploit/windows/smb/ms17_010_eternalblue`. Configured the exploit by setting `RHOSTS` to the target IP and using the payload `windows/x64/shell/reverse_tcp`. Running the exploit successfully established a reverse shell, creating multiple sessions (expected behavior).

## 🧠 Post-Exploitation
Accessed the Meterpreter session and used `shell` to spawn a Windows command shell when needed, returning back using `exit`. Listed running processes with `ps` and migrated into `explorer.exe` using `migrate <PID>` for a stable and user-associated session.

## 🔑 Credential Dumping
With elevated privileges, executed `hashdump` to extract password hashes. Identified the non-default user **Jon** from the dumped hashes.

## 🔓 Password Cracking
Saved the hash and used offline cracking tools (such as John the Ripper) to crack it. Successfully retrieved the credentials:
- User: Jon  
- Password: alqfna22  

## 🚩 Flags
Flag 1 was found in the system root (`C:\`). After navigating using `cd C:\` and listing files with `dir`, the file `flag1.txt` was discovered and read using `type flag1.txt`, revealing `flag{access_the_machine}`.

Other flags were located inside the user directory (`C:\Users\Jon\`) through manual enumeration, based on hints indicating that the user had stored their password in a file.

## ⚠️ Note (Errata)
In some cases, flag files may disappear due to system behavior. If this occurs, restarting the machine and rerunning the exploit resolves the issue.

## 📂 Important System Path
The SAM file is located at `C:\Windows\System32\config\SAM`, which stores password hashes. Direct access is restricted, but tools like Meterpreter’s `hashdump` can extract the data when running with SYSTEM privileges.

## 💡 Key Learnings
- Enumeration is the foundation of exploitation  
- Understanding SMB vulnerabilities like MS17-010 is critical  
- Metasploit simplifies exploitation workflows  
- Difference between command shell and Meterpreter  
- Process migration improves session stability  
- Password hashes can be extracted and cracked  
- Post-exploitation is essential in real-world scenarios  

## 🚀 Tools Used
Nmap, Metasploit Framework, Meterpreter, and password cracking tools such as John the Ripper.

## 🧠 Conclusion
The Blue Room provides a complete hands-on experience of exploiting a Windows machine using a real-world vulnerability. It reinforces practical penetration testing skills from initial access to credential compromise and system exploration.
