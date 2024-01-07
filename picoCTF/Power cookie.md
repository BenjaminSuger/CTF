## Power Cookie

Nous avons un accès à un site internet. Sur celui-ci il y a un seul bouton "continue as a guest". 

Si on utilise ce bouton nous obtenons ce message "We apologize, but we have no guest services at the moment."

En regardant dans le debugger, nous pouvons observer ce code; 
``````
function continueAsGuest()
{
  window.location.href = '/check.php';
  document.cookie = "isAdmin=0";
}
``````
La solution semble toute trouver, il faut changer isAdmin pour la valeur 1.

Vous pouvez faire cela dans le navigateur (dans storage => cookies), vous retrouverez isAdmin et en changeant de valeur vous obtenez;


**Answer; picoCTF{gr4d3_A_c00k13_65fd1e1a}**