---
layout: post
category: blue
tags: Wazuh OpenCTI Tutorial BlueTeam
author: RedDev
title: Integrando Wazuh con OpenCTI
---

 
# Instalación Opencti

Por requisitos de un cliente, nos vimos en un aprieto al tener que integrar Wazuh con OpenCTI, estos sistemas, aun con integraciones ya hechas nos llevó un rato de realizarlas debido a que se pensaron para versiones anteriores, y no había demasiada documentación de como hacerlas.
Por lo que decidimos crear esta pequeña guía de como hacerlo:

## 🧰 Requisitos previos

Asegúrate de tener instalado:

- Docker
    
- Docker Compose
    
- Git
    
- `uuidgen` (para generar el token)
    

### En Ubuntu/Debian:

```bash
sudo apt update && sudo apt install -y docker.io docker-compose git uuid-runtime
```

## 🔧 Paso 1: Clonar y preparar los archivos de OpenCTI

```bash
mkdir -p ~/opencti && cd ~/opencti git clone https://github.com/OpenCTI-Platform/docker.git .
```

Esto descargará todos los archivos necesarios para levantar OpenCTI con Docker.

---

## ⚙️ Paso 2: Configurar el entorno (.env)

Copia el archivo de ejemplo `.env.sample`:

```bash
cp .env.sample .env
```

Ahora edítalo con tu editor favorito (ejemplo con `nano`):

```bash
nano .env
```

Modifica y configura al menos los siguientes valores:

```yaml
OPENCTI_ADMIN_EMAIL=admin@opencti.io (cambiar)
OPENCTI_ADMIN_PASSWORD=changeme (cambiar)
OPENCTI_ADMIN_TOKEN=85e81635-7c9b-4c3f-af85-a4a5d95db188 (generar uno)
OPENCTI_BASE_URL=http://localhost:8080
OPENCTI_HEALTHCHECK_ACCESS_KEY=changeme
MINIO_ROOT_USER=opencti
MINIO_ROOT_PASSWORD=changeme
RABBITMQ_DEFAULT_USER=opencti
RABBITMQ_DEFAULT_PASS=changeme
CONNECTOR_EXPORT_FILE_STIX_ID=dd817c8b-abae-460a-9ebc-97b1551e70e6
CONNECTOR_EXPORT_FILE_CSV_ID=7ba187fb-fde8-4063-92b5-c3da34060dd7
CONNECTOR_EXPORT_FILE_TXT_ID=ca715d9c-bd64-4351-91db-33a8d728a58b
CONNECTOR_IMPORT_FILE_STIX_ID=72327164-0b35-482b-b5d6-a5a3f76b845f
CONNECTOR_IMPORT_DOCUMENT_ID=c3970f8a-ce4b-4497-a381-20b7256f56f0
CONNECTOR_ANALYSIS_ID=4dffd77c-ec11-4abe-bca7-fd997f79fa36
SMTP_HOSTNAME=localhost
ELASTIC_MEMORY_SIZE=4G
```
### Generar token real:

```bash
uuidgen
```

Copia el resultado y pégalo en `OPENCTI_ADMIN_TOKEN`.

También puedes revisar y cambiar otros valores como:

`MINIO_ROOT_USER=minio MINIO_ROOT_PASSWORD=minio123 RABBITMQ_DEFAULT_USER=opencti RABBITMQ_DEFAULT_PASS=opencti`

Guarda y cierra el archivo.

---

## 🛠️ Paso 3: Levantar la plataforma

Ejecuta:

```bash
docker-compose up -d
```

Esto descargará e iniciará todos los servicios: OpenCTI, ElasticSearch, Redis, MinIO, RabbitMQ, etc.

### Verifica los contenedores:

```bash
docker-compose ps
```

Deberías ver varios servicios corriendo (`opencti`, `minio`, `elasticsearch`, etc.).

---

## 🌐 Paso 4: Acceder a OpenCTI

Abre en el navegador:

👉 [http://localhost:8080](http://localhost:8080)

Usa los valores que configuraste en `.env`:

- **Email**: `admin@tuempresa.com`
    
- **Password**: `AdminPasswordFuerte123`

# Conector Threatfox

## 🧾 PASO 1: Crear un usuario conector en OpenCTI

1. Accede a la interfaz web de OpenCTI:  
    👉 `http://localhost:8080`
    
2. Ve a:  
    `Settings → Security → Users → +`
    
3. Rellena:
    
    - **Name**: `[C] ThreatFox`
        
    - **Login email**: `threatfox@connector.local`
        
    - **Role**: `Connector`
        
    - **Group**: selecciona `Connectors`
        
    - Guarda y **copia el token que se genera**.
        

📌 **Ese token lo usaremos en la configuración del conector.**

---

## 🧾 PASO 2: Crear o editar `docker-compose.override.yml`

Esto permite agregar el conector ThreatFox a tu entorno Docker sin tocar el `docker-compose.yml` base.

### 1. Entra a la carpeta donde está tu OpenCTI:

```bash
cd /root/opencti
```
### 2. Abre (o crea) el archivo:

```bash
nano docker-compose.override.yml
```
### 3. Agrega este bloque (ajusta el TOKEN):

```yaml
version: '3'
services:
  connector-threatfox:
    image: opencti/connector-threatfox:6.7.3
    environment:
      - OPENCTI_URL=http://opencti:8080
      - OPENCTI_TOKEN=TU_TOKEN_DE_CONNECTOR
      - CONNECTOR_ID=threatfox-connector
      - CONNECTOR_NAME=ThreatFox
      - CONNECTOR_SCOPE=threatfox
      - CONNECTOR_TYPE=EXTERNAL_IMPORT
      - CONNECTOR_CONFIDENCE_LEVEL=70
      - CONNECTOR_UPDATE_EXISTING_DATA=true
      - CONNECTOR_LOG_LEVEL=info
      - THREATFOX_INTERVAL=3600
      - THREATFOX_TLP=White
      - THREATFOX_CREATE_INDICATORS=true
    restart: always
```

>⚠️ Cambia `TU_TOKEN_DE_CONNECTOR` por el que copiaste al crear el usuario `[C] ThreatFox`.

---

## 🧾 PASO 3: Levantar el conector

Después de guardar el archivo (`Ctrl + O`, luego `Enter`, luego `Ctrl + X` en `nano`), ejecuta:

```bash
docker-compose up -d connector-threatfox
```

Verifica que el conector esté funcionando:

```bash
docker-compose logs -f connector-threatfox
```

---

## 🧾 PASO 4: Verificar en la interfaz de OpenCTI

1. Ve a `Data → Ingestion → Connectors`
    
2. Deberías ver **"ThreatFox"** como conector activo.
    
3. Luego ve a `Knowledge → Indicators` o `Threats` para ver los IOCs que se han importado (IPs, hashes, dominios, etc.) 

# Instalar sysmon en el dispositivo monitorizado

## 🧾PASO 1: Descargar archivo configuración
- Sysmon requiere de un archivo XML con el que configurarse para la depuración de logs, para esto hemos visto que el mas completo a la hora de monitorizar es: 
- Guardamos el archivo de configuración como sysmonconfig.xml
	https://github.com/olafhartong/sysmon-modular/blob/master/sysmonconfig.xml
## 🧾 PASO 2: Descargar sysmon
- Windows
	- Para sistemas windows utilizaremos este enlace:
	  https://learn.microsoft.com/es-es/sysinternals/downloads/sysmon

## 🧾PASO 3: Configurar sysmon
A continuación con un Powershell/Consola como usuario administrador usaremos el siguiente comando:

Windows:
```powershell
Sysmon64.exe -accepteula -i sysmonconfig.xml
```

Linux:
```bash
sudo sysmon -accepteula -i sysmonconfig.xml
```

# Configuración Agente

## Windows
- Abrimos una powershell con permisos de administración y escribimos:
  ```powershell
notepad.exe "C:\Program Files (x86)\ossec-agent\ossec.conf"
```
- Añadimos lo siguiente a nuestra configuración en la zona donde veamos que hay más "localfile":
```xml
<localfile>
	<location>Microsoft-Windows-Sysmon/Operational</location>
	<log_format>eventchannel</log_format>
</localfile>
```

- Reiniciamos el agente
  ```powershell
net stop WazuhSvc
net start WazuhSvc
```

# Configuración Wazuh

## Configuración

### Wazuh
#### Ossec
En el archivo ossec.conf (/var/ossec/etc/ossec.conf), añadiremos lo siguiente al final del archivo, sustituyendo API_KEY y URL_OPENCTI:

```xml
<ossec_config>
  <integration>
     <name>custom-opencti</name><group>sysmon_event1,sysmon_event3,sysmon_event6,sysmon_event7,sysmon_event_15,sysmon_event_22,syscheck</group>
     <alert_format>json</alert_format>
     <api_key>API_KEY</api_key>
     <hook_url>URL_OPENCTI/graphql</hook_url>
  </integration>
</ossec_config>
```
#### Scripts
Añadimos los archivos descargables en este [repositorio](https://github.com/reycotallo98/Blue-Team-Scripts/tree/main/openCTI-Wazuh) en el directorio de integraciones (/var/ossec/integrations), manteniendo sus nombres, y le damos los permisos necesarios, para hacer este proceso podeis utilizar el siguiente comando:
```bash
git clone https://github.com/reycotallo98/Blue-Team-Scripts.git
mv Blue-Team-Scripts/openCTI-Wazuh/* /var/ossec/integrations/*
rm -rf Blue-Team-Scripts
chmod 755 /var/ossec/integrations/custom-opencti*
```
#### Reglas
Añadir las siguientes reglas a Wazuh:
```xml
<group name="threat_intel,">
 <rule id="100623" level="10">
    <field name="integration">opencti</field>
    <description>OpenCTI</description>
    <group>opencti,</group>
    <options>no_full_log</options>
  </rule>
<rule id="100624" level="5">
    <if_sid>100623</if_sid>
    <field name="opencti.error">\.+</field>
    <description>OpenCTI - Error connecting to API</description>
    <options>no_full_log</options>
    <group>opencti,opencti_error,</group>
  </rule>
<rule id="100625" level="12">
    <if_sid>100623</if_sid>
    <field name="opencti.id">\.+</field>
    <description>OpenCTI - IoC found in Threat Intel - $(opencti.observable_value)</description>
    <options>no_full_log</options>
    <group>opencti,opencti_alert,</group>
  </rule>
</group>
```
#### Reiniciar Wazuh Manager
Por último reiniciamos Wazuh:
```bash
sudo systemctl restart wazuh-manager
```
# Probando la integración
A continuación os mostramos como probar la integración realizando un Ping a uno de los Indicators encontrados en OpenCTI:
<img width="645" height="213" alt="image" src="https://github.com/user-attachments/assets/060f258e-07e1-4d64-9c85-cc02a111c026" />
Y nos mostrará la siguiente alerta en Wazuh:
<img width="1447" height="79" alt="image" src="https://github.com/user-attachments/assets/f264eba1-42dc-4407-9c75-464cfc974a66" />
