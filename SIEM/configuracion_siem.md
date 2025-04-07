# Configuración de SIEM: Open Source vs Comercial

## 🆓 SIEM Open Source: Wazuh

### 🔍 ¿Qué es Wazuh?

Wazuh es una plataforma de seguridad gratuita basada en OSSEC que permite:

- Recolección y análisis de logs.
- Detección de amenazas.
- Visualización con ELK (ElasticSearch + Kibana).
- Integración con MITRE ATT&CK y automatización básica.

---

### 🧱 Componentes principales

- **Wazuh Manager**: Analiza y centraliza eventos.
- **Agentes**: Se instalan en endpoints para enviar logs.
- **Filebeat**: Transporta datos al stack ELK.
- **Kibana**: Visualización mediante dashboards.

---

## ⚙️ Pasos para la configuración

### 🐧 Guía de instalación del agente Wazuh en Linux

El agente de Wazuh se ejecuta en el host que se desea monitorear y se comunica con el servidor (manager) Wazuh, enviando datos casi en tiempo real a través de un canal **encriptado y autenticado**.

---

### ⚙️ Requisitos

- Acceso como `root` o superusuario.
- Conexión a internet.
- Dirección IP o nombre de host del servidor Wazuh.

---

### 📌 Paso 1: Agregar el repositorio oficial de Wazuh

### Instalar la clave GPG
```bash
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | \
sudo gpg --no-default-keyring --keyring /usr/share/keyrings/wazuh.gpg --import

```
```bash
chmod 644 /usr/share/keyrings/wazuh.gpg
```

### Agregar el repositorio
```bash
echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | \
tee -a /etc/apt/sources.list.d/wazuh.list
```

### Actualizar información del paquete
```bash
apt-get update
```
💡 Para Debian 7, 8 o Ubuntu 14, usa en su lugar:
```bash
apt-get install gnupg apt-transport-https

curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | apt-key add -

echo "deb https://packages.wazuh.com/4.x/apt/ stable main" | \
tee -a /etc/apt/sources.list.d/wazuh.list

apt-get update
```

### 🧩 Paso 2: Instalar el agente de Wazuh

 Reemplaza <IP_DEL_MANAGER> con la IP de tu servidor Wazuh
```bash
WAZUH_MANAGER="<IP_DEL_MANAGER>" apt-get install wazuh-agent
```
También puedes agregar otras variables:
```bash
WAZUH_MANAGER="<IP>"
WAZUH_AGENT_NAME="nombre-agente"
WAZUH_AGENT_GROUP="grupo-agentes"
WAZUH_REGISTRATION_PASSWORD="clave"
```


### ▶️ Paso 3: Habilitar e iniciar el servicio del agente
```bash
systemctl daemon-reload
systemctl enable wazuh-agent
systemctl start wazuh-agent
```
✅ Verificar el estado del agente
```bash
systemctl status wazuh-agent
```
🚫 Deshabilitar actualizaciones automáticas del agente

Opción 1: Comentar el repositorio
```bash
sed -i "s/^deb/#deb/" /etc/apt/sources.list.d/wazuh.list
apt-get update
```
Opción 2: Bloquear el paquete
```bash
echo "wazuh-agent hold" | dpkg --set-selections
```
🛠 Configuración de reglas personalizadas
Edita el archivo:
```bash
sudo nano /var/ossec/etc/rules/local_rules.xml
```
Guarda los cambios y reinicia el agente:
```bash
systemctl restart wazuh-agent
```
🔐 Registro manual del agente (opcional)
Si prefieres registrar el agente manualmente desde el servidor Wazuh:
```bash
/var/ossec/bin/manage_agents
```
Selecciona las opciones:


Agregar un nuevo agente


Establecer nombre y grupo


Extraer clave


En el agente: usar manage_agents para importar la clave


Reiniciar el agente

🧪 Prueba de conectividad
Desde el servidor:
```bash
/var/ossec/bin/agent_control -lc
```
Verifica que el nuevo agente aparezca en la lista.

🧠 Integraciones recomendadas
MITRE ATT&CK para clasificación de amenazas.

Alertas por correo para eventos críticos.

Dashboards personalizados en Kibana para análisis visual centralizado.

📊 Visualización
Accede al dashboard de Kibana desde tu navegador:
```bash
http://localhost:5601
```
Asegúrate de que los servicios de Wazuh y Kibana estén activos.
# 💲 SIEM Comercial: Splunk Enterprise Security (ES)

---

## 🔍 ¿Qué es Splunk ES?

Splunk ES es una solución comercial avanzada para:

- ✅ Correlación de eventos
- ✅ Recolección de datos desde cualquier fuente
- ✅ Detección con machine learning
- ✅ Integración con SOAR (automatización de respuesta)

---

## 🧱 Componentes principales

- **Splunk Core**: Recolecta, indexa y permite búsquedas en los datos.
- **Forwarders**: Envían logs desde los endpoints al servidor Splunk.
- **App ES**: Módulo específico de seguridad (SIEM) sobre la plataforma Splunk.
- **Dashboards y reportes personalizados**: Interfaces visuales interactivas para análisis.

---

## ⚙️ Pasos para la configuración

### 📥 Instalación del core Splunk

Descargar desde el sitio oficial:  
➡️ [https://www.splunk.com/en_us/download](https://www.splunk.com/en_us/download)

En sistemas Linux:

```bash
dpkg -i splunk_package.deb
/opt/splunk/bin/splunk start --accept-license
```
### 🔐 Acceso web

- **URL**: [http://localhost:8000](http://localhost:8000)
- **Usuario por defecto**: `admin`

---

### 🔗 Conexión de datos
Navegar a:

Settings → Data Inputs

Fuentes compatibles:

-Syslog

-Logs de Windows

-Logs de servicios en la nube (AWS, Azure, GCP)

-APIs externas como VirusTotal

### 📦 Instalación de la App Enterprise Security

Descargar desde Splunkbase:  
➡️ [https://splunkbase.splunk.com/app/263/](https://splunkbase.splunk.com/app/263/)

### ⚠️ Reglas de correlación

Splunk utiliza **SPL (Splunk Processing Language)** para crear reglas de detección personalizadas.

**Ejemplos comunes:**

- Detección de inicios de sesión anómalos
- Escaneos de red internos
- Tráfico sospechoso de beaconing hacia servidores C2 (Command & Control)

---

### 🆚 Comparativa rápida

| Característica                 | 🆓 **Wazuh**              | 💲 **Splunk Enterprise Security**  |
|-------------------------------|---------------------------|-------------------------------------|
| **Licencia**                  | Gratuito                  | Comercial                           |
| **Visualización**             | Kibana (ELK)              | Dashboards avanzados                |
| **Reglas de correlación**     | XML / JSON                | SPL (lenguaje propio)               |
| **Integración con MITRE**     | ✅                         | ✅                                  |
| **Automatización (SOAR)**     | Limitada                  | Avanzada (Splunk SOAR / Phantom)    |
| **Facilidad de uso**          | Media                     | Alta (GUI muy amigable)             |
| **Escalabilidad**             | Alta                      | Muy alta                            |
| **Ideal para**                | PYMEs, educación, labs    | Empresas, banca, industria, gobierno|

---

### 🎯 Conclusión

- **Wazuh** es una solución robusta y gratuita, ideal para entornos con recursos limitados, laboratorios, PYMEs o instituciones educativas.
- **Splunk ES** es una plataforma comercial poderosa, ideal para organizaciones grandes que requieren detección avanzada, automatización y análisis profundo de amenazas.
- Hay que tener en cuenta que Slunk tambien cuenta con una prueba gratuita por 60 dias.

Ambos pueden ser puntos de partida sólidos dentro de una **estrategia de ciberseguridad basada en SIEM**.
