# Blame Game

## Descripcion
Someone's commits seems to be preventing the program from working. Who is it?You can download the challenge files here:

- [challenge.zip](https://artifacts.picoctf.net/c_titan/157/challenge.zip)

## Solucion
Descargamos y descomprimimos el archivo:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ 7z x challenge.zip

7-Zip 24.09 (x64) : Copyright (c) 1999-2024 Igor Pavlov : 2024-11-29
 64-bit locale=C.UTF-8 Threads:16 OPEN_MAX:1024, ASM

Scanning the drive for archives:
1 file, 293587 bytes (287 KiB)

Extracting archive: challenge.zip
--
Path = challenge.zip
Type = zip
Physical Size = 293587

Everything is Ok

Folders: 231
Files: 528
Size:       259934
Compressed: 293587
```

Vemos el contenido del directorio pero solo vemos un scrpt de python y pues vemos que falta un parentesis para que funcione:

```bash
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ ls
message.py
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ cat message.py 
───────┬─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: message.py
───────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ print("Hello, World!"
───────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```

Entonces hay que buscar donde comenzo a fallar, pero vemos que son demasiados commits los que se han hecho:
```bash
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ git status
On branch master
nothing to commit, working tree clean
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ git log   
commit b7f1fb20f72e493f604ccb3b9f2639a00c566939 (HEAD -> master)
Author: picoCTF <ops@picoctf.com>
Date:   Tue Mar 12 00:07:08 2024 +0000

    important business work

commit c16a2576a68c7166d13f3e877ea4b4cfc675d343
Author: picoCTF <ops@picoctf.com>
Date:   Tue Mar 12 00:07:08 2024 +0000

    important business work
    ...
    ...
    ...
```

Entonces para buscar entre todos estos commits filtramos por los que se hicieron sobre el archivo de python:
```bash
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ git log -- message.py      

commit 2466febd40004b9ca644ce924181d07e23dcfaeb
Author: picoCTF{@sk_th3_1nt3rn_cfca95b2} <ops@picoctf.com>
Date:   Tue Mar 12 00:07:06 2024 +0000

    optimize file size of prod code

commit 05f26d123cde97b714aaae28ba8f18db3f385af5
Author: picoCTF <ops@picoctf.com>
Date:   Tue Mar 12 00:07:06 2024 +0000

    create top secret project

```

Y aqui podemos ver al usuario que hizo los cambios en el archivo y nos dan la flag:
```flag
picoCTF{@sk_th3_1nt3rn_cfca95b2}
```


## Notas adicionales

## Referencias
