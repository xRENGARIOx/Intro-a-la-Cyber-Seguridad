# Glitch Cat

## Descripcion
Our flag printing service has started glitching!`$ nc saturn.picoctf.net 59446`
## Solucion
Nos conectamos al servidor con el comando que nos proporcionan
```sh
nc saturn.picoctf.net 59446
```

Y nos entrega como salida la flag incompleta, y con caracteres en hexadecimal:
```
'picoCTF{gl17ch_m3_n07_' + chr(0x61) + chr(0x34) + chr(0x33) + chr(0x39) + chr(0x32) + chr(0x64) + chr(0x32) + chr(0x65) + '}'
```
Entonces solo convertimos los caracteres que faltan a ASCII con una herramienta online: 

```flag
picoCTF{gl17ch_m3_n07_a4392d2e}
```

Tambien, por el formato de la flag parece codigo de python, entonces solo lo imprimimos:
```python
Python 3.12.8 (main, Dec 13 2024, 13:19:48) [GCC 14.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> print('picoCTF{gl17ch_m3_n07_' + chr(0x61) + chr(0x34) + chr(0x33) + chr(0x39) + chr(0x32) + chr(0x64) + chr(0x32) + chr(0x65) + '}')
picoCTF{gl17ch_m3_n07_a4392d2e}

```


## Notas adicionales

## Referencias
https://www.duplichecker.com/hex-to-text.php
