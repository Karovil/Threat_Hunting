# 🕵️‍♂️ ¿Qué es el Threat Hunting?

El **Threat Hunting** o caza de amenazas es una práctica **proactiva** dentro de la ciberseguridad que busca detectar amenazas que han eludido las defensas tradicionales, como antivirus, firewalls o sistemas de detección de intrusos (IDS).

A diferencia de los métodos **reactivos**, donde se espera a que una alerta indique un problema, el hunting implica buscar activamente **indicadores de compromiso (IoCs)**, así como **tácticas, técnicas y procedimientos (TTPs)** utilizados por actores maliciosos.

---

## 🎯 ¿Para qué se hace Threat Hunting?

En un entorno donde las amenazas evolucionan constantemente, **esperar alertas ya no es suficiente**. El Threat Hunting permite:

- **Anticipar** ataques antes de que generen daño.
- **Descubrir** patrones de comportamiento anómalos.
- **Comprender** cómo piensan y actúan los adversarios.

No se trata solo de encontrar malware, sino de **entender cómo operan los atacantes** y detectar las brechas que aún no han sido explotadas.

---

## 🧠 Tipos de Threat Hunting

### 🔍 Basado en hipótesis
Se formula una suposición basada en inteligencia de amenazas o comportamientos observados.

> Ejemplo: “Sospechamos que un atacante interno está usando técnicas de ‘lateral movement’ a través de RDP”.

### 🧩 Basado en IoCs (Indicadores de Compromiso)
Se buscan elementos concretos como:
- Direcciones IP maliciosas
- Hashes de archivos
- Nombres de dominio relacionados con campañas conocidas

### 🛠️ Basado en TTPs (Tácticas, Técnicas y Procedimientos)
Se enfoca en las **técnicas utilizadas por los atacantes**, apoyándose en marcos como MITRE ATT&CK.

---

## 🧰 Herramientas utilizadas en el Hunting

### 📊 SIEMs (Security Information and Event Management)
- Splunk
- QRadar
- ELK Stack
- EventLog Analyzer

### 🖥️ EDR (Endpoint Detection and Response)
- CrowdStrike
- SentinelOne
- Microsoft Defender for Endpoint

### 🌐 Plataformas de Threat Intelligence
- MISP
- VirusTotal
- AlienVault OTX

---

## 🧱 Frameworks utilizados

- MITRE ATT&CK
- Cyber Kill Chain
- Diamond Model
- DeTT&CT

---

## 🔁 Ciclo del Threat Hunting

1. **Planificación y definición de hipótesis**
2. **Recolección de datos** (logs, tráfico de red, eventos de endpoints)
3. **Análisis de datos** e identificación de patrones anómalos
4. **Validación de la amenaza**
5. **Respuesta y mitigación**
6. **Documentación** y retroalimentación para mejorar defensas

---

## 📚 Requisitos para ser un buen Threat Hunter

- Conocimiento de redes, protocolos y sistemas operativos.
- Comprensión de tácticas de ciberataques.
- Familiaridad con logs (Windows Event Logs, syslog, etc.).
- Capacidad de análisis y pensamiento crítico.
-Conocimiento de scripting (Python, PowerShell, Bash) para automatizar búsquedas.
