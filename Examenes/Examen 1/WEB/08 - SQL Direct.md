# Reto
Connect to this PostgreSQL server and find the flag!`psql -h saturn.picoctf.net -p 54005 -U postgres pico`Password is `postgres`
## Descripcion
Connect to this PostgreSQL server and find the flag!`psql -h saturn.picoctf.net -p 54005 -U postgres pico`Password is `postgres`
## Solucion
Nos conectamos a la base de datos con el comando que nos dan:
```sh
┌──(xrengariox㉿PC)-[~]
└─$ psql -h saturn.picoctf.net -p 54005 -U postgres pico
Password for user postgres: 
psql (17.4 (Debian 17.4-1+b1), server 15.2 (Debian 15.2-1.pgdg110+1))
Type "help" for help.

pico=# 
```

Y empazamos a ver el contenido:
```
pico=# \l
                                                    List of databases
   Name    |  Owner   | Encoding | Locale Provider |  Collate   |   Ctype    | Locale | ICU Rules |   Access privileges   
-----------+----------+----------+-----------------+------------+------------+--------+-----------+-----------------------
 pico      | postgres | UTF8     | libc            | en_US.utf8 | en_US.utf8 |        |           | 
 postgres  | postgres | UTF8     | libc            | en_US.utf8 | en_US.utf8 |        |           | 
 template0 | postgres | UTF8     | libc            | en_US.utf8 | en_US.utf8 |        |           | =c/postgres          +
           |          |          |                 |            |            |        |           | postgres=CTc/postgres
 template1 | postgres | UTF8     | libc            | en_US.utf8 | en_US.utf8 |        |           | =c/postgres          +
           |          |          |                 |            |            |        |           | postgres=CTc/postgres
(4 rows)

pico=# \connect pico
psql (17.4 (Debian 17.4-1+b1), server 15.2 (Debian 15.2-1.pgdg110+1))
You are now connected to database "pico" as user "postgres".
pico=# \dt
         List of relations
 Schema | Name  | Type  |  Owner   
--------+-------+-------+----------
 public | flags | table | postgres
(1 row)

pico=# SELECT * from flags;
 id | firstname | lastname  |                address                 
----+-----------+-----------+----------------------------------------
  1 | Luke      | Skywalker | picoCTF{L3arN_S0m3_5qL_t0d4Y_73b0678f}
  2 | Leia      | Organa    | Alderaan
  3 | Han       | Solo      | Corellia
(3 rows)

pico=# 
```

Y pues asi encontramos la flag:
```flag
picoCTF{L3arN_S0m3_5qL_t0d4Y_73b0678f}
```

## Notas adicionales

## Referencias
