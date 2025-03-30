# Roboto Sans

## Descripcion
The flag is somewhere on this web application not necessarily on the website. Find it.Check [this](http://saturn.picoctf.net:58816/) out.
## Solucion
Vamos al reto con el link que nos proporcionan.
Por el nombre del reto, podemos hacernos una idea de que debemos de buscar en los `robots.txt`  entonces vamos a ver que econtramos:
```robots
User-agent *
Disallow: /cgi-bin/
Think you have seen your flag or want to keep looking.

ZmxhZzEudHh0;anMvbXlmaW
anMvbXlmaWxlLnR4dA==
svssshjweuiwl;oiho.bsvdaslejg
Disallow: /wp-admin/
```
Parece ser un base64, asi que con ayuda de cyberchef vamos a ver que nos dice:
```cyberchef
input:ZmxhZzEudHh0      

recipe:From Base64

output:flag1.txtjs/myfi
```

```cyberchef
input: anMvbXlmaWxlLnR4dA==

recipe: From Base64

output: js/myfile.txt
```
Lo que parecen ser 2 archivos, asi que vamos a ver esas rutas para ver que hay ahi:
Si copiamos la primer "ruta" en el navegador no nos lleva a ningun lado, pero si usamos la segunda:
`http://saturn.picoctf.net:58816/js/myfile.txt`
Vemos que nos arroja la bandera:
```flag
picoCTF{Who_D03sN7_L1k5_90B0T5_032f1c2b}
```

## Notas adicionales

## Referencias
