# c0rrupt

## Descripcion
We found this [file](https://jupiter.challenges.picoctf.org/static/ab30fcb7d47364b4190a7d3d40edb551/mystery). Recover the flag.
## Solucion
Primero descargamos el archivo que nos proporciona el reto:
```sh
┌──(xrengariox㉿PC)-[~/Clase/corru]
└─$ wget https://jupiter.challenges.picoctf.org/static/ab30fcb7d47364b4190a7d3d40edb551/mystery       
--2025-04-28 12:40:03--  https://jupiter.challenges.picoctf.org/static/ab30fcb7d47364b4190a7d3d40edb551/mystery
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 202940 (198K) [application/octet-stream]
Saving to: ‘mystery’

mystery                              100%[===================================================================>] 198.18K   192KB/s    in 1.0s    

2025-04-28 12:40:12 (192 KB/s) - ‘mystery’ saved [202940/202940]

```

Ahora vemos que es un archivo de datos:
```sh
┌──(xrengariox㉿PC)-[~/Clase/corru]
└─$ file mystery       
mystery: data
```

Entonces al ver el codigo hexadecimal podemos ver que parece no tener orden:
```sh
┌──(xrengariox㉿PC)-[~/Clase/corru]
└─$ xxd -l 100 mystery 
00000000: 8965 4e34 0d0a b0aa 0000 000d 4322 4452  .eN4........C"DR
00000010: 0000 066a 0000 0447 0802 0000 007c 8bab  ...j...G.....|..
00000020: 7800 0000 0173 5247 4200 aece 1ce9 0000  x....sRGB.......
00000030: 0004 6741 4d41 0000 b18f 0bfc 6105 0000  ..gAMA......a...
00000040: 0009 7048 5973 aa00 1625 0000 1625 0149  ..pHYs...%...%.I
00000050: 5224 f0aa aaff a5ab 4445 5478 5eec bd3f  R$......DETx^..?
00000060: 8e64 cd71                                .d.q
```

Entonces, viendo los magic bytes podemos ver que algunos coinciden como imagen, por lo cual posiblemente lo sea, entonces vamos a modificar estos magic bytes con hexedit, al hacer esto, podemos ver que el archivo sigue sin funcionar de manera adecuada, por lo cual vamos a hacer uso de una herramienta llamada `pngcheck` la cual nos puede decir mas o menos que es lo que le falta al archivo, o que se debe de verificar para que esta funcione correctamente.
Y en este caso lo que debemos de hacer es reparar los chunks del archivo (IHDR).

```sh
00000000  89 50 4E 47  0D 0A 1A 0A   00 00 00 0D  49 48 44 52   .PNG........IHDR
00000010  00 00 06 6A  00 00 04 47   08 02 00 00  00 7C 8B AB   ...j...G.....|..
00000020  78 00 00 00  01 73 52 47   42 00 AE CE  1C E9 00 00   x....sRGB.......
00000030  00 04 67 41  4D 41 00 00   B1 8F 0B FC  61 05 00 00   ..gAMA......a...
00000040  00 09 70 48  59 73 00 00   16 25 00 00  16 25 01 49   ..pHYs...%...%.I
00000050  52 24 F0 00  00 FF A5 49   44 41 54 78  5E EC BD 3F   R$.....IDATx^..?
00000060  8E 64 CD 71  BD 2D 8B 20   20 80 90 41  83 02 08 D0   .d.q.-.  ..A....
00000070  F9 ED 40 A0  F3 6E 40 7B   90 23 8F 1E  D7 20 8B 3E   ..@..n@{.#... .>
```

Y finalmente al terminar de repararlo, y abrir la imagen, podemos leer la flag:
```flag
picoCTF{c0rrupt10n_1847995}
```
## Notas adicionales

## Referencias
