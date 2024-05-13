---
layout: post
category: dev
tags: Script Tool Python Linux 
author: RedDev
title : Penguinator, tu mejor amigo en linux
---

## ¿Qué es penguinator?
Penguinator es un asistente orientado a gente cuyo objetivo es empezar en linux, tarea algo complicada al principio.

![image](https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/908c492b-29d3-4769-ba6f-c134eea25a96)

<a href="https://github.com/reycotallo98/penguinator" class="btn btn-github m-2"><span class="icon"></span>Penguinator</a>

## ¿Qué necesito para implementar penguinator?
Penguinator es una herramienta opensource, por lo que unicamente necesitas esto:
- Distribución de Linux
- Descargar la herramienta
- Una API Key de OpenAI

## Implementando la herramienta
Para implementar penguinator unicamente tendremos que hacer estos 3 sencillos pasos:

Descargar la herramienta y descargar la libreria de openai
```bash
git clone https://github.com/reycotallo98/penguinator.git
pip install openai
```
Ahora abriremos el código, ya que tendremos que insertar nuestra ApiKey de [OpenAI](https://platform.openai.com/account/api-keys).
Para ellos haremos:
```bash
nano penguinator.py
```
Sustituiremos #APIKEY por nuestra APIKEY cerraremos guardando los cambios con CTR+X.

## Demo
É voilá, ya tenemos nuestro penguinator totalmente funcional.
### Ahora, ¿qué posibilidades nos brinda?
Penguinator tiene dos objetivos, enseñar y ayudar.

### Cambiando los permisos de un archivo
Tenemos un script en bash llamado script.sh, que no podemos ejecutar ya que no tiene los permisos necesarios:

![image](https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/955efc17-a50f-4f35-9446-7f1967ff9a15)

Entonces abrimos penguinator y se lo contamos:

![image](https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/b74c597f-61da-4c22-ac8e-eb33614e3ebd)

Y nuestro amigo tan servicial como siempre, no solo nos da el comando que debes usar, si no que nos lo ejecuta:

![image](https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/8cef4509-b221-4145-aed6-041d5db22681)

Por lo que sin ni si quiera tener que ejecutarlo:

![image](https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/cc526628-0da8-4aa0-8557-c9c62e4a172f)

### Creando servidor en python
Esto no se queda en modificar un archivo:

![image](https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/bc6139f3-a3fe-4858-8c79-f4ef0a649cf7)

Y....

![image](https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/01d7768d-98fc-402d-91de-2ac9067df0e3)

## Conclusiones
Esta herramienta tiene mucho potencial para gente que este iniciandose, así como en próximas features en profesionales. Ya que me gustaría implementarle un control por voz, lo que lo haría mucho más ágil al uso.

## Consideraciones
- La herramienta trabaja en el directorio en el que se encuentra, por lo que si se quiere operar en otro directorio, se deberá especificar
- El sudo no está activado, y la herramienta no está preparada para ello para evitar fallos fatales en el sistema, aunque te dará el comando, no lo podrá ejecutar por falta de permisos.

