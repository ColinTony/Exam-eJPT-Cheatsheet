# Exam-eJPT-Cheatsheet
Ayuda de algunos comandos que pueden utilizarse en el eJPT o en algun CTF.

## Common ports
| Port | Protocol | Hint                   |
|------|----------|------------------------|
| 22   | SSH      |                        |
| 25   | SMTP     |                        |
| 110  | POP3     |                        |
| 115  | SFTP     |                        |
| 143  | IMAP     |                        |
| 80   | HTTP     |                        |
| 443  | HTTPS    |                        |
| 23   | TELNET   |                        |
| 21   | FTP      |                        |
| 3389 | RDP      |                        |
| 3306 | MYSQL    |                        |
| 1433 | MS SQL   |                        |
| 137  | NETBIOS  | find work groups       |
| 138  | NETBIOS  | list shares & machines |
| 139  | NETBIOS  | transit data           |
| 53   | DNS      |                        |

### Nmap Scans
#### OS Detection
    nmap -Pn -O 10.10.10.10
#### Nmap Scan ports
    nmap -p- --open -T5 -n <IP> -oG allPorts
    nmap -p- --open -sS --min-rate 5000 -n -Pn <IP> -oN allPorts (Rapido)
#### Nmap Scan Scripts reconocimiento.
    nmap -sC -sV -p<ports> 10.10.10.10 -oN target
#### Nmap Scan (UDP Quick)
    nmap -sU -sV 10.10.10.10 
#### Other nmap scan useful during exam
    nmap -sV -Pn -T4 -A -p- -iL hosts.nmap -oN ports.nmap
    nmap --script vuln --script-args=unsafe=1 -iL hosts.nmap
