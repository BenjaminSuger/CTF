## PicoBrowser

Dans ce challenge web, on nous donne un site avec un bouton "flag".

Si on essaie ce bouton, nous avons un message d'erreur ;    
"You're not picobrowser! Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0"

Que faut-il faire ? Il faut que nous changions notre "user-agent" pour le bon navigateur. On fait croire au site internet que nous avons un autre navigateur internet.

Pour cela, vous pouvez faire cela dans Burpsuite; 

``````
User-Agent: picobrowser! Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0 
``````
**Answer: picoCTF{p1c0_s3cr3t_ag3nt_51414fa7}** 