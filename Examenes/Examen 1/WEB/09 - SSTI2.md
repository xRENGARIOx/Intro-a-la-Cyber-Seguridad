# SSTI2

## Descripcion
I made a cool website where you can announce whatever you want! I read about input sanitization, so now I remove any kind of characters that could be a problem :)I heard templating is a cool and modular way to build web apps! Check out my website [here](http://shape-facility.picoctf.net:56656/)!
## Solucion

SSTI es una **vulnerabilidad web** que ocurre cuando una aplicación **interpreta entradas del usuario como parte de una plantilla de servidor**, sin sanitizarlas adecuadamente.

Esto le permite a un atacante **inyectar código malicioso** en el motor de plantillas para **leer datos, ejecutar comandos o incluso tomar control del servidor**.

Pidiendo ayuda a chat de como debía manejar esto y especificando que buscaba una bandera me devolvió el siguiente `payload`, que se describe paso a paso:

```js
{{ request|attr('application')|attr('\x5f\x5fglobals\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fbuiltins\x5f\x5f')|attr('\x5f\x5fgetitem\x5f\x5f')('\x5f\x5fimport\x5f\x5f')('os')|attr('popen')('cat flag')|attr('read')() }}
```

### 1. `request`

- **Objeto `request`**: se refiere a la solicitud HTTP en frameworks como **Flask**.
- Este objeto está disponible en el entorno de plantillas **Jinja2**.

---

### 2. `|attr('application')`

- **Obtiene el atributo `application`** del objeto `request`.
- En **Flask**, esto devuelve la instancia de la aplicación **WSGI** (`Flask`).
- Esto es crucial porque desde ahí se puede acceder a más atributos globales del entorno.

---

### 3. `|attr('__globals__')`

- **Accede al diccionario de variables globales** dentro del entorno del template.
- Esto normalmente no es accesible directamente, pero aquí se hace gracias al motor de plantillas.

---

### 4. `|attr('__getitem__')('__builtins__')`

- Usa **`__getitem__`** (el método de acceso por índice) para obtener el diccionario `__builtins__`.
- `__builtins__` contiene funciones como `print`, `open`, `eval`, `__import__`, etc.
- Acceder a esto permite al atacante "hackear" el entorno y obtener funciones poderosas.

---

### 5. `|attr('__getitem__')('__import__')('os')`

- Aquí se accede a la función **`__import__`** dentro de `__builtins__`.
- Luego se llama `__import__('os')`, que **importa el módulo `os`** de Python
- Ya se tiene acceso al **sistema operativo** desde el template.

---

### 6. `|attr('popen')('cat flag')`

- Usa `os.popen('cat flag')`: abre un subproceso y ejecuta el comando **`cat flag`**.
- Este comando **lee el contenido del archivo `flag`** (muy común en retos CTF).
- `popen` permite ejecutar comandos del sistema operativo.

---

### 7. `|attr('read')()`

- Finalmente se llama `.read()` sobre el resultado del **`popen()`**.
- Esto **lee el contenido devuelto por el comando `cat flag`**.

Al pegarlo en la pagina donde nos dirigía, nos muestra la bandera:
```
picoCTF{sst1_f1lt3r_byp4ss_eb2a60e7}
```
## Notas adicionales
Basicamente es SSTI1, pero encodeado.
## Referencias
