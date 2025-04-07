# What Lies Within

## Descripcion
There's something in the [building](https://jupiter.challenges.picoctf.org/static/011955b303f293d60c8116e6a4c5c84f/buildings.png). Can you retrieve the flag?
## Solucion
Descargamos el achivo que nos proporciona el reto y vemos que tipo de archivo es:
```sh
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ file buildings.png  
buildings.png: PNG image data, 657 x 438, 8-bit/color RGBA, non-interlaced
```

Parece ser una imagen, entonces vamos a ver si tiene la flag dentro:
```sh
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ strings buildings.png | grep pico

```

No se ve nada, entonces vamos a ver si en sus metadatos tiene algo:
```sh
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ exiftool buildings.png  
ExifTool Version Number         : 13.10
File Name                       : buildings.png
Directory                       : .
File Size                       : 625 kB
File Modification Date/Time     : 2025:04:07 12:24:43-06:00
File Access Date/Time           : 2025:04:07 12:24:43-06:00
File Inode Change Date/Time     : 2025:04:07 12:24:43-06:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 657
Image Height                    : 438
Bit Depth                       : 8
Color Type                      : RGB with Alpha
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Image Size                      : 657x438
Megapixels                      : 0.288
```

Vamos a abrir la imagen para ver que contiene:
Solo vemos una imagen con un paisaje de varios edicios.
Entonces vamos a probar a hacer stenografía para ver si encontramos algo con ayuda de zsteg:
```sh
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ zsteg buildings.png           
b1,r,lsb,xy         .. text: "^5>R5YZrG"
b1,rgb,lsb,xy       .. text: "picoCTF{h1d1ng_1n_th3_b1t5}"
b1,abgr,msb,xy      .. file: PGP Secret Sub-key -
b2,b,lsb,xy         .. text: "XuH}p#8Iy="
b3,abgr,msb,xy      .. text: "t@Wp-_tH_v\r"
b4,r,lsb,xy         .. text: "fdD\"\"\"\" "
b4,r,msb,xy         .. text: "%Q#gpSv0c05"
b4,g,lsb,xy         .. text: "fDfffDD\"\""
b4,g,msb,xy         .. text: "f\"fff\"\"DD"
b4,b,lsb,xy         .. text: "\"$BDDDDf"
b4,b,msb,xy         .. text: "wwBDDDfUU53w"
b4,rgb,msb,xy       .. text: "dUcv%F#A`"
b4,bgr,msb,xy       .. text: " V\"c7Ga4"
b4,abgr,msb,xy      .. text: "gOC_$_@o"

```

Y asi encontramos la flag:
```flag
picoCTF{h1d1ng_1n_th3_b1t5}
```

## Notas adicionales

## Referencias
