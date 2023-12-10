## picoCTF Unpackme.py

Avec ce challenge, nous avons uniquement un accès à un script python "unpackme.py"

Pas de restriction, nous pouvons ouvrir le fichier sans problème pour essayer de comprendre ce qu'il fait. 

Si on essaie d'exécuter ce code, nous avons une question; "What's the password?"

Pour répondre à cela nous devons examiner le code et il y a une solution assez simple à ce problème. 

On peut observer qu'il y un chiffrage asymétrique avec Fernet. Même s'il n'est pas clair pour vous de quoi il s'agit, il faut comprendre que c'est la dernière ligne qui nous donne la question. 

``````
exec(plain.decode())
``````
Si au lieu d'exécuter cette partie, nous pouvions juste l'afficher avec print()?

En remplacant cela nous obtenons le résultat suivant; 
``````
pw = input('What\'s the password? ')

if pw == 'batteryhorse':
  print('picoCTF{175_chr157m45_5274ff21}')
else:
  print('That password is incorrect.')
``````
Maintenant c'est beaucoup plus clair, la variable payload contient ce code et cette question qu'on ne pouvait pas voir. Toute l'opération de déchiffrement est dans le but d'exécuter ce code. 

Réponse: **picoCTF{175_chr157m45_5274ff21}**

