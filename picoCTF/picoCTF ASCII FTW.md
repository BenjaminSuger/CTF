## PicoCTF ASCII FTW 

Dans ce challenge on nous donne un binaire, avec la commande file voici les détails ; 

````
asciiftw: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=c29491782ee13aa7c5734d77b281865b608e46e9, for GNU/Linux 3.2.0, not stripped
`````

Les deux informations intéressantes qu'on peut en tirer ;   
-ELF 64-bit => on peut lancer le programme sur notre machine linux  
-not stripped => pratique car on peut retrouver les fonctions facilement si nécessaire      

En executant l'executable (jeu de mot); 

````
The flag starts with 70
````

On a pas plus d'informations. On sait juste qu'un flag sur picoCTF est toujours dans le format ;    
picoCTF{???????}

Le challenge a pour nom ASCII ; il s'agit de la table ASCII ou "traduit" les caractères par de l'hexadecimal ou du decimal. 

Globalement...on a l'idée du challenge de base.

Mais pour aller plus loin, j'ai ouvert le fichier avec Ghidra (l'outil de la NSA, n'hésitez pas a voir ma video sur youtube !) 

````
        00101184 c6 45 d0 70     MOV        byte ptr [RBP + local_38],0x70
        00101188 c6 45 d1 69     MOV        byte ptr [RBP + local_37],0x69
        0010118c c6 45 d2 63     MOV        byte ptr [RBP + local_36],0x63
        00101190 c6 45 d3 6f     MOV        byte ptr [RBP + local_35],0x6f
        00101194 c6 45 d4 43     MOV        byte ptr [RBP + local_34],0x43
        00101198 c6 45 d5 54     MOV        byte ptr [RBP + local_33],0x54
        0010119c c6 45 d6 46     MOV        byte ptr [RBP + local_32],0x46
        001011a0 c6 45 d7 7b     MOV        byte ptr [RBP + local_31],0x7b
        001011a4 c6 45 d8 41     MOV        byte ptr [RBP + local_30],0x41
        001011a8 c6 45 d9 53     MOV        byte ptr [RBP + local_2f],0x53
        001011ac c6 45 da 43     MOV        byte ptr [RBP + local_2e],0x43
        001011b0 c6 45 db 49     MOV        byte ptr [RBP + local_2d],0x49
        001011b4 c6 45 dc 49     MOV        byte ptr [RBP + local_2c],0x49
        001011b8 c6 45 dd 5f     MOV        byte ptr [RBP + local_2b],0x5f
        001011bc c6 45 de 49     MOV        byte ptr [RBP + local_2a],0x49
        001011c0 c6 45 df 53     MOV        byte ptr [RBP + local_29],0x53
        001011c4 c6 45 e0 5f     MOV        byte ptr [RBP + local_28],0x5f
        001011c8 c6 45 e1 45     MOV        byte ptr [RBP + local_27],0x45
        001011cc c6 45 e2 41     MOV        byte ptr [RBP + local_26],0x41
        001011d0 c6 45 e3 53     MOV        byte ptr [RBP + local_25],0x53
        001011d4 c6 45 e4 59     MOV        byte ptr [RBP + local_24],0x59
        001011d8 c6 45 e5 5f     MOV        byte ptr [RBP + local_23],0x5f
        001011dc c6 45 e6 33     MOV        byte ptr [RBP + local_22],0x33
        001011e0 c6 45 e7 43     MOV        byte ptr [RBP + local_21],0x43
        001011e4 c6 45 e8 46     MOV        byte ptr [RBP + local_20],0x46
        001011e8 c6 45 e9 34     MOV        byte ptr [RBP + local_1f],0x34
        001011ec c6 45 ea 42     MOV        byte ptr [RBP + local_1e],0x42
        001011f0 c6 45 eb 46     MOV        byte ptr [RBP + local_1d],0x46
        001011f4 c6 45 ec 41     MOV        byte ptr [RBP + local_1c],0x41
        001011f8 c6 45 ed 44     MOV        byte ptr [RBP + local_1b],0x44
        001011fc c6 45 ee 7d     MOV        byte ptr [RBP + local_1a],0x7d

````

Dans cette enorme bloc, on retrouve le flag du challenge. Mais comment ? 

Si on prend la première ligne;  
MOV        byte ptr [RBP + local_38],0x70   
il faut comprendre qu'on va mettre la valeur 0x70 dans une adresse.      

70, doesn't ring a bell ? 0x70 en décimal devient la lettre 'p' en char sur la table ASCII. 

Donc il suffit de "traduire" l'héxadecimal en "char". L'outil ghidra nous permet de faire cette opération. 

**flag : picoCTF{ASCII_IS_EASY_3CF4BFAD}**
