# Cookie Monster Secret Recipe

## Descripcion
Cookie Monster has hidden his top-secret cookie recipe somewhere on his website. As an aspiring cookie detective, your mission is to uncover this delectable secret. Can you outsmart Cookie Monster and find the hidden recipe?You can access the Cookie Monster [here](http://verbal-sleep.picoctf.net:56241/) and good luck
## Solucion
Vamos al sitio con el link que nos da el reto.
Vemos un sitio en el cual podemos hacer loggin y pues vamos a probar con credenciales por defecto como:
```
username: admin
password: admin
```

El sitio nos dice lo siguiente:
```
# Access Denied

Cookie Monster says: 'Me no need password. Me just need cookies!'

Hint: Have you checked your cookies lately?

[Go back](http://verbal-sleep.picoctf.net:56241/)
```

Entonces usamos la extension cookie editor y vemos una cookie:
```
name: secret_recipe
value: cGljb0NURntjMDBrMWVfbTBuc3Rlcl9sMHZlc19jMDBraWVzXzZDMkZCN0YzfQ%3D%3D
```

Eso se ve como un base64, entonces usamos cyberchef:
```
input: cGljb0NURntjMDBrMWVfbTBuc3Rlcl9sMHZlc19jMDBraWVzXzZDMkZCN0YzfQ%3D%3D
recipe: from base64
output: picoCTF{c00k1e_m0nster_l0ves_c00kies_6C2FB7F3}
```

Y pues asi obtenemos la flag:
```flag
picoCTF{c00k1e_m0nster_l0ves_c00kies_6C2FB7F3}
```

## Notas adicionales

## Referencias

https://gchq.github.io/CyberChef/
