# Webnet1
## Descripcion
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/fbf98e695555a2a48fe42c9a245de376/capture.pcap) and [key](https://jupiter.challenges.picoctf.org/static/fbf98e695555a2a48fe42c9a245de376/picopico.key). Recover the flag.
## Solucion
Descargamos los archivos que nos proporciona el reto:
```sh
┌──(xrengariox㉿PC)-[~/Clase/webnet1]
└─$ wget https://jupiter.challenges.picoctf.org/static/fbf98e695555a2a48fe42c9a245de376/capture.pcap
--2025-05-05 12:25:52--  https://jupiter.challenges.picoctf.org/static/fbf98e695555a2a48fe42c9a245de376/capture.pcap
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 92525 (90K) [application/octet-stream]
Saving to: ‘capture.pcap’

capture.pcap                         100%[===================================================================>]  90.36K   223KB/s    in 0.4s    

2025-05-05 12:26:02 (223 KB/s) - ‘capture.pcap’ saved [92525/92525]

┌──(xrengariox㉿PC)-[~/Clase/webnet1]
└─$ wget https://jupiter.challenges.picoctf.org/static/fbf98e695555a2a48fe42c9a245de376/picopico.key
--2025-05-05 12:26:09--  https://jupiter.challenges.picoctf.org/static/fbf98e695555a2a48fe42c9a245de376/picopico.key
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1704 (1.7K) [application/octet-stream]
Saving to: ‘picopico.key’

picopico.key                         100%[===================================================================>]   1.66K  --.-KB/s    in 0s      

2025-05-05 12:26:17 (23.7 MB/s) - ‘picopico.key’ saved [1704/1704]

```

Ahora abrimos el archivo de captura con wireshark:
```sh
┌──(xrengariox㉿PC)-[~/Clase/webnet1]
└─$ wireshark capture.pcap &>/dev/null &disown                                                      
[1] 13986
```

Entonces ahora hacemos lo mismo vamos a Edit>Preferences>Protocols>TLS y configuramos la llave RSA.
Vemos que aunque hayamos echo eso, aun no vemos la bandera, pero vemos que se puede exportar los objetos, dentro de esto, vemos que se descargo una imagen, entonces nos vamos a File>Export Objetct>HTTP y descargamos el archivo jpg. Entonces la salvamos y si le hacemos un strings obtenemos la flag:
```sh
┌──(xrengariox㉿PC)-[~/Clase/webnet1]
└─$ ls
capture.pcap  picopico.key  vulture.jpg
                                                                                                                                                 
┌──(xrengariox㉿PC)-[~/Clase/webnet1]
└─$ strings vulture.jpg | grep pic
picoCTF{honey.roasted.peanuts}
```

```flag
picoCTF{honey.roasted.peanuts}
```

## Notas adicionales

## Referencias
