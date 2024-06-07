## Easy1 - cryptochallenge picoCTF

Description; 
`````
The one time pad can be cryptographically secure, but not when you know the key. Can you solve this? We've given you the encrypted flag, key, and a table to help UFJKXQZQUNB with the key of SOLVECRYPTO. Can you use this table to solve it?.
`````

Il y a un lien pour la "table" qui nous donne ceci; 
`````
   A B C D E F G H I J K L M N O P Q R S T U V W X Y Z 
   +----------------------------------------------------
A | A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
B | B C D E F G H I J K L M N O P Q R S T U V W X Y Z A
C | C D E F G H I J K L M N O P Q R S T U V W X Y Z A B
D | D E F G H I J K L M N O P Q R S T U V W X Y Z A B C
E | E F G H I J K L M N O P Q R S T U V W X Y Z A B C D
F | F G H I J K L M N O P Q R S T U V W X Y Z A B C D E
G | G H I J K L M N O P Q R S T U V W X Y Z A B C D E F
H | H I J K L M N O P Q R S T U V W X Y Z A B C D E F G
I | I J K L M N O P Q R S T U V W X Y Z A B C D E F G H
J | J K L M N O P Q R S T U V W X Y Z A B C D E F G H I
K | K L M N O P Q R S T U V W X Y Z A B C D E F G H I J
L | L M N O P Q R S T U V W X Y Z A B C D E F G H I J K
M | M N O P Q R S T U V W X Y Z A B C D E F G H I J K L
N | N O P Q R S T U V W X Y Z A B C D E F G H I J K L M
O | O P Q R S T U V W X Y Z A B C D E F G H I J K L M N
P | P Q R S T U V W X Y Z A B C D E F G H I J K L M N O
Q | Q R S T U V W X Y Z A B C D E F G H I J K L M N O P
R | R S T U V W X Y Z A B C D E F G H I J K L M N O P Q
S | S T U V W X Y Z A B C D E F G H I J K L M N O P Q R
T | T U V W X Y Z A B C D E F G H I J K L M N O P Q R S
U | U V W X Y Z A B C D E F G H I J K L M N O P Q R S T
V | V W X Y Z A B C D E F G H I J K L M N O P Q R S T U
W | W X Y Z A B C D E F G H I J K L M N O P Q R S T U V
X | X Y Z A B C D E F G H I J K L M N O P Q R S T U V W
Y | Y Z A B C D E F G H I J K L M N O P Q R S T U V W X
Z | Z A B C D E F G H I J K L M N O P Q R S T U V W X Y
`````

La tout de suite ca nous parle! Dans la cas contraire avec une petite recherche sur le terme "one time pad" + "cipher" vous allez tomber sur ca ; 
https://en.wikipedia.org/wiki/One-time_pad

En francais on appelle ca, "masque jettable" et "chiffre de vernam" 
Sur l'article wikipedia dont j'ai mis le lien, vous trouverez la manière de résoudre cela mais en gros ; 

  U (20) F (5) J (9) K (10) X (23) Q (16) Z (25) Q (16) U (20) N (13) B (1)      message   
-S (18) O (14) L (11) V (21) E (4) C (2) R (17) Y (24) P (15) T (19) O (14) masque      
2,          -9,     -2,    -11,     19,    14,    8,     -8,     5,      -6,     -13  
2, 17 (-9+26), 24 (-2+26), 15 (-11+26), 19, 14, 8, 18, 5, 20, 13

CRYPTOISFUN


la réponse **picoCTF{CRYPTOISFUN}**

Si besoin;  
0 a   
1 b   
2 c   
3 d   
4 e   
5 f   
6 g   
7 h     
8 i   
9 j   
10 k    
11 l    
12 m    
13 n    
14 o    
15 p    
16 q    
17 r    
18 s    
19 t    
20 u    
21 v    
22 w    
23 x    
24 y    
25 z    


