# Mind your Ps and Qs

## Descripcion
In RSA, a small `e` value can be problematic, but what about `N`? Can you decrypt this? [values](https://mercury.picoctf.net/static/bf5e2c8811afb4669f4a6850e097e8aa/values)
## Solucion
Primero descargamos el archivo que nos da el reto:
```sh
┌──(xrengariox㉿PC)-[~/Clase/crypto/mind]
└─$ wget https://mercury.picoctf.net/static/bf5e2c8811afb4669f4a6850e097e8aa/values    
--2025-05-21 12:00:11--  https://mercury.picoctf.net/static/bf5e2c8811afb4669f4a6850e097e8aa/values
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 205 [application/octet-stream]
Saving to: ‘values’

values                               100%[===================================================================>]     205  --.-KB/s    in 0s      

2025-05-21 12:00:12 (182 MB/s) - ‘values’ saved [205/205]

┌──(xrengariox㉿PC)-[~/Clase/crypto/mind]
└─$ ls
values

┌──(xrengariox㉿PC)-[~/Clase/crypto/mind]
└─$ file values 
values: ASCII text

┌──(xrengariox㉿PC)-[~/Clase/crypto/mind]
└─$ cato values    
Decrypt my super sick RSA:
c: 421345306292040663864066688931456845278496274597031632020995583473619804626233684
n: 631371953793368771804570727896887140714495090919073481680274581226742748040342637
e: 65537   
```

Vamos a comenzar viendo a ver si encontramos los factores de n, usaremos factor db:
y los encontramos:
```
p = 1461849912200000206276283741896701133693
q = 431899300006243611356963607089521499045809
```

Ahora vamos a hacer un codigo en python:
```python 
c = 421345306292040663864066688931456845278496274597031632020995583473619804626233684
n = 631371953793368771804570727896887140714495090919073481680274581226742748040342637
e = 65537
p = 1461849912200000206276283741896701133693
q = 431899300006243611356963607089521499045809  
tn = (p-1) * (q-1)
d = pow(e, -1, tn)
m = pow(c, d, n)
mensaje_bytes = bytes.fromhex(hex(m)[2:])
print(mensaje_bytes)
```

Y asi obtenemos la flag:
```
┌──(xrengariox㉿PC)-[~/Clase/crypto/mind]
└─$ python3 exploit.py
b'picoCTF{sma11_N_n0_g0od_55304594}'
```

Flag:
```flag
picoCTF{sma11_N_n0_g0od_55304594}
```
## Notas adicionales

## Referencias
https://factordb.com/index.php?query=

