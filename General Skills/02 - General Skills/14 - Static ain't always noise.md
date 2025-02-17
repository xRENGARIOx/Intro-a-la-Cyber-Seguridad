# Static ain't always noise

## Descripcion
Can you look at the data in this binary: [static](https://mercury.picoctf.net/static/66932732825076cad4ba43e463dae82f/static)? This [BASH script](https://mercury.picoctf.net/static/66932732825076cad4ba43e463dae82f/ltdis.sh) might help!
## Solucion
Primero descargamos el archivo y vemos que tipo de archivo es:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ file static  
static: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=277d07901cf99a335a8107fbdd6642d9c6140bb5, not stripped
```
Vemos que es un archivo ejecutable, entonces probamos a usar el comando strings para obtener las cadenas y las filtramos con ayuda de grep.

```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ strings static | grep "pico"
picoCTF{d15a5m_t34s3r_f5aeda17}
```
Y asi obtenemos la flag.
```flag
picoCTF{d15a5m_t34s3r_f5aeda17}
```


## Notas adicionales

## Referencias
