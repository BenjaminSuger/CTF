# YOU CANT C ME 

Challenge de reverse sur HackTheBox 

On nous donne un seul fichier "auth"

step 1 ; file auth      
````
auth: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, stripped
````

Les informations qu'on peut voir;   
ELF     
x86  
stripped    
dynamically linked      

step 2 ;  executer l'executable

````
./auth
Welcome!
test #mon input a moi
I said, you can't c me!
````

Avec le nom du fichier 'auth' (pour authentication) et le resultat, on comprend qu'il faut trouver un mot passe.

step 3 ; ghidra

J'ai voulu voir avec ghidra si je pouvais trouver la solution. Avec cette recherche j'ai trouvé la fonction suivante ; 

````
undefined4 FUN_00401160(void)

{
  int iVar1;
  undefined8 local_48;
  undefined8 local_40;
  undefined4 local_38;
  char *UserInput;
  undefined8 Password;
  undefined8 local_20;
  undefined4 local_18;
  undefined local_14;
  int i;
  undefined4 local_c;
  
  local_c = 0;
  i = 0;
  printf("Welcome!\n");
  Password._0_1_ = 't';
  Password._1_1_ = 'h';
  Password._2_1_ = 'i';
  Password._3_1_ = 's';
  Password._4_1_ = '_';
  Password._5_1_ = 'i';
  Password._6_1_ = 's';
  Password._7_1_ = '_';
  local_20._0_1_ = 't';
  local_20._1_1_ = 'h';
  local_20._2_1_ = 'e';
  local_20._3_1_ = '_';
  local_20._4_1_ = 'p';
  local_20._5_1_ = 'a';
  local_20._6_1_ = 's';
  local_20._7_1_ = 's';
  local_18 = 0x64726f77;
  local_14 = 0;
  UserInput = (char *)malloc(0x15); #0x15 parce qu'il y a le \n à la fin => donc 21 cara
  local_48 = 0x5517696626265e6d;
  local_40 = 0x555a275a556b266f;
  local_38 = 0x29635559;
  for (i = 0; i < 0x14; i = i + 1) {     
    *(char *)((long)&Password + (long)i) = *(char *)((long)&local_48 + (long)i) + '\n';
  }
  fgets(UserInput,0x15,stdin);
  iVar1 = strcmp((char *)&Password,UserInput);
  if (iVar1 == 0) {
    printf("HTB{%s}\n",UserInput);
  }
  else {
    printf("I said, you can\'t c me!\n");
  }
  return local_c;
}
````

Qu'est-ce qu'on apprend de cela ? (ici j'ai renomer certains variable)


-l'input user est fait par fgets => il doit comporter 20 caractère (+le \n)     
-il fait une comparaison avec la fonction strcmp() ce qui va nous aider à trouver la solution plus tard     
-avant de faire la comparaisons la chaine de caractère password est modifié dans une boucle for avec local_48 => chaque caractère étant remplacé        

step 5 ; solution       
A partir de ghidra je n'ai pas réussis à trouver la solution.   
Du coup j'ai pensé au strcmp() et à l'outil ltrace. 

````
ltrace ./auth
printf("Welcome!\n"Welcome!
)                                     = 9
malloc(21)                                               = 0xe146b0
fgets(test
"test\n", 21, 0x7f3ad0cb8a80)                      = 0xe146b0
strcmp("wh00ps!_y0u_d1d_c_m3", "test\n")                 = 3
printf("I said, you can't c me!\n"I said, you can't c me!
)                      = 24
+++ exited (status 0) +++

````

On trouve notre flag avec la bonne longueur ; wh00ps!_y0u_d1d_c_m3