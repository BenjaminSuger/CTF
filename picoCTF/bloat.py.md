## Bloat.py

Dans ce challenge on nous donne 2 fichiers;     
un fichier en .py   
un fichier flag

Il faut utiliser le fichier python pour avoir accès au flag qui valide le challenge. 

En lancant le fichier python, on nous demande un mot de passe;  
"Please enter correct password for flag:"   

Pour trouver le mot de passe il faut examiner le code. Voici les éléments pertinents de ce code; 

````
a = "!\"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ"+ \
            "[\\]^_`abcdefghijklmnopqrstuvwxyz{|}~ "

def arg133(arg432):
  if arg432 == a[71]+a[64]+a[79]+a[79]+a[88]+a[66]+a[71]+a[64]+a[77]+a[66]+a[68]:
    return True
````

Premièrement nous avons une variable 'a' qui est de type string, une chaine de caractères.

Ensuite on a une fonction qui compare l'argument que l'on passe quand on execute le script python et le compare à un autre élément. 

a[71] revient à dire "le 71ième élément de a" ca veut dire que c'est la première lettre de notre mot de passe à trouver.

Astuce; dans votre terminal vous pouvez taper "python3" ce qui va vous permettre d'entrer des lignes de code en python. 
Ensuite vous pouvez copier-coller la définition de a    
a = "!\"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ"+ \
            "[\\]^_`abcdefghijklmnopqrstuvwxyz{|}~ "    
Puis vous allez utiliser la fonction print(), pourquoi ?    
Vous allez "imprimer" la valeur qui est vérifié dans le code donc   
print(a[71]+a[64]+a[79]+a[79]+a[88]+a[66]+a[71]+a[64]+a[77]+a[66]+a[68])

Cela vous donne le mot de passe ; **happychance**

Ainsi que le flag ; **picoCTF{d30bfu5c4710n_f7w_b8062eec}**