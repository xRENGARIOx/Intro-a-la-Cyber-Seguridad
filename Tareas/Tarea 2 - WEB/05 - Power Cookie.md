# Power Cookie

## Descripcion
Can you get the flag?Go to this [website](http://saturn.picoctf.net:54884/) and see what you can discover.
## Solucion
Accedemos al reto con el link que nos proporcionan, y vemos un solo un boton que al presionarlo nos dice: We apologize, but we have no guest services at the moment.
Por el nombre del reto nos damos una idea de que tal vez tenga que ver con cookies, asi que vamos a ver las cookies que tenemos:
Vemos una llamda `isAdmin` con valor de 0, entonces lo cambiamos a 1 y recargamos la pagina, lo que finalmente nos da la flag:
```flag
picoCTF{gr4d3_A_c00k13_5d2505be}
```

## Notas adicionales

## Referencias
