#pnpt 

[PNPT exam review](https://sunainwho.hashnode.dev/why-i-failed-my-first-attempt-at-pnpt)

[PNPT: Practical Network Penetration Tester — Review | by Shaun Whorton | Medium](https://medium.com/@shaunwhorton/pnpt-practical-network-penetration-tester-review-d2000bcb4e0b)

[https://phind.com/search?q=how+to+study+for+practical+network+penetration+tester](https://phind.com/search?q=how+to+study+for+practical+network+penetration+tester)

[explainshell.com - match command-line arguments to their help text](https://explainshell.com/)

ls -la -> list long all
man ls
ls --help
cd ~ -> back to home folder
cp -> copy
echo ' ' > test.txt -> write text in file
mv -> move
rm -> remove
updatedb -> execute before 'locate'
locate -> find a file on my machine
passwd -> change root password

Users and privileges
![[Pasted image 20221112123626.png]]
d -> directory
l -> link
- - > file
chmod +rwx test.txt
chmod 777
![[Pasted image 20221112125454.png]]
sudo adduser bogdan
su bogdan -> change user 
cat /etc/passwd
sudo /etc/shadow
su -> switch user
sudo cat /etc/suduoers
grep 'sudo' /etc/group
sudo -l

<mark style="background: #FF5582A6;">## Common Network Commands</mark>
ip -a -> the new way of doing
ifconfig -> old way
ip n / arp -a
ip r / route
ping

<mark style="background: #FF5582A6;">## Introduction to Python</mark>
The scripts are on Ubuntu and Kali VM's


Information Gathering (Reconnaissance)
![[Pasted image 20221120195933.png]]

<mark style="background: #FF5582A6;">Scanning & Enumeration</mark>

Installing Kioptrix - Kioptrix Download - [https://tcm-sec.com/kioptrix](https://tcm-sec.com/kioptrix)

## Scanning with Nmap 
nmap -T4 -p- -A ip_add
arp-scan -l
netdiscover -r 192.168.163.0/24
128 - Kioptrix
130 - Kali

do research on google, searchsploit


![[Pasted image 20221212221250.png]]

[Dosar – Google Drive](https://drive.google.com/drive/folders/1VXEuyySgzsSo-MYmyCareTnJ5rAeVKeH)

Blue
accounts:
user - Password123!
admin - Password456!
192.168.163.131 

![[Pasted image 20221213205919.png]]
![[Pasted image 20221213213623.png]]


<mark style="background: #D2B3FFA6;"><mark style="background: #FF5582A6;"><mark style="background: #FFB86CA6;">**Testing the Top 10 Web Application Vulnerabilities</mark></mark></mark>

OWASP
[https://owasp.org/www-project-web-security-testing-guide/assets/archive/OWASP_Testing_Guide_v4.pdf](https://owasp.org/www-project-web-security-testing-guide/assets/archive/OWASP_Testing_Guide_v4.pdf)

[GitHub - tanprathan/OWASP-Testing-Checklist: OWASP based Web Application Security Testing Checklist is an Excel based checklist which helps you to track the status of completed and pending test cases.](https://github.com/tanprathan/OWASP-Testing-Checklist)


## Legal Documents and Report Writing

### Common_Legal_Documents

![[Pasted image 20230418165438.png]]


Sample Pentest Report: [https://github.com/hmaverickadams/TCM-Security-Sample-Pentest-Report](https://github.com/hmaverickadams/TCM-Security-Sample-Pentest-Report)

