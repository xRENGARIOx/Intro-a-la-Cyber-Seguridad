# picobrowser

## Descripcion
This website can be rendered only by **picobrowser**, go and catch the flag! `https://jupiter.challenges.picoctf.org/problem/28921/` ([link](https://jupiter.challenges.picoctf.org/problem/28921/)) or http://jupiter.challenges.picoctf.org:28921

## Solucion
Vamos al link que nos dieron:
```url
https://jupiter.challenges.picoctf.org/problem/28921/
```

Vemos un sitio en el que debemos de pedir la flag, pero al hacer click, nos dice que no estamos usando picobrowser, entonces con ayuda de burpsuite vamos a ver como se genera la peticion para ver si podemos cambiar esto:
```
GET /problem/28921/flag HTTP/1.1
Host: jupiter.challenges.picoctf.org
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
Referer: https://jupiter.challenges.picoctf.org/problem/28921/
Accept-Encoding: gzip, deflate, br
Priority: u=0, i
Connection: keep-alive
```

Y la respuesta nos da lo siguiente:
```
HTTP/1.1 200 OK
Server: nginx
Date: Mon, 24 Mar 2025 18:57:41 GMT
Content-Type: text/html; charset=utf-8
Connection: keep-alive
Set-Cookie: session=; Expires=Thu, 01-Jan-1970 00:00:00 GMT; Max-Age=0; Path=/
Strict-Transport-Security: max-age=0
Content-Length: 2063

<!DOCTYPE html>
<html lang="en">

<head>
    <title>My New Website</title>

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
                    <li role="presentation" class="active"><a href="#">Home</a>
                    </li>
                    <li role="presentation"><a href="/unimplemented">Sign In</a>
                    </li>
                    <li role="presentation"><a href="/unimplemented">Sign Out</a>
                    </li>
                </ul>
            </nav>
            <h3 class="text-muted">My New Website</h3>
        </div>
         
        <!-- Categories: success (green), info (blue), warning (yellow), danger (red) -->
        
        
        <div class="alert alert-danger alert-dismissible" role="alert" id="myAlert">
          <button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button>
          <!-- <strong>Title</strong> --> You&#39;re not picobrowser!
Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36
            </div>
      
      
      
        <div class="jumbotron">
            <p class="lead"></p>
            <p><a href="/flag" class="btn btn-lg btn-success btn-block"> Flag</a></p>
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

Entonces vemos que esta detectando el navegador que usamos nosotros por lo cual solo cambiamos esto en la peticion:
```
User-Agent: picobrowser
```

Y ya el sitio nos devuelve la bandera:
```flag
picoCTF{p1c0_s3cr3t_ag3nt_84f9c865}
```

## Notas adicionales

## Referencias
