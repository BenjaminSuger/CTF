## picoCTF asm1

Dans ce challenge hard de reverse engineering, nous devons trouver la valeur de fin apres l'execution d'une fonction en assembleur. 

Quelques informations importantes ;     
-le flag est une valeur hexadecimal, nous ne devons pas utiliser le format habituelle picoCTF{flag}     
-on nous donne le paramètre asm1(0x2e0), il n'y a qu'un seul paramètre qui va etre facile a identifier      
-x86, intel syntax 

Voici le contenu du fichier en .s (assembleur); 

````
<+0>:	push   ebp
<+1>:	mov    ebp,esp
<+3>:	cmp    DWORD PTR [ebp+0x8],0x3fb
<+10>:	jg     0x512 <asm1+37>
<+12>:	cmp    DWORD PTR [ebp+0x8],0x280
<+19>:	jne    0x50a <asm1+29>
<+21>:	mov    eax,DWORD PTR [ebp+0x8]
<+24>:	add    eax,0xa
<+27>:	jmp    0x529 <asm1+60>
<+29>:	mov    eax,DWORD PTR [ebp+0x8]
<+32>:	sub    eax,0xa
<+35>:	jmp    0x529 <asm1+60>
<+37>:	cmp    DWORD PTR [ebp+0x8],0x559
<+44>:	jne    0x523 <asm1+54>
<+46>:	mov    eax,DWORD PTR [ebp+0x8]
<+49>:	sub    eax,0xa
<+52>:	jmp    0x529 <asm1+60>
<+54>:	mov    eax,DWORD PTR [ebp+0x8]
<+57>:	add    eax,0xa
<+60>:	pop    ebp
<+61>:	ret    
````

Ma méthode de résolution ;  
Je vais lire ligne par ligne et supprimer / simplifier le contenu au fur et à mesure. Par exemple, je supprime les lignes suivantes ; 
````
<+0>:	push   ebp
<+1>:	mov    ebp,esp
````
Il s'agit de la mise en place des registres ebp et esp (base pointer & stack pointer) qu'on retrouve dans tous les programmes

````
<+3>:	cmp    DWORD PTR [ebp+0x8],0x3fb
````
On compare DWORD PTR[ebp+0x8] à la valeur 0x3fb     
DWORD PTR[ebp+0x8] est notre paramètre soit 0x2e0   
on peut écrire notre ligne ainsi 
````
<+3> on compare 0x2e0 à 0x3fb   
````
Mais pourquoi faire ? 
Une comparaison est suivie par une instruction jump. Les instructions jump peuvent prendre plusieurs formes. Ici il s'agit de "jg" => jump if greater   

donc on peut écrire ;
````
<+3> on compare 0x2e0 à 0x3fb 
<+10> et si c'est plus grand on va a la ligne +37
````
Ce n'est pas le cas, 0x2e0 n'est pas plus grand que 0x3fb donc on ne fait pas de saut et on continue à lire notre programme. 
````
<+12>:	cmp    DWORD PTR [ebp+0x8],0x280
````
Idem, une comparaison qui va etre suivie d'un saut;
````
<+19>:	jne    0x50a <asm1+29>
````

Toujours dans l'idée de l'ecrire d'une manière plus "humaine" (mais suis-je humain ?)   
````
<+12> compare la valeur 0x2e0 et 0x280
<+19> saute à la ligne +29 si les deux valeurs ne sont pas égale
````
Ce qui est le cas ! On saute donc à la ligne 29 sans lire les autres; 
````
<+29>:	mov    eax,DWORD PTR [ebp+0x8]
````
L'instruction mov, permet de bouger une valeur dans une autre de la manière suivante ; 
````
mov destination, source
````
A noter qu'ici il s'agit d'une syntaxe Intel et non pas AT&T. Si c'était AT&T => mov source, destination    
On peut vite prendre le reflexe de reconnaitre cette syntaxe avec la première ligne ; mov ebp, esp 
On bouge le stack pointer au niveau du base pointer 

Ici dans notre cas ; 
````
eax = DWORD PTR[ebp+0x8] = 0x2e0   
autrement dit 
eax = 0x2e0 
````

La ligne suivante vient soustraire une valeur au registre eax; 
````
<+32>:	sub    eax,0xa
````
On peut écrire 
````
eax = 0x2e0 - 0xa
eax = 0x2D6
````
Cette fois on va sauter sans condition ! 
````
<+35>:	jmp    0x529 <asm1+60>
````
Si j'essaie de traduire ; 
````
<+35> va a la ligne 60 
````

Les lignes 60 et 61 vont ensemble, il s'agit de la fin du programme;
````
<+60>:	pop    ebp
<+61>:	ret 
````
en gros il dit ; 
````
termine le programme
et return la valeur dans eax 
````

# Conclusion 

Si on mt tout bout à bout ; 
````
<+3> on compare 0x2e0 à 0x3fb   
<+10> et si c'est plus grand on va a la ligne +37
<+12> compare la valeur 0x2e0 et 0x280
<+19> saute à la ligne +29 si les deux valeurs ne sont pas égale
<+29> eax = 0x2e0 
<+32> eax = 0x2D6
<+35> va a la ligne 60
<+60> finit le programme
<+61> donne moi la valeur de eax
````

**le flag = 0x2d6**






