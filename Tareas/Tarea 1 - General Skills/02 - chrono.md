# chrono

## Descripcion
How to automate tasks to run at intervals on linux servers?Use ssh to connect to this server:

```
Server: saturn.picoctf.net
Port: 61233
Username: picoplayer 
Password: 5wf1w1hVxt
```
## Solucion
Primero nos conectamos al reto con las credenciales que nos propocionan: 
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ ssh -p 63634 saturn.picoctf.net -l picoplayer
```

Luego dentro del reto, buscamos algun archivo en el directorio del usuario, pero no hay nada. Por el nombre del reto, nos podemos hacer una idea de que a lo mejor esta relacionado a las tareas cron en linux, pero toca investigar mas, tal vez para hacer un escalado de privilegios o algo.

Con la informacion buscada, veo que tal vez si se pueda hacer un escalado de privilegios, pero al intentar listar los privilegios del usuario, no se puede:
```bash
picoplayer@challenge:/etc$ sudo -l
[sudo] password for picoplayer: 
Sorry, user picoplayer may not run sudo on challenge.
```

Entonces tal vez el reto no vaya por ahi, pero igual vamos a buscar si tiene que ver algo con tareas cron, por lo que vamos al directorio /etc
```bash
picoplayer@challenge:/$ cd /etc
```

Ahora en el directorio filtramos por cron:
```bash
picoplayer@challenge:/etc$ ls -la | grep "cron"
drwxr-xr-x 1 root   root       26 Aug  4  2023 cron.d
drwxr-xr-x 1 root   root       26 Aug  4  2023 cron.daily
drwxr-xr-x 2 root   root       26 Aug  4  2023 cron.hourly
drwxr-xr-x 2 root   root       26 Aug  4  2023 cron.monthly
drwxr-xr-x 2 root   root       26 Aug  4  2023 cron.weekly
-rw-r--r-- 1 root   root       43 Aug  4  2023 crontab
```

Y podemos ver un archivo de texto crontab, en el cual hay tareas que se automatizan, entonces lo leemos para ver si nos dice algo o nos da una pista, en lugar de eso, nos da la flag: 
```bash
picoplayer@challenge:/etc$ cat crontab 
# picoCTF{Sch3DUL7NG_T45K3_L1NUX_9d5cb744}
```

```flag
picoCTF{Sch3DUL7NG_T45K3_L1NUX_9d5cb744}
```

## Notas adicionales

## Referencias

* https://labex.io/tutorials/linux-privilege-escalation-via-cron-jobs-416140
* https://www.redeszone.net/tutoriales/servidores/cron-crontab-linux-programar-tareas/
* https://gtfobins.github.io/gtfobins/timedatectl/
* https://deephacking.tech/cronjobs-privilege-escalation-en-linux/

