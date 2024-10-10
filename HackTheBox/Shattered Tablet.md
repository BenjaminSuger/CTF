## Shattered Tablet

On a affaire un challenge de reverse engineering assez simple

Il s'agit d'un ELF (x86). Si on essaie de le lancer il nous demande un mot de passe. 

Ici pas de strcmp ou autres, les commandes comme ltrace/strace ou strings ne nous donne pas d'indication. 

Il faut utiliser un outil comme Ghidra pour résoudre le challenge. 

A l'intérieur de celui-ci on va voir ; 

````
  if (((((local_28._2_1_ == '4') && (local_38._4_1_ == '3')) && (local_28._4_1_ == 'r')) &&
      ((((local_48._1_1_ == 'T' && (local_38._5_1_ == 'v')) &&
        ((local_48._6_1_ == '0' && ((local_28._7_1_ == '}' && (local_28._6_1_ == 'd')))))) &&
       (local_30._7_1_ == 'r')))) &&
     ((((((local_30._5_1_ == '3' && ((char)local_40 == '3')) && (local_38._6_1_ == 'e')) &&
        ((local_28._3_1_ == '1' && (local_48._5_1_ == 'r')))) &&
       (((char)local_48 == 'H' && (((char)local_28 == '3' && (local_38._2_1_ == '.')))))) &&
      (((((local_40._5_1_ == '4' &&
          (((((local_48._3_1_ == '{' && (local_40._2_1_ == '_')) && ((char)local_38 == '.')) &&
            ((local_48._4_1_ == 'b' && (local_48._7_1_ == 'k')))) && (local_40._7_1_ == 't')))) &&
         (((local_40._6_1_ == 'r' && (local_38._3_1_ == 'n')) &&
          ((local_30._1_1_ == 't' &&
           (((local_38._1_1_ == '.' && (local_40._1_1_ == 'n')) && (local_30._6_1_ == '_')))))))) &&
        (((local_30._2_1_ == '0' && ((char)local_30 == '_')) && (local_40._4_1_ == 'p')))) &&
       ((((local_38._7_1_ == 'r' && (local_30._4_1_ == 'b')) &&
         ((local_28._1_1_ == 'p' &&
          (((local_48._2_1_ == 'B' && (local_30._3_1_ == '_')) && (local_40._3_1_ == '4')))))) &&
        (local_28._5_1_ == '3'))))))))
````

En gros, il y a une vérification avec un IF statement. Ce IF statement va verifier chaque lettre du mot de passe.

Techniquement on a le mot de passe qui est le flag en clair, il est juste bien mélangé. 

Si on prend les "local_variable" dans l'ordre de déclaration dans le code. Cela nous donne l'ordre suivant ; 

````
local_48 == 'H' 
local_48._1_1_ == 'T'
local_48._2_1_ == 'B'
local_48._3_1_ == '{' 
local_48._4_1_ == 'b' 
local_48._5_1_ == 'r'
local_48._6_1_ == '0'
local_48._7_1_ == 'k'
HTB{br0k

local_40 == '3'
local_40._1_1_ == 'n' 
local_40._2_1_ == '_'
local_40._3_1_ == '4'
local_40._4_1_ == 'p'
local_40._5_1_ == '4'
local_40._6_1_ == 'r'
local_40._7_1_ == 't'
3n_4p4rt

local_38 == '.'
local_38._1_1_ == '.' 
local_38._2_1_ == '.'
local_38._3_1_ == 'n'
local_38._4_1_ == '3'
local_38._5_1_ == 'v'
local_38._6_1_ == 'e'
local_38._7_1_ == 'r'
...n3ver

local_30 == '_'
local_30._1_1_ == 't'
local_30._2_1_ == '0' 
local_30._3_1_ == '_'
local_30._4_1_ == 'b'
local_30._5_1_ == '3'
local_30._6_1_ == '_'
local_30._7_1_ == 'r'
_t0_b3_r

local_28 == '3'
local_28._1_1_ == 'p'
local_28._2_1_ == '4'
local_28._3_1_ == '1'
local_28._4_1_ == 'r'
local_28._5_1_ == '3'
local_28._6_1_ == 'd'
local_28._7_1_ == '}'
3p41r3d}
````

**Le flag ; HTB{br0k3n_4p4rt...n3ver_t0_b3_r3p41r3d}**
