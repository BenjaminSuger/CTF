## FLAG COMMAND

Dans ce challenge on nous donne une adresse IP pour un site qui se déroule un peu comme un jeu de rôles à l'ancienne. 

On peut faire des choix d'action, qui vont nous amener vers d'autres possibilités avec des succès ou des échecs (aka la mort). 

J'ai testé pour voir déjà comment cela se comporte;         

-Certaines commandes fonctionnent mais pas toutes.      
Le choix du début de la direction est obligatoirement HEAD NORTH    

-Mort assuré quoi qu'il arrive.         
Peu importe le choix que vous allez faire, vous allez mourir.          

-Vous ne pouvez pas faire d'autres commandes comme "ls", "pwd", "dir".      
Que cela soit avec | || & && etc....            

La solution réside dans le code JS de la page quand vous l'examinez.

Vous allez trouver plusieurs informations; 
`````
<script src="/static/terminal/js/commands.js" type="module"></script>
<script src="/static/terminal/js/main.js" type="module"></script>
<script src="/static/terminal/js/game.js" type="module"></script>
````
Le plus intéressant étant main.js

````
async function CheckMessage() {
    fetchingResponse = true;
    currentCommand = commandHistory[commandHistory.length - 1];

    if (availableOptions[currentStep].includes(currentCommand) || availableOptions['secret'].includes(currentCommand)) {
        await fetch('/api/monitor', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ 'command': currentCommand })
        })
            .then((res) => res.json())
            .then(async (data) => {
                console.log(data)
                await displayLineInTerminal({ text: data.message });

                if(data.message.includes('Game over')) {
                    playerLost();
                    fetchingResponse = false;
                    return;
                }

                if(data.message.includes('HTB{')) {
                    playerWon();
                    fetchingResponse = false;

                    return;
                }

                if (currentCommand == 'HEAD NORTH') {
                    currentStep = '2';
                }
                else if (currentCommand == 'FOLLOW A MYSTERIOUS PATH') {
                    currentStep = '3'
                }
                else if (currentCommand == 'SET UP CAMP') {
                    currentStep = '4'
                }

                let lineBreak = document.createElement("br");


                beforeDiv.parentNode.insertBefore(lineBreak, beforeDiv);
                displayLineInTerminal({ text: '<span class="command">You have 4 options!</span>' })
                displayLinesInTerminal({ lines: availableOptions[currentStep] })
                fetchingResponse = false;
            });


    }
    else {
        displayLineInTerminal({ text: "You do realise its not a park where you can just play around and move around pick from options how are hard it is for you????" });
        fetchingResponse = false;
    }
}
`````

Dans ce code voici ce qui nous intéresse; 

-On nous parle de /api/monitor (qu'on peut trouver aussi avec Burp Suite). C'est quelque chose à tester. Voir s'il y a d'autres /api/[...]

-on nous parle d'un secret => availableOptions['secret'] il doit donc y avoir une commande qu'on ne connait pas qui débloque la solution


-nos précédentes observations tiennent toujours sur les choix possibles;     

        if (currentCommand == 'HEAD NORTH') {
                    currentStep = '2';
                }
                else if (currentCommand == 'FOLLOW A MYSTERIOUS PATH') {
                    currentStep = '3'
                }
                else if (currentCommand == 'SET UP CAMP') {
                    currentStep = '4'

Pour tester /api/, j'ai utilisé gobuster;      
gobuster dir -u http://[IP_DU_SITE]/api/ -w /usr/share/wordlists/dirbuster/directory-list-1.0.txt

En résultat j'ai trouvé /options
si vous allez sur http://[IP_DU_SITE]/api/options vous aurez le résultat suivant; 

	
allPossibleCommands	        
1	        
0	"HEAD NORTH"        
1	"HEAD WEST"     
2	"HEAD EAST"     
3	"HEAD SOUTH"        
2	        
0	"GO DEEPER INTO THE FOREST"     
1	"FOLLOW A MYSTERIOUS PATH"      
2	"CLIMB A TREE"      
3	"TURN BACK"     
3	
0	"EXPLORE A CAVE"        
1	"CROSS A RICKETY BRIDGE"        
2	"FOLLOW A GLOWING BUTTERFLY"        
3	"SET UP CAMP"       
4	
0	"ENTER A MAGICAL PORTAL"        
1	"SWIM ACROSS A MYSTERIOUS LAKE"     
2	"FOLLOW A SINGING SQUIRREL"     
3	"BUILD A RAFT AND SAIL DOWNSTREAM"      
secret	        
0	"Blip-blop, in a pickle with a hiccup! Shmiggity-shmack"        

On a donc la commande secrète à mettre dans les choix. SI on l'insère, on obtient le flag;   
HTB{D3v3l0p3r_t00l5_4r3_b35t__t0015_wh4t_d0_y0u_Th1nk??}


