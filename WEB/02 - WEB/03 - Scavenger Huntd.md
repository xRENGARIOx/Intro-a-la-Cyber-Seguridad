# Scavenger Huntd

## Descripcion
There is some interesting information hidden around this site [http://mercury.picoctf.net:55079/](http://mercury.picoctf.net:55079/). Can you find it?
## Solucion
Vamos al link que nos proporciona la descripcion, despues vemos el codigo fuente y vemos la primera parte de la flag:
```html
|<!doctype html>|
||<html>|
||<head>|
||<title>Scavenger Hunt</title>|
||<link href="[https://fonts.googleapis.com/css?family=Open+Sans\|Roboto](https://fonts.googleapis.com/css?family=Open+Sans\|Roboto)" rel="stylesheet">|
||<link rel="stylesheet" type="text/css" href="[mycss.css](http://mercury.picoctf.net:55079/mycss.css)">|
||<script type="application/javascript" src="[myjs.js](http://mercury.picoctf.net:55079/myjs.js)"></script>|
||</head>|
|||
||<body>|
||<div class="container">|
||<header>|
||<h1>Just some boring HTML</h1>|
||</header>|
|||
||<button class="tablink" onclick="openTab('tabintro', this, '#222')" id="defaultOpen">How</button>|
||<button class="tablink" onclick="openTab('tababout', this, '#222')">What</button>|
|||
||<div id="tabintro" class="tabcontent">|
||<h3>How</h3>|
||<p>How do you like my website?</p>|
||</div>|
|||
||<div id="tababout" class="tabcontent">|
||<h3>What</h3>|
||<p>I used these to make this site: <br/>|
||HTML <br/>|
||CSS <br/>|
||JS (JavaScript)|
||</p>|
||<!-- Here's the first part of the flag: picoCTF{t -->|
||</div>|
|||
||</div>|
|||
||</body>|
||</html>|
||
```

Seguimos buscando entre los archivos de la pagina y encontramos la segunda parte en el CSS:
```css
div.container {
    width: 100%;
}

header {
    background-color: black;
    padding: 1em;
    color: white;
    clear: left;
    text-align: center;
}

body {
    font-family: Roboto;
}

h1 {
    color: white;
}

p {
    font-family: "Open Sans";
}

.tablink {
    background-color: #555;
    color: white;
    float: left;
    border: none;
    outline: none;
    cursor: pointer;
    padding: 14px 16px;
    font-size: 17px;
    width: 50%;
}

.tablink:hover {
    background-color: #777;
}

.tabcontent {
    color: #111;
    display: none;
    padding: 50px;
    text-align: center;
}

#tabintro { background-color: #ccc; }
#tababout { background-color: #ccc; }

/* CSS makes the page look nice, and yes, it also has part of the flag. Here's part 2: h4ts_4_l0 */
```

Ahora vamos al JS y vemos que nos da una pista de donde buscar la parte 3:
```js
function openTab(tabName,elmnt,color) {
    var i, tabcontent, tablinks;
    tabcontent = document.getElementsByClassName("tabcontent");
    for (i = 0; i < tabcontent.length; i++) {
	tabcontent[i].style.display = "none";
    }
    tablinks = document.getElementsByClassName("tablink");
    for (i = 0; i < tablinks.length; i++) {
	tablinks[i].style.backgroundColor = "";
    }
    document.getElementById(tabName).style.display = "block";
    if(elmnt.style != null) {
	elmnt.style.backgroundColor = color;
    }
}

window.onload = function() {
    openTab('tabintro', this, '#222');
}

/* How can I keep Google from indexing my website? */
```

Vemos los robots.txt:
```robots
User-agent: *
Disallow: /index.html
# Part 3: t_0f_pl4c
# I think this is an apache server... can you Access the next flag?
```

Ahora vemos que nos dice algo sobre apache y Access, buscando un poco, encontramos un archivo llamado `.htaccess` asi que vamos a ver si podemos verlo:

```
 Part 4: 3s_2_lO0k
# I love making websites on my Mac, I can Store a lot of information there.
```

Buscando un poco, cada que se almacenan archivo en MAC, se generan algunos archivos como: `.DS_Store`  Que se genera en cada carpeta y almacena información sobre la disposición de los iconos, el tamaño de la ventana, el orden de los archivos, etc.
Entonces vamos y lo buscamos:
```
Congrats! You completed the scavenger hunt. Part 5: _74cceb07}
```
Y asi obtenemos la ultima parte de la flag:

```flag
picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k_74cceb07}
```

## Notas adicionales

## Referencias

https://axarnet.es/blog/archivo-htaccess#:~:text=relacionados%20con%20.htaccess-,El%20archivo%20.,la%20web%20en%20el%20servidor.


