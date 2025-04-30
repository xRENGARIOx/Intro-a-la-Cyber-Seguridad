# m00nwalk

## Descripcion
Decode this [message](https://jupiter.challenges.picoctf.org/static/14393e18d98fedbaedbc28896d7ef31a/message.wav) from the moon.
## Solucion
Primero descargamos el archivo que nos proporciona el reto:
```sh
┌──(xrengariox㉿PC)-[~/Clase/moon]
└─$ wget https://jupiter.challenges.picoctf.org/static/14393e18d98fedbaedbc28896d7ef31a/message.wav                                        
--2025-04-28 12:08:04--  https://jupiter.challenges.picoctf.org/static/14393e18d98fedbaedbc28896d7ef31a/message.wav
Resolving jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)... 3.131.60.8
Connecting to jupiter.challenges.picoctf.org (jupiter.challenges.picoctf.org)|3.131.60.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 11066998 (11M) [application/octet-stream]
Saving to: ‘message.wav’

message.wav                          100%[===================================================================>]  10.55M   139KB/s    in 74s     

2025-04-28 12:09:27 (145 KB/s) - ‘message.wav’ saved [11066998/11066998]
```

Vemos ante que clase de archivo estamos:
```sh
┌──(xrengariox㉿PC)-[~/Clase/moon]
└─$ file message.wav 
message.wav: RIFF (little-endian) data, WAVE audio, Microsoft PCM, 16 bit, mono 48000 Hz

┌──(xrengariox㉿PC)-[~/Clase/moon]
└─$ open message.wav            
VLC media player 3.0.21 Vetinari (revision 3.0.21-0-gdd8bfdbabe8)
```
Entonces vemos que es un archivo de audio, que al abrirlo reproduce sonidos. Por las pistas, nos damos cuenta que tienen que ver con la trasmision de imagenes por SSTV. Entonces vamos a descargar una herramienta llamada SSTV Decoder:
```sh
┌──(root㉿PC)-[/opt]
└─# git clone https://github.com/colaclanth/sstv.git

Cloning into 'sstv'...
remote: Enumerating objects: 221, done.
remote: Counting objects: 100% (59/59), done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 221 (delta 51), reused 49 (delta 49), pack-reused 162 (from 1)
Receiving objects: 100% (221/221), 1.01 MiB | 84.00 KiB/s, done.
Resolving deltas: 100% (139/139), done.
```

Lo instalamos:
```sh
┌──(root㉿PC)-[/opt/sstv]
└─# python3 setup.py install
```

Y ahora usamos la herramienta con el archivo que teniamos:
```sh
┌──(xrengariox㉿PC)-[~/Clase/moon]
└─$ sstv -d message.wav -o flag              
[sstv] Searching for calibration header... Found!    
[sstv] Detected SSTV mode Scottie 1
[sstv] Decoding image...              [####################################################################################################] 100%
[sstv] Drawing image data...
[sstv] ...Done!
[sstv] Error saving file, saved to result.png instead
```

Y dentro de la imagen viene la flag:
```flag
picoCTF{beep_boop_im_in_space}
```
## Notas adicionales

## Referencias

https://github.com/colaclanth/sstv

