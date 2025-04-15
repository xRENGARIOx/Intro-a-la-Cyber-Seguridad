# HashingJobApp

## Descripcion
If you want to hash with the best, beat this test!`nc saturn.picoctf.net 62986`
## Solucion
Nos conectamos al reto con el commando que nos dan: 
```sh
nc saturn.picoctf.net 62986
```

Y pues nos dan una palabra y nos piden que calculemos el hash, entonces vamos a usar Cyberchef:
```
Please md5 hash the text between quotes, excluding the quotes: 'a locker room'
Answer:
```
Cyberchef:
```
input: a locker room
recipe: md5
output: 9be86a0fa0b3b24d0d18d78dc45808f1
```
Respondemos y nos dan otra, por lo cual, hay que repetir el proceso en cyberchef tanto como nos lo pidan:
```
9be86a0fa0b3b24d0d18d78dc45808f1
9be86a0fa0b3b24d0d18d78dc45808f1
Correct.
Please md5 hash the text between quotes, excluding the quotes: 'Joan of Arc'
Answer:
19ba425a542946fcf13228d9ddd53139
19ba425a542946fcf13228d9ddd53139
Correct.
Please md5 hash the text between quotes, excluding the quotes: 'Keanu Reeves'
Answer: 
4d2e1f8eabca061706aec58b21c2e199
4d2e1f8eabca061706aec58b21c2e199
Correct.
picoCTF{4ppl1c4710n_r3c31v3d_674c1de2}
```

Y finalmente asi es como obtenemos la flag:
```flag
picoCTF{4ppl1c4710n_r3c31v3d_674c1de2}
```




## Notas adicionales

## Referencias
