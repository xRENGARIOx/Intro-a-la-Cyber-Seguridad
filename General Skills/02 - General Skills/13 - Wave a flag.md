# Wave a flag

## Descripcion
Can you invoke help flags for a tool or binary? [This program](https://mercury.picoctf.net/static/a14be2648c73e3cda5fc8490a2f476af/warm) has extraordinarily helpful information...
## Solucion
Primero hacemos un file para ver que tipo de archivo es el que descargamos:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ file warm   
warm: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=3181a501366281ab5eba1c41e54a1f40800e3966, with debug_info, not stripped

```
Nos dice que es un ELF de 64 bits, entonces podemos hacer uso de la herramienta strings para ver las cadenas que tiene, y si las filtramos por pico con ayuda de grep, obtenemos la flag:
```
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ strings warm | grep "pico"
Oh, help? I actually don't do much, but I do have this flag here: picoCTF{b1scu1ts_4nd_gr4vy_755f3544}
```

```flag
picoCTF{b1scu1ts_4nd_gr4vy_755f3544}
```


Adicional a esto, si le damos permisos de ejecucion al archivo y despues lo corremos y le pasamos como argumento el -h, nos da tambien la flag:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ chmod +x warm
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ ./warm              
Hello user! Pass me a -h to learn what I can do!
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ ./warm -h
Oh, help? I actually don't do much, but I do have this flag here: picoCTF{b1scu1ts_4nd_gr4vy_755f3544}

```
## Notas adicionales

## Referencias
