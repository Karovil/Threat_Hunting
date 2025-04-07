# 🛠️ Punto 3: Herramientas que facilitan la integración

Para que los equipos de **Threat Hunting** y **Respuesta a Incidentes (IR)** trabajen de forma fluida y eficaz, es fundamental contar con herramientas especializadas que permitan **detectar, investigar, contener y automatizar** acciones frente a amenazas. Estas herramientas permiten:

- Recolectar grandes volúmenes de datos.
- Correlacionar eventos dispersos.
- Ejecutar acciones automatizadas o manuales.
- Visualizar patrones de ataque.
- Compartir hallazgos de manera estructurada.

A continuación se detallan las principales herramientas que apoyan esta integración:

---

## 🔍 1. SIEM (Security Information and Event Management)

### ¿Qué hace?
Centraliza, normaliza y analiza logs provenientes de distintos dispositivos (firewalls, servidores, endpoints, aplicaciones, etc.). Detecta comportamientos anómalos mediante correlación de eventos y reglas personalizadas.

### Ejemplos:
- **Splunk**: Plataforma muy flexible, permite dashboards avanzados y consultas personalizadas.
- **ELK Stack (Elasticsearch, Logstash, Kibana)**: Ideal para análisis profundo de logs y visualización en tiempo real.
- **IBM QRadar**: Automatiza análisis de comportamiento y facilita la respuesta integrada.

### ¿Cómo ayuda en la integración?
- Proporciona **visibilidad total del entorno**.
- Permite a los hunters hacer búsquedas y crear alertas.
- Permite al equipo IR recibir esas alertas y ejecutar respuestas en base a playbooks.

---

## 🖥️ 2. EDR (Endpoint Detection and Response)

### ¿Qué hace?
Monitorea continuamente la actividad en los endpoints (PCs, servidores) y permite responder ante eventos sospechosos como ejecución de procesos maliciosos, conexiones externas o cambios en el sistema.

### Ejemplos:
- **CrowdStrike Falcon**: Detecta TTPs en tiempo real y permite aislamiento remoto.
- **Microsoft Defender for Endpoint**: Integrado con el ecosistema Windows, ofrece análisis de comportamiento, reglas personalizadas y respuesta automatizada.

### ¿Cómo ayuda en la integración?
- Los hunters pueden investigar eventos detallados de endpoints.
- El IR puede **aislar equipos, eliminar procesos maliciosos o recolectar artefactos** forenses rápidamente.

---

## 🌐 3. Threat Intelligence Feeds

### ¿Qué hace?
Suministra información actualizada sobre indicadores de compromiso (IOCs) y tácticas utilizadas por actores maliciosos. Se integra en otras plataformas (SIEM, EDR, firewalls, etc.).

### Ejemplos:
- **VirusTotal Intelligence**
- **AlienVault OTX**
- **MISP (Malware Information Sharing Platform)**

### ¿Cómo ayuda en la integración?
- Alimenta el hunting con nuevos IOCs.
- Permite al IR bloquear o detectar amenazas emergentes antes de que afecten a la red.

---

## ⚙️ 4. SOAR (Security Orchestration, Automation and Response)

### ¿Qué hace?
Automatiza flujos de trabajo relacionados con la seguridad. Permite que ante una alerta se ejecuten acciones predefinidas como bloquear una IP, enviar un correo o crear un ticket.

### Ejemplos:
- **Palo Alto Cortex XSOAR**
- **Splunk SOAR**
- **IBM Resilient**

### ¿Cómo ayuda en la integración?
- Conecta hunting e IR mediante flujos automatizados.
- Permite **reducir el tiempo de respuesta** y mantener trazabilidad.

---

## 🧠 5. Marcos de referencia compartidos

### MITRE ATT&CK
- Base de datos de TTPs utilizadas por atacantes.
- Permite a ambos equipos hablar el mismo lenguaje técnico y táctico.

### Cyber Kill Chain (Lockheed Martin)
- Modelo que describe las etapas de un ataque.
- Ayuda a posicionar en qué punto está la amenaza y cómo actuar.

### ¿Cómo ayudan?
- Facilitan la documentación estandarizada.
- Permiten comparar tácticas de adversarios con hallazgos internos.
- Son base para crear hipótesis de hunting y playbooks de respuesta.

---

## ✅ Conclusión

Las herramientas no solo facilitan el trabajo técnico de cada equipo, sino que **actúan como puentes de colaboración entre hunting e IR**, permitiendo:

- Detectar amenazas con mayor precisión.
- Responder rápidamente a incidentes reales.
- Compartir información útil en tiempo real.
- Automatizar tareas repetitivas para enfocarse en lo estratégico.

> 🧠 *Con las herramientas adecuadas, la caza se convierte en defensa, y la respuesta se vuelve más inteligente.*


