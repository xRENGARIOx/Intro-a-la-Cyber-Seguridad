# Glory of the Garden

## Descripcion
This [garden](https://jupiter.challenges.picoctf.org/static/43c4743b3946f427e883f6b286f47467/garden.jpg) contains more than it seems.
## Solucion
Descargamos la imagen que nos proporciona el reto.
Y primero le hacemos un file para saber que tipo de archivo es.
```sh
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ file garden.jpg                         
garden.jpg: JPEG image data, JFIF standard 1.01, resolution (DPI), density 72x72, segment length 16, baseline, precision 8, 2999x2249, components 3
```

Dice que es una simple imagen, entonces vamos a ver si tiene algun string en ella:

```sh
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ strings garden.jpg
JFIF
XICC_PROFILE
HLino
.
.
.
]hWP&
jc#k
=7g&
mjx/
s\]|."Ue
\qZf
Here is a flag "picoCTF{more_than_m33ts_the_3y3657BaB2C}"

```

Y obtenemos la flag:
```flag
picoCTF{more_than_m33ts_the_3y3657BaB2C}
```

## Notas adicionales

## Referencias
