# Sleuthkit Apprentice

## Descripcion
Download this disk image and find the flag.Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

- [Download compressed disk image](https://artifacts.picoctf.net/c/137/disk.flag.img.gz)
## Solucion
Descargamos el archivo que nos proporciona el reto y lo descomprimimos:
```sh
┌──(xrengariox㉿PC)-[~/Clase/aprendiz]
└─$ wget https://artifacts.picoctf.net/c/137/disk.flag.img.gz
--2025-05-07 23:06:47--  https://artifacts.picoctf.net/c/137/disk.flag.img.gz
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.26, 3.161.55.100, 3.161.55.61, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.26|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 47534568 (45M) [application/octet-stream]
Saving to: ‘disk.flag.img.gz’

disk.flag.img.gz                     100%[===================================================================>]  45.33M  12.1MB/s    in 3.9s    

2025-05-07 23:06:52 (11.7 MB/s) - ‘disk.flag.img.gz’ saved [47534568/47534568]


┌──(xrengariox㉿PC)-[~/Clase/aprendiz]
└─$ 7z x disk.flag.img.gz 

7-Zip 24.09 (x64) : Copyright (c) 1999-2024 Igor Pavlov : 2024-11-29
 64-bit locale=C.UTF-8 Threads:16 OPEN_MAX:1024, ASM

Scanning the drive for archives:
1 file, 47534568 bytes (46 MiB)

Extracting archive: disk.flag.img.gz
--
Path = disk.flag.img.gz
Type = gzip
Headers Size = 24

Everything is Ok    

Size:       314572800
Compressed: 47534568


┌──(xrengariox㉿PC)-[~/Clase/aprendiz]
└─$ ls
disk.flag.img  disk.flag.img.gz
```

Vamos a buscar la bandera, primero vemos que particiones tiene:
```sh
┌──(xrengariox㉿PC)-[~/Clase/aprendiz]
└─$ mmls disk.flag.img 
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000360447   0000153600   Linux Swap / Solaris x86 (0x82)
004:  000:002   0000360448   0000614399   0000253952   Linux (0x83)

```

Con esta informacion usamos fls para obtener informacion de los directorios usando `fls`, al cual le debemos de especificar el offset en la imagen de disco:
```
┌──(xrengariox㉿PC)-[~/Clase/aprendiz]
└─$ fls -o 360448 disk.flag.img
d/d 451:        home
d/d 11: lost+found
d/d 12: boot
d/d 1985:       etc
d/d 1986:       proc
d/d 1987:       dev
d/d 1988:       tmp
d/d 1989:       lib
d/d 1990:       var
d/d 3969:       usr
d/d 3970:       bin
d/d 1991:       sbin
d/d 1992:       media
d/d 1993:       mnt
d/d 1994:       opt
d/d 1995:       root
d/d 1996:       run
d/d 1997:       srv
d/d 1998:       sys
d/d 2358:       swap
V/V 31745:      $OrphanFiles


┌──(xrengariox㉿PC)-[~/Clase/aprendiz]
└─$ fls -o 360448 disk.flag.img 1995
r/r 2363:       .ash_history
d/d 3981:       my_folder

┌──(xrengariox㉿PC)-[~/Clase/aprendiz]
└─$ fls -o 360448 disk.flag.img 3981     
r/r * 2082(realloc):    flag.txt
r/r 2371:       flag.uni.txt
```

Leemos el contenido de la falg con icat:
```sh
┌──(xrengariox㉿PC)-[~/Clase/aprendiz]
└─$ icat -o 360448 disk.flag.img 2082
            3.449677            13.056403


┌──(xrengariox㉿PC)-[~/Clase/aprendiz]
└─$ icat -o 360448 disk.flag.img 2371
picoCTF{by73_5urf3r_adac6cb4}
```

En el primer archivo no obtenemos nada, pero en el segundo obtenemos la flag:
```flag
picoCTF{by73_5urf3r_adac6cb4}
```
## Notas adicionales

## Referencias
https://medium.com/@MonlesYen/pico-ctf-writeup-sleuthkit-intro-sleuthkit-apprentice-operation-orchid-70a5b6c5c90a
