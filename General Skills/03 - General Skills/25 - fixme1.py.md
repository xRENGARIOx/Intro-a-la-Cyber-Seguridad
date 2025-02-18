# fixme1.py

## Descripcion
Fix the syntax error in this Python script to print the flag.[Download Python script](https://artifacts.picoctf.net/c/25/fixme1.py)
## Solucion
Descargamos el script de python y vemos su contenido:
```python
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ cat fixme1.py            

import random



def str_xor(secret, key):
    #extend key to secret length
    new_key = key
    i = 0
    while len(new_key) < len(secret):
        new_key = new_key + key[i]
        i = (i + 1) % len(key)        
    return "".join([chr(ord(secret_c) ^ ord(new_key_c)) for (secret_c,new_key_c) in zip(secret,new_key)])


flag_enc = chr(0x15) + chr(0x07) + chr(0x08) + chr(0x06) + chr(0x27) + chr(0x21) + chr(0x23) + chr(0x15) + chr(0x5a) + chr(0x07) + chr(0x00) + chr(0x46) + chr(0x0b) + chr(0x1a) + chr(0x5a) + chr(0x1d) + chr(0x1d) + chr(0x2a) + chr(0x06) + chr(0x1c) + chr(0x5a) + chr(0x5c) + chr(0x55) + chr(0x40) + chr(0x3a) + chr(0x58) + chr(0x0a) + chr(0x5d) + chr(0x53) + chr(0x43) + chr(0x06) + chr(0x56) + chr(0x0d) + chr(0x14)

  
flag = str_xor(flag_enc, 'enkidu')
  print('That is correct! Here\'s your flag: ' + flag)

```

Podemos ejecutar el script para ver donde esta el error:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ python3 fixme1.py   
  File "/home/xrengariox/Downloads/fixme1.py", line 20
    print('That is correct! Here\'s your flag: ' + flag)
IndentationError: unexpected indent
```

Y vemos que simplemente es corregir la identacion del codigo, usamos una herramienta como vim:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ vi fixme1.py 
```

Tras corregir el error, ejecutamos el script y ahora nos da la flag:
```

┌──(xrengariox㉿PC)-[~/Downloads]
└─$ python3 fixme1.py
That is correct! Here's your flag: picoCTF{1nd3nt1ty_cr1515_6a476c8f}
```

```flag
picoCTF{1nd3nt1ty_cr1515_6a476c8f}
```


## Notas adicionales

## Referencias
