## Web Enumeration

Room TryHackMe; https://tryhackme.com/room/webenumerationv2 

**GOBUSTER**

On nous avertit bien avant d'ajouter dans /etc/hosts 
echo "MACHINE_IP webenum".

*"Run a directory scan on the host. Other than the standard css, images and js directories, what other directories are available?"*

La commande a utilisé;     
gobuster dir -u http://webenum.thm/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x.html,.css,.js

Commentaire; si on reprend cette wordlist c'est un peu long mais c'est celle donnée en indication avant. Si vous essayez avec la plus petite /usr/share/wordlists/dirb/common.txt vous ne trouverez pas Changes ni VIDEO.

**Réponse; public,Changes,VIDEO**

*"Run a directory scan on the host. In the "C******" directory, what file extensions exist?"*

Techniquement, il n'y a pas besoin de chercher avec gobuster, si vous allez tout de suite sur http://webenum.thm/Changes/ vous aurez la réponse 

**Réponse; conf,js**

*"There's a flag out there that can be found by directory scanning! Find it!"*

Ici, il ne faut pas continuer sur /Changes/ mais aller sur /VIDEO/

**Réponse; thm{n1c3_w0rk}**

*"There are some virtual hosts running on this server. What are they?"*

Commande; gobuster vhost -u http://webenum.thm/ -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt

**Réponse; learning,products**

*"There's another flag to be found in one of the virtual hosts! Find it!"*

Ajoutez les deux dans /etc/hosts => puis il faut faire un dir avec gobuster     
Dans la commande il faut noter que j'ai ajouté le .txt;

gobuster dir -u http://products.webenum.thm/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x.html,.css,.js,.txt

**Réponse; thm{gobuster_is_fun}**


**WPSCAN**

*"What would be the full URL for the theme "twentynineteen" installed on the WordPress site: "http://cmnatics.playground""*

**Réponse; http://cmnatics.playground/wp-content/themes/twentynineteen**


*"What argument would we provide to enumerate a WordPress site?"*

**Réponse; enumerate**

*"What is the name of the other aggressiveness profile that we can use in our WPScan command?"*

**Réponse; passive**

*"Enumerate the site, what is the name of the theme that is detected as running?"*

N'oubliez pas d'ajouter à /etc/hosts    

Commande; wpscan --url http://wpscan.thm/ --enumerate t

**Réponse; twentynineteen**

*"Enumerate the site, what is the name of the plugin that WPScan has found?"*

Commande; wpscan --url http://wpscan.thm/ --enumerate p

**Réponse; nextgen-gallery**

*"Enumerate the site, what username can WPScan find?"*

Commande; wpscan --url http://wpscan.thm/ --enumerate u

**Réponse; phreakazoid**

*"Construct a WPScan command to brute-force the site with this username, using the rockyou wordlist as the password list. What is the password to this user?"*

Commande; wpscan --url http://wpscan.thm/ --usernames phreakazoid --passwords /usr/share/wordlists/rockyou.txt

**Réponse; linkinpark**

**NIKTO**

*"What argument would we use if we wanted to scan port 80 and 8080 on a host?"*

**Réponse; -p 80,8080**

*"What argument would we use if we wanted to see any cookies given by the web server? "*

**Réponse; -Display 2**

*"What is the name & version of the web server that  Nikto has determined running on port 80?"*

Commande; nikto -h [IP]

**Réponse; Apache/2.4.7**

*"There is another web server running on another port. What is the name & version of this web server?"*

Commandes; nmap [ip]    
nikto -h [ip] -p 8080

**Réponse; Apache-Coyote/1.1**

*"What is the name of the Cookie that this JBoss server gives?"*

Commande; nikto -h 10.10.218.103 -p 8080 -Display 2

**Réponse; JSESSIONID**