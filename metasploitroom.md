---

METASPLOIT: METERPRETER — SUMMARY

---

CORE FLOW

Scan → Exploit → Access → Post-Exploit → Extract

---

1. EXPLOITATION (GETTING ACCESS)

* Used Metasploit module: exploit/windows/smb/psexec
* Credentials:
  Username: ballen
  Password: Password1
* Result: Meterpreter session obtained

---

2. METERPRETER BASICS

* You are inside the target system via an advanced shell
* Key commands:
  sysinfo → system details
  getuid → current user
  background → return to msfconsole
  sessions -i → re-enter session

---

3. PAYLOAD CONCEPT

* Reverse shell used
* Meaning: target connects back to attacker
* Types:
  Staged → /
  Stageless → _

---

4. POST-EXPLOITATION

DOMAIN ENUMERATION

* Domain: FLASH.local

SHARE ENUMERATION

* User-created share: speedster

CREDENTIAL DUMPING

* Used: hashdump
* NTLM hash (jchambers):
  69596c7aa1e8daee17f8e78870e25a5c

PASSWORD CRACKING

* Result: Trustno1

---

5. FILE ENUMERATION

secrets.txt
Location:
C:\Program Files (x86)\Windows Multimedia Platform\secrets.txt
Content:
KDSvbsw3849!

realsecret.txt
Location:
C:\inetpub\wwwroot\realsecret.txt
Content:
The Flash is the fastest man alive

---

6. KEY CONCEPTS

* Exploitation → gaining access
* Post-exploitation → using access
* Domain → centralized network control
* NTLM hash → can be cracked or reused
* Shares → network-accessible folders
* Lateral movement → spreading across systems

---

FINAL MEMORY LINE

Access → Explore → Extract → Escalate → Expand

---
