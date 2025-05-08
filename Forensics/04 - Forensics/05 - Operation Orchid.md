# Operation Orchid

## Descripcion
Download this disk image and find the flag.Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

- [Download compressed disk image](https://artifacts.picoctf.net/c/213/disk.flag.img.gz)
## Solucion
Primero descargamos el archivo que nos proporciona el reto y lo descomprimimos:
```sh
┌──(xrengariox㉿PC)-[~/Clase/operation]
└─$ wget https://artifacts.picoctf.net/c/213/disk.flag.img.gz
--2025-05-07 23:20:36--  https://artifacts.picoctf.net/c/213/disk.flag.img.gz
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.26, 3.161.55.61, 3.161.55.64, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.26|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 44360922 (42M) [application/octet-stream]
Saving to: ‘disk.flag.img.gz’

disk.flag.img.gz                     100%[===================================================================>]  42.31M  11.9MB/s    in 3.6s    

2025-05-07 23:20:40 (11.8 MB/s) - ‘disk.flag.img.gz’ saved [44360922/44360922]


┌──(xrengariox㉿PC)-[~/Clase/operation]
└─$ 7z x disk.flag.img.gz 

7-Zip 24.09 (x64) : Copyright (c) 1999-2024 Igor Pavlov : 2024-11-29
 64-bit locale=C.UTF-8 Threads:16 OPEN_MAX:1024, ASM

Scanning the drive for archives:
1 file, 44360922 bytes (43 MiB)

Extracting archive: disk.flag.img.gz
--
Path = disk.flag.img.gz
Type = gzip
Headers Size = 24

Everything is Ok    

Size:       419430400
Compressed: 44360922


┌──(xrengariox㉿PC)-[~/Clase/operation]
└─$ ls
disk.flag.img  disk.flag.img.gz
```

Ahora vemos las particiones que tiene:
```sh
┌──(xrengariox㉿PC)-[~/Clase/operation]
└─$ mmls disk.flag.img
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000411647   0000204800   Linux Swap / Solaris x86 (0x82)
004:  000:002   0000411648   0000819199   0000407552   Linux (0x83)

```

Y comenzamos a bucar y ver directorios:
```sh
┌──(xrengariox㉿PC)-[~/Clase/operation]
└─$ fls -o 411648 disk.flag.img
d/d 460:        home
d/d 11: lost+found
d/d 12: boot
d/d 13: etc
d/d 81: proc
d/d 82: dev
d/d 83: tmp
d/d 84: lib
d/d 87: var
d/d 96: usr
d/d 106:        bin
d/d 120:        sbin
d/d 466:        media
d/d 470:        mnt
d/d 471:        opt
d/d 472:        root
d/d 473:        run
d/d 475:        srv
d/d 476:        sys
d/d 2041:       swap
V/V 51001:      $OrphanFiles
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Clase/operation]
└─$ fls -o 411648 disk.flag.img 472
r/r 1875:       .ash_history
r/r * 1876(realloc):    flag.txt
r/r 1782:       flag.txt.enc
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Clase/operation]
└─$ icat -o 411648 disk.flag.img 1782
Salted__�ށ��e��B�J▒�c�$QE&$��4jM�KGeE�1�^Ȥ7� ���؎$�'%                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Clase/operation]
└─$ icat -o 411648 disk.flag.img 1875
touch flag.txt
nano flag.txt 
apk get nano
apk --help
apk add nano
nano flag.txt 
openssl
openssl aes256 -salt -in flag.txt -out flag.txt.enc -k unbreakablepassword1234567
shred -u flag.txt
ls -al
halt
```

Vemos que la flag parece estar encryptada, pero tenemos la key, entonces tal vez podamos desencriptar el contenido:
```sh
┌──(xrengariox㉿PC)-[~/Clase/operation]
└─$ icat -o 411648 disk.flag.img 1782 > flag.enc


┌──(xrengariox㉿PC)-[~/Clase/operation]
└─$ openssl aes256 -d -salt -in flag.enc -out flag.txt -k unbreakablepassword1234567
*** WARNING : deprecated key derivation used.
Using -iter or -pbkdf2 would be better.
bad decrypt
40171FA73A7F0000:error:1C800064:Provider routines:ossl_cipher_unpadblock:bad decrypt:../providers/implementations/ciphers/ciphercommon_block.c:107:


┌──(xrengariox㉿PC)-[~/Clase/operation]
└─$ cat flag.txt
───────┬─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: flag.txt
───────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ picoCTF{h4un71ng_p457_5113beab}^A
───────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```

Y asi obtenemos la flag:
```flag
picoCTF{h4un71ng_p457_5113beab}
```
## Notas adicionales

## Referencias
https://medium.com/@atigamli/picoctf-1-writeup-operation-orchid-af876fd2b392