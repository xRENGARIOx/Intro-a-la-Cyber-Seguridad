# Scan Surprise

## Descripcion
I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead?You can download the challenge files here:

- [challenge.zip](https://artifacts.picoctf.net/c_atlas/2/challenge.zip)

The same files are accessible via SSH here:`ssh -p 56457 ctf-player@atlas.picoctf.net`Using the password `1ad5be0d`. Accept the fingerprint with `yes`, and `ls` once connected to begin. Remember, in a shell, passwords are hidden!

## Solucion
Primero descargamos el archivo que nos da el reto y lo descomprimimos:
```sh
┌──(xrengariox㉿PC)-[~/Clase/hideme/scan]
└─$ wget https://artifacts.picoctf.net/c_atlas/2/challenge.zip
--2025-05-11 19:52:51--  https://artifacts.picoctf.net/c_atlas/2/challenge.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.26, 3.161.55.61, 3.161.55.64, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.26|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 736 [application/octet-stream]
Saving to: ‘challenge.zip’

challenge.zip                        100%[===================================================================>]     736  --.-KB/s    in 0s      

2025-05-11 19:52:52 (10.1 MB/s) - ‘challenge.zip’ saved [736/736]

┌──(xrengariox㉿PC)-[~/Clase/hideme/scan]
└─$ unzip challenge.zip 
Archive:  challenge.zip
   creating: home/ctf-player/drop-in/
 extracting: home/ctf-player/drop-in/flag.png  
```

Comenzamos el analisis con diferentes herramientas:
```
┌──(xrengariox㉿PC)-[~/Clase/hideme/scan]
└─$ ls
challenge.zip  home

┌──(xrengariox㉿PC)-[~/Clase/hideme/scan]
└─$ cd home  

┌──(xrengariox㉿PC)-[~/Clase/hideme/scan/home]
└─$ ls
ctf-player

┌──(xrengariox㉿PC)-[~/Clase/hideme/scan/home]
└─$ cd ctf-player 

┌──(xrengariox㉿PC)-[~/…/hideme/scan/home/ctf-player]
└─$ ls
drop-in

┌──(xrengariox㉿PC)-[~/…/hideme/scan/home/ctf-player]
└─$ cd drop-in   

┌──(xrengariox㉿PC)-[~/…/scan/home/ctf-player/drop-in]
└─$ ls
flag.png

┌──(xrengariox㉿PC)-[~/…/scan/home/ctf-player/drop-in]
└─$ file flag.png 
flag.png: PNG image data, 99 x 99, 1-bit colormap, non-interlaced

┌──(xrengariox㉿PC)-[~/…/scan/home/ctf-player/drop-in]
└─$ exiftool flag.png
ExifTool Version Number         : 13.10
File Name                       : flag.png
Directory                       : .
File Size                       : 346 bytes
File Modification Date/Time     : 2024:03:11 17:50:25-06:00
File Access Date/Time           : 2025:05:11 19:53:11-06:00
File Inode Change Date/Time     : 2025:05:11 19:52:55-06:00
File Permissions                : -rw-r--r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 99
Image Height                    : 99
Bit Depth                       : 1
Color Type                      : Palette
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Palette                         : (Binary data 6 bytes, use -b option to extract)
Transparency                    : 255 255
Pixels Per Unit X               : 2834
Pixels Per Unit Y               : 2834
Pixel Units                     : meters
Image Size                      : 99x99
Megapixels                      : 0.010

┌──(xrengariox㉿PC)-[~/…/scan/home/ctf-player/drop-in]
└─$ binwalk flag.png

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 99 x 99, 1-bit colormap, non-interlaced


┌──(xrengariox㉿PC)-[~/…/scan/home/ctf-player/drop-in]
└─$ zsteg flag.png     
scanline extradata  .. ["\xFF" repeated 61 times]

┌──(xrengariox㉿PC)-[~/…/scan/home/ctf-player/drop-in]
└─$ open flag.png 
```

Al abrir la imagen vemos que es un codigo QR, entonces vamos a escanearlo, y al hacerlo obtenemos la flag:
```flag
picoCTF{p33k_@_b00_b5ce2572}
```

## Notas adicionales

## Referencias
