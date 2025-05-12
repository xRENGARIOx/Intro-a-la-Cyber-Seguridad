# Secret of the Polyglot

## Descripcion
The Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file?Download the suspicious file [here](https://artifacts.picoctf.net/c_titan/97/flag2of2-final.pdf).
## Solucion
Primero descargamos el archivo que nos proporciona el reto:
```sh
┌──(xrengariox㉿PC)-[~/Clase/secret]
└─$ wget https://artifacts.picoctf.net/c_titan/97/flag2of2-final.pdf
--2025-05-11 19:59:29--  https://artifacts.picoctf.net/c_titan/97/flag2of2-final.pdf
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.26, 3.161.55.61, 3.161.55.100, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.26|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3362 (3.3K) [application/octet-stream]
Saving to: ‘flag2of2-final.pdf’

flag2of2-final.pdf                   100%[===================================================================>]   3.28K  --.-KB/s    in 0s      

2025-05-11 19:59:29 (50.5 MB/s) - ‘flag2of2-final.pdf’ saved [3362/3362]

```

Comenzamos el analisis con nuestras herramientas:
```
┌──(xrengariox㉿PC)-[~/Clase/secret]
└─$ file flag2of2-final.pdf 
flag2of2-final.pdf: PNG image data, 50 x 50, 8-bit/color RGBA, non-interlaced

┌──(xrengariox㉿PC)-[~/Clase/secret]
└─$ open flag2of2-final.pdf
```

Al abrir la imagen podemos ver lo que parece ser una parte de la flag:
```
1n_pn9_&_pdf_724b1287}
```

Continuamos el analisis:
```sh
┌──(xrengariox㉿PC)-[~/Clase/secret]
└─$ exiftool flag2of2-final.pdf 
ExifTool Version Number         : 13.10
File Name                       : flag2of2-final.pdf
Directory                       : .
File Size                       : 3.4 kB
File Modification Date/Time     : 2024:03:11 18:36:50-06:00
File Access Date/Time           : 2025:05:11 19:59:35-06:00
File Inode Change Date/Time     : 2025:05:11 19:59:29-06:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 50
Image Height                    : 50
Bit Depth                       : 8
Color Type                      : RGB with Alpha
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Profile Name                    : ICC profile
Profile CMM Type                : Little CMS
Profile Version                 : 4.3.0
Profile Class                   : Display Device Profile
Color Space Data                : RGB
Profile Connection Space        : XYZ
Profile Date Time               : 2023:11:02 17:42:31
Profile File Signature          : acsp
Primary Platform                : Apple Computer Inc.
CMM Flags                       : Not Embedded, Independent
Device Manufacturer             : 
Device Model                    : 
Device Attributes               : Reflective, Glossy, Positive, Color
Rendering Intent                : Perceptual
Connection Space Illuminant     : 0.9642 1 0.82491
Profile Creator                 : Little CMS
Profile ID                      : 0
Profile Description             : GIMP built-in sRGB
Profile Copyright               : Public Domain
Media White Point               : 0.9642 1 0.82491
Chromatic Adaptation            : 1.04788 0.02292 -0.05022 0.02959 0.99048 -0.01707 -0.00925 0.01508 0.75168
Red Matrix Column               : 0.43604 0.22249 0.01392
Blue Matrix Column              : 0.14305 0.06061 0.71393
Green Matrix Column             : 0.38512 0.7169 0.09706
Red Tone Reproduction Curve     : (Binary data 32 bytes, use -b option to extract)
Green Tone Reproduction Curve   : (Binary data 32 bytes, use -b option to extract)
Blue Tone Reproduction Curve    : (Binary data 32 bytes, use -b option to extract)
Chromaticity Channels           : 3
Chromaticity Colorant           : Unknown
Chromaticity Channel 1          : 0.64 0.33002
Chromaticity Channel 2          : 0.3 0.60001
Chromaticity Channel 3          : 0.15001 0.06
Device Mfg Desc                 : GIMP
Device Model Desc               : sRGB
Pixels Per Unit X               : 11811
Pixels Per Unit Y               : 11811
Pixel Units                     : meters
Modify Date                     : 2023:11:02 17:57:06
Comment                         : Created with GIMP
Warning                         : [minor] Trailer data after PNG IEND chunk
Image Size                      : 50x50
Megapixels                      : 0.003


┌──(xrengariox㉿PC)-[~/Clase/secret]
└─$ binwalk flag2of2-final.pdf 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 50 x 50, 8-bit/color RGBA, non-interlaced
914           0x392           PDF document, version: "1.4"
1149          0x47D           Zlib compressed data, default compression
****


```

Probamos a cambiarle la extension, y al hacer esto, vemos la otra mitad de la flag:
```sh
┌──(xrengariox㉿PC)-[~/Clase/secret]
└─$ cp flag2of2-final.pdf imagen.png                 

┌──(xrengariox㉿PC)-[~/Clase/secret]
└─$ open imagen.png 
```

```flag
picoCTF{f1u3n7_
```

Por lo que la flag queda asi:
```flag
picoCTF{f1u3n7_1n_pn9_&_pdf_724b1287}
```
## Notas adicionales

## Referencias
