# Operation Oni

## Descripcion
Download this disk image, find the key and log into the remote machine.Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

- [Download disk image](https://artifacts.picoctf.net/c/69/disk.img.gz)
- Remote machine: `ssh -i key_file -p 59804 ctf-player@saturn.picoctf.net`
## Solucion
Descargamos el archivo que nos da el reto y lo descomprimimos:
```sh
┌──(xrengariox㉿PC)-[~/Clase/oni]
└─$ wget https://artifacts.picoctf.net/c/69/disk.img.gz      
--2025-05-07 23:33:00--  https://artifacts.picoctf.net/c/69/disk.img.gz
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.26, 3.161.55.61, 3.161.55.100, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.26|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 48132743 (46M) [application/octet-stream]
Saving to: ‘disk.img.gz’

disk.img.gz                          100%[===================================================================>]  45.90M  11.7MB/s    in 3.9s    

2025-05-07 23:33:05 (11.8 MB/s) - ‘disk.img.gz’ saved [48132743/48132743]



┌──(xrengariox㉿PC)-[~/Clase/oni]
└─$ 7z x disk.img.gz                                   

7-Zip 24.09 (x64) : Copyright (c) 1999-2024 Igor Pavlov : 2024-11-29
 64-bit locale=C.UTF-8 Threads:16 OPEN_MAX:1024, ASM

Scanning the drive for archives:
1 file, 48132743 bytes (46 MiB)

Extracting archive: disk.img.gz
--
Path = disk.img.gz
Type = gzip
Headers Size = 19

Everything is Ok

Size:       241172480
Compressed: 48132743


┌──(xrengariox㉿PC)-[~/Clase/oni]
└─$ ls
disk.img  disk.img.gz

```

Comenzamos a ver las particiones y ver los directorios:
```sh
┌──(xrengariox㉿PC)-[~/Clase/oni]
└─$ mmls disk.img
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000471039   0000264192   Linux (0x83)

┌──(xrengariox㉿PC)-[~/Clase/oni]
└─$ fls -o 206848 disk.img 
d/d 458:        home
d/d 11: lost+found
d/d 12: boot
d/d 13: etc
d/d 79: proc
d/d 80: dev
d/d 81: tmp
d/d 82: lib
d/d 85: var
d/d 94: usr
d/d 104:        bin
d/d 118:        sbin
d/d 464:        media
d/d 468:        mnt
d/d 469:        opt
d/d 470:        root
d/d 471:        run
d/d 473:        srv
d/d 474:        sys
V/V 33049:      $OrphanFiles


┌──(xrengariox㉿PC)-[~/Clase/oni]
└─$ fls -o 206848 disk.img 470
r/r 2344:       .ash_history
d/d 3916:       .ssh


┌──(xrengariox㉿PC)-[~/Clase/oni]
└─$ icat -o 206848 disk.img 2344      
ssh-keygen -t ed25519
ls .ssh/
halt


┌──(xrengariox㉿PC)-[~/Clase/oni]
└─$ icat -o 206848 disk.img 3916 
L
 .�
   ..)
id_ed25519*     �id_ed25519.pub
                               ޻��/                               

┌──(xrengariox㉿PC)-[~/Clase/oni]
└─$ fls -o 206848 disk.img 3916
r/r 2345:       id_ed25519
r/r 2346:       id_ed25519.pub

┌──(xrengariox㉿PC)-[~/Clase/oni]
└─$ icat -o 206848 disk.img 2345 > id_ed25519


┌──(xrengariox㉿PC)-[~/Clase/oni]
└─$ icat -o 206848 disk.img 2346 > id_ed25519.pub

┌──(xrengariox㉿PC)-[~/Clase/oni]
└─$ ls -la
total 282544
drwxrwxr-x  2 xrengariox xrengariox      4096 May  7 23:39 .
drwxrwxr-x 18 xrengariox xrengariox      4096 May  7 23:32 ..
-rw-rw-r--  1 xrengariox xrengariox 241172480 Oct  6  2021 disk.img
-rw-rw-r--  1 xrengariox xrengariox  48132743 Aug  4  2023 disk.img.gz
-rw-rw-r--  1 xrengariox xrengariox       411 May  7 23:39 id_ed25519
-rw-rw-r--  1 xrengariox xrengariox        96 May  7 23:39 id_ed25519.pub

┌──(xrengariox㉿PC)-[~/Clase/oni]
└─$ chmod 600 id_ed25519

```



Nos conectamos con SSH al servidor con el comando que nos prooprcionan:
```sh
┌──(xrengariox㉿PC)-[~/Clase/oni]
└─$ ssh -i id_ed25519 -p 59804 ctf-player@saturn.picoctf.net 
The authenticity of host '[saturn.picoctf.net]:59804 ([13.59.203.175]:59804)' can't be established.
ED25519 key fingerprint is SHA256:XBSvB1lk28EctsAVdKJtsl0A7C5bonqPrvHCYH8aEy4.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[saturn.picoctf.net]:59804' (ED25519) to the list of known hosts.
Welcome to Ubuntu 20.04.5 LTS (GNU/Linux 6.5.0-1023-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

ctf-player@challenge:~$ whoami
ctf-player
ctf-player@challenge:~$ sudo -l
-bash: sudo: command not found
ctf-player@challenge:~$ ls
flag.txt
ctf-player@challenge:~$ cat flag.txt 
picoCTF{k3y_5l3u7h_339601ed}ctf-player@challenge:~$
```

Y asi obtenemos la flag:
```flag
picoCTF{k3y_5l3u7h_339601ed}
```

## Notas adicionales
Nota: Se le quitan ciertos permisos al archivo de la llave para que no haya problema con SSH.
## Referencias
https://medium.com/@brownguy231256/picoctf-challenge-writeup-operation-oni-41fded2b3ba9
