# What's a net cat?

## Descripcion
Using netcat (nc) is going to be pretty important. Can you connect to 
`jupiter.challenges.picoctf.org` at port `41120` to get the flag?

## Solucion
Construimos nuestro comando de net cat con ayuda de:
```shell
man nc
```

```sh
nc jupiter.challenges.picoctf.org 41120
```
Y nos arroja el siguiente texto con la flag:

```flag
You're on your way to becoming the net cat master
picoCTF{nEtCat_Mast3ry_3214be47}
```

## Notas adicionales

## Referencias
