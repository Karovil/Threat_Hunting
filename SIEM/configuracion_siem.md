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

### ⚙️ Pasos para la configuración

#### 📥 Instalación del servidor Wazuh

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
bash ./wazuh-install.sh -a
```

---

#### 📦 Instalación de agentes en los endpoints

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-agent.sh
sudo bash ./wazuh-agent.sh -m <IP_DEL_MANAGER>
```
#### 🔧 Configuración de reglas personalizadas
Edita el archivo:
```bash
/var/ossec/etc/rules/local_rules.xml
```
#### 🧠 Integraciones recomendadas
MITRE ATT&CK para clasificación de amenazas.

Alertas por correo.

Dashboards personalizados en Kibana.

#### 📊 Visualización
Accede a: http://localhost:5601 para dashboards en Kibana.

💲 SIEM Comercial: Splunk Enterprise Security
🔍 ¿Qué es Splunk ES?
Splunk ES es una solución comercial avanzada para:

Correlación de eventos.

Recolección de datos desde cualquier fuente.

Detección con machine learning.

Integración con SOAR (automatización de respuesta).

🧱 Componentes principales
Splunk Core: Recolecta, indexa y busca datos.

Forwarders: Envían logs desde los endpoints.

App ES: Módulo de seguridad (SIEM) sobre Splunk.

Dashboards y reportes personalizados.

⚙️ Pasos para la configuración
📥 Instalación del core Splunk
Descargar desde: https://www.splunk.com/en_us/download

En Linux:

bash
Copiar
Editar
dpkg -i splunk_package.deb
/opt/splunk/bin/splunk start --accept-license
🔐 Acceso web
URL: http://localhost:8000

Usuario por defecto: admin

🔗 Conexión de datos
Navega a: Settings → Data Inputs

Puedes ingresar:

Syslog

Logs de Windows

Logs de nube (AWS, Azure, GCP)

APIs como VirusTotal

📦 Instalar la App Enterprise Security
Desde: https://splunkbase.splunk.com/app/263/

⚠️ Reglas de correlación
Usan SPL (Splunk Processing Language).

Ejemplos:

Inicios de sesión anómalos.

Escaneos internos.

Beaconing a C2.

🆚 Comparativa rápida
Característica	🆓 Wazuh	💲 Splunk Enterprise Security
Licencia	Gratuito	Comercial
Visualización	Kibana (ELK)	Dashboards avanzados
Reglas de correlación	XML / JSON	SPL (lenguaje propio)
Integración con MITRE	✅	✅
Automatización (SOAR)	Limitada	Avanzada (Splunk SOAR / Phantom)
Facilidad de uso	Media	Alta (GUI muy amigable)
Escalabilidad	Alta	Muy alta
Ideal para	PYMEs, educación, labs	Empresas, banca, industria, gobierno
🎯 Conclusión
Wazuh es excelente para entornos con recursos limitados o laboratorios de aprendizaje.

Splunk ofrece potencia, automatización y análisis de amenazas a gran escala.

Ambos pueden ser puntos de partida sólidos para estrategias de detección y respuesta.


