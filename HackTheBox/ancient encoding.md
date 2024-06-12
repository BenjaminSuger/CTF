## Ancient encoding

Description;        
*"Your initialization sequence requires loading various programs to gain the necessary knowledge and skills for your journey. Your first task is to learn the ancient encodings used by the aliens in their communication."*

On nous donne 2 fichiers;       
-output.txt     
-source.py

Output.txt; 
0x53465243657a51784d56383361444e664d32356a4d475178626a6c664e44497a5832677a4d6a4e664e7a42664e5463306558303d      

source.py;

````
from Crypto.Util.number import bytes_to_long
from base64 import b64encode
from secret import FLAG


def encode(message):
    return hex(bytes_to_long(b64encode(message)))


def main():
    encoded_flag = encode(FLAG)
    with open("output.txt", "w") as f:
        f.write(encoded_flag)


if __name__ == "__main__":
    main()
````

Si on regarde ce code, il est composé de 3 blocs;      

Le premier bloc qui commence par "from...." permet de charger les outils nécessaires; bytes_to_long, b64encode et le FLAG.

Le second bloc crée la fonction encode(), c'est la partie la plus intéressante car ca va nous permettre de trouver comment inverser le processus. 
Il va d'abord encoder notre message en b64 puis en hex. Donc logiquement si on fait l'inverse => hex => b64 ca va nous permettre d'avoir notre flag. 

Pour ce qui est du dernier bloc de code, il vient juste faire l'opération de mettre le résultat dans "output.txt" qui est le fichier qu'on nous a donné. 

ASTUCE; pour gagner du temps, vous pouvez utiliser CyberChef https://gchq.github.io/CyberChef/ 

De la vous pouvez faire "From Hex" et "From Base64" et tout de suite avoir le résultat

**HTB{411_7h3_3nc0d1n9_423_h323_70_574y}**