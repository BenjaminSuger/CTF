# Bit-O-Asm-1 

Goal ; Trouver la valeur du registre EAX 

on nous donne un fichier texte ; 

````
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x4],edi
<+11>:    mov    QWORD PTR [rbp-0x10],rsi
<+15>:    mov    eax,0x30
<+20>:    pop    rbp
<+21>:    ret

````

Qu'est-ce que c'est ?   
C'est de l'assembly (assembleur x86)

Ici il y a beaucoup de bruit, c'est à dire de ligne inutiles pour nous, on ne recherche que la valeur de EAX. 

la ligne qui nous intéresse est la ligne +15; 
`````
<+15>:    mov    eax,0x30
``````
L'instruction mov met la valeur de la source vers la destination en sachant que mov destination, source

Donc ici nous avons un la valeur 0x30 qui est mise dans le registre eax

On traduit 0x30 en valeur décimale et on trouve notre solution
``solution ;  picoCTF{48}``

J'ai fais une vidéo youtube avec plus d'explications et différents challenge du picoCTF ; https://www.youtube.com/watch?v=rIGCalb-H7k 
