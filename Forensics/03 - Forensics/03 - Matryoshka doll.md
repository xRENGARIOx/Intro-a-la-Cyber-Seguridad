#  Matryoshka doll

## Descripcion
Matryoshka dolls are a set of wooden dolls of decreasing size placed one inside another. What's the final one? Image: [this](https://mercury.picoctf.net/static/205adad23bf9d8303081a0e71c9beab8/dolls.jpg)
## Solucion
Descargamos el archivo que nos proporciona el reto:
```sh
┌──(xrengariox㉿PC)-[~/Clase/matr]
└─$ wget https://mercury.picoctf.net/static/205adad23bf9d8303081a0e71c9beab8/dolls.jpg              
--2025-05-05 12:38:19--  https://mercury.picoctf.net/static/205adad23bf9d8303081a0e71c9beab8/dolls.jpg
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 651632 (636K) [application/octet-stream]
Saving to: ‘dolls.jpg’

dolls.jpg                            100%[===================================================================>] 636.36K   625KB/s    in 1.0s    

2025-05-05 12:38:28 (625 KB/s) - ‘dolls.jpg’ saved [651632/651632]
```

Si la abrimos vemos que no muestra realmente mucho, pero vamos a ver si es que tiene archivos ocultos:
```sh
┌──(xrengariox㉿PC)-[~/Clase/matr]
└─$ binwalk dolls.jpg            

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 594 x 1104, 8-bit/color RGBA, non-interlaced
3226          0xC9A           TIFF image data, big-endian, offset of first image directory: 8
272492        0x4286C         Zip archive data, at least v2.0 to extract, compressed size: 378952, uncompressed size: 383937, name: base_images/2_c.jpg
651610        0x9F15A         End of Zip archive, footer length: 22
```

Vemos que tiene un .zip, entonces vamos a descomprimirlo:
```sh
┌──(xrengariox㉿PC)-[~/Clase/matr]
└─$ unzip dolls.jpg    
Archive:  dolls.jpg
warning [dolls.jpg]:  272492 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: base_images/2_c.jpg     

┌──(xrengariox㉿PC)-[~/Clase/matr]
└─$ ls
base_images  dolls.jpg

┌──(xrengariox㉿PC)-[~/Clase/matr]
└─$ cd base_images  

┌──(xrengariox㉿PC)-[~/Clase/matr/base_images]
└─$ ls
2_c.jpg

┌──(xrengariox㉿PC)-[~/Clase/matr/base_images]
└─$ unzip 2_c.jpg  
Archive:  2_c.jpg
warning [2_c.jpg]:  187707 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: base_images/3_c.jpg     

┌──(xrengariox㉿PC)-[~/Clase/matr/base_images]
└─$ cd base_images 

┌──(xrengariox㉿PC)-[~/Clase/matr/base_images/base_images]
└─$ unzip 3_c.jpg 
Archive:  3_c.jpg
warning [3_c.jpg]:  123606 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: base_images/4_c.jpg     

┌──(xrengariox㉿PC)-[~/Clase/matr/base_images/base_images]
└─$ cd base_images 

┌──(xrengariox㉿PC)-[~/…/matr/base_images/base_images/base_images]
└─$ unzip 4_c.jpg 
Archive:  4_c.jpg
warning [4_c.jpg]:  79578 extra bytes at beginning or within zipfile
  (attempting to process anyway)
  inflating: flag.txt                

┌──(xrengariox㉿PC)-[~/…/matr/base_images/base_images/base_images]
└─$ cato flag.txt  
picoCTF{96fac089316e094d41ea046900197662}
```

Repetimos el proceso varias veces y al final obtenemos la flag:
```flag
picoCTF{96fac089316e094d41ea046900197662}
```
## Notas adicionales

## Referencias
