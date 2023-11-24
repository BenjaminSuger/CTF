# picoCTF - crackme-py

Ce challenge est assez facile et rapide.

On nous donne accès à un fichier sans autre indication, "crackme.py". Vous pouvez l'ouvrir sans problème sur VScode. 

Il y a 2 parties sur ce code;
1. Celui qui nous intéresse pour résoudre le CTF
2. Une fonction pour manipuler des chiffres

Cette seconde partie n'est pas du tout utile et vous pouvez la supprimer. Elle n'a aucun lien avec le début. 

Avec les commentaires, on nous donne un code à déchiffrer 
``````
bezos_cc_secret = "A:4@r%uL`M-^M0c0AbcM-MFE0d_a3hgc3N"
``````
On nous donne aussi un alphabet;
``````
alphabet = "!\"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ"+ \
            "[\\]^_`abcdefghijklmnopqrstuvwxyz{|}~"
``````
Enfin pour finir, il y a une fonction decode_secret(). On découvre alors qu'il s'agit d'un décodeur d'un code de césar. 

Le code de césar qu'on appelle aussi "chiffrement par décalage". Le décalage étant donné dans la fonction decode_secret().

L'astuce à utiliser est simple, vous pouvez exécuter la fonction decode_secret(bezos_cc_secret). Pas besoin d'essayer de le faire manuellement. 

**Réponse: picoCTF{1|\/|_4_p34|\|ut_502b984b}** 