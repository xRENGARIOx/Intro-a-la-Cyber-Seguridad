# Collaborative Development

## Descripcion
My team has been working very hard on new features for our flag printing program! I wonder how they'll work together?You can download the challenge files here:

- [challenge.zip](https://artifacts.picoctf.net/c_titan/177/challenge.zip)

## Solucion
Descargamos y descomprimimos el archivo:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ 7z x challenge.zip

7-Zip 24.09 (x64) : Copyright (c) 1999-2024 Igor Pavlov : 2024-11-29
 64-bit locale=C.UTF-8 Threads:16 OPEN_MAX:1024, ASM

Scanning the drive for archives:
1 file, 24646 bytes (25 KiB)

Extracting archive: challenge.zip
--
Path = challenge.zip
Type = zip
Physical Size = 24646

Everything is Ok

Folders: 28
Files: 40
Size:       23485
Compressed: 24646
```

Una vez dentro, vemos el contenido, y solo vemos un archivo de python que no tiene nada relevante:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ cd drop-in
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ ls
flag.py
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ cat flag.py   
───────┬─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: flag.py
───────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ print("Printing the flag...")
───────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```

Procedemos a ver si es un repositorio y vemos que tiene diferentes ramas:
```bash
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ git status           
On branch main
nothing to commit, working tree clean
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Downloads/drop-in]
└─$ git branch -a 
  feature/part-1
  feature/part-2
  feature/part-3
* main
```

Entonces ahora deberemos de ver el contenido de cada branch para ver el contenido de la flag, pero para hacerlo mas facil y rapido, voy a usar visual estudio code y ver cada branch mas rapido:
feature/part-1:
```python
print("Printing the flag...")

print("picoCTF{t3@mw0rk_", end='')
```
feature/part-2:
```python
print("Printing the flag...")

  

print("m@k3s_th3_dr3@m_", end='')
```
feature/part-3:
```python
print("Printing the flag...")

  

print("w0rk_7ae8dd33}")
```

Ahora solo juntamos las 3 partes y obtenemos la flag:
```flag
picoCTF{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_7ae8dd33}
```


## Notas adicionales

## Referencias
