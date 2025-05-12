# RED

## Descripcion
RED, RED, RED, REDDownload the image: [red.png](https://challenge-files.picoctf.net/c_verbal_sleep/831307718b34193b288dde31e557484876fb84978b5818e2627e453a54aa9ba6/red.png)
## Solucion
Primero descargamos el archivo que nos proporciona el reto:
```sh
┌──(xrengariox㉿PC)-[~/Clase/red]
└─$ wget https://challenge-files.picoctf.net/c_verbal_sleep/831307718b34193b288dde31e557484876fb84978b5818e2627e453a54aa9ba6/red.png
--2025-05-11 20:06:16--  https://challenge-files.picoctf.net/c_verbal_sleep/831307718b34193b288dde31e557484876fb84978b5818e2627e453a54aa9ba6/red.png
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 65.9.149.85, 65.9.149.24, 65.9.149.95, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|65.9.149.85|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 796 [application/octet-stream]
Saving to: ‘red.png’

red.png                              100%[===================================================================>]     796  --.-KB/s    in 0s      

2025-05-11 20:06:17 (27.3 MB/s) - ‘red.png’ saved [796/796]

```

Ahora comenzamos a analizarlo con nuestras herramientas:
```sh
┌──(xrengariox㉿PC)-[~/Clase/red]
└─$ file red.png               
red.png: PNG image data, 128 x 128, 8-bit/color RGBA, non-interlaced

┌──(xrengariox㉿PC)-[~/Clase/red]
└─$ exiftool red.png           
ExifTool Version Number         : 13.10
File Name                       : red.png
Directory                       : .
File Size                       : 796 bytes
File Modification Date/Time     : 2025:03:05 21:34:15-06:00
File Access Date/Time           : 2025:05:11 20:07:08-06:00
File Inode Change Date/Time     : 2025:05:11 20:06:17-06:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 128
Image Height                    : 128
Bit Depth                       : 8
Color Type                      : RGB with Alpha
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Poem                            : Crimson heart, vibrant and bold,.Hearts flutter at your sight..Evenings glow softly red,.Cherries burst with sweet life..Kisses linger with your warmth..Love deep as merlot..Scarlet leaves falling softly,.Bold in every stroke.
Image Size                      : 128x128
Megapixels                      : 0.016

┌──(xrengariox㉿PC)-[~/Clase/red]
└─$ binwalk red.png           

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 128 x 128, 8-bit/color RGBA, non-interlaced
284           0x11C           Zlib compressed data, default compression


┌──(xrengariox㉿PC)-[~/Clase/red]
└─$ zsteg red.png 
meta Poem           .. text: "Crimson heart, vibrant and bold,\nHearts flutter at your sight.\nEvenings glow softly red,\nCherries burst with sweet life.\nKisses linger with your warmth.\nLove deep as merlot.\nScarlet leaves falling softly,\nBold in every stroke."                          
b1,rgba,lsb,xy      .. text: "cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ=="   
b1,rgba,msb,xy      .. file: OpenPGP Public Key
b2,g,lsb,xy         .. text: "ET@UETPETUUT@TUUTD@PDUDDDPE"
b2,rgb,lsb,xy       .. file: OpenPGP Secret Key
b2,bgr,msb,xy       .. file: OpenPGP Public Key
b2,rgba,lsb,xy      .. file: OpenPGP Secret Key
b2,rgba,msb,xy      .. text: "CIkiiiII"
b2,abgr,lsb,xy      .. file: OpenPGP Secret Key
b2,abgr,msb,xy      .. text: "iiiaakikk"
b3,rgba,msb,xy      .. text: "#wb#wp#7p"
b3,abgr,msb,xy      .. text: "7r'wb#7p"
b4,b,lsb,xy         .. file: 0421 Alliant compact executable not stripped

┌──(xrengariox㉿PC)-[~/Clase/red]
└─$ echo "cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==" | base64 -d
picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}    
```

Y asi encontramos la flag:
```sh
picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_} 
```
## Notas adicionales

## Referencias
