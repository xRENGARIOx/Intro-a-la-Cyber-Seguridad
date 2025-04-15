# WebSockFish

## Descripcion
Can you win in a convincing manner against this chess bot? He won't go easy on you!You can find the challenge [here](http://verbal-sleep.picoctf.net:59467/).

## Solucion
Al ingresar a la página, se presenta un juego de ajedrez en el que compites contra un bot. Al inspeccionar el código fuente, se observan referencias a varios archivos que gestionan la funcionalidad del juego.

Analizando más a fondo el código, descubrimos que se establece una conexión mediante WebSocket, lo cual permite el intercambio de datos en tiempo real. Al desplazarnos por el código, encontramos una sección que se comunica con un servidor y muestra respuestas dentro del chat del juego. Esto nos ayudara a explotarla como vulnerabilidad.

Abrimos la consola del navegador para observar el comportamiento del sistema. Al enviar una jugada de mate, el resultado aparece como “indefinido”, lo mismo ocurre si utilizamos `eval`. Pero, ¿qué sucede si enviamos un número negativo?

Al observar con más atención, notamos que “mate” representa a la computadora (el bot) y “eval” representa al jugador.

Cuando enviamos un valor negativo grande, el sistema nos regresa la bandera:

```r
sendMessage("eval -100000")
```

Y el pescadito nos regresa la bandera:
```flag
picoCTF{c1i3nt_s1d3_w3b_s0ck3t5_e5e75e69}
```
## Notas adicionales

## Referencias
hackadvisermx. (2025, 26 marzo). _PicoCTF 2025 - [ Forensic ] - WebSockFish_ [Vídeo](https://www.youtube.com/watch?v=xqopwb8Iv90)
