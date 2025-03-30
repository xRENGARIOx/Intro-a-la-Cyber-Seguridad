# WebDecode

## Descripcion
Do you know how to use the web inspector?Start searching [here](http://titan.picoctf.net:57838/) to find the flag
## Solucion
Nos conectamos al reto con el link que nos propocionan y vemos que tenemos 3 botones, home, about y contact, en home y contact realmente no hay nada importante, pero al ver el codigo fuente de about encontramos algo interesante:
```HTML
|   |   |
|---|---|
||<!DOCTYPE html>|
||<html lang="en">|
||<head>|
||<meta charset="utf-8"/>|
||<meta content="IE=edge" http-equiv="X-UA-Compatible"/>|
||<meta content="width=device-width, initial-scale=1.0" name="viewport"/>|
||<link href="[style.css](http://titan.picoctf.net:57838/style.css)" rel="stylesheet"/>|
||<link href="[img/favicon.png](http://titan.picoctf.net:57838/img/favicon.png)" rel="shortcut icon" type="image/x-icon"/>|
||<!-- font (google) -->|
||<link href="[https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,400;0,700;1,400&amp;display=swap](https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,400;0,700;1,400&display=swap)" rel="stylesheet"/>|
||<title>|
||About me|
||</title>|
||</head>|
||<body>|
||<header>|
||<nav>|
||<div class="logo-container">|
||<a href="[index.html](http://titan.picoctf.net:57838/index.html)">|
||<img alt="logo" src="[img/binding_dark.gif](http://titan.picoctf.net:57838/img/binding_dark.gif)"/>|
||</a>|
||</div>|
||<div class="navigation-container">|
||<ul>|
||<li>|
||<a href="[index.html](http://titan.picoctf.net:57838/index.html)">|
||Home|
||</a>|
||</li>|
||<li>|
||<a href="[about.html](http://titan.picoctf.net:57838/about.html)">|
||About|
||</a>|
||</li>|
||<li>|
||<a href="[contact.html](http://titan.picoctf.net:57838/contact.html)">|
||Contact|
||</a>|
||</li>|
||</ul>|
||</div>|
||</nav>|
||</header>|
||<section class="about" notify_true="cGljb0NURnt3ZWJfc3VjYzNzc2Z1bGx5X2QzYzBkZWRfMDdiOTFjNzl9">|
||<h1>|
||Try inspecting the page!! You might find it there|
||</h1>|
||<!-- .about-container -->|
||</section>|
||<!-- .about -->|
||<section class="why">|
||<footer>|
||<div class="bottombar">|
||Copyright © 2023 Your_Name. All rights reserved.|
||</div>|
||</footer>|
||</section>|
||</body>|
||</html>|
```

Vemos lo que parece ser un base64, asi que vamos a usar cyberchef para ver que dice:
```cyberchef
input: cGljb0NURnt3ZWJfc3VjYzNzc2Z1bGx5X2QzYzBkZWRfMDdiOTFjNzl9

recipe: From Base64

output: picoCTF{web_succ3ssfully_d3c0ded_07b91c79}
```

Y asi obtenemos la flag:
```flag
picoCTF{web_succ3ssfully_d3c0ded_07b91c79}
```
## Notas adicionales

## Referencias
