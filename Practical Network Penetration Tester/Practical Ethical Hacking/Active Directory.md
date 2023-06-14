

## Attacking Active Directory: Initial Attack Vectors

### LLMNR poisoning


### Capturing NTLMv2 Hashes with Responder


### Password Cracking with Hashcat


### LLMNR Poisoning Defense


### SMB Relay Attacks Overview

![[Pasted image 20230418125414.png]]

[SMB Relay - Pentest Everything](https://viperone.gitbook.io/pentest-everything/everything/everything-active-directory/adversary-in-the-middle/smb-relay)

dump SAM hashes

### Discovering Hosts with SMB Signing Disabled

nmap --script=smb2-security-mode.nse -p445 192.168.57.0/24

gedit targets.txt
put ip 192.168.57.142 of Spider-Man
![[Pasted image 20230418131228.png]]


### SMB Relay Attack Defenses
![[Pasted image 20230418132210.png]]


### IPv6 Attacks Overview

