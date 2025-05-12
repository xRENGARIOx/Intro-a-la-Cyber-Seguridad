# Tapping

## Descripcion
Theres tapping coming in from the wires. What's it saying `nc jupiter.challenges.picoctf.org 21610`.
## Solucion
Primero nos conectamos al reto con el comando que nos dan:
```sh
┌──(xrengariox㉿PC)-[~/Clase/crypto/table]
└─$ nc jupiter.challenges.picoctf.org 21610 
.--. .. -.-. --- -.-. - ..-. { -- ----- .-. ... ...-- -.-. ----- -.. ...-- .---- ... ..-. ..- -. ...-- ----. ----- ..--- ----- .---- ----. ..... .---- ----. }
```

Nos da una serie de puntos y guiones en lo que parece ser codigo morse, asi que vamos a buscar una herramienta online:
```
input: .--. .. -.-. --- -.-. - ..-. { -- ----- .-. ... ...-- -.-. ----- -.. ...-- .---- ... ..-. ..- -. ...-- ----. ----- ..--- ----- .---- ----. ..... .---- ----. }

output: picoctfm0rs3c0d31sfun3902019519
```

Y la bandera queda asI:
```flag
picoctf{m0rs3c0d31sfun3902019519}
```
## Notas adicionales

## Referencias
