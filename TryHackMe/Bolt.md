## Bolt

Lien; https://tryhackme.com/r/room/bolt 

````
What port number has a web server with a CMS running?
````

commande ; nmap -sC -sV [IP]

*22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux;  protocol 2.0) | ssh-hostkey:           
80/tcp   open  http    Apache httpd 2.4.29 ((Ubuntu))   
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: Apache2 Ubuntu Default Page: It works
8000/tcp open  http    PHP 7.2.32-1*

**Réponse; 8000**
````
What is the username we can find in the CMS?
````

Sur la page internet du site (http://[IP]:8000/) on va trouver deux messages, voici les extraits intéressants;

*Welcome to this site, myself Jake and my username is bolt*

*Regards,
Jake (Admin)*

*i suppose this is our secret forum right? I posted my first message for our readers today but there seems to be a lot of freespace out there. Please check it out! my password is boltadmin123 just incase you need it!*

**Réponse; bolt**
````
What is the password we can find for the username?
````
**Réponse; boltadmin123**

````
What version of the CMS is installed on the server? (Ex: Name 1.1.1)
````

Pour trouver l'information, je me suis connecté avec l'identifiant et le mot de passe qu'on à trouvé plus tôt. 

Pour se connecter, il n'y a pas de bouton par défaut sur la page mais en regardant ici ; https://docs.boltcms.io/5.2/manual/login (même s'il s'agit d'une version plus moderne) on nous indique utiliser /bolt. 
Donc sur http://[IP]:8000/bolt vous pourrez vous connecter. 

**Réponse; bolt 3.7.1**
````
There's an exploit for a previous version of this CMS, which allows authenticated RCE. Find it on Exploit DB. What's its EDB-ID?
```` 

Qu'est-ce que le EDB-ID ? Exploit DB ID => donc a chercher sur le site https://www.exploit-db.com/

Le lien; https://www.exploit-db.com/exploits/48296

**Réponse; 48296**

On nous demande ensuite le chemin de l'exploit dans Metasploit; 

**Réponse; exploit/unix/webapp/bolt_authenticated_rce**

Pouis vous devez l'utiliser (si vous ne savez pas utiliser Metasploit => aller voir les cours sur TryHackMe sur ce sujet)

**flag; THM{wh0_d035nt_l0ve5_b0l7_r1gh7?}**

