# Secrets

## Descripcion
We have several pages hidden. Can you find the one with the flag?The website is running [here](http://saturn.picoctf.net:57258/).
## Solucion
Nos conectamos al reto con el link que nos proporcionan.

Podemos ver una pagina que realmente no nos dice mucho

Viendo el codigo fuente nos damos cuenta de que la imagen de home esta de local en el servidor, y podemos acceder a su ruta.

Intentamos ir carpetas atras, en la de assets no tenemos exito, pero en la de secret si.

Es una nueva pagina con un gift, ahora en el codigo fuente de esta podemos ver un .css pero al hacer clic no nos lleva a ningun lado, mas que una pagina en blanco, pero tiene la ruta [http://saturn.picoctf.net:58984/secret/hidden/file.css](http://saturn.picoctf.net:58984/secret/hidden/file.css), por lo que ahora vamos atras y encontramos una pagina para iniciar sesion

Vemos el codigo fuente y nos da una pista de una ruta nueva con [http://saturn.picoctf.net:58984/secret/hidden/superhidden/](http://saturn.picoctf.net:58984/secret/hidden/superhidden/)

Nos dice que ya esta, pero que no lo podemos ver, asi que vemos el codigo fuente y asi encontramos la flag. picoCTF{succ3ss_@h3n1c@10n_39849bcf} 

## Notas adicionales
Anteriormente no aparecia la flag, pero esta ultima vez que revise el reto, solamente con estar en la ultima ruta se muestra sin necesidad de ver el codigo fuente.
## Referencias
