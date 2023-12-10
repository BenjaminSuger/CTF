# picoCTF Keygenme-py

Pour ce challenge dans la catégorie "Reverse Engineering", nous avons uniquement accès à un fichier 'keygenme-trial.py'

Il s'agit d'un code en python

Nous pouvons ouvrir ce fichier sans problème (idéalement avec VSCode)

Dès les premières lignes nous avons une partie du flag que nous devons compléter;

```
key_part_static1_trial = "picoCTF{1n_7h3_|<3y_of_"
key_part_dynamic1_trial = "xxxxxxxx"
key_part_static2_trial = "}"
key_full_template_trial = key_part_static1_trial + key_part_dynamic1_trial + key_part_static2_trial
```

La recherche que nous devons effectuer est sur la partie key_part_dynamic1_trial qui nous est pour le moment inconnu

Notre recherche va continuer dans la définition de la fonction check_key() => ligne 140

```
  # TODO : test performance on toolbox container
        # Check dynamic part --v
        if key[i] != hashlib.sha256(username_trial).hexdigest()[4]:
            return False
        else:
            i += 1
```

Ici plusieurs choses découlent du username_trial, qui est donné au début du code 'SCHOFIELD'

1. hashlib.sha256() => va créer un hash à partir du username
2. .hexdigest() => va convertir le hash en une chaine de caractère hexadecimal
3. [4] va prendre le "quatrième" (attention nous sommes sous python, on commence donc à compter par 0) pour vérifier qu'il s'agit du bon caractère

Toute cette opération va être faites à plusieurs reprises. Le conseil que je peux vous donner si vous lisez cette solution car bloqué dans ce challenge => dans votre terminal faite l'opération 1 et 2.
Ce qui va vous permettre de retrouver la chaine de charactère et de compter pour retrouver le flag.


La réponse ; **picoCTF{1n_7h3_|<3y_of_e584b363}**
