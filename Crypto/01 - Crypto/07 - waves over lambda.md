# waves over lambda

## Descripcion
We made a lot of substitutions to encrypt this. Can you decrypt it? Connect with `nc jupiter.challenges.picoctf.org 13758`.
## Solucion
Nos conectamos al reto con el comando que nos dieron:
```sh
┌──(xrengariox㉿PC)-[~/Clase/crypto/intere]
└─$ nc jupiter.challenges.picoctf.org 13758 
-------------------------------------------------------------------------------
xbrkioqs pziz ds abwi mjok - mizewzrxa_ds_x_buzi_jovlfo_fruqmiqoaw
-------------------------------------------------------------------------------
tz tziz rbq vwxp vbiz qpor o ewoiqzi bm or pbwi bwq bm bwi spdy qdjj tz sot pzi sdrn, orf qpzr d wrfzisqbbf mbi qpz mdisq qdvz tpoq tos vzorq la o spdy mbwrfzidrk dr qpz szo.  d vwsq oxnrbtjzfkz d pof poifja zazs qb jbbn wy tpzr qpz szovzr qbjf vz spz tos sdrndrk; mbi mibv qpz vbvzrq qpoq qpza ioqpzi ywq vz drqb qpz lboq qpor qpoq d vdkpq lz sodf qb kb dr, va pzoiq tos, os dq tziz, fzof tdqpdr vz, yoiqja tdqp midkpq, yoiqja tdqp pbiibi bm vdrf, orf qpz qpbwkpqs bm tpoq tos azq lzmbiz vz.

```

Vemos que este texto no es un cifrado caesar ni un posible vigenere, por lo que posibllemente es un cifrado por sustitucion, entonces vamos a usar una herramienta para romper el cifrado:
```
input: 
-------------------------------------------------------------------------------
xbrkioqs pziz ds abwi mjok - mizewzrxa_ds_x_buzi_jovlfo_fruqmiqoaw
-------------------------------------------------------------------------------
tz tziz rbq vwxp vbiz qpor o ewoiqzi bm or pbwi bwq bm bwi spdy qdjj tz sot pzi sdrn, orf qpzr d wrfzisqbbf mbi qpz mdisq qdvz tpoq tos vzorq la o spdy mbwrfzidrk dr qpz szo.  d vwsq oxnrbtjzfkz d pof poifja zazs qb jbbn wy tpzr qpz szovzr qbjf vz spz tos sdrndrk; mbi mibv qpz vbvzrq qpoq qpza ioqpzi ywq vz drqb qpz lboq qpor qpoq d vdkpq lz sodf qb kb dr, va pzoiq tos, os dq tziz, fzof tdqpdr vz, yoiqja tdqp midkpq, yoiqja tdqp pbiibi bm vdrf, orf qpz qpbwkpqs bm tpoq tos azq lzmbiz vz.

output:
-------------------------------------------------------------------------------
congrats here is your flag - frequency_is_c_over_lambda_dnvtfrtayu
-------------------------------------------------------------------------------
we were not much more than a quarter of an hour out of our ship till we saw her sink, and then i understood for the first time what was meant by a ship foundering in the sea.  i must acknowledge i had hardly eyes to look up when the seamen told me she was sinking; for from the moment that they rather put me into the boat than that i might be said to go in, my heart was, as it were, dead within me, partly with fright, partly with horror of mind, and the thoughts of what was yet before me.


abcdefghijklmnopqrstuvwxyz     
yoziqdxjrlgbfkahtnswvmucpe
```

Y asi obtenemos la flag (Aqui no hay que poner el formato de siempre):
```flag
frequency_is_c_over_lambda_dnvtfrtayu
```
## Notas adicionales

## Referencias
https://www.guballa.de/substitution-solver

