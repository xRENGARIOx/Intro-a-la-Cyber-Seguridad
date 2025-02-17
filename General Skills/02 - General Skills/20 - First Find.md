# First Find

## Descripcion
Unzip this archive and find the file named 'uber-secret.txt'

- [Download zip file](https://artifacts.picoctf.net/c/502/files.zip)

## Solucion
Descargamos el archivo y despues lo descomprimimos:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ 7z x files.zip 

7-Zip 24.09 (x64) : Copyright (c) 1999-2024 Igor Pavlov : 2024-11-29
 64-bit locale=C.UTF-8 Threads:16 OPEN_MAX:1024

Scanning the drive for archives:
1 file, 3995553 bytes (3902 KiB)

Extracting archive: files.zip
--
Path = files.zip
Type = zip
Physical Size = 3995553

Everything is Ok

Folders: 10
Files: 12
Size:       10362839
Compressed: 3995553
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ cd files 
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/files]
└─$ ls
13771.txt.utf-8  14789.txt.utf-8  acceptable_books  adequate_books  satisfactory_books

```

Ahora el reto nos pide que busquemos un archivo con un nombre especifico, asi que usamos el comando find:

```bash
┌──(xrengariox㉿PC)-[~/Downloads/files]
└─$ find -name 'uber-secret.txt'
./adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/uber-secret.txt
```

Ahora nos dirijimos a ese directorio y vemos el contenido de ese archivo:
```bash
┌──(xrengariox㉿PC)-[~/Downloads/files]
└─$ cd adequate_books/more_books/.secret/deeper_secrets/deepest_secrets/ 
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/…/more_books/.secret/deeper_secrets/deepest_secrets]
└─$ ls
uber-secret.txt
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/…/more_books/.secret/deeper_secrets/deepest_secrets]
└─$ cat uber-secret.txt                                                 
picoCTF{f1nd_15_f457_ab443fd1}
```
Y asi encontramos la flag:
```flag
picoCTF{f1nd_15_f457_ab443fd1}
```

## Notas adicionales

## Referencias
