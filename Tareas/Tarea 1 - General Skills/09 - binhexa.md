# binhexa

## Descripcion
How well can you perfom basic binary operations?Start searching for the flag here `nc titan.picoctf.net 62345`
## Solucion
Nos conectamos al reto con las credenciales que nos propocionan:
```bash
┌──(xrengariox㉿PC)-[~/Downloads/home/ctf-player/drop-in]
└─$ nc titan.picoctf.net 62345
```

Y comenzamos a resolver los retos que nos dan:
```bash
Welcome to the Binary Challenge!"
Your task is to perform the unique operations in the given order and find the final result in hexadecimal that yields the flag.

Binary Number 1: 00001100
Binary Number 2: 11010000


Question 1/6:
Operation 1: '|'
Perform the operation on Binary Number 1&2.
Enter the binary result: 11011100
Correct!

Question 2/6:
Operation 2: '+'
Perform the operation on Binary Number 1&2.
Enter the binary result: 11011100
Correct!

Question 3/6:
Operation 3: '<<'
Perform a left shift of Binary Number 1 by 1 bits.
Enter the binary result: 00011000
Correct!

Question 4/6:
Operation 4: '*'
Perform the operation on Binary Number 1&2.
Enter the binary result: 0100111000000
Correct!

Question 5/6:
Operation 5: '&'
Perform the operation on Binary Number 1&2.
Enter the binary result: 00000000
Correct!

Question 6/6:
Operation 6: '>>'
Perform a right shift of Binary Number 2 by 1 bits .
Enter the binary result: 10100001
Incorrect. Try again
Enter the binary result: 01101000
Correct!

Enter the results of the last operation in hexadecimal: 68

Correct answer!
The flag is: picoCTF{b1tw^3se_0p3eR@tI0n_su33essFuL_675602ae}

```

Y al final nos dan la flag:
```flag
picoCTF{b1tw^3se_0p3eR@tI0n_su33essFuL_675602ae}
```

## Notas adicionales

## Referencias
