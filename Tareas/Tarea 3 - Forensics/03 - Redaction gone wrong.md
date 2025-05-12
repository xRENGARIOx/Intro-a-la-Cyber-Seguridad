# Redaction gone wrong

## Descripcion
Now you DON’T see me.This [report](https://artifacts.picoctf.net/c/84/Financial_Report_for_ABC_Labs.pdf) has some critical data in it, some of which have been redacted correctly, while some were not. Can you find an important key that was not redacted properly?
## Solucion
Primero descargamos el archivo que nos proporciona el reto:
```sh
┌──(xrengariox㉿PC)-[~/Clase/redaction]
└─$ wget https://artifacts.picoctf.net/c/84/Financial_Report_for_ABC_Labs.pdf
--2025-05-11 19:33:14--  https://artifacts.picoctf.net/c/84/Financial_Report_for_ABC_Labs.pdf
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.26, 3.161.55.100, 3.161.55.64, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.26|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 34915 (34K) [application/octet-stream]
Saving to: ‘Financial_Report_for_ABC_Labs.pdf’

Financial_Report_for_ABC_Labs.pdf    100%[===================================================================>]  34.10K  --.-KB/s    in 0.01s   

2025-05-11 19:33:15 (2.27 MB/s) - ‘Financial_Report_for_ABC_Labs.pdf’ saved [34915/34915]

```

Ahora comenzamos con el analisis para ver que podemos encontrar:
```sh
┌──(xrengariox㉿PC)-[~/Clase/redaction]
└─$ file Financial_Report_for_ABC_Labs.pdf 
Financial_Report_for_ABC_Labs.pdf: PDF document, version 1.7, 1 page(s)
```

Y si abrimos el documento, podemos ver que hay texto oculto con color negro, sin embargo al pasar el mouse por encima y seleccionar el texto somos capaces de ver la bandera:
```flag
picoCTF{C4n_Y0u_S33_m3_fully}
```
## Notas adicionales

## Referencias
