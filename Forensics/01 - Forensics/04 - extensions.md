# extensions

## Descripcion
This is a really weird text file [TXT](https://jupiter.challenges.picoctf.org/static/e7e5d188621ee705ceeb0452525412ef/flag.txt)? Can you find the flag?
## Solucion
Descargamos el archivo y para verificar de que tipo es usamos un file:
```sh
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ file flag\ \(1\).txt 
flag (1).txt: PNG image data, 1697 x 608, 8-bit/color RGB, non-interlaced
```

Vemos que realmente no es un archivo de texto, si no una imagen, entonces vamos a aplicar un strings para ver si tiene cadenas:
```sh
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ strings flag\ \(1\).txt 
IHDR
sRGB
.
.
.
```

No vemos nada relevante, entonces vamos a ver si tiene algunos metadatos interesante:
```sh
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ exiftool flag\ \(1\).txt 
ExifTool Version Number         : 13.10
File Name                       : flag (1).txt
Directory                       : .
File Size                       : 10.0 kB
File Modification Date/Time     : 2025:04:07 12:19:29-06:00
File Access Date/Time           : 2025:04:07 12:19:40-06:00
File Inode Change Date/Time     : 2025:04:07 12:19:29-06:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 1697
Image Height                    : 608
Bit Depth                       : 8
Color Type                      : RGB
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
SRGB Rendering                  : Perceptual
Gamma                           : 2.2
Pixels Per Unit X               : 5669
Pixels Per Unit Y               : 5669
Pixel Units                     : meters
Image Size                      : 1697x608
Megapixels                      : 1.0

```

Pero tampoco encontramos nada interesante, entonces vamos a renombrar la imagen para poderla abrir y ver que tiene dentro:
```sh
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ mv flag\ \(1\).txt banderita.png  
```

Y al abrirla vemos la flag:
```flag
picoCTF{now_you_know_about_extensions}
```


## Notas adicionales

## Referencias
