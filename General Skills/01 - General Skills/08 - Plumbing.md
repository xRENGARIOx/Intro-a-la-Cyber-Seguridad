# Plumbing

## Descripcion
Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag? Connect to `jupiter.challenges.picoctf.org 14291`.
## Solucion
Construimos nuestro comando para conectarnos al servidor:
```sh
nc jupiter.challenges.picoctf.org 14291
```

La salida nos entrega pura basura en la cual es dificil ver la flag:
```sh
I don't think this is a flag either
Not a flag either
Again, I really don't think this is a flag
Again, I really don't think this is a flag
Not a flag either
Not a flag either
Not a flag either
Not a flag either
I don't think this is a flag either
This is defintely not a flag
Not a flag either
Again, I really don't think this is a flag
Not a flag either
```
Por lo tanto vamos a usar grep para buscar entre el texto de salida:
```sh
nc jupiter.challenges.picoctf.org 14291 | grep "pico"
```

Y asi nos entrega la flag
```flag
picoCTF{digital_plumb3r_ea8bfec7}
```

## Notas adicionales

## Referencias
