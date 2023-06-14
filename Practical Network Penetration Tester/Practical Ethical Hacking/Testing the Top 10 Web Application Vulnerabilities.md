## The OWASP Top 10 and OWASP Testing Checklist

OWASP Top 10: [https://owasp.org/www-pdf-archive/OWASP_Top_10-2017_%28en%29.pdf.pdf](https://owasp.org/www-pdf-archive/OWASP_Top_10-2017_%28en%29.pdf.pdf)

OWASP Testing Checklist: [https://github.com/tanprathan/OWASP-Testing-Checklist](https://github.com/tanprathan/OWASP-Testing-Checklist)

OWASP Testing Guide: [https://owasp.org/www-project-web-security-testing-guide/assets/archive/OWASP_Testing_Guide_v4.pdf](https://owasp.org/www-project-web-security-testing-guide/assets/archive/OWASP_Testing_Guide_v4.pdf)


## Installing OWASP Juice Shop

# !!!! Am instalat pe PC acasa in locatia: 
#### G:\PEH\kali-linux-2022.4-vmware-amd64-7z\kali-linux-2022.4-vmware-amd64.vmwarevm

Installing Docker on Kali: [https://medium.com/@airman604/installing-docker-in-kali-linux-2017-1-fbaa4d1447fe](https://medium.com/@airman604/installing-docker-in-kali-linux-2017-1-fbaa4d1447fe)

OWASP Juice Shop: [https://github.com/bkimminich/juice-shop](https://github.com/bkimminich/juice-shop)


**Practic:
open terminal and paste: 
```bash 
docker run --rm -p 3000:3000 bkimminich/juice-shop
```

## Exploring Burp Suite

With web apps, you have 3 stages of testing:
- unauthenticated stage
- user tier
- admin user

## SQL Injection

OWASP A1-Injection: [https://www.owasp.org/index.php/Top_10-2017_A1-Injection](https://www.owasp.org/index.php/Top_10-2017_A1-Injection)

![[Pasted image 20230419231602.png]]

![[Pasted image 20230419231728.png]]

![[Pasted image 20230419231838.png]]

![[Pasted image 20230419232002.png]]

![[Pasted image 20230419232237.png]]


## SQL Injection Walkthrough
``
``` SQL
Input: test
SQL: SELECT * FROM Users WHERE email='test';

Input: test'
SQL: SELECT * FROM Users WHERE email='test'';

Input: test' OR 1=1; --
SQL: SELECT * FROM Users WHERE email='test' OR 1=1 --';
```
1 admin

Next: do Christmas Special
Go to Challenge solutions an follow along, take notes

![[Pasted image 20230420232920.png]]



## Cross-Site Scripting (XSS) Overview

![[Pasted image 20230420233443.png]]


## Broken Authentication Overview and Defenses

OWASP A2-Broken Authentication: [https://www.owasp.org/index.php/Top_10-2017_A2-Broken_Authentication](https://www.owasp.org/index.php/Top_10-2017_A2-Broken_Authentication)


##  Sensitive Data Exposure Overview and Defenses

OWASP A3-Sensetive Data Exposure: [https://www.owasp.org/index.php/Top_10-2017_A3-Sensitive_Data_Exposure](https://www.owasp.org/index.php/Top_10-2017_A3-Sensitive_Data_Exposure)

DirBuster wordlist location: 
#### /usr/share/wordlists/dirbuster/

## XML External Entities (XXE) Overview

OWASP A4-XML External Entities: [https://www.owasp.org/index.php/Top_10-2017_A4-XML_External_Entities_(XXE)](https://www.owasp.org/index.php/Top_10-2017_A4-XML_External_Entities_(XXE))

![[Pasted image 20230422210042.png]]


## Broken Access Control Overview

OWASP A5-Broken Access Control: [https://www.owasp.org/index.php/Top_10-2017_A5-Broken_Access_Control](https://www.owasp.org/index.php/Top_10-2017_A5-Broken_Access_Control)


## Security Misconfiguration Attacks and Defenses

OWASP A6-Security Misconfigurations: [https://www.owasp.org/index.php/Top_10-2017_A6-Security_Misconfiguration](https://www.owasp.org/index.php/Top_10-2017_A6-Security_Misconfiguration)


## Cross-Site Scripting (XSS) Overview

#### it is a client side attack

OWASP A7-Cross Site Scripting: [https://www.owasp.org/index.php/Top_10-2017_A7-Cross-Site_Scripting_(XSS)](https://www.owasp.org/index.php/Top_10-2017_A7-Cross-Site_Scripting_(XSS))

DOM Based XSS: [https://www.scip.ch/en/?labs.20171214](https://www.scip.ch/en/?labs.20171214)

XSS Game: [https://xss-game.appspot.com/](https://xss-game.appspot.com/)

you can intercept traffic with burp suite, send it to intruder and give a list of xss payloads


## Insecure Deserialization

OWASP A8-Insecure Deserialization: [https://www.owasp.org/index.php/Top_10-2017_A8-Insecure_Deserialization](https://www.owasp.org/index.php/Top_10-2017_A8-Insecure_Deserialization)

ysoserial


## Using Components with Known Vulnerabilities

OWASP A9-Using Components with Known Vulnerabilities: [https://www.owasp.org/index.php/Top_10-2017_A9-Using_Components_with_Known_Vulnerabilities](https://www.owasp.org/index.php/Top_10-2017_A9-Using_Components_with_Known_Vulnerabilities)


## Insufficient Logging and Monitoring

OWASP A10-Insufficient Logging & Monitoring: [https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A10-Insufficient_Logging%252526Monitoring.html](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/Top_10-2017_A10-Insufficient_Logging%252526Monitoring.html)

