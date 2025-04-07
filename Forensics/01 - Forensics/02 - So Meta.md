# So Meta

## Descripcion
Find the flag in this [picture](https://jupiter.challenges.picoctf.org/static/916b07b4c87062c165ace1d3d31ef655/pico_img.png).
## Solucion
Descargamos el archivo que nos da el reto y por el nombre del reto, suponemos que tiene algo que ver con los metadatos, por lo tanto vamos a ver si esta imagen contiene metadatos:
```sh
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ exiftool pico_img.png 
ExifTool Version Number         : 13.10
File Name                       : pico_img.png
Directory                       : .
File Size                       : 109 kB
File Modification Date/Time     : 2025:04:07 12:12:32-06:00
File Access Date/Time           : 2025:04:07 12:12:32-06:00
File Inode Change Date/Time     : 2025:04:07 12:12:32-06:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 600
Image Height                    : 600
Bit Depth                       : 8
Color Type                      : RGB
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Software                        : Adobe ImageReady
XMP Toolkit                     : Adobe XMP Core 5.3-c011 66.145661, 2012/02/06-14:56:27
Creator Tool                    : Adobe Photoshop CS6 (Windows)
Instance ID                     : xmp.iid:A5566E73B2B811E8BC7F9A4303DF1F9B
Document ID                     : xmp.did:A5566E74B2B811E8BC7F9A4303DF1F9B
Derived From Instance ID        : xmp.iid:A5566E71B2B811E8BC7F9A4303DF1F9B
Derived From Document ID        : xmp.did:A5566E72B2B811E8BC7F9A4303DF1F9B
Warning                         : [minor] Text/EXIF chunk(s) found after PNG IDAT (may be ignored by some readers)
Artist                          : picoCTF{s0_m3ta_d8944929}
Image Size                      : 600x600
Megapixels                      : 0.360
```

Y obtenemos la flag:
```flag
picoCTF{s0_m3ta_d8944929}
```

## Notas adicionales

## Referencias
