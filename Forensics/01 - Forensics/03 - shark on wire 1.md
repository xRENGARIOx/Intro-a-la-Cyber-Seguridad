# shark on wire 1

## Descripcion
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/483e50268fe7e015c49caf51a69063d0/capture.pcap). Recover the flag.
## Solucion
Descargamos el archivo que nos proporciona el reto, y ahora abrimos wireshark para comenzar a analizarlo:
Seleccionamos un paquete UPD y le damos a seguir stream.
Y encontramos que en el Stream 6 se encuentra la bandera:
```flag
picoCTF{StaT31355_636f6e6e}
```

## Notas adicionales

## Referencias
