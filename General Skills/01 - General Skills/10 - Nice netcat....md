# Nice netcat

## Descripcion
There is a nice program that you can talk to by using this command in a shell: `$ nc mercury.picoctf.net 43239`, but it doesn't speak English...
## Solucion
Nos conectamos al servidor con el comando que nos proporcionan:
```sh
nc mercury.picoctf.net 43239
```
Y nos entrega la siguiente salida
```
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ nc mercury.picoctf.net 43239           
112 
105 
99 
111 
67 
84 
70 
123 
103 
48 
48 
100 
95 
107 
49 
116 
116 
121 
33 
95 
110 
49 
99 
51 
95 
107 
49 
116 
116 
121 
33 
95 
55 
99 
48 
56 
50 
49 
102 
53 
125 
10 
```
Entonces tomamos la salida y la pasamos a una herramienta online para convertir a caracteres.
```flag
picoCTF{g00d_k1tty!_n1c3_k1tty!_7c082f5}
```

## Notas adicionales

## Referencias
https://www.duplichecker.com/ascii-to-text.php

