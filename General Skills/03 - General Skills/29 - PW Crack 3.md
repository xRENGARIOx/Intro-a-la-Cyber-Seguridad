# PW Crack 3

## Descripcion
Can you crack the password to get the flag?Download the password checker [here](https://artifacts.picoctf.net/c/17/level3.py) and you'll need the encrypted [flag](https://artifacts.picoctf.net/c/17/level3.flag.txt.enc) and the [hash](https://artifacts.picoctf.net/c/17/level3.hash.bin) in the same directory too. There are 7 potential passwords with 1 being correct. You can find these by examining the password checker script.

## Solucion
Descargamos los archivos que nos da el reto y vemos el contenido del script de python:
```python
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ cat level3.py 
import hashlib

### THIS FUNCTION WILL NOT HELP YOU FIND THE FLAG --LT ########################
def str_xor(secret, key):
    #extend key to secret length
    new_key = key
    i = 0
    while len(new_key) < len(secret):
        new_key = new_key + key[i]
        i = (i + 1) % len(key)        
    return "".join([chr(ord(secret_c) ^ ord(new_key_c)) for (secret_c,new_key_c) in zip(secret,new_key)])
###############################################################################

flag_enc = open('level3.flag.txt.enc', 'rb').read()
correct_pw_hash = open('level3.hash.bin', 'rb').read()


def hash_pw(pw_str):
    pw_bytes = bytearray()
    pw_bytes.extend(pw_str.encode())
    m = hashlib.md5()
    m.update(pw_bytes)
    return m.digest()


def level_3_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    user_pw_hash = hash_pw(user_pw)
    
    if( user_pw_hash == correct_pw_hash ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")



level_3_pw_check()


# The strings below are 7 possibilities for the correct password. 
#   (Only 1 is correct)
pos_pw_list = ["f09e", "4dcf", "87ab", "dba8", "752e", "3961", "f159"]
```

Entonces aqui podemos hacer 2 cosas, una es correr el codigo de python probando con las 7 passwords que nos da el propio archivo, o podemos seguir las pistas y ver el contenido del archivo de hash con el comando:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ bvi level3.hash.bin 

bvi version 1.4.2 (C) GPL 1996-2023 by Gerhard Buergmann

```

O tambien con la herramienta:
```bash
hexedit level3.hash.bin
```

Ambas opciones nos dan el siguiente hash:
```hash
E1 6D 55 A5 5D 80 DD DD 52 A8 3E AB EA 57 2B 7B
```

Entonces ahora de la lista de posibles passwords buscamos la que tenga el mismo hash md5 que es el que se usa en el script, hacemos ayuda de cyberchef:
```
Input: 87ab

Receipt: MD5

Output: e16d55a55d80dddd52a83eabea572b7b
```

Y asi tenemos la respuesta de cual es la password correcta, la ingresamos al script:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ python3 level3.py
Please enter correct password for flag: 87ab
Welcome back... your flag, user:
picoCTF{m45h_fl1ng1ng_cd6ed2eb}
```

Y nos arroja la flag:
```flag
picoCTF{m45h_fl1ng1ng_cd6ed2eb}
```


## Notas adicionales
Podemos pasarle el hash a la pagina https://crackstation.net la cual es muy buena para decirnos a que palabra pertenece ese hash y hasta el tipo de hash usado.

## Referencias

* https://crackstation.net
* https://gchq.github.io/CyberChef/#recipe=MD5()&input=ODdhYg
