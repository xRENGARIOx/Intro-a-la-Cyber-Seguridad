# Codebook

## Descripcion
## Solucion
Simplemente descargamos ambos archivos que nos proporciona el reto y corremos el script de python:

```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ python3 code.py 
```
Y nos da la flag:
```flag
picoCTF{c0d3b00k_455157_d9aa2df2}
```

Podemos ver el contenido de los archivos, el script de python:
```python
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ cat code.py 

import random
import sys



def str_xor(secret, key):
    #extend key to secret length
    new_key = key
    i = 0
    while len(new_key) < len(secret):
        new_key = new_key + key[i]
        i = (i + 1) % len(key)        
    return "".join([chr(ord(secret_c) ^ ord(new_key_c)) for (secret_c,new_key_c) in zip(secret,new_key)])


flag_enc = chr(0x13) + chr(0x01) + chr(0x17) + chr(0x07) + chr(0x2c) + chr(0x3a) + chr(0x2f) + chr(0x1a) + chr(0x0d) + chr(0x53) + chr(0x0c) + chr(0x47) + chr(0x0a) + chr(0x5f) + chr(0x5e) + chr(0x02) + chr(0x3e) + chr(0x5a) + chr(0x56) + chr(0x5d) + chr(0x45) + chr(0x5d) + chr(0x58) + chr(0x31) + chr(0x0d) + chr(0x58) + chr(0x0f) + chr(0x02) + chr(0x5a) + chr(0x10) + chr(0x0e) + chr(0x5d) + chr(0x13)



def print_flag():
  try:
    codebook = open('codebook.txt', 'r').read()
    
    password = codebook[4] + codebook[14] + codebook[13] + codebook[14] +\
               codebook[23]+ codebook[25] + codebook[16] + codebook[0]  +\
               codebook[25]
               
    flag = str_xor(flag_enc, password)
    print(flag)
  except FileNotFoundError:
    print('Couldn\'t find codebook.txt. Did you download that file into the same directory as this script?')



def main():
  print_flag()



if __name__ == "__main__":
  main()

```

Y el contenido del archivo codebook.txt:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ cat codebook.txt 
azbycxdwevfugthsirjqkplomn
```


## Notas adicionales

## Referencias
