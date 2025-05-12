# caesar

## Descripcion
Decrypt this [message](https://jupiter.challenges.picoctf.org/static/7d707a443e95054dc4cf30b1d9522ef0/ciphertext).
## Solucion
Descargamos el archivo que nos proporciona el reto:
```sh

┌──(xrengariox㉿PC)-[~/Clase/crypto/caesar]
└─$ wget https://jupiter.challenges.picoctf.org/static/7d707a443e95054dc4cf30b1d9522ef0/ciphertext     
--2025-05-11 22:35:14--  https://jupiter.challenges.picoctf.org/static/7d707a443e95054dc4cf30b1d9522ef0/ciphertext
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 35 [application/octet-stream]
Saving to: ‘ciphertext’

ciphertext                           100%[===================================================================>]      35  --.-KB/s    in 0s      

2025-05-11 22:35:14 (17.7 MB/s) - ‘ciphertext’ saved [35/35]
```

Vemos su contenido:
```
picoCTF{gvswwmrkxlivyfmgsrhnrisegl}
```

Ahora vamos a dcode para romper el cifrado caesar:
```
input: gvswwmrkxlivyfmgsrhnrisegl

bruteforce

output: crossingtherubicondjneoach 
```

Y ya tenemos nuestra flag:
```flag
picoCTF{crossingtherubicondjneoach}
```

## Notas adicionales

## Referencias
https://www.dcode.fr/caesar-cipher