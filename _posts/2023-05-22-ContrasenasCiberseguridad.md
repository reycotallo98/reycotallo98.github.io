---
layout: post
category: blue
tags: password 2FA 3FA old
author: RedDev
title : Contraseñas, el abuelo de la ciberseguridad 
---

## Contraseñas
Las contraseñas o passwords, han sido durante mucho tiempo el método de identificación en la red por excelencia.
Estas se basan en una combinación de carácteres la cual podiamos inventarnos o se generaban, con la cual nos logeamos en nuestras redes sociales, correos electrónicos, cuentas de pc...

## ¿Qué ocurre con las contraseñas?¿Son seguras?¿Estoy seguro?
Lo primero que debemos saber es de que manera se tratan nuestras contraseñas. 
En una web con distintos usuarios y sus respectivas contraseñas, estas son almacenadas en una base de datos y mayoritariamente encriptadas, con un cifrado más seguro o menos.

¿No os parece raro esto?¿No sería más sencillo tenerlas en texto claro?

Esto se hace con el motivo de que se asume que tarde o temprano estas van a ser filtradas, de hecho hay miles de bases de datos en venta en distintos portales por X cantidad de dinero, a todos nos ha llegado el cada vez más típico correo de "se ha encontrado tu contraseña en un repositorio online, para iniciar sesión, debes restablecerla".
Por eso se cifran.

Puedes comprobar la seguridad de tus cuentas introduciendo tu email aquí -> <a href="https://haveibeenpwned.com/">Have i been pwned?</a>

A los que hasta este punto se sientan seguros, dejadme deciros que no lo estais. Aunque si que es cierto que el cifrado debe romperse mediante ataques de fuerza bruta, cada vez más sofisticados, debemos tener en cuenta que con la llegada de la computación cuantica esto cambiará, aquí os dejo una tabla del tiempo que lleva romper un hash encriptado de una password a dia de hoy.
![image](https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/8c9833ec-4d2c-4b9a-907c-90edfae2e5f4)

Aquí os adjunto una noticia, que hace poco generó terror en EEUU.
<a href="https://www.elconfidencial.com/tecnologia/novaceno/2022-04-25/china-eeuu-computacion-cuantica_3412816/">China afirma que puede romper los hases de cifrado de contraseñas</a>

## Viendo como está el panorama, ¿qué opciones tenemos para protegernos?
La opción más utilizada a día de hoy es la molesta para algunos, o la salvadora de otros, el 2FA(2 factor authentication), este se basa en un segundo control de seguridad además de la contraseña, normalmente un código enviado al número de teléfono o al correo vinculado a la cuenta.
Aún así, esto es insuficiente, ya que es posible captar estos códigos mediante diferentes técnicas, como tener hackeado el correo de la persona, así como directamente bypasear este control.

¿Entonces que hacemos?

Existe un 3FA, utilizado a nivel empresarial sobre todo, en empresas con alta madurez en ciberseguridad. Este se basa en:
- Contraseña
- Objeto personal(móvil, pc...)
- Identificación biométrica

## ¿Qué es la identificación biométrica?
Todos conocemos el famoso Face ID de apple o el login con la huella digital de los smartphones android.
Estas funciones, mejoran significativamente la seguridad e integridad de nuestras cuentas en internet.

Aunque con técnicas, eso si, muy sofisticadas, que requieren material especifico o muchas horas de ejecución como son el deep fake en el caso del Face ID, podrían ser vulneradas estas medidas.

## Reflexión del autor
En mi opinión, los esfuerzos en obligar a la gente a generar contraseñas seguras, que luego son repetidas en varias cuentas o que sea una contraseña del tipo "MigatoSeLlamaAlan1234", no sirven de nada.
Se debe enfocar el futuro de la auteticación hacia opciones biometricas o de diferentes sistemas como Google Authenticator, que realmente verifican la identidad de la persona.
