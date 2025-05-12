# The Numbers

## Descripcion
The [numbers](https://jupiter.challenges.picoctf.org/static/f209a32253affb6f547a585649ba4fda/the_numbers.png)... what do they mean?
## Solucion
Descargamos el archivo que nos da el reto para comenzar a analizarlo:
```sh
┌──(xrengariox㉿PC)-[~/Clase/crypto/numbers]
└─$ wget https://jupiter.challenges.picoctf.org/static/f209a32253affb6f547a585649ba4fda/the_numbers.png
--2025-05-11 22:26:04--  https://jupiter.challenges.picoctf.org/static/f209a32253affb6f547a585649ba4fda/the_numbers.png
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 100721 (98K) [application/octet-stream]
Saving to: ‘the_numbers.png’

the_numbers.png                      100%[===================================================================>]  98.36K  --.-KB/s    in 0.1s    

2025-05-11 22:26:04 (672 KB/s) - ‘the_numbers.png’ saved [100721/100721]


┌──(xrengariox㉿PC)-[~/Clase/crypto/numbers]
└─$ open the_numbers.png 

```

Al abrir la imagen vemos los siguientes numeros:
```sh
16 9 3 15 3 20 6 { 20 8 5 14 21 13 2 5 18 19 13 1 19 15 14 }
```

Como podemos ver tiene el formato de la bandera:
```
picoCTF{}
```

Entonces vamos a convertirlo a caracteres y obtener la flag:
```sh
picoctf{thenumbersmason}
```
## Notas adicionales
Que buena referencia a Call of Duty.
## Referencias
