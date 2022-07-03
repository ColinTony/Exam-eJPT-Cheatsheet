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
    nmap -Pn -O <IP>
#### Nmap Scan ports
    nmap -p- --open -T5 -n <IP> -oG allPorts
    nmap -p- --open -sS --min-rate 5000 -n -Pn <IP> -oN allPorts (Rapido)
#### Nmap Scan Scripts reconocimiento.
    nmap -sC -sV -p<ports> 10.10.10.10 -oN target
#### Nmap Scan (UDP Quick)
    nmap -sU -sV <IP> 
#### Other nmap scan useful during exam
    nmap -sV -Pn -T4 -A -p- -iL hosts.nmap -oN ports.nmap
    nmap --script vuln --script-args=unsafe=1 -iL hosts.nmap
# FUZZING
## mi herramienta favorita para hacer fuzzing  es wfuzz pero existen otras que podemos utilizar.
    wfuzz -c --hc=404,400 -w <dictionaryFile> http://<IP>/FUZZ
#### subdominios pordemos usa el -Z en wfuzz
    wfuzz -c --hc=404,400 -Z -w <dictionaryFile> http://<IP>/FUZZ
#### Herramientas dirsearch , dirb podemos usar tambien gobuster
    dirsearch.py [-u|--url] target [-e|--extensions] extensions [options]
    dirb http://<IP>
### Buscar exploits
### Sabemos que para buscar vulnerabilidades podemos usar google u tirar de esta  herramienta llamada searchsploit
#### Busqueda 
    searchsploit <Name>
#### Inspectionar
    searchsploit -x path : example searchsploit -x linux_x86-64/47151.c
#### copiar exploit
    searchsploit -m path : example searchsploit -m linux_x86-64/47151.c
