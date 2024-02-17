## Forbidden Paths

Dans ce challenge, on a beaucoup d'éléments qui vont nous aider à résoudre le challenge dans la description.

````
We know that the website files live in /usr/share/nginx/html/ and the flag is at /flag.txt but the website is filtering absolute file paths. Can you get past the filter to read the flag?
````

Sur le site on retrouve une page qui nous demande de choisir entre 3 textes affichés (divine-comedy.txt, oliver-twist.txt, the-happy-prince.txt).   
Pour choisir les textes, il y a une case où l'on peut écrire le nom du texte....

Tout de suite on comprend que c'est ici que réside la faille. De plus pour ceux qui vont bien observer l'affiche du site (et qui n'ont pas lu la description du challenge), vous pouvez voir aussi cela avant le premier texte "..". 

Il s'agit d'un path traversal; https://owasp.org/www-community/attacks/Path_Traversal 

Avec la description on sait que nous sommes dans "/usr/share/nginx/html/".

Donc pour accèder au /falg.txt, il n'y a besoin que de 4 fois ../

../../../../flag.txt vous donne 

**picoCTF{7h3_p47h_70_5ucc355_e5fe3d4d}**