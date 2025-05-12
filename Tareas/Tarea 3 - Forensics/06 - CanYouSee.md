#  CanYouSee

## Descripcion
How about some hide and seek?Download this file [here](https://artifacts.picoctf.net/c_titan/128/unknown.zip).
## Solucion

Primero descargamos el archivo que nos da el reto y lo descomprimimos:

```sh
┌──(xrengariox㉿PC)-[~/Clase/canyou]
└─$ wget https://artifacts.picoctf.net/c_titan/128/unknown.zip
--2025-05-10 23:53:33--  https://artifacts.picoctf.net/c_titan/128/unknown.zip
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 2600:9000:25ed:8000:16:5ec5:2840:93a1, 2600:9000:25ed:d600:16:5ec5:2840:93a1, 2600:9000:25ed:5a00:16:5ec5:2840:93a1, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|2600:9000:25ed:8000:16:5ec5:2840:93a1|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2252108 (2.1M) [application/octet-stream]
Saving to: ‘unknown.zip’

unknown.zip                          100%[===================================================================>]   2.15M  7.20MB/s    in 0.3s    

2025-05-10 23:53:33 (7.20 MB/s) - ‘unknown.zip’ saved [2252108/2252108]


┌──(xrengariox㉿PC)-[~/Clase/canyou]
└─$ 7z x unknown.zip 

7-Zip 24.09 (x64) : Copyright (c) 1999-2024 Igor Pavlov : 2024-11-29
 64-bit locale=C.UTF-8 Threads:16 OPEN_MAX:1024, ASM

Scanning the drive for archives:
1 file, 2252108 bytes (2200 KiB)

Extracting archive: unknown.zip
--
Path = unknown.zip
Type = zip
Physical Size = 2252108

Everything is Ok

Size:       2263756
Compressed: 2252108
```

Vemos que es una imagen jpg, asi que comenzamos a analizarla:
```sh
┌──(xrengariox㉿PC)-[~/Clase/canyou]
└─$ ls
ukn_reality.jpg  unknown.zip

┌──(xrengariox㉿PC)-[~/Clase/canyou]
└─$ file ukn_reality.jpg 
ukn_reality.jpg: JPEG image data, JFIF standard 1.01, resolution (DPI), density 72x72, segment length 16, baseline, precision 8, 4308x2875, components 3

```

Todo se ve normal, veamos si al abrirla tambien se ve todo en orden, y busquemos por algun string en ella:
```sh
┌──(xrengariox㉿PC)-[~/Clase/canyou]
└─$ open ukn_reality.jpg                                                            
┌──(xrengariox㉿PC)-[~/Clase/canyou]
└─$ strings ukn_reality.jpg | grep pico           
```

Vamos a ver si en los metadatos encontramos algo:
```sh
┌──(xrengariox㉿PC)-[~/Clase/canyou]
└─$ exiftool ukn_reality.jpg 
ExifTool Version Number         : 13.10
File Name                       : ukn_reality.jpg
Directory                       : .
File Size                       : 2.3 MB
File Modification Date/Time     : 2024:03:11 18:05:51-06:00
File Access Date/Time           : 2025:05:10 23:50:35-06:00
File Inode Change Date/Time     : 2025:05:10 23:50:28-06:00
File Permissions                : -rw-r--r--
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : inches
X Resolution                    : 72
Y Resolution                    : 72
XMP Toolkit                     : Image::ExifTool 11.88
Attribution URL                 : cGljb0NURntNRTc0RDQ3QV9ISUREM05fM2I5MjA5YTJ9Cg==
Image Width                     : 4308
Image Height                    : 2875
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 4308x2875
Megapixels                      : 12.4

┌──(xrengariox㉿PC)-[~/Clase/canyou]
└─$ echo "cGljb0NURntNRTc0RDQ3QV9ISUREM05fM2I5MjA5YTJ9Cg==" | base64 -d 
picoCTF{ME74D47A_HIDD3N_3b9209a2}
```

Y asi encontramos la flag:
```flag
picoCTF{ME74D47A_HIDD3N_3b9209a2}
```
## Notas adicionales

## Referencias
