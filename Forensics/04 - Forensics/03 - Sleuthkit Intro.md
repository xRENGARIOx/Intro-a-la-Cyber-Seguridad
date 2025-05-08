# Sleuthkit Intro

## Descripcion
Download the disk image and use `mmls` on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag.Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.[Download disk image](https://artifacts.picoctf.net/c/164/disk.img.gz)Access checker program: `nc saturn.picoctf.net 58008`
## Solucion
Primero descargamos la imagen del disco que nos proporciona el reto:
```sh
┌──(xrengariox㉿PC)-[~/Clase/intro]
└─$ wget https://artifacts.picoctf.net/c/164/disk.img.gz                                            
--2025-05-07 22:58:31--  https://artifacts.picoctf.net/c/164/disk.img.gz
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.100, 3.161.55.64, 3.161.55.26, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.100|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 29714372 (28M) [application/octet-stream]
Saving to: ‘disk.img.gz’

disk.img.gz                          100%[===================================================================>]  28.34M  11.8MB/s    in 2.4s    

2025-05-07 22:58:34 (11.8 MB/s) - ‘disk.img.gz’ saved [29714372/29714372]
```

Lo descomprimimos:
```sh
┌──(xrengariox㉿PC)-[~/Clase/intro]
└─$ 7z x disk.img.gz            

7-Zip 24.09 (x64) : Copyright (c) 1999-2024 Igor Pavlov : 2024-11-29
 64-bit locale=C.UTF-8 Threads:16 OPEN_MAX:1024, ASM

Scanning the drive for archives:
1 file, 29714372 bytes (29 MiB)

Extracting archive: disk.img.gz
--
Path = disk.img.gz
Type = gzip
Headers Size = 19

Everything is Ok

Size:       104857600
Compressed: 29714372

┌──(xrengariox㉿PC)-[~/Clase/intro]
└─$ ls
disk.img  disk.img.gz
```

Usamos la herramienta `mmls` para saber informacion acerca de la imagen de disco que descargamos:
```sh
┌──(xrengariox㉿PC)-[~/Clase/intro]
└─$ mmls disk.img
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000204799   0000202752   Linux (0x83)
```

Y vemos que nos da informacion de las particiones, entonces nos conectamos al servidor con el comando que nos da el reto y contestamos:
```sh
┌──(xrengariox㉿PC)-[~/Clase/intro]
└─$ nc saturn.picoctf.net 58008
What is the size of the Linux partition in the given disk image?
Length in sectors: 0000202752
0000202752
Great work!
picoCTF{mm15_f7w!}
```

Y asi obtenemos la flag:
```flag
picoCTF{mm15_f7w!}
```

## Notas adicionales

## Referencias
