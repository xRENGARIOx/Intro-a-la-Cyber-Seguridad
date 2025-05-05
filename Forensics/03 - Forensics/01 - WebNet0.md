# WebNet0

## Descripcion
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/0c84d3636dd088d9fe4efd5d0d869a06/capture.pcap) and [key](https://jupiter.challenges.picoctf.org/static/0c84d3636dd088d9fe4efd5d0d869a06/picopico.key). Recover the flag.
## Solucion
Primero descargamos los archivos que nos proporciona el reto:
```sh
┌──(xrengariox㉿PC)-[~/Clase/webnet]
└─$ wget https://jupiter.challenges.picoctf.org/static/0c84d3636dd088d9fe4efd5d0d869a06/capture.pcap
--2025-05-05 12:11:31--  https://jupiter.challenges.picoctf.org/static/0c84d3636dd088d9fe4efd5d0d869a06/capture.pcap
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 13163 (13K) [application/octet-stream]
Saving to: ‘capture.pcap’

capture.pcap                         100%[===================================================================>]  12.85K  --.-KB/s    in 0s      

2025-05-05 12:11:39 (146 MB/s) - ‘capture.pcap’ saved [13163/13163]

┌──(xrengariox㉿PC)-[~/Clase/webnet]
└─$ wget https://jupiter.challenges.picoctf.org/static/0c84d3636dd088d9fe4efd5d0d869a06/picopico.key
--2025-05-05 12:11:43--  https://jupiter.challenges.picoctf.org/static/0c84d3636dd088d9fe4efd5d0d869a06/picopico.key
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1704 (1.7K) [application/octet-stream]
Saving to: ‘picopico.key’

picopico.key                         100%[===================================================================>]   1.66K  --.-KB/s    in 0s      

2025-05-05 12:11:51 (22.8 MB/s) - ‘picopico.key’ saved [1704/1704]

```

Abrimos el archivo de captura con wireshark:
```sh
┌──(xrengariox㉿PC)-[~/Clase/webnet]
└─$ wireshark capture.pcap &>/dev/null &disown
[1] 6252
```

Vemos que el trafico esta encriptado, entonces vamos a usar la llave que nos dan para desencriptarlo, nos vamos a Edit>Preferencias>Protocolos>TLS y agregamos el archivo de la key en las RSA keys.
Despues solo seguimos el trafico TLS y veremos la bandera:

```flag
picoCTF{nongshim.shrimp.crackers}
```
## Notas adicionales
```sh
ssldump -r capture.pcap -k picopico.key -d | grep pico -A 2
```
## Referencias
