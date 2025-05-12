# Easy 1

## Descripcion
The one time pad can be cryptographically secure, but not when you know the key. Can you solve this? We've given you the encrypted flag, key, and a table to help `UFJKXQZQUNB` with the key of `SOLVECRYPTO`. Can you use this [table](https://jupiter.challenges.picoctf.org/static/1fd21547c154c678d2dab145c29f1d79/table.txt) to solve it?.
## Solucion
Primero descargamos el archivo que nos da el reto:
```sh
┌──(xrengariox㉿PC)-[~/Clase/crypto/table]
└─$ wget https://jupiter.challenges.picoctf.org/static/1fd21547c154c678d2dab145c29f1d79/table.txt 
--2025-05-11 22:39:48--  https://jupiter.challenges.picoctf.org/static/1fd21547c154c678d2dab145c29f1d79/table.txt
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1571 (1.5K) [application/octet-stream]
Saving to: ‘table.txt’

table.txt                            100%[===================================================================>]   1.53K  --.-KB/s    in 0s      

2025-05-11 22:39:48 (62.6 MB/s) - ‘table.txt’ saved [1571/1571]

```

Ahora con la llave que nos dan vamos a intentar romper el cifrado, para ello primero vemos el contenido de la tabla:
```
    A B C D E F G H I J K L M N O P Q R S T U V W X Y Z 
   +----------------------------------------------------
A | A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
B | B C D E F G H I J K L M N O P Q R S T U V W X Y Z A
C | C D E F G H I J K L M N O P Q R S T U V W X Y Z A B
D | D E F G H I J K L M N O P Q R S T U V W X Y Z A B C
E | E F G H I J K L M N O P Q R S T U V W X Y Z A B C D
F | F G H I J K L M N O P Q R S T U V W X Y Z A B C D E
G | G H I J K L M N O P Q R S T U V W X Y Z A B C D E F
H | H I J K L M N O P Q R S T U V W X Y Z A B C D E F G
I | I J K L M N O P Q R S T U V W X Y Z A B C D E F G H
J | J K L M N O P Q R S T U V W X Y Z A B C D E F G H I
K | K L M N O P Q R S T U V W X Y Z A B C D E F G H I J
L | L M N O P Q R S T U V W X Y Z A B C D E F G H I J K
M | M N O P Q R S T U V W X Y Z A B C D E F G H I J K L
N | N O P Q R S T U V W X Y Z A B C D E F G H I J K L M
O | O P Q R S T U V W X Y Z A B C D E F G H I J K L M N
P | P Q R S T U V W X Y Z A B C D E F G H I J K L M N O
Q | Q R S T U V W X Y Z A B C D E F G H I J K L M N O P
R | R S T U V W X Y Z A B C D E F G H I J K L M N O P Q
S | S T U V W X Y Z A B C D E F G H I J K L M N O P Q R
T | T U V W X Y Z A B C D E F G H I J K L M N O P Q R S
U | U V W X Y Z A B C D E F G H I J K L M N O P Q R S T
V | V W X Y Z A B C D E F G H I J K L M N O P Q R S T U
W | W X Y Z A B C D E F G H I J K L M N O P Q R S T U V
X | X Y Z A B C D E F G H I J K L M N O P Q R S T U V W
Y | Y Z A B C D E F G H I J K L M N O P Q R S T U V W X
Z | Z A B C D E F G H I J K L M N O P Q R S T U V W X Y
```

Lo podemos hacer manual o con ayuda de una herramienta online, simplemente ingresamos el texto cifrado y la llave y nos entregan la salida:
```
CRYPTOISFUN
```

Manualmente, hay que buscar en la columna de la izquierda la letra de la llave, y luego buscar a la derecha el caracter cifrado y donde este, hasta arriba encontraremos el texto plano.

Entonces la flag queda:
```flag
picoCTF{CRYPTOISFUN}
```
## Notas adicionales
Tambien se puede usar un script de python:
```python
def otp_decrypt(ciphertext, key):
    plaintext = ''
    for c, k in zip(ciphertext, key):
        c_val = ord(c) - ord('A')
        k_val = ord(k) - ord('A')
        p_val = (c_val - k_val) % 26
        plaintext += chr(p_val + ord('A'))
    return plaintext

ciphertext = "UFJKXQZQUNB" 
key = "SOLVECRYPTO" 

plaintext = otp_decrypt(ciphertext, key)
print("picoCTF{"+plaintext+"}")
```
## Referencias
https://www.boxentriq.com/code-breaking/one-time-pad