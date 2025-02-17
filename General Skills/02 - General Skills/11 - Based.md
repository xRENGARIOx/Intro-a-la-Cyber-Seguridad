# Based

## Descripcion
To get truly 1337, you must understand different data encodings, such as hexadecimal or binary. Can you get the flag from this program to prove you are on the way to becoming 1337? Connect with `nc jupiter.challenges.picoctf.org 29956`.

## Solucion


Primero nos conectamos al reto con el comando que nos proporciona el mismo reto:
```bash
┌──(xrengariox㉿PC)-[~]
└─$ nc jupiter.challenges.picoctf.org 29956
Let us see how data is stored
street
Please give the 01110011 01110100 01110010 01100101 01100101 01110100 as a word.
...
you have 45 seconds.....

Input:

WRONG!

```
Vemos que nos dan varios numeros y nos pide que los ingresemos pero como palabra.
Usamos una herramienta como cyberchef:
```
Input: 01110011 01110100 01110010 01100101 01100101 01110100

Receipt: From Binary, Delimiter=Space, ByteLength=8

Output: street
```
Y ahora con la salida, probamos a nuevamente conectarnos al reto e ingresar la palabra que obtuvimos.
```bash
Please give me the  155 141 160 as a word.
Input:
```
Analizando la tabla ASCII podemos ver que no representan valores Decimales, mas bien parecen ser valores Octales, asi que cambiamos la receta para esta palabra:
```
Input: 155 141 160

Receipt: From Octal, Delimiter=Space

Output: map
```
Y por ultimo nos arroja una palabra mas:
```bash
Please give me the 6c697a617264 as a word.
Input:
```
Y parece ser que esta en Hexadecimal, asi que usamos esa receta:
```
Input: 6c697a617264

Receipt: From_Hex, Delimiter=None

Output: lizard
```
y finalmente nos arroja la flag.
#### FLAG
```flag
You've beaten the challenge
Flag: picoCTF{learning_about_converting_values_b375bb16}
```
## Notas adicionales
Nota: Como el reto nos da tiempo limitado, seria recomendable tener varias ventanas abiertas con las recetas para simplemente poner las entradas rapidamente. Y tambien porque cada vez que se hace la conexion al reto las palabras cambian.
## Referencias
* https://gchq.github.io/CyberChef/#recipe=From_Binary('Space',8)&input=MDExMDAxMTAgMDExMDAwMDEgMDExMDExMDAgMDExMDAwMTEgMDExMDExMTEgMDExMDExMTA
* https://www.ascii-code.com

