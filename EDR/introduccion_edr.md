# 🖥️ Introducción a los EDR (Endpoint Detection and Response)

---

## ❓ ¿Qué es un EDR?

Un **EDR (Endpoint Detection and Response)** es una solución de ciberseguridad diseñada para **monitorear continuamente los endpoints** (laptops, servidores, estaciones de trabajo) y detectar actividades sospechosas, brindando herramientas para:

- Investigación
- Contención
- Respuesta ante incidentes

El EDR complementa a los antivirus tradicionales con un enfoque **más avanzado y proactivo**, enfrentando amenazas como:

- Malware sin archivos (fileless malware)
- Ataques de día cero (zero-day)
- Movimiento lateral dentro de redes
- Persistencia y evasión avanzada

---

## ⚙️ ¿Cómo funciona un EDR?

### 📡 Monitoreo Continuo

- Captura actividades en los endpoints en tiempo real.
- Observa procesos, conexiones, cambios en archivos, etc.

### 📦 Almacenamiento de Datos

- Guarda eventos localmente o en la nube.
- Permite análisis forense e histórico.

### 🧠 Análisis y Detección

- Utiliza firmas, heurísticas, inteligencia artificial y análisis de comportamiento.
- Detecta comportamientos como:
  - Ejecución de PowerShell sospechoso
  - Accesos no autorizados
  - Comunicación con servidores de comando y control (C2)

### 🚨 Generación de Alertas

- Crea alertas personalizadas ante eventos sospechosos.

### 🛡️ Contención y Respuesta

Permite tomar acciones inmediatas como:

- Aislar el endpoint de la red
- Finalizar procesos maliciosos
- Eliminar archivos sospechosos
- Ejecutar scripts de remediación

---

## 🧩 Componentes Clave de un EDR

- **Agente**: Software instalado en cada endpoint para recolección y monitoreo.
- **Consola Centralizada**: Panel de gestión para visualizar alertas y tomar decisiones.
- **Motor de Detección**: Analiza datos con reglas, firmas y machine learning.
- **Repositorio de Eventos**: Base de datos con logs para búsquedas, investigaciones y correlaciones.

---

## 🆚 Comparativa: EDR Open Source vs Comerciales

### 🆓 Soluciones EDR Open Source

| Solución   | Características Principales |
|------------|------------------------------|
| **Wazuh**  | Capacidad HIDS + EDR, integración MITRE ATT&CK |
| **OpenEDR**| Proyecto de Comodo, telemetría y dashboards |
| **Osquery**| Consultas SQL sobre endpoints, ideal para auditoría |

### 💲 Soluciones Comerciales

| Solución                        | Características Destacadas |
|--------------------------------|-----------------------------|
| **CrowdStrike Falcon**         | IA avanzada, protección cloud-native, threat hunting |
| **SentinelOne**                | Respuesta autónoma, rollback de ataques |
| **Microsoft Defender for Endpoint** | Integración con Windows, despliegue sencillo |
| **Trend Micro Apex One**       | Protección contra APTs, integración con SIEM |

---

## 🕵️ Aplicación del EDR en Threat Hunting

Los EDR son herramientas esenciales para analistas de amenazas. Permiten:

- Buscar proactivamente amenazas no detectadas por antivirus o SIEM.
- Crear consultas personalizadas basadas en TTPs (tácticas, técnicas y procedimientos).
- Investigar incidentes con contexto completo.
- Recolectar indicadores de compromiso (IoCs).
- Validar hipótesis de intrusión o actividad sospechosa.

---

## 📈 Ventajas y ❗Limitaciones

### ✅ Ventajas

- Visibilidad profunda en los endpoints
- Detección de amenazas sofisticadas
- Capacidad de contención y respuesta inmediata
- Integración con SIEM y plataformas SOAR

### ❌ Limitaciones

- Consumo de recursos (CPU/RAM) en los dispositivos
- Posibles falsos positivos si no se ajusta bien
- Soluciones comerciales pueden tener **costos elevados**

---

