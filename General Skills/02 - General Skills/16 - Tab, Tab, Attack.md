# Tab, Tab, Attack

## Descripcion
Using tabcomplete in the Terminal will add years to your life, esp. when dealing with long rambling directory structures and filenames: [Addadshashanammu.zip](https://mercury.picoctf.net/static/9689f2b453ad5daeb73ca7534e4d1521/Addadshashanammu.zip)
## Solucion
Primero descomprimimos el archivo que nos dan:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ 7z x Addadshashanammu.zip 

7-Zip 24.09 (x64) : Copyright (c) 1999-2024 Igor Pavlov : 2024-11-29
 64-bit locale=C.UTF-8 Threads:16 OPEN_MAX:1024

Scanning the drive for archives:
1 file, 4519 bytes (5 KiB)

Extracting archive: Addadshashanammu.zip
--
Path = Addadshashanammu.zip
Type = zip
Physical Size = 4519

Everything is Ok

Folders: 7
Files: 1
Size:       8320
Compressed: 4519

```
Luego accedemos a la carpeta:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ cd Addadshashanammu       
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/Addadshashanammu]
└─$ ls
Almurbalarammi
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/Addadshashanammu]
└─$ cd Almurbalarammi  
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/Addadshashanammu/Almurbalarammi]
└─$ ls
Ashalmimilkala
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/Addadshashanammu/Almurbalarammi]
└─$ cd Ashalmimilkala 
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/Addadshashanammu/Almurbalarammi/Ashalmimilkala]
└─$ cd Assurnabitashpi 
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/…/Addadshashanammu/Almurbalarammi/Ashalmimilkala/Assurnabitashpi]
└─$ cd Maelkashishi   
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/…/Almurbalarammi/Ashalmimilkala/Assurnabitashpi/Maelkashishi]
└─$ cd Onnissiralis 
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/…/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis]
└─$ ls
Ularradallaku
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/…/Ashalmimilkala/Assurnabitashpi/Maelkashishi/Onnissiralis]
└─$ cd Ularradallaku 
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/…/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku]
└─$ ls  
```
Y finalmente llegamos a un archivo ejecutable el cual le hacemos un strings y filtramos por pico para obtener la flag:

```bash
┌──(xrengariox㉿PC)-[~/…/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku]
└─$ file fang-of-haynekhtnamet 
fang-of-haynekhtnamet: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=72a56ba85df661b5a985999a435927c01095cccf, not stripped
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/…/Assurnabitashpi/Maelkashishi/Onnissiralis/Ularradallaku]
└─$ strings fang-of-haynekhtnamet | grep "pico"  
*ZAP!* picoCTF{l3v3l_up!_t4k3_4_r35t!_2bcfb2ab}

```


```flag
picoCTF{l3v3l_up!_t4k3_4_r35t!_2bcfb2ab}
```

## Notas adicionales

## Referencias
