# Local Authority

## Descripcion
Can you get the flag?Go to this [website](http://saturn.picoctf.net:65018/) and see what you can discover.
## Solucion
Nos conectamos al sitio con el link que nos proporciona el reto y vemos un formulario, probamos con credenciales como `admin | admin` y vemos que nos dice login failed.
Vamos a burpsuite para ver si ahi podemos obtener mas pistas:
Vemos como se genera la peticion:
```
POST /login.php HTTP/1.1
Host: saturn.picoctf.net:65018
Content-Length: 36
Cache-Control: max-age=0
Accept-Language: en-US,en;q=0.9
Origin: http://saturn.picoctf.net:65018
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://saturn.picoctf.net:65018/
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

username=admin&password=admin&login=
```
Y la respuesta que obtenemos nos da una pista muy importante:
```
HTTP/1.1 200 OK
Server: nginx
Date: Sun, 30 Mar 2025 02:42:47 GMT
Content-Type: text/html; charset=UTF-8
Connection: keep-alive
Vary: Accept-Encoding
Content-Length: 1886

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="style.css">
    <title>Login Page</title>
  </head>
  <body>
    <script src="secure.js"></script>
    
    <p id='msg'></p>
    
    <form hidden action="admin.php" method="post" id="hiddenAdminForm">
      <input type="text" name="hash" required id="adminFormHash">
    </form>
    
    <script type="text/javascript">
      function filter(string) {
        filterPassed = true;
        for (let i =0; i < string.length; i++){
          cc = string.charCodeAt(i);
          
          if ( (cc >= 48 && cc <= 57) ||
               (cc >= 65 && cc <= 90) ||
               (cc >= 97 && cc <= 122) )
          {
            filterPassed = true;     
          }
          else
          {
            return false;
          }
        }
        
        return true;
      }
    
      window.username = "admin";
      window.password = "admin";
      
      usernameFilterPassed = filter(window.username);
      passwordFilterPassed = filter(window.password);
      
      if ( usernameFilterPassed && passwordFilterPassed ) {
      
        loggedIn = checkPassword(window.username, window.password);
        
        if(loggedIn)
        {
          document.getElementById('msg').innerHTML = "Log In Successful";
          document.getElementById('adminFormHash').value = "2196812e91c29df34f5e217cfd639881";
          document.getElementById('hiddenAdminForm').submit();
        }
        else
        {
          document.getElementById('msg').innerHTML = "Log In Failed";
        }
      }
      else {
        document.getElementById('msg').innerHTML = "Illegal character in username or password."
      }
    </script>
    
  </body>
</html>
```
En la cual nos dice como se hace la validacion de los caracteres, pero tambien tenemos un script de js, en el cual, podemos ver cual es el username y password correctos:
```js
function checkPassword(username, password)
{
  if( username === 'admin' && password === 'strongPassword098765' )
  {
    return true;
  }
  else
  {
    return false;
  }
}
```
Entonces probamos a loggearnos con esas credenciales y obtenemos la bandera:
```flag
picoCTF{j5_15_7r4n5p4r3n7_b0c2c9cb}
```
## Notas adicionales

## Referencias
