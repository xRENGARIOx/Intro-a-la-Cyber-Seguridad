# Time machine

## Descripcion
What was I last working on? I remember writing a note to help me remember...You can download the challenge files here:

- [challenge.zip](https://artifacts.picoctf.net/c_titan/160/challenge.zip)

## Solucion
Descargamos el archivo y lo descomprimimos:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ 7z x challenge.zip

7-Zip 24.09 (x64) : Copyright (c) 1999-2024 Igor Pavlov : 2024-11-29
 64-bit locale=C.UTF-8 Threads:16 OPEN_MAX:1024, ASM

Scanning the drive for archives:
1 file, 17740 bytes (18 KiB)

Extracting archive: challenge.zip
--
Path = challenge.zip
Type = zip
Physical Size = 17740

Everything is Ok

Folders: 17
Files: 25
Size:       20373
Compressed: 17740

```

Nos metemos al directorio y comenzamos a buscar que tiene:
```bash
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ git status
On branch master
nothing to commit, working tree clean
```

Vemos que es un repositorio de git, y vemos el contenido del directorio, en el cual encontramos un mensaje, que al leerlo nos dice que debemos de hacer: 
```bash
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ ls
message.txt
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ cat message.txt 
───────┬─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: message.txt
───────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ This is what I was working on, but I'd need to look at my commit history to know why...
───────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```

Entonces vemos el registro de versiones y nos da la flag:
```
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ git log   
commit 89d296ef533525a1378529be66b22d6a2c01e530 (HEAD -> master)
Author: picoCTF <ops@picoctf.com>
Date:   Tue Mar 12 00:07:22 2024 +0000

    picoCTF{t1m3m@ch1n3_186cd7d7}
```

```flag
picoCTF{t1m3m@ch1n3_186cd7d7}
```


## Notas adicionales

## Referencias
