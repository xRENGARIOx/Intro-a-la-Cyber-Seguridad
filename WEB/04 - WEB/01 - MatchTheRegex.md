# MatchTheRegex

## Descripcion
How about trying to match a regular expressionThe website is running [here](http://saturn.picoctf.net:63070/).
## Solucion
Accedemos al sitio, es un buscador que no nos dice gran cosa.
Vemos el codigo fuente y vemos una funcion de js:

```js
function send_request() {
	let val = document.getElementById("name").value;
	// ^p.....F!?|
	fetch(`/flag?input=${val}`)
		.then(res => res.text())
		.then(res => {
			const res_json = JSON.parse(res);
			alert(res_json.flag)
			return false;
		})
	return false;
}
```

Vemos un comentario sospechoso que parece tener el formato `picoCTF`, probamos a ingresarlo en el buscador y efectivamente era eso

```flag
picoCTF{succ3ssfully_matchtheregex_8ad436ed}
```

## Notas adicionales

## Referencias
