## Login

*ce challenge a eu une modification il y a peu de temps en janvier 2023*

Avec ce challenge on nous donne uniquement un site web avec une page de connexion. 

Aucune indication, sauf si on fait des tests comme admin:admin on nous dit s'il s'agit du bon ou mauvais login.

Au début j'ai pensé à utiliser hydra, mais avant de sortir l'artillerie lourde, j'ai en réalité creusé du coté du debugger dans firefox. 

``````
async()=>{await new Promise((e=>window.addEventListener("load",e))),document.querySelector("form").addEventListener("submit",(e=>{e.preventDefault();const r={u:"input[name=username]",p:"input[name=password]"},t={};for(const e in r)t[e]=btoa(document.querySelector(r[e]).value).replace(/=/g,"");return"YWRtaW4"!==t.u?alert("Incorrect Username"):"cGljb0NURns1M3J2M3JfNTNydjNyXzUzcnYzcl81M3J2M3JfNTNydjNyfQ"!==t.p?alert("Incorrect Password"):void alert(`Correct Password! Your flag is ${atob(t.p)}.`)}))})();
``````````

On obtient ce bloc d'information. Ce qui saute à l'oeil est l'indication    
cGljb0NURns1M3J2M3JfNTNydjNyXzUzcnYzcl81M3J2M3JfNTNydjNyfQ 

Si vous utilisez cyberchef (from base64), vous obtenez  
**Answer:  picoCTF{53rv3r_53rv3r_53rv3r_53rv3r_53rv3r}**