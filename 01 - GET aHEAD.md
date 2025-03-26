# GET aHEAD

## Descripcion
Find the flag being held on this server to get ahead of the competition [http://mercury.picoctf.net:21939/](http://mercury.picoctf.net:21939/)

## Solucion
Nos conectamos al sitio con el link que nos proporciona la descripcion, vemos un sitio web en el que podemos cambiar el color al presionar un boton.
Viendo el codigo fuente podemos ver que lo unico que cambia es el header:
```html
||<!doctype html>|
||<html>|
||<head>|
||<title>Blue</title>|
||<link rel="stylesheet" type="text/css" href="[//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css](http://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css)">|
||<style>body {background-color: blue;}</style>|
||</head>|
||<body>|
||<div class="container">|
||<div class="row">|
||<div class="col-md-6">|
||<div class="panel panel-primary" style="margin-top:50px">|
||<div class="panel-heading">|
||<h3 class="panel-title" style="color:red">Red</h3>|
||</div>|
||<div class="panel-body">|
||<form action="index.php" method="GET">|
||<input type="submit" value="Choose Red"/>|
||</form>|
||</div>|
||</div>|
||</div>|
||<div class="col-md-6">|
||<div class="panel panel-primary" style="margin-top:50px">|
||<div class="panel-heading">|
||<h3 class="panel-title" style="color:blue">Blue</h3>|
||</div>|
||<div class="panel-body">|
||<form action="index.php" method="POST">|
||<input type="submit" value="Choose Blue"/>|
||</form>|
||</div>|
||</div>|
||</div>|
||</div>|
||</div>|
||</body>|
||</html>|
```
```html
|   |
|---|
|<!doctype html>|
||<html>|
||<head>|
||<title>Red</title>|
||<link rel="stylesheet" type="text/css" href="[//maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css](http://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css)">|
||<style>body {background-color: red;}</style>|
||</head>|
||<body>|
||<div class="container">|
||<div class="row">|
||<div class="col-md-6">|
||<div class="panel panel-primary" style="margin-top:50px">|
||<div class="panel-heading">|
||<h3 class="panel-title" style="color:red">Red</h3>|
||</div>|
||<div class="panel-body">|
||<form action="index.php" method="GET">|
||<input type="submit" value="Choose Red"/>|
||</form>|
||</div>|
||</div>|
||</div>|
||<div class="col-md-6">|
||<div class="panel panel-primary" style="margin-top:50px">|
||<div class="panel-heading">|
||<h3 class="panel-title" style="color:blue">Blue</h3>|
||</div>|
||<div class="panel-body">|
||<form action="index.php" method="POST">|
||<input type="submit" value="Choose Blue"/>|
||</form>|
||</div>|
||</div>|
||</div>|
||</div>|
||</div>|
||</body>|
||</html>|
```

En el codigo podemos ver que dependiendo el boton que se presione se envia un GET o un POST, para lo cual vamos a abrir Burpsuite y ver como es que se esta realizando la peticion al presionar el boton.

```
HEAD /index.php HTTP/1.1
Host: mercury.picoctf.net:21939
Content-Length: 0
Cache-Control: max-age=0
Accept-Language: en-US,en;q=0.9
Origin: http://mercury.picoctf.net:21939
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://mercury.picoctf.net:21939/index.php?
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

```
Vemos como se forma la peticion y con ayuda del nombre del reto, probamos a mandarle un HEAD:
```
HTTP/1.1 200 OK
flag: picoCTF{r3j3ct_th3_du4l1ty_6ef27873}
Content-type: text/html; charset=UTF-8
```
Y asi obtenemos la flag:
```flag
picoCTF{r3j3ct_th3_du4l1ty_6ef27873}
```




## Notas adicionales

## Referencias
