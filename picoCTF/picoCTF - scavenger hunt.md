## picoCTF - Scavenger hunt - web challenge 

Ici nous avons uniquement une adresse d'un site web; http://mercury.picoctf.net:5080/ 

Le flag est divisé en plusieurs parties;

1. Il faut inspecter la page et regarder la section index (avec google chrome il faut aller dans "sources")

``````
	<!-- Here's the first part of the flag: picoCTF{t -->
``````

2. toujours en inspectant, nous pouvons aller dans la section "mycss.css"
``````
/* CSS makes the page look nice, and yes, it also has part of the flag. Here's part 2: h4ts_4_l0 */
``````
3. encore une fois, toujours en inspectant il faut aller dans la section "myjs.js" pour avoir un indice
``````
/* How can I keep Google from indexing my website? */
``````
La réponse à cette question est la page /robots.txt     
Il faut donc vous rendre ici ; http://mercury.picoctf.net:5080/robots.txt   
``````
Part 3: t_0f_pl4c
``````
4. Avec notre précédente trouvaille, nous avons un indice 
``````
 I think this is an apache server... can you Access the next flag?
 ``````
 Un des endroits que vous pouvez vérifier est le .htaccess. Qu'est ce que c'est ?   
 Hypertext Access est un fichier de configuration utilisé par Apache.    
Sur cette adresse ; http://mercury.picoctf.net:5080/.htaccess 
``````
# Part 4: 3s_2_lO0k
# I love making websites on my Mac, I can Store a lot of information there.
``````
En plus d'avoir une partie du flag, nous avons aussi un indice pour une autre partie    

5. (c'est la partie où j'ai eu le plus de mal)  

L'indice nous parle des .DS_Store. La définition;   
.DS_Store (Desktop Services Store) est un fichier caché créé sur les systèmes d'exploitation macOS.

Sur cette adresse; http://mercury.picoctf.net:5080/.DS_Store    
``````
Congrats! You completed the scavenger hunt. Part 5: _35844447}
``````

Réponse;  picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k_35844447}
