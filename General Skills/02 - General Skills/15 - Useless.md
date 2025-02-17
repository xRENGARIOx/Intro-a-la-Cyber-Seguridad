# Useless

## Descripcion
There's an interesting script in the user's home directoryThe work computer is running SSH. We've been given a script which performs some basic calculations, explore the script and find a flag.

```
Hostname: saturn.picoctf.net
Port:     61782
Username: picoplayer
Password: password
```

## Solucion
Primero nos concetamos al reto mediante ssh con las credenciales que nos proporcionan:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ ssh saturn.picoctf.net -p 61782 -l picoplayer
```
Hacemos un ls para ver que archivos tienen el usuario en su directorio:
```
picoplayer@challenge:~$ ls
useless
```
Solo vemos un archivo llamado useless, asi que vemos el contenido de este archivo
```bash
picoplayer@challenge:~$ cat useless 
#!/bin/bash
# Basic mathematical operations via command-line arguments

if [ $# != 3 ]
then
  echo "Read the code first"
else
        if [[ "$1" == "add" ]]
        then 
          sum=$(( $2 + $3 ))
          echo "The Sum is: $sum"  

        elif [[ "$1" == "sub" ]]
        then 
          sub=$(( $2 - $3 ))
          echo "The Substract is: $sub" 

        elif [[ "$1" == "div" ]]
        then 
          div=$(( $2 / $3 ))
          echo "The quotient is: $div" 

        elif [[ "$1" == "mul" ]]
        then
          mul=$(( $2 * $3 ))
          echo "The product is: $mul" 

        else
          echo "Read the manual"
         
        fi
fi

```
Pero solamente vemos que es un codigo que realiza operaciones basicas.
Entonces procedemos a ver el manual escribiendo el comando:
```bash
man useless
```
Y vemos que en el manual nos dice la flag:
```
picoplayer@challenge:~$ man useless 

useless
     useless, — This is a simple calculator script

SYNOPSIS
     useless, [add sub mul div] number1 number2

DESCRIPTION
     Use the useless, macro to make simple calulations like addition,subtraction, multiplication and division.

Examples
     ./useless add 1 2
       This will add 1 and 2 and return 3

     ./useless mul 2 3
       This will return 6 as a product of 2 and 3

     ./useless div 6 3
       This will return 2 as a quotient of 6 and 3

     ./useless sub 6 5
       This will return 1 as a remainder of substraction of 5 from 6

Authors
     This script was designed and developed by Cylab Africa

     picoCTF{us3l3ss_ch4ll3ng3_3xpl0it3d_8504}
```

```flag
picoCTF{us3l3ss_ch4ll3ng3_3xpl0it3d_8504}
```

## Notas adicionales

## Referencias
