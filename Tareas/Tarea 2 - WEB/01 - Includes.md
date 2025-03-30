# Includes

## Descripcion
Can you get the flag?Go to this [website](http://saturn.picoctf.net:50743/) and see what you can discover.
## Solucion
Accedemos al sitio con el link que nos proporciona el reto, y vemos que es un sitio que solo tiene texto, vamos a ver el codigo fuente, y vemos includes, un css y un js.
En el css esta la primera parte de la flag:
```css
body {
  background-color: lightblue;
}

/*  picoCTF{1nclu51v17y_1of2_  */
```
Y en el js la segunda parte de la flag:
```js
  
function greetings()
{
  alert("This code is in a separate file!");
}

//  f7w_2of2_df589022}
```
Y ya tendriamos la flag:
```flag
picoCTF{1nclu51v17y_1of2_f7w_2of2_df589022}
```

## Notas adicionales

## Referencias
