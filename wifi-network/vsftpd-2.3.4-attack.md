# CVE-2011-2523 — vsftpd 2.3.4 Backdoor

## Overview

This document describes a **known backdoor vulnerability** in **vsftpd 2.3.4**, cataloged as **CVE-2011-2523**.

The vulnerability allows **unauthenticated remote command execution** via a maliciously crafted username, which opens a shell on **TCP port 6200**.

---

## Vulnerability Details

- **CVE**: CVE-2011-2523  
- **Service**: vsftpd  
- **Affected Version**: 2.3.4  
- **Protocol**: FTP  
- **Port**: 21 (FTP), 6200 (Backdoor Shell)  
- **Impact**: Remote Shell Access  
- **Tested on**: Debian  

---

## Root Cause

A **backdoored version** of vsftpd 2.3.4 was distributed publicly.

If a username containing the string `:)` is supplied during FTP authentication, the server spawns a shell listener on **port 6200**.

---

## Attack Flow (Conceptual)

```text
FTP CONNECT (21)
   |
   v
SEND USER :)
   |
   v
BACKDOOR TRIGGERED
   |
   v
SHELL BINDS TO 6200
   |
   v
REMOTE ACCESS
```

## Attention! This attack is old; to successfully execute it, please download the Metasploitable image, install VirtualBox or VMware, and always simulate the attack in a test environment.


# Or you can use the Metasploit framework in Kali Linux

# Metasploit Framework — Documentation

## Overview

The **Metasploit Framework** is an open-source platform used for **security testing, exploitation development, vulnerability validation and post-exploitation**.

It is widely adopted by:
- Penetration testers
- Red teams
- Blue teams
- SOC analysts
- Security researchers

Metasploit provides a **modular architecture**, allowing exploits, payloads, scanners and auxiliary modules to be reused and combined efficiently.

---

## Key Components

```text
exploit     -> triggers a vulnerability
payload     -> code executed on target
auxiliary   -> scanners, fuzzers, brute-force
post        -> post-exploitation actions
encoder     -> obfuscates payloads
nop         -> padding for exploits
```
```text
USER
 |
 v
msfconsole
 |
 v
MODULE
 |
 +--> exploit
 |       |
 |       v
 |    payload
 |
 +--> auxiliary
 |
 +--> post
