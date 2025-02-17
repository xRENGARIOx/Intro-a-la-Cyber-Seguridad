#  Magikarp Ground Mission

## Descripcion
Do you know how to move between directories and read files in the shell? Start the container, `ssh` to it, and then `ls` once connected to begin. Login via `ssh` as `ctf-player` with the password, `481e7b14`

## Solucion
Nos conectamos con el comando que nos proporciona el reto:
 ```bash
 ssh ctf-player@venus.picoctf.net -p 52939
```  

Al conectarnos al servidor podemos ver los archivos que tiene, asi como leer el contenido de estos, y vemos que nos da una parte de la flag:
```bash
ctf-player@pico-chall$ ls
1of3.flag.txt  instructions-to-2of3.txt
ctf-player@pico-chall$ cat 1of3.flag.txt 
picoCTF{xxsh_
ctf-player@pico-chall$ cat instructions-to-2of3.txt 
Next, go to the root of all things, more succinctly `/`
```
Ahora seguimos la instruccion y vamos a la raiz, donde encontramos la segunda parte de la flag:
```bash
ctf-player@pico-chall$ cd /
ctf-player@pico-chall$ ls
2of3.flag.txt  bin  boot  dev  etc  home  instructions-to-3of3.txt  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
ctf-player@pico-chall$ cat 2of3.flag.txt 
0ut_0f_\/\/4t3r_
```

Seguimos las instrucciones para llegar a la tercera parte y asi encontramos la ultima parte de la flag:
```
ctf-player@pico-chall$ cat instructions-to-3of3.txt 
Lastly, ctf-player, go home... more succinctly `~`
ctf-player@pico-chall$ cd ~
ctf-player@pico-chall$ ls
3of3.flag.txt  drop-in
ctf-player@pico-chall$ cat 3of3.flag.txt 
1118a9a4}

```

```flag
picoCTF{xxsh_0ut_0f_\/\/4t3r_1118a9a4}
```
## Notas adicionales

## Referencias
