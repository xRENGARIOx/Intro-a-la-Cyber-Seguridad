# Disk, disk, sleuth!

## Descripcion
Use `srch_strings` from the sleuthkit and some terminal-fu to find a flag in this disk image: [dds1-alpine.flag.img.gz](https://mercury.picoctf.net/static/4f3df7052b4121aff89af1a3f517afb1/dds1-alpine.flag.img.gz)
## Solucion
Descargamos el archivo que nos proporciona el reto y lo descomprimimos:
```sh
┌──(xrengariox㉿PC)-[~/Clase/disk]
└─$ wget https://mercury.picoctf.net/static/4f3df7052b4121aff89af1a3f517afb1/dds1-alpine.flag.img.gz
--2025-05-07 22:46:40--  https://mercury.picoctf.net/static/4f3df7052b4121aff89af1a3f517afb1/dds1-alpine.flag.img.gz
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 29768910 (28M) [application/octet-stream]
Saving to: ‘dds1-alpine.flag.img.gz’

dds1-alpine.flag.img.gz              100%[===================================================================>]  28.39M  10.4MB/s    in 2.7s    

2025-05-07 22:46:43 (10.4 MB/s) - ‘dds1-alpine.flag.img.gz’ saved [29768910/29768910]


┌──(xrengariox㉿PC)-[~/Clase/disk]
└─$ 7z x dds1-alpine.flag.img.gz 

7-Zip 24.09 (x64) : Copyright (c) 1999-2024 Igor Pavlov : 2024-11-29
 64-bit locale=C.UTF-8 Threads:16 OPEN_MAX:1024, ASM

Scanning the drive for archives:
1 file, 29768910 bytes (29 MiB)

Extracting archive: dds1-alpine.flag.img.gz
--
Path = dds1-alpine.flag.img.gz
Type = gzip
Headers Size = 31

Everything is Ok           

Size:       134217728
Compressed: 29768910

┌──(xrengariox㉿PC)-[~/Clase/disk]
└─$ ls
dds1-alpine.flag.img  dds1-alpine.flag.img.gz
```

Vemos que parece ser un sector de un disco duro, entonces vamos a usar el comando que el mismo reto nos dice para ver si encontramos algo:
```sh
┌──(xrengariox㉿PC)-[~/Clase/disk]
└─$ srch_strings dds1-alpine.flag.img | grep picoCTF
  SAY picoCTF{f0r3ns1c4t0r_n30phyt3_a011c142}
```

Y efectivamente encotramos la flag:
```flag
picoCTF{f0r3ns1c4t0r_n30phyt3_a011c142}
```

## Notas adicionales

## Referencias
https://github.com/HHousen/PicoCTF-2021/blob/master/Forensics/Disk,%20disk,%20sleuth!/README.md
