# Client-side-again

## Descripcion
Can you break into this super secure portal? `https://jupiter.challenges.picoctf.org/problem/56816/` ([link](https://jupiter.challenges.picoctf.org/problem/56816/)) or http://jupiter.challenges.picoctf.org:56816
## Solucion
Primero vamos al link que nos proporciona el reto, y por el nombre, podemos ver que el reto es similar al anterior de client-side, entonces probamos nuevamente credenciales por defecto como 'admin', y no pasa nada.
Vamos a ver el codigo fuente y vemos que se esta guardando la flag:
```js
var _0x5a46=['37115}','_again_3','this','Password\x20Verified','Incorrect\x20password','getElementById','value','substring','picoCTF{','not_this'];
```
Entonces simplemente desde aqui comenzamos a reconstruirla siguiendo la estructura de las banderas y listo:

```flag
picoCTF{not_this_again_337115}
```

## Notas adicionales

## Referencias
