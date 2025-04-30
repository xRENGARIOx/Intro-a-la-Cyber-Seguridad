# shark on wire 2

## Descripcion
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/b506393b6f9d53b94011df000c534759/capture.pcap). Recover the flag that was pilfered from the network.
## Solucion
Primero descargamos el archivo para comenzar a analizarlo:
```sh
┌──(xrengariox㉿PC)-[~/Clase/shark]
└─$ wget https://jupiter.challenges.picoctf.org/static/b506393b6f9d53b94011df000c534759/capture.pcap
--2025-04-28 13:04:21--  https://jupiter.challenges.picoctf.org/static/b506393b6f9d53b94011df000c534759/capture.pcap
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 112318 (110K) [application/octet-stream]
Saving to: ‘capture.pcap’

capture.pcap                         100%[===================================================================>] 109.69K   619KB/s    in 0.2s    

2025-04-28 13:04:30 (619 KB/s) - ‘capture.pcap’ saved [112318/112318]
```

Vemos que es un archivo de wireshark, entonces vamos a abrirlo para ver el contenido:
```sh
┌──(xrengariox㉿PC)-[~/Clase/shark]
└─$ wireshark capture.pcap
```

Entonces, al analizarlo nos damos cuenta que la comunicacion fue a traves de UDP y que el puerto de origen es el 22, entonces vamos a hacer un script en python para analizar los paquetes y formar la flag:

```python
from scapy.all import *

packets = rdpcap('capture.pcap')
flag = ""

for p in packets:
        if UDP in p and p[UDP].dport == 22:
                if p[UDP].sport > 5000:
                        flag += chr(p[UDP].sport - 5000)
print(flag)
```

Lo corremos:
```
┌──(xrengariox㉿PC)-[~/Clase/shark]
└─$ python3 exploit.py
picoCTF{p1LLf3r3d_data_v1a_st3g0}
```

Y obtenemos la flag:
```flag
picoCTF{p1LLf3r3d_data_v1a_st3g0}
```
## Notas adicionales

## Referencias
