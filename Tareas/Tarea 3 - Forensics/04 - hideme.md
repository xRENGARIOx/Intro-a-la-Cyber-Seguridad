# hideme

## Descripcion
Every file gets a flag.The SOC analyst saw one image been sent back and forth between two people. They decided to investigate and found out that there was more than what meets the eye [here](https://artifacts.picoctf.net/c/261/flag.png).
## Solucion
Primero descargamos el archivo que nos da el reto: 
```sh
┌──(xrengariox㉿PC)-[~/Clase/hideme]
└─$ wget https://artifacts.picoctf.net/c/261/flag.png                        
--2025-05-11 19:45:28--  https://artifacts.picoctf.net/c/261/flag.png
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 
3.161.55.100, 3.161.55.26, 3.161.55.61, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.100|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 42919 (42K) [application/octet-stream]
Saving to: ‘flag.png’

flag.png                             100%[===================================================================>]  41.91K  --.-KB/s    in 0.05s   

2025-05-11 19:45:29 (785 KB/s) - ‘flag.png’ saved [42919/42919]
```

Ahora comenzamos a analizar la imagen con las herramientas:
```sh
┌──(xrengariox㉿PC)-[~/Clase/hideme]
└─$ file flag.png                         
flag.png: PNG image data, 512 x 504, 8-bit/color RGBA, non-interlaced

┌──(xrengariox㉿PC)-[~/Clase/hideme]
└─$ exiftool flag.png                                
ExifTool Version Number         : 13.10
File Name                       : flag.png
Directory                       : .
File Size                       : 43 kB
File Modification Date/Time     : 2023:03:15 21:15:31-06:00
File Access Date/Time           : 2025:05:11 19:46:59-06:00
File Inode Change Date/Time     : 2025:05:11 19:45:29-06:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 512
Image Height                    : 504
Bit Depth                       : 8
Color Type                      : RGB with Alpha
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Warning                         : [minor] Trailer data after PNG IEND chunk
Image Size                      : 512x504
Megapixels                      : 0.258

┌──(xrengariox㉿PC)-[~/Clase/hideme]
└─$ binwalk flag.png  

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 512 x 504, 8-bit/color RGBA, non-interlaced
41            0x29            Zlib compressed data, compressed
39739         0x9B3B          Zip archive data, at least v1.0 to extract, name: secret/
39804         0x9B7C          Zip archive data, at least v2.0 to extract, compressed size: 2858, uncompressed size: 3015, name: secret/flag.png
42897         0xA791          End of Zip archive, footer length: 22

```

Vemos un archivo zip oculto, asi que vamos a descomprimirlo:
```sh
┌──(xrengariox㉿PC)-[~/Clase/hideme]
└─$ unzip flag.png               
Archive:  flag.png
warning [flag.png]:  39739 extra bytes at beginning or within zipfile
  (attempting to process anyway)
   creating: secret/
  inflating: secret/flag.png         

┌──(xrengariox㉿PC)-[~/Clase/hideme]
└─$ ls
flag.png  secret


┌──(xrengariox㉿PC)-[~/Clase/hideme]
└─$ cd secret   


┌──(xrengariox㉿PC)-[~/Clase/hideme/secret]
└─$ ls
flag.png


┌──(xrengariox㉿PC)-[~/Clase/hideme/secret]
└─$ cat flag.png 
───────┬─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: flag.png   <BINARY>
───────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

┌──(xrengariox㉿PC)-[~/Clase/hideme/secret]
└─$ file flag.png 
flag.png: PNG image data, 600 x 50, 16-bit grayscale, non-interlaced


┌──(xrengariox㉿PC)-[~/Clase/hideme/secret]
└─$ open flag.png 
```

Y dentro de la imagen de secret podemos ver la flag:
```flag
picoCTF{Hiddinng_An_imag3_within_@n_ima9e_96539bea}
```
## Notas adicionales

## Referencias
