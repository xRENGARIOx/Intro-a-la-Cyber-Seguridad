# Big zip

## Descripcion
Unzip this archive and find the flag.
- [Download zip file](https://artifacts.picoctf.net/c/504/big-zip-files.zip)

## Solucion
Primero descargamos y descomprimimos el archivo:
```bash
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ 7z x big-zip-files.zip   

7-Zip 24.09 (x64) : Copyright (c) 1999-2024 Igor Pavlov : 2024-11-29
 64-bit locale=C.UTF-8 Threads:16 OPEN_MAX:1024

Scanning the drive for archives:
1 file, 3182988 bytes (3109 KiB)

Extracting archive: big-zip-files.zip
--            
Path = big-zip-files.zip
Type = zip
Physical Size = 3182988

Everything is Ok

Folders: 358
Files: 8732
Size:       740217
Compressed: 3182988
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ ls
Addadshashanammu          code_1.94.1-1728111316_amd64.deb  discord-0.0.85.deb              ltdis.sh                              strings
Addadshashanammu.zip      code_1.97.0-1738713410_amd64.deb  enc_flag                        null.png                              warm
Martinez_42102866_P5.mp4  discord-0.0.71.deb                file                            opera-stable_114.0.5282.86_amd64.deb
VPN                       discord-0.0.77.deb                flag                            static
big-zip-files             discord-0.0.80.deb                flag.txt                        static.ltdis.strings.txt
big-zip-files.zip         discord-0.0.84.deb                ida-free-pc_90sp1_x64linux.run  static.ltdis.x86_64.txt
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ cd big-zip-files
```

Vemos que son demasiados archivos y subdirectorios
```
┌──(xrengariox㉿PC)-[~/Downloads/big-zip-files]
└─$ ls
acurqdgqyoi.txt               folder_guneyklias             jwdwrzfxwmdu.txt              rxohaqrmsfjwtc.txt
aecwqhyouxkugpjtn.txt         folder_gyemxikwvn             jwhddpxrgckcchaeqsbclf.txt    rxyhwlastxfmu.txt

```

Usamos grep para buscar entre los archivos y subdirectorios:
```bash
┌──(xrengariox㉿PC)-[~/Downloads/big-zip-files]
└─$ grep -r "pico"
folder_pmbymkjcya/folder_cawigcwvgv/folder_ltdayfmktr/folder_fnpfclfyee/whzxrpivpqld.txt:information on the record will last a billion years. Genes and brains and books encode picoCTF{gr3p_15_m4g1c_ef8790dc}
```
Y obtenemos la flag:
```flag
picoCTF{gr3p_15_m4g1c_ef8790dc}
```

## Notas adicionales

## Referencias
