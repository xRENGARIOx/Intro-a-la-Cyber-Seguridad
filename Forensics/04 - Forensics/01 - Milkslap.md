# Milkslap

## Descripcion
[🥛](http://mercury.picoctf.net:48380/)
## Solucion
Primero, si le damos cliick al emoji, nos lleva a un sitio donde se puede ver una especie de imagen que se reproduce al pasar el mouse sobre ella.
Si vemos el CSS, podemos ver que dice algo sobre una imagen, asi que vamos a probar este endpoint:
```css
/* source: milkslap-milkslap.scss */
body {
  margin: 0;
  padding: 0;
  overflow: hidden; }

a {
  color: inherit; }

.center {
  width: 1080px;
  height: 720px;
  margin: 0 auto; }

#image {
  height: 720px;
  margin-top: 5%;
  margin-bottom: 20px;
  background-image: url(concat_v.png);
  background-position: 0 0; }

#foot {
  margin-bottom: 5px;
  color: #999999; }
  #foot h1 {
    font-family: serif;
    font-weight: normal;
    font-size: 1rem;
    text-align: center; }
```

```
http://mercury.picoctf.net:48380/concat_v.png
```
Vemos que efectivamente es un recurso accesible, asi que vamos a descargarlo y ver que podemos hacer con el:
```sh
┌──(xrengariox㉿PC)-[~/Clase/milk]
└─$ wget http://mercury.picoctf.net:48380/concat_v.png                                                
--2025-05-07 22:34:15--  http://mercury.picoctf.net:48380/concat_v.png
Resolving mercury.picoctf.net (mercury.picoctf.net)... 18.189.209.142
Connecting to mercury.picoctf.net (mercury.picoctf.net)|18.189.209.142|:48380... connected.
HTTP request sent, awaiting response... 200 OK
Length: 18095920 (17M) [image/png]
Saving to: ‘concat_v.png’

concat_v.png                         100%[===================================================================>]  17.26M  10.4MB/s    in 1.7s    

2025-05-07 22:34:17 (10.4 MB/s) - ‘concat_v.png’ saved [18095920/18095920]
```

Hacemos un cheque con diferentes herramientas:
```
┌──(xrengariox㉿PC)-[~/Clase/milk]
└─$ binwalk concat_v.png               

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
41            0x29            Zlib compressed data, default compression
1364499       0x14D213        JBOOT SCH2 kernel header, compression type: none, Entry Point: 0xC911A155, image size: 4113974432 bytes, data CRC: 0x3030F6F0, Data Address: 0xD792122B, rootfs offset: 0xE683325B, rootfs size: 4142915508 bytes, rootfs CRC: 0xE9B020D0, header CRC: 0x5510C4D2, header size: 62453 bytes, cmd line length: 60903 bytes
3210141       0x30FB9D        MySQL ISAM compressed data file Version 2
11738439      0xB31D47        JBOOT STAG header, image id: 6, timestamp 0xD1410605, image size: 2284567946 bytes, image JBOOT checksum: 0x9345, header JBOOT checksum: 0x9211

┌──(xrengariox㉿PC)-[~/Clase/milk]
└─$ exiftool concat_v.png 
ExifTool Version Number         : 13.10
File Name                       : concat_v.png
Directory                       : .
File Size                       : 18 MB
File Modification Date/Time     : 2021:03:15 12:24:47-06:00
File Access Date/Time           : 2025:05:07 22:35:27-06:00
File Inode Change Date/Time     : 2025:05:07 22:34:17-06:00
File Permissions                : -rw-rw-r--
File Type                       : PNG
File Type Extension             : png
MIME Type                       : image/png
Image Width                     : 1280
Image Height                    : 47520
Bit Depth                       : 8
Color Type                      : RGB
Compression                     : Deflate/Inflate
Filter                          : Adaptive
Interlace                       : Noninterlaced
Image Size                      : 1280x47520
Megapixels                      : 60.8


┌──(xrengariox㉿PC)-[~/Clase/milk]
└─$ zsteg concat_v.png            
/var/lib/gems/3.3.0/gems/zpng-0.4.5/lib/zpng/scan_line.rb:369:in `prev_scanline_byte': stack level too deep (SystemStackError)
        from /var/lib/gems/3.3.0/gems/zpng-0.4.5/lib/zpng/scan_line.rb:319:in `block in decoded_bytes'
        from /var/lib/gems/3.3.0/gems/zpng-0.4.5/lib/zpng/scan_line.rb:318:in `upto'
        from /var/lib/gems/3.3.0/gems/zpng-0.4.5/lib/zpng/scan_line.rb:318:in `decoded_bytes'
        from /var/lib/gems/3.3.0/gems/zpng-0.4.5/lib/zpng/scan_line/mixins.rb:17:in `prev_scanline_byte'
        from /var/lib/gems/3.3.0/gems/zpng-0.4.5/lib/zpng/scan_line.rb:377:in `prev_scanline_byte'
        from /var/lib/gems/3.3.0/gems/zpng-0.4.5/lib/zpng/scan_line.rb:319:in `block in decoded_bytes'
        from /var/lib/gems/3.3.0/gems/zpng-0.4.5/lib/zpng/scan_line.rb:318:in `upto'
        from /var/lib/gems/3.3.0/gems/zpng-0.4.5/lib/zpng/scan_line.rb:318:in `decoded_bytes'
         ... 10225 levels...
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg.rb:26:in `run'
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/bin/zsteg:8:in `<top (required)>'
        from /usr/local/bin/zsteg:25:in `load'
        from /usr/local/bin/zsteg:25:in `<main>'
```

Al intentar correr la stenografia, vemos que dice que la carga es demasiada, entonces vamos a modificar un parametro en `.zshrc` para poder solucionar esto, y tras hacerlo:
```
┌──(xrengariox㉿PC)-[~/Clase/milk]
└─$ zsteg concat_v.png            
imagedata           .. text: "\n\n\n\n\n\n\t\t"
b1,b,lsb,xy         .. text: "picoCTF{imag3_m4n1pul4t10n_sl4p5}\n"
b1,bgr,lsb,xy       .. /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg/checker/wbstego.rb:41:in `to_s': stack level too deep (SystemStackError)
        from /var/lib/gems/3.3.0/gems/iostruct-0.4.0/lib/iostruct.rb:175:in `inspect'
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg/checker/wbstego.rb:41:in `to_s'
        from /var/lib/gems/3.3.0/gems/iostruct-0.4.0/lib/iostruct.rb:175:in `inspect'
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg/checker/wbstego.rb:41:in `to_s'
        from /var/lib/gems/3.3.0/gems/iostruct-0.4.0/lib/iostruct.rb:175:in `inspect'
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg/checker/wbstego.rb:41:in `to_s'
        from /var/lib/gems/3.3.0/gems/iostruct-0.4.0/lib/iostruct.rb:175:in `inspect'
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg/checker/wbstego.rb:41:in `to_s'
         ... 5208346 levels...
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/lib/zsteg.rb:26:in `run'
        from /var/lib/gems/3.3.0/gems/zsteg-0.2.13/bin/zsteg:8:in `<top (required)>'
        from /usr/local/bin/zsteg:25:in `load'
        from /usr/local/bin/zsteg:25:in `<main>'

```

Seguimos obteniendo el error, pero al menos obtuvimos la flag:
```flag
picoCTF{imag3_m4n1pul4t10n_sl4p5}
```

## Notas adicionales

## Referencias

https://github.com/zed-0xff/zsteg/issues/30
https://medium.com/@matus.vaclav1/picoctf-milkslap-a26734fe1b1f


