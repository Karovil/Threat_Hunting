# Introducción Detallada a los Sistemas SIEM

## ¿Qué es un SIEM?

Un **SIEM (Security Information and Event Management)** es una tecnología que centraliza, analiza y correlaciona eventos de seguridad provenientes de diferentes dispositivos, aplicaciones y servicios de una red para:

- **Monitorear en tiempo real** actividades sospechosas.
- **Detectar amenazas** mediante reglas y algoritmos de correlación.
- **Responder ante incidentes** de forma proactiva.
- **Almacenar logs históricos** para auditoría, cumplimiento y análisis forense.

---

## ¿Cómo funciona un SIEM?

El funcionamiento de un SIEM se puede entender como un **proceso en cadena** que sigue estos pasos:

1. ### 📥 Recolección de Datos
   - Recibe logs desde dispositivos como firewalls, antivirus, sistemas operativos, routers, servidores, aplicaciones web, EDRs, etc.
   - Soporta protocolos como Syslog, agentes instalados, APIs, integraciones nativas.

2. ### 🔄 Normalización
   - Transforma los logs a un formato unificado para que todos los datos, sin importar el origen, puedan ser interpretados de manera homogénea.

3. ### 🧠 Correlación de Eventos
   - Usa reglas lógicas para combinar distintos eventos en un contexto significativo.
   - Ejemplo: 
     - Evento 1: Usuario "admin" intenta iniciar sesión.
     - Evento 2: 5 intentos fallidos en 1 minuto.
     - Evento 3: Login exitoso desde IP extranjera.
     - 👉 Resultado: posible ataque de fuerza bruta con éxito.

4. ### 🚨 Generación de Alertas
   - Si las reglas de correlación detectan una amenaza, se dispara una alerta.
   - Las alertas pueden enviarse por correo, sistemas de tickets o integrarse con SOAR (orquestación automática de respuesta).

5. ### 📊 Visualización
   - Crea dashboards e informes con datos gráficos para facilitar la supervisión.
   - Permite el análisis visual de patrones de seguridad, tendencias, y KPIs.

6. ### 🗃️ Almacenamiento y Auditoría
   - Los logs se archivan con opciones de retención personalizadas (días, meses, años).
   - Sirve para cumplir con normativas, análisis forense y generación de reportes legales.

---

## Componentes Fundamentales de un SIEM

1. **Recolección de Logs**
   - Reúne datos desde firewalls, EDRs, sistemas operativos, servidores web, aplicaciones, etc.
   - Soporta múltiples formatos (syslog, JSON, CSV, etc.).

2. **Normalización de Datos**
   - Convierte todos los registros a un formato común y legible.

3. **Correlación de Eventos**
   - Identifica relaciones entre eventos aparentemente aislados (por ejemplo, muchos intentos fallidos de login + cambio de permisos = posible ataque).

4. **Alertas y Notificaciones**
   - Genera alarmas configurables ante comportamientos anómalos o ataques conocidos.

5. **Almacenamiento y Retención**
   - Guarda información para cumplir normativas (como ISO 27001, HIPAA, etc.) y realizar investigaciones futuras.

6. **Visualización y Reportes**
   - Dashboards interactivos, gráficos y generación de informes automáticos.

---

## ¿Por qué es clave para la ciberseguridad?

Los SIEM permiten:

- Tener **visibilidad total** del entorno de TI.
- Reducir el tiempo de detección y respuesta (**MTTD/MTTR**).
- Cumplir con requisitos legales o regulatorios.
- Fortalecer el trabajo del equipo de **Threat Hunting** y **Blue Team**.

---

## SIEM Gratuitos vs SIEM Comerciales

### 🆓 SIEM Gratuitos / Open Source

| SIEM                 | Características principales                                                   |
|----------------------|--------------------------------------------------------------------------------|
| **Wazuh**            | Basado en OSSEC, detección de amenazas, integraciones con ELK y MITRE ATT&CK. |
| **SIEMonster (Free)**| Dashboard intuitivo, basado en ELK stack.                                     |
| **Apache Metron**    | Integración con Big Data, alto rendimiento para entornos complejos.           |
| **Security Onion**   | Distribución Linux con herramientas integradas para análisis de seguridad.     |
| **ELK Stack (Elastic SIEM)** | Muy personalizable, ideal para análisis y visualización de logs.       |



### 💲 SIEM Comerciales / Pagos

| SIEM               | Características destacadas                                                        |
|--------------------|-----------------------------------------------------------------------------------|
| **Splunk Enterprise Security** | Líder del mercado, interfaz avanzada, uso de machine learning.        |
| **IBM QRadar**      | Muy utilizado en entornos corporativos, correlación avanzada, soporte robusto.  |
| **LogRhythm**       | Foco en automatización y respuesta a incidentes.                                |
| **AlienVault USM**  | Buen equilibrio entre precio y funcionalidades.                                 |
| **Microsoft Sentinel (Azure)** | SIEM nativo en la nube, integración con servicios Microsoft.         |






