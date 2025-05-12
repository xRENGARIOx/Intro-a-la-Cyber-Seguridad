# flags are stepic

## Descripcion
A group of underground hackers might be using this legit site to communicate. Use your forensic techniques to uncover their messageTry it [here](http://standard-pizzas.picoctf.net:50716/)!
## Solucion
Primero nos conectamos al reto con el link que nos proporcionan
De todas las banderas que estan ahi, la unica que no corresponde a un pais es la de UPANZI, entonces vamos a descargar esta imagen para analizarla:
```sh
┌──(xrengariox㉿PC)-[~/Clase/flags]
└─$ wget http://standard-pizzas.picoctf.net:50716/flags/upz.png                     
--2025-05-11 20:26:39--  http://standard-pizzas.picoctf.net:50716/flags/upz.png
Resolving standard-pizzas.picoctf.net (standard-pizzas.picoctf.net)... 3.22.195.189
Connecting to standard-pizzas.picoctf.net (standard-pizzas.picoctf.net)|3.22.195.189|:50716... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1788398 (1.7M) [image/png]
Saving to: ‘upz.png’

upz.png                              100%[===================================================================>]   1.71M  3.28MB/s    in 0.5s    

2025-05-11 20:26:39 (3.28 MB/s) - ‘upz.png’ saved [1788398/1788398]
```

Ahora vamos a analizarla con nuestras herramientas:
```sh
┌──(xrengariox㉿PC)-[~/Clase/flags]
└─$ file upz.png 
upz.png: PNG image data, 14173 x 10630, 8-bit/color RGBA, non-interlaced

┌──(xrengariox㉿PC)-[~/Clase/flags]
└─$ exiftool upz.png               
ExifTool Version Number         : 13.10
File Name                       : upz.png
Directory                       : .
File Size                       : 1788 kB
File Modification Date/Time     : 2025:03:05 21:59:01-06:00
File Access Date/Time           : 2025:05:11 20:26:57-06:00
File Inode Change Date/Time     : 2025:05:11 20:26:39-06:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 14173
Image Height                    : 10630
Bit Depth                       : 8
Color Type                      : RGB with Alpha
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Image Size                      : 14173x10630
Megapixels                      : 150.7

┌──(xrengariox㉿PC)-[~/Clase/flags]
└─$ binwalk upz.png      

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
41            0x29            Zlib compressed data, default compression
1024331       0xFA14B         ESP Image (ESP32): segment count: 11, flash mode: SLOW_READ, flash speed: 40MHz, flash size: 1MB, entry address: 0x0, hash: none
1042515       0xFE853         ESP Image (ESP32): segment count: 9, flash mode: QUIO, flash speed: 40MHz, flash size: 1MB, entry address: 0x0, hash: none


┌──(xrengariox㉿PC)-[~/Clase/flags]
└─$ zsteg upz.png              

b1,bgr,lsb,xy       .. /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg/checker/wbstego.rb:41:in `to_s': stack level too deep (SystemStackError)
        from /var/lib/gems/3.3.0/gems/iostruct-0.4.0/lib/iostruct.rb:175:in `inspect'
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg/checker/wbstego.rb:41:in `to_s'
        from /var/lib/gems/3.3.0/gems/iostruct-0.4.0/lib/iostruct.rb:175:in `inspect'
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg/checker/wbstego.rb:41:in `to_s'
        from /var/lib/gems/3.3.0/gems/iostruct-0.4.0/lib/iostruct.rb:175:in `inspect'
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg/checker/wbstego.rb:41:in `to_s'
        from /var/lib/gems/3.3.0/gems/iostruct-0.4.0/lib/iostruct.rb:175:in `inspect'
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg/checker/wbstego.rb:41:in `to_s'
         ... 5208346 levels...
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg.rb:26:in `run'
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/bin/zsteg:8:in `<top (required)>'
        from /usr/local/bin/zsteg:25:in `load'
        from /usr/local/bin/zsteg:25:in `<main>'


┌──(xrengariox㉿PC)-[~/Clase/flags]
└─$ 

┌──(xrengariox㉿PC)-[~/Clase/flags]
└─$ strings upz.png | grep "pico"

```

Por el nombre del reto y tras un poco de investigacion, vemos que stepic es una herramienta de estenografia, entonces vamos a usarla para ver el contenido oculto:
```
┌──(xrengariox㉿PC)-[~/Clase/flags]
└─$ sudo apt install stepic   

┌──(xrengariox㉿PC)-[~/Clase/flags]
└─$ stepic -d -i upz.png -o flag.txt
/usr/lib/python3/dist-packages/PIL/Image.py:3402: DecompressionBombWarning: Image size (150658990 pixels) exceeds limit of 89478485 pixels, could be decompression bomb DOS attack.
  warnings.warn(

┌──(xrengariox㉿PC)-[~/Clase/flags]
└─$ ls
flag.txt  upz.png

┌──(xrengariox㉿PC)-[~/Clase/flags]
└─$ cato flag.txt       
picoCTF{fl4g_h45_fl4g1a2a9157} 
```

Vemos que tira un warning pero aun asi nos da la flag: 
```flag
picoCTF{fl4g_h45_fl4g1a2a9157}
```
## Notas adicionales

## Referencias
