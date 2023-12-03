## HackTheBox Reverse challenge - Baby RE

Avec ce challenge on nous donne juste accès à un fichier "baby".    

La première chose que j'essaye de faire à chaque challenge, la commande file.
``````
file baby 

baby: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=25adc53b89f781335a27bf1b81f5c4cb74581022, for GNU/Linux 3.2.0, not stripped
``````

Peut-être que plus tard cela va nous donner des indications intéressantes.....ou pas

L'autre commande que j'essaye de faire souvent; strings 
``````
strings baby
``````  
Dans les résultats on peut voir la chose suivante;     
``````
Dont run `strings` on this challenge, that is not the way!!!!   
``````  
On peut bien sur exécuter le fichier pour voir ce qui se produit (n'oubliez pas d'utiliser chmod +x)

``````
─$ ./baby                
Insert key: 
``````
Il faut donc entrer un mot de passe/key

La solution est "simple", il faut ouvrir le fichier avec Ghidra. Rien à faire spéciale, pas besoin de savoir beaucoup l'utiliser mais juste de charger un fichier dans Ghidra. Le plus difficile pour moi c'était d'installer sur ma VM GHidra (soucis avec OpenJDK....bref).    

Maintenant dans Ghidra, en scrollant on va trouver la réponse. 
Vous allez retrouver la section que l'on a vue avec strings "Dont' run strings....."
et un peu en dessous;   
``````
='abcde122313\n'    
``````
On exécute de nouveau; 
``````
─$ ./baby                
Insert key: 
abcde122313
HTB{B4BY_R3V_TH4TS_EZ}
``````  
**Réponse; HTB{B4BY_R3V_TH4TS_EZ}** 