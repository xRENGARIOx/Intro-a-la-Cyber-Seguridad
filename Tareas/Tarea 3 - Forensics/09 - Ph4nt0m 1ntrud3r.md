#  Ph4nt0m 1ntrud3r

## Descripcion
A digital ghost has breached my defenses, and my sensitive data has been stolen! 😱💻 Your mission is to uncover how this phantom intruder infiltrated my system and retrieve the hidden flag.To solve this challenge, you'll need to analyze the provided PCAP file and track down the attack method. The attacker has cleverly concealed his moves in well timely manner. Dive into the network traffic, apply the right filters and show off your forensic prowess and unmask the digital intruder!Find the PCAP file here [Network Traffic PCAP file](https://challenge-files.picoctf.net/c_verbal_sleep/a917f567b9cc0f1a730a7801b309955df4d2234a8114326857b9759e9e5d0453/myNetworkTraffic.pcap) and try to get the flag.
## Solucion
Descargamos el archivo que nos proporciona el reto y abrimos wireshark para analizarlo:
```sh
┌──(xrengariox㉿PC)-[~/Clase/phantom]
└─$ wget https://challenge-files.picoctf.net/c_verbal_sleep/a917f567b9cc0f1a730a7801b309955df4d2234a8114326857b9759e9e5d0453/myNetworkTraffic.pcap
--2025-05-11 20:11:13--  https://challenge-files.picoctf.net/c_verbal_sleep/a917f567b9cc0f1a730a7801b309955df4d2234a8114326857b9759e9e5d0453/myNetworkTraffic.pcap
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 65.9.149.95, 65.9.149.85, 65.9.149.24, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|65.9.149.95|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1452 (1.4K) [application/octet-stream]
Saving to: ‘myNetworkTraffic.pcap’

myNetworkTraffic.pcap                100%[===================================================================>]   1.42K  --.-KB/s    in 0s      

2025-05-11 20:11:14 (26.5 MB/s) - ‘myNetworkTraffic.pcap’ saved [1452/1452]

┌──(xrengariox㉿PC)-[~/Clase/phantom]
└─$ wireshark myNetworkTraffic.pcap  
```

Podemos ver 22 paquetes que parecen tener contenido en base64 asi que vamos a tranformar cada uno:
```sh
┌──(xrengariox㉿PC)-[~/Clase/phantom]
└─$ echo "ezF0X3c0cw==" | base64 -d            
{1t_w4s

┌──(xrengariox㉿PC)-[~/Clase/phantom]
└─$ echo "cGljb0NURg==" | base64 -d                                              
picoCTF

┌──(xrengariox㉿PC)-[~/Clase/phantom]
└─$ echo "bnRfdGg0dA==" | base64 -d
nt_th4t

┌──(xrengariox㉿PC)-[~/Clase/phantom]
└─$ echo "YmhfNHJfOQ==" | base64 -d
bh_4r_9

┌──(xrengariox㉿PC)-[~/Clase/phantom]
└─$ echo "fQ==" | base64 -d
} 

┌──(xrengariox㉿PC)-[~/Clase/phantom]
└─$ echo "XzM0c3lfdA==" | base64 -d
_34sy_t

┌──(xrengariox㉿PC)-[~/Clase/phantom]
└─$ echo "NTlmNTBkMw==" | base64 -d
59f50d3  
```

Entonces ahora solo tenemos que formar la flag ordenandolos:
```flag
picoCTF{1t_w4snt_th4t_34sy_tbh_4r_959f50d3}
```

## Notas adicionales

## Referencias
