# MacroHard WeakEdge

## Descripcion
I've hidden a flag in this file. Can you find it? [Forensics is fun.pptm](https://mercury.picoctf.net/static/2e739f9e0dc9f4c1556ea6b033c3ec8e/Forensics%20is%20fun.pptm)
## Solucion
Descargamos el archivo que nos da el reto:
```sh
┌──(xrengariox㉿PC)-[~/Clase/macro]
└─$ wget https://mercury.picoctf.net/static/2e739f9e0dc9f4c1556ea6b033c3ec8e/Forensics%20is%20fun.pptm
--2025-05-05 13:06:54--  https://mercury.picoctf.net/static/2e739f9e0dc9f4c1556ea6b033c3ec8e/Forensics%20is%20fun.pptm
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 100093 (98K) [application/octet-stream]
Saving to: ‘Forensics is fun.pptm’

Forensics is fun.pptm                100%[===================================================================>]  97.75K   333KB/s    in 0.3s    

2025-05-05 13:07:03 (333 KB/s) - ‘Forensics is fun.pptm’ saved [100093/100093]
```

Vemos que tipo de archivo es:
```sh
┌──(xrengariox㉿PC)-[~/Clase/macro]
└─$ file Forensics\ is\ fun.pptm 
Forensics is fun.pptm: Microsoft PowerPoint 2007+
```

Lo descomprimimos:
```
┌──(xrengariox㉿PC)-[~/Clase/macro]
└─$ unzip Forensics\ is\ fun.pptm 
Archive:  Forensics is fun.pptm
  inflating: [Content_Types].xml     
  inflating: _rels/.rels             
  inflating: ppt/presentation.xml    
  inflating: ppt/slides/_rels/slide46.xml.rels  
  inflating: ppt/slides/slide1.xml   
  inflating: ppt/slides/slide2.xml   
  inflating: ppt/slides/slide3.xml   
  inflating: ppt/slides/slide4.xml   
  inflating: ppt/slides/slide5.xml   
  inflating: ppt/slides/slide6.xml   
  inflating: ppt/slides/slide7.xml   
  inflating: ppt/slides/slide8.xml   
  inflating: ppt/slides/slide9.xml   
  inflating: ppt/slides/slide10.xml  
  inflating: ppt/slides/slide11.xml  
  inflating: ppt/slides/slide12.xml  
  inflating: ppt/slides/slide13.xml  
  inflating: ppt/slides/slide14.xml  
  inflating: ppt/slides/slide15.xml  
  inflating: ppt/slides/slide16.xml  
  inflating: ppt/slides/slide17.xml  
  inflating: ppt/slides/slide18.xml  
  inflating: ppt/slides/slide19.xml  
  inflating: ppt/slides/slide20.xml  
  inflating: ppt/slides/slide21.xml  
  inflating: ppt/slides/slide22.xml  
  inflating: ppt/slides/slide23.xml  
  inflating: ppt/slides/slide24.xml  
  inflating: ppt/slides/slide25.xml  
  inflating: ppt/slides/slide26.xml  
  inflating: ppt/slides/slide27.xml  
  inflating: ppt/slides/slide28.xml  
  inflating: ppt/slides/slide29.xml  
  inflating: ppt/slides/slide30.xml  
  inflating: ppt/slides/slide31.xml  
  inflating: ppt/slides/slide32.xml  
  inflating: ppt/slides/slide33.xml  
  inflating: ppt/slides/slide34.xml  
  inflating: ppt/slides/slide35.xml  
  inflating: ppt/slides/slide36.xml  
  inflating: ppt/slides/slide37.xml  
  inflating: ppt/slides/slide38.xml  
  inflating: ppt/slides/slide39.xml  
  inflating: ppt/slides/slide40.xml  
  inflating: ppt/slides/slide41.xml  
  inflating: ppt/slides/slide42.xml  
  inflating: ppt/slides/slide43.xml  
  inflating: ppt/slides/slide44.xml  
  inflating: ppt/slides/slide45.xml  
  inflating: ppt/slides/slide46.xml  
  inflating: ppt/slides/slide47.xml  
  inflating: ppt/slides/slide48.xml  
  inflating: ppt/slides/slide49.xml  
  inflating: ppt/slides/slide50.xml  
  inflating: ppt/slides/slide51.xml  
  inflating: ppt/slides/slide52.xml  
  inflating: ppt/slides/slide53.xml  
  inflating: ppt/slides/slide54.xml  
  inflating: ppt/slides/slide55.xml  
  inflating: ppt/slides/slide56.xml  
  inflating: ppt/slides/slide57.xml  
  inflating: ppt/slides/slide58.xml  
  inflating: ppt/slides/_rels/slide47.xml.rels  
  inflating: ppt/slides/_rels/slide48.xml.rels  
  inflating: ppt/slides/_rels/slide49.xml.rels  
  inflating: ppt/slides/_rels/slide50.xml.rels  
  inflating: ppt/slides/_rels/slide32.xml.rels  
  inflating: ppt/slides/_rels/slide52.xml.rels  
  inflating: ppt/slides/_rels/slide53.xml.rels  
  inflating: ppt/slides/_rels/slide54.xml.rels  
  inflating: ppt/slides/_rels/slide55.xml.rels  
  inflating: ppt/slides/_rels/slide56.xml.rels  
  inflating: ppt/slides/_rels/slide57.xml.rels  
  inflating: ppt/slides/_rels/slide58.xml.rels  
  inflating: ppt/slides/_rels/slide51.xml.rels  
  inflating: ppt/slides/_rels/slide13.xml.rels  
  inflating: ppt/_rels/presentation.xml.rels  
  inflating: ppt/slides/_rels/slide1.xml.rels  
  inflating: ppt/slides/_rels/slide2.xml.rels  
  inflating: ppt/slides/_rels/slide3.xml.rels  
  inflating: ppt/slides/_rels/slide4.xml.rels  
  inflating: ppt/slides/_rels/slide5.xml.rels  
  inflating: ppt/slides/_rels/slide6.xml.rels  
  inflating: ppt/slides/_rels/slide7.xml.rels  
  inflating: ppt/slides/_rels/slide8.xml.rels  
  inflating: ppt/slides/_rels/slide9.xml.rels  
  inflating: ppt/slides/_rels/slide10.xml.rels  
  inflating: ppt/slides/_rels/slide11.xml.rels  
  inflating: ppt/slides/_rels/slide12.xml.rels  
  inflating: ppt/slides/_rels/slide14.xml.rels  
  inflating: ppt/slides/_rels/slide15.xml.rels  
  inflating: ppt/slides/_rels/slide16.xml.rels  
  inflating: ppt/slides/_rels/slide17.xml.rels  
  inflating: ppt/slides/_rels/slide18.xml.rels  
  inflating: ppt/slides/_rels/slide19.xml.rels  
  inflating: ppt/slides/_rels/slide20.xml.rels  
  inflating: ppt/slides/_rels/slide21.xml.rels  
  inflating: ppt/slides/_rels/slide22.xml.rels  
  inflating: ppt/slides/_rels/slide23.xml.rels  
  inflating: ppt/slides/_rels/slide24.xml.rels  
  inflating: ppt/slides/_rels/slide25.xml.rels  
  inflating: ppt/slides/_rels/slide26.xml.rels  
  inflating: ppt/slides/_rels/slide27.xml.rels  
  inflating: ppt/slides/_rels/slide28.xml.rels  
  inflating: ppt/slides/_rels/slide29.xml.rels  
  inflating: ppt/slides/_rels/slide30.xml.rels  
  inflating: ppt/slides/_rels/slide31.xml.rels  
  inflating: ppt/slides/_rels/slide33.xml.rels  
  inflating: ppt/slides/_rels/slide34.xml.rels  
  inflating: ppt/slides/_rels/slide35.xml.rels  
  inflating: ppt/slides/_rels/slide36.xml.rels  
  inflating: ppt/slides/_rels/slide37.xml.rels  
  inflating: ppt/slides/_rels/slide38.xml.rels  
  inflating: ppt/slides/_rels/slide39.xml.rels  
  inflating: ppt/slides/_rels/slide40.xml.rels  
  inflating: ppt/slides/_rels/slide41.xml.rels  
  inflating: ppt/slides/_rels/slide42.xml.rels  
  inflating: ppt/slides/_rels/slide43.xml.rels  
  inflating: ppt/slides/_rels/slide44.xml.rels  
  inflating: ppt/slides/_rels/slide45.xml.rels  
  inflating: ppt/slideMasters/slideMaster1.xml  
  inflating: ppt/slideLayouts/slideLayout1.xml  
  inflating: ppt/slideLayouts/slideLayout2.xml  
  inflating: ppt/slideLayouts/slideLayout3.xml  
  inflating: ppt/slideLayouts/slideLayout4.xml  
  inflating: ppt/slideLayouts/slideLayout5.xml  
  inflating: ppt/slideLayouts/slideLayout6.xml  
  inflating: ppt/slideLayouts/slideLayout7.xml  
  inflating: ppt/slideLayouts/slideLayout8.xml  
  inflating: ppt/slideLayouts/slideLayout9.xml  
  inflating: ppt/slideLayouts/slideLayout10.xml  
  inflating: ppt/slideLayouts/slideLayout11.xml  
  inflating: ppt/slideMasters/_rels/slideMaster1.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout1.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout2.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout3.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout4.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout5.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout6.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout7.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout8.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout9.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout10.xml.rels  
  inflating: ppt/slideLayouts/_rels/slideLayout11.xml.rels  
  inflating: ppt/theme/theme1.xml    
 extracting: docProps/thumbnail.jpeg  
  inflating: ppt/vbaProject.bin      
  inflating: ppt/presProps.xml       
  inflating: ppt/viewProps.xml       
  inflating: ppt/tableStyles.xml     
  inflating: docProps/core.xml       
  inflating: docProps/app.xml        
  inflating: ppt/slideMasters/hidden  

┌──(xrengariox㉿PC)-[~/Clase/macro]
└─$ cd ppt/slideMasters/  

┌──(xrengariox㉿PC)-[~/Clase/macro/ppt/slideMasters]
└─$ cat hidden                                           
───────┬─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
       │ File: hidden
───────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
   1   │ Z m x h Z z o g c G l j b 0 N U R n t E M W R f d V 9 r b j B 3 X 3 B w d H N f c l 9 6 M X A 1 f Q
───────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
```

Y vemos que en hidden se ve sospechoso, por lo cual vamos a tratar de ver si es algo:
```sh
┌──(xrengariox㉿PC)-[~/Clase/macro/ppt/slideMasters]
└─$ cato hidden | tr -d ' ' 
ZmxhZzogcGljb0NURntEMWRfdV9rbjB3X3BwdHNfcl96MXA1fQ 
```

Y parece base64 por lo cual vamos a ver el contenido:
```sh
┌──(xrengariox㉿PC)-[~/Clase/macro/ppt/slideMasters]
└─$ cato hidden | tr -d ' ' | base64 -d
flag: picoCTF{D1d_u_kn0w_ppts_r_z1p5} 
```

```flag
picoCTF{D1d_u_kn0w_ppts_r_z1p5}
```

## Notas adicionales

## Referencias
