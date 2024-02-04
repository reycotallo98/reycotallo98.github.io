---
layout: post
category: red
tags: Bluethoot Hacking Flipper Zero 
author: RedDev
title : Hackeando un smartphone con un Flipper Zero
---

En los últimos años, las herramientas de hacking ético han ganado popularidad por su capacidad para simular ataques y probar la fortaleza de los sistemas. Este artículo explora el uso innovador del Flipper Zero como un Rubber Ducky Bluetooth, un concepto que plantea importantes preguntas sobre la seguridad de los smartphones modernos.

## Qué es el Flipper Zero
### Definición y Características
El Flipper Zero es un dispositivo multifunción que actúa como una navaja suiza para los entusiastas de la ciberseguridad. A diferencia de otros dispositivos de hacking, el Flipper Zero es notablemente pequeño y portátil, pero con una amplia gama de funcionalidades. Entre sus capacidades se encuentran la interacción con sistemas de radiofrecuencia, NFC, RFID, y hardware de bajo nivel.

### Impacto en la Comunidad de Seguridad
Desde su lanzamiento, el Flipper Zero ha sido adoptado tanto por profesionales de la seguridad como por aficionados. Su versatilidad, facilidad de uso y la gran comunidad que tiene detrás permite a los usuarios explorar vulnerabilidades en una variedad de sistemas, desde cerraduras inteligentes hasta sistemas de comunicación inalámbrica.

<img src="https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/7d5cf455-0963-40ca-b98c-39bdc1197465" alt="Imagen de un Flipper Zero">


## El concepto de Rubber Ducky
### ¿Qué es un Rubber Ducky?
Un Rubber Ducky es, en esencia, un dispositivo que se hace pasar por un teclado USB. Al ser conectado a una computadora, ejecuta una serie de comandos preprogramados. Su diseño permite realizar ataques de inyección de teclado de manera rápida y discreta, una técnica comúnmente utilizada en pruebas de penetración y auditorías de seguridad, debido a la capacidad mencioanda anteriormente, se pueden introducir instrucciones o realizar acciones dentro del ordenador pudiendo llegar a tomar el control de este.

<img src="https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/6d92afff-f06c-48b5-8d58-29170cd83d99" alt="Imagen rubber ducky proveniente de la página oficial de Hak5">


## Flipper Zero como Rubber Ducky Bluetooth
### Transformación y Funcionalidad
Al integrar capacidades Bluetooth, el Flipper Zero trasciende la funcionalidad de un Rubber Ducky tradicional sumando la posibilidad a este de usarse mediante bluethoot. Puede emparejarse con smartphones y enviar comandos sin necesidad de una conexión física, aprovechando vulnerabilidades en la gestión de dispositivos Bluetooth.

### Implicaciones de Seguridad
Esta capacidad representa un riesgo significativo para los usuarios de smartphones. Un atacante podría, por ejemplo, enviar comandos para abrir mensajes, aplicaciones o incluso realizar transacciones si el dispositivo no está debidamente protegido.

### ¿Cómo se crean estos scripts?
Los scripts de la funcionalidad bad bluethoot se crean mediante una herramienta facilitada port los creadores originales del Rubber Ducky (HAK5) y se llama [Payload Studio](https://payloadstudio.com/community/), aunque podemos encontrar una biblioteca bastante completa de payloads en [Github](https://github.com/hak5/omg-payloads/tree/master)

<img src="https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/66a2fb8b-86b7-408c-ae3e-ae2b821ed310" alt="Brand de Flipper Zero">

## Escenarios de Uso y Riesgos Asociados
### Ejemplos Prácticos
Veamos un ejemplo concreto: Un usuario va paseando por un centro comercial, este encuentra un bluethoot llamado speakers_CentroComercial, y decide conectarse para intentar poner su música en los altavoces, hay que indicar que este tiene un Iphone 13 Pro Max actualizado a la última versión de IOS.

<blockquote class="tiktok-embed" cite="https://www.tiktok.com/@_jorge.rey_/video/7331480397563399457" data-video-id="7331480397563399457" style="max-width: 605px;min-width: 325px;" > <section> <a target="_blank" title="@_jorge.rey_" href="https://www.tiktok.com/@_jorge.rey_?refer=embed">@_jorge.rey_</a> Iphone hackeado con flipper zero!!!<a title="fypシ" target="_blank" href="https://www.tiktok.com/tag/fyp%E3%82%B7?refer=embed">#fypシ</a> <a title="fyp" target="_blank" href="https://www.tiktok.com/tag/fyp?refer=embed">#fyp</a> <a title="fypシ゚viral" target="_blank" href="https://www.tiktok.com/tag/fyp%E3%82%B7%E3%82%9Aviral?refer=embed">#fypシ゚viral</a> <a title="hack" target="_blank" href="https://www.tiktok.com/tag/hack?refer=embed">#hack</a> <a title="hacking" target="_blank" href="https://www.tiktok.com/tag/hacking?refer=embed">#hacking</a> <a title="informatica" target="_blank" href="https://www.tiktok.com/tag/informatica?refer=embed">#informatica</a> <a title="interesting" target="_blank" href="https://www.tiktok.com/tag/interesting?refer=embed">#interesting</a> <a title="iphone" target="_blank" href="https://www.tiktok.com/tag/iphone?refer=embed">#iphone</a> <a title="iphone13promax" target="_blank" href="https://www.tiktok.com/tag/iphone13promax?refer=embed">#iphone13promax</a> <a title="smartphone" target="_blank" href="https://www.tiktok.com/tag/smartphone?refer=embed">#smartphone</a> <a title="android" target="_blank" href="https://www.tiktok.com/tag/android?refer=embed">#android</a> <a title="samsung" target="_blank" href="https://www.tiktok.com/tag/samsung?refer=embed">#samsung</a> <a title="huawei" target="_blank" href="https://www.tiktok.com/tag/huawei?refer=embed">#huawei</a> <a title="flipper" target="_blank" href="https://www.tiktok.com/tag/flipper?refer=embed">#flipper</a> <a title="flipperzero" target="_blank" href="https://www.tiktok.com/tag/flipperzero?refer=embed">#flipperzero</a> <a target="_blank" title="♬ Chill and gentle lo-fi&#47;10 minutes(1455687) - nightbird_bgm" href="https://www.tiktok.com/music/Chill-and-gentle-lo-fi10-minutes-1455687-7247207913034614785?refer=embed">♬ Chill and gentle lo-fi&#47;10 minutes(1455687) - nightbird_bgm</a> </section> </blockquote> <script async src="https://www.tiktok.com/embed.js"></script>

### Reflexiones sobre la Seguridad
Este escenario resalta la importancia de medidas de seguridad como la desactivación de Bluetooth cuando no está en uso y la conciencia sobre los dispositivos cercanos. Además, plantea preguntas sobre cómo los fabricantes de smartphones pueden mejorar la seguridad contra este tipo de ataques.

## Más allá de esta "geek prank"
El Flipper Zero y su capacidad como navaja sueca hacker nos recuerda que la seguridad es un campo en constante evolución. A medida que surgen nuevas herramientas y técnicas, tanto los profesionales de la seguridad como los usuarios deben permanecer vigilantes y educados para protegerse contra amenazas emergentes.
