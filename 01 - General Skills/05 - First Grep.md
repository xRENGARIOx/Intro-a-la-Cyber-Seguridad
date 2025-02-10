# First Grep

## Descripcion
Can you find the flag in [file](https://jupiter.challenges.picoctf.org/static/515f19f3612bfd97cd3f0c0ba32bd864/file)? This would be really tedious to look through manually, something tells me there is a better way.
## Solucion
Desde la consola usar el comando grep para buscar dentro del archivo.
Como ya sabemos el formato de las flags simplemente buscamos un patron que coincida.
```shell
grep "pico" file
```

```flag
picoCTF{grep_is_good_to_find_things_5af9d829}
```

## Notas adicionales

## Referencias
