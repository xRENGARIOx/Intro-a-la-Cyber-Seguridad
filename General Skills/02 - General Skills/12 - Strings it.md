# String it

## Descripcion
Can you find the flag in [file](https://jupiter.challenges.picoctf.org/static/fae9ac5267cd6e44124e559b901df177/strings) without running it?
## Solucion
Con ayuda del nombre del reto nos podemos dar una idea de que debemos de usar el comando strings de Linux, asi que primero descargamos el archivo y despues hacemos un strings al archivo, pero la salida es muy grande, asi que entre todas las lineas que nos arroja filtramos por "pico" y obtenemos la flag.
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ strings strings | grep "pico"
picoCTF{5tRIng5_1T_7f766a23}
```

```flag
picoCTF{5tRIng5_1T_7f766a23}
```

## Notas adicionales

## Referencias
https://linux.die.net/man/1/strings
