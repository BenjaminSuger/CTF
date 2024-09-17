# Bit-O-Asm-2

Sur ma chaine youtube j'ai fais une vidéo avec les 4 challenges ; https://www.youtube.com/watch?v=rIGCalb-H7k 

Goal ; trouver la valeur du registre eax à partir d'une serie d'instruction en assembly (x86)

On nous donne le fichier txt suivant ; 

````
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0x4],0x9fe1a
<+22>:    mov    eax,DWORD PTR [rbp-0x4]
<+25>:    pop    rbp
<+26>:    ret
````

Si vous vous basez sur le précedent challenge, vous savez qu'il n'y a que toutes les lignes ne sont pas importantes. 

Si on supprime les lignes inutiles on obtient ; 

````
<+15>:    mov    DWORD PTR [rbp-0x4],0x9fe1a
<+22>:    mov    eax,DWORD PTR [rbp-0x4]
````

Donc sur la ligne +15 => on met la valeur 0x9fe1a dans DWORD PTR [rbp-0x4]  
qui va lui même etre transmit dans la ligne +22 à eax 

donc la valeur de eax = 0x9fe1a
Il faut le traduire en décimale et le mettre dans le flag picoCTF{}