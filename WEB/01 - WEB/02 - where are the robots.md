# where are the robots

## Descripcion
Can you find the robots? `https://jupiter.challenges.picoctf.org/problem/56830/` ([link](https://jupiter.challenges.picoctf.org/problem/56830/)) or http://jupiter.challenges.picoctf.org:56830

## Solucion
Vamos el link que nos proporciona la pagina, y como el nombre del reto nos da la pista, vamos a buscar directamente en el robots.txt:
```url
https://jupiter.challenges.picoctf.org/problem/56830/robots.txt
```

En el archivo vemos una ruta o endpoint que llama la atencion, asi que vamos a ver que oculta:
```url
https://jupiter.challenges.picoctf.org/problem/56830/1bb4c.html
```
Y aqui vemos la flag:
```flag
picoCTF{ca1cu1at1ng_Mach1n3s_1bb4c}
```

## Notas adicionales

## Referencias
