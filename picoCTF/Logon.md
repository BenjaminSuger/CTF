## Logon

Pour résoudre ce challenge vous allez avoir besoin de BurpSuite. 
Ce qui implique l'utilisation d'une VM idéalement. 


Nous avons uniquement accès à une page d'un site pour se connecter. 

Si vous essayez en utilisateur admin et en en mot de passe admin, vous obtenez le message suivant   
```Success: You logged in! Not sure you'll be able to see the flag though. No flag for you ```

En examinant le site on observe assez peu de choses. On pourrait penser à utiliser hydra pour résoudre ce challenge en premier lieu mais avec aussi peu d'informations autant essayer d'autres choses avant cela. 

J'ai utilisé burpsuite depuis une machine virtuelle (Kali).
Avec Kali, vous avez déjà sur mozilla firefox l'outil foxyproxy installé, il suffit juste de l'activer. 
Dans la section "proxy" de Burp => vous pouvez mettre "Intercetp is on"

Cela va vous permettre de voir tout le chemin que va parcourir votre connexion. 

A un moment (2ième forward), vous allez pouvoir observer quelque chose; 

``````
GET /flag HTTP/1.1

Host: jupiter.challenges.picoctf.org

Cookie: password=admin; username=admin; admin=False
``````

J'ai changé admin=False pour admin=True puis cliquer sur "forward" 

Sur cette page vous aurez alors le flag;    
picoCTF{th3_c0nsp1r4cy_l1v3s_6edb3f5f}
