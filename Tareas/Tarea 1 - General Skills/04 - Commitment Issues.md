# Commitment Issues

## Descripcion
I accidentally wrote the flag down. Good thing I deleted it!You download the challenge files here:

- [challenge.zip](https://artifacts.picoctf.net/c_titan/139/challenge.zip)

## Solucion
Descargamos el archivo y lo decomprimimos:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ 7z x challenge.zip

7-Zip 24.09 (x64) : Copyright (c) 1999-2024 Igor Pavlov : 2024-11-29
 64-bit locale=C.UTF-8 Threads:16 OPEN_MAX:1024, ASM

Scanning the drive for archives:
1 file, 19193 bytes (19 KiB)

Extracting archive: challenge.zip
--
Path = challenge.zip
Type = zip
Physical Size = 19193

Everything is Ok

Folders: 20
Files: 28
Size:       20746
Compressed: 19193
```

Luego nos metemos a la carpeta y vemos que realmente no tiene nada:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ cd drop-in  
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ ls
message.txt
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ cat message.txt 
───────┬─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: message.txt
───────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ TOP SECRET
───────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
     
```

Vemos que las pistas nos dicen que podemos usar Git para ver el control de versiones, entonces vamos a probar a ver los cambios que han habido con ayuda de Git:
```bash
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ git status
On branch master
nothing to commit, working tree clean
```

Vemos que estamos en la rama master, asi que procedemos a ver que encontramos en el registro:
```bash
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ git log   
commit 144fdc44b09058d7ea7f224121dfa5babadddbb9 (HEAD -> master)
Author: picoCTF <ops@picoctf.com>
Date:   Tue Mar 12 00:06:25 2024 +0000

    remove sensitive info

commit 7d3aa557ff7ba7d116badaf5307761efb3622249
Author: picoCTF <ops@picoctf.com>
Date:   Tue Mar 12 00:06:25 2024 +0000

    create flag
```

Ahora vemos que hubo un commit en el que se creo la flag, asi que vamos a checar que paso en ese commit:
```bash
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ git checkout 7d3aa557ff7ba7d116badaf5307761efb3622249
Note: switching to '7d3aa557ff7ba7d116badaf5307761efb3622249'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 7d3aa55 create flag
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ git status                                           
HEAD detached at 7d3aa55
nothing to commit, working tree clean
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ ls    
message.txt
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ cat message.txt
───────┬─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: message.txt
───────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ picoCTF{s@n1t1z3_be3dd3da}
───────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```

Y vemos que asi el reto nos arroja la flag:
```flag
picoCTF{s@n1t1z3_be3dd3da}
```


## Notas adicionales

## Referencias

* https://primer.picoctf.org/#_git_version_control
