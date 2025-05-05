# tunn3l v1s10n

## Descripcion
We found this [file](https://mercury.picoctf.net/static/da18eed3d15fd04f7b076bdcecf15b27/tunn3l_v1s10n). Recover the flag.
## Solucion
Primero descargamos el archivo que nos proporciona el reto:
```sh
┌──(xrengariox㉿PC)-[~/Clase/tunel]
└─$ wget https://mercury.picoctf.net/static/da18eed3d15fd04f7b076bdcecf15b27/tunn3l_v1s10n
--2025-05-05 12:44:03--  https://mercury.picoctf.net/static/da18eed3d15fd04f7b076bdcecf15b27/tunn3l_v1s10n
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2893454 (2.8M) [application/octet-stream]
Saving to: ‘tunn3l_v1s10n’

tunn3l_v1s10n                        100%[===================================================================>]   2.76M   165KB/s    in 8.3s    

2025-05-05 12:44:19 (342 KB/s) - ‘tunn3l_v1s10n’ saved [2893454/2893454]
```

Es un archivo que parece querese abrir como imagen BMP, pero esta damaged, entonces vamos a tener que repararlo con el editor hexadecimal:

```sh
00000000   42 4D 8E 26  2C 00 00 00  00 00 28 00  00 00 28 00  00 00 6E 04  00 00 32 01  00 00 01 00  BM.&,.....(...(...n...2.....
```

Asi quedaria reparado el header, pero ahora nos falta acomodar el alto:
```sh
00000000   42 4D 8E 26  2C 00 00 00  00 00 28 00  00 00 28 00  00 00 6E 04  00 00 40 03  00 00 01 00  BM.&,.....(...(...n...@.....
```

Y asi vemos la bandera en la imagen: 
```flag
picoCTF{qu1t3_a_v13w_2020}
```


## Notas adicionales

## Referencias
