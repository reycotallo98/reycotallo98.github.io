---
layout: post
category: blue
tag: AD
NTLM Relay Attacks: Surfeando el AD
---

## ¿Qué es un NTLM Relay Attack?
Lo primero de todo es conocer NTLM.

### Entonces,¿qué es NTLM?

NTLM(New Technology LAN Manager) es un conjunto de protocolos de autentificación desarrollado por Microsoft, para sustituir al antiguo NTLAN Manager.
Estos protocolos funcionan de esta manera, el servidor nos entrega una cadena numérica, la cual el usuario cifra desde su ordenador con la contraseña que introduce; entonces se envía a el controlador de dominio, el cual tenía previamente la misma cadena numérica cifrada con nuestra contraseña, y tras compararla nos validará como usuario o no.

![image](https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/3f19b484-e51f-4d49-8f21-ded4b8f474f4)


## Ahora sí, así funciona un NTLM Relay attack

Un ataque NTLM Relay, es del tipo MITM( Men in the Middle).
Lo que significa que el atacante se situa entre la comunicación cliente-servidor, sniffando todo el tráfico que pasa por el canal creado. Esto se consigue haciendo que el cliente nos vea como el servidor al que se dirige, y el servidor como su cliente. 
Por lo que cuando el cliente se autentifique, nos enviará la petición a nosotros y nosotros a el servidor, y con las respuestas ocurrirá lo mismo pero en dirección contraria.
De esta manera, enviaremos la cadena numérica al cliente para que nos la cifre y poder enviarsela al servidor, y así consiguir acceso al servicio que utilice estos protocolos de autentificación.
![image](https://github.com/reycotallo98/reycotallo98.github.io/assets/93315382/f80fb8ef-4127-4be7-a0c1-c1735f4f6ea7)

