# interencdec

## Descripcion
Can you get the real meaning from this file.Download the file [here](https://artifacts.picoctf.net/c_titan/111/enc_flag).
## Solucion
Primero descargamos el achivo que nos da el reto:
```sh
┌──(xrengariox㉿PC)-[~/Clase/crypto/intere]
└─$ wget https://artifacts.picoctf.net/c_titan/111/enc_flag                                      
--2025-05-12 13:13:55--  https://artifacts.picoctf.net/c_titan/111/enc_flag
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.61, 3.161.55.26, 3.161.55.64, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.61|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 73 [application/octet-stream]
Saving to: ‘enc_flag’

enc_flag                             100%[===================================================================>]      73  --.-KB/s    in 0s      

2025-05-12 13:13:55 (60.7 MB/s) - ‘enc_flag’ saved [73/73]
```

Ahora vamos a ver el contenido:
```sh
YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclh6ZzVNR3N5TXpjNWZRPT0nCg==
```

Parece un base64, asi que vamos a desencriptarlo:
```sh
┌──(xrengariox㉿PC)-[~/Clase/crypto/intere]
└─$ echo "YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclh6ZzVNR3N5TXpjNWZRPT0nCg==" | base64 -d
b'd3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrXzg5MGsyMzc5fQ=='
```

Y nos da otra cadena que parece base64:
```sh
┌──(xrengariox㉿PC)-[~/Clase/crypto/intere]
└─$ echo "d3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrXzg5MGsyMzc5fQ==" |base64 -d                         
wpjvJAM{jhlzhy_k3jy9wa3k_890k2379}  
```

Entonces ahora esto ya tiene el formato de la flag, pero parece rotado, entonces vamos a usar cyberchef para rotarlo:
```
input: wpjvJAM{jhlzhy_k3jy9wa3k_890k2379}  

recipe: rot19

output: picoCTF{caesar_d3cr9pt3d_890d2379}
```

Y asi encontramos la flag:
```flag
picoCTF{caesar_d3cr9pt3d_890d2379}
```

## Notas adicionales

## Referencias
