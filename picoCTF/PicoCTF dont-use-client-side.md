## picoCTF dont-use-client-side

Nous avons uniquement une adresse ; https://jupiter.challenges.picoctf.org/problem/29835/   

Sur la page web on nous demande ;    
*This is the secure login portal*   
*Enter valid credentials to proceed*    

En inspectant la page, et en allant dans "sources" si vous êtes sur Google chrome ou dans "debug" dans Mozilla.
``````
function verify() {
    checkpass = document.getElementById("pass").value;
    split = 4;
    if (checkpass.substring(0, split) == 'pico') {
      if (checkpass.substring(split*6, split*7) == '723c') {
        if (checkpass.substring(split, split*2) == 'CTF{') {
         if (checkpass.substring(split*4, split*5) == 'ts_p') {
          if (checkpass.substring(split*3, split*4) == 'lien') {
            if (checkpass.substring(split*5, split*6) == 'lz_7') {
              if (checkpass.substring(split*2, split*3) == 'no_c') {
                if (checkpass.substring(split*7, split*8) == 'e}') {
                  alert("Password Verified")
``````
Il faut alors juste recomposer la séquence.

Pour la reconstruire on commence par la première ligne avec la mention "pico" (on sait que tous les flags du picoCTF commencent comme ca). 
Puis vous prenez toujours le second argument dans "checkpass.substring(arugment1, argument2)

**ANSWER; picoCTF{no_clients_plz_7723ce}**
