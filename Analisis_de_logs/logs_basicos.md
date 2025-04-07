# 📘 Introducción a los Logs Básicos en Threat Hunting

---

## 🧾 ¿Qué son los logs?

Los **logs** son registros cronológicos generados por sistemas operativos, aplicaciones, redes o dispositivos de seguridad.  
Contienen información detallada sobre eventos, acciones, errores y comportamientos.

En el contexto de **Threat Hunting**, los logs son la **fuente primaria** para:

- Identificar patrones maliciosos.
- Detectar anomalías en el comportamiento del sistema.
- Confirmar Indicadores de Compromiso (IoCs).

---

## 🔐 Importancia de los Logs para el Blue Team

El **Blue Team** es el equipo responsable de la **defensa cibernética activa** de una organización. Utiliza herramientas como SIEM, EDR y análisis de logs para proteger el entorno.

### ¿Por qué son importantes los logs?

- 📌 Detectan actividad maliciosa o no autorizada.
- 🔎 Permiten realizar análisis forense tras un incidente.
- 📊 Alimentan al **SIEM** para generar correlaciones y alertas.
- 📁 Ayudan a cumplir requisitos legales y auditorías.

Un analista del Blue Team debe dominar los diferentes tipos de logs y cómo analizarlos eficientemente.

---

## 🗂️ Tipos de Logs Básicos

### 1. 🖥️ Logs del Sistema Operativo

#### 📄 Windows Event Logs

- 📍 Ubicación: `C:\Windows\System32\winevt\Logs\`
- Tipos:
  - **Security**: inicios de sesión, cambios de políticas, accesos fallidos.
  - **System**: eventos de hardware, errores del sistema.
  - **Application**: mensajes generados por aplicaciones instaladas.

**Ejemplo:**
Event ID 4625 - Failed logon attempt Account Name: johndoe Logon Type: 3 Source IP: 192.168.1.15
#### 🐧 Linux Syslogs

- 📍 Ubicación: `/var/log/`
- Archivos importantes:
  - `auth.log` / `secure`: intentos de autenticación.
  - `syslog` / `messages`: mensajes generales del sistema.
  - `dmesg`: eventos del kernel.

**Ejemplo:**
Failed password for root from 10.10.10.5 port 22 ssh2

---

### 2. 🔥 Logs de Firewall

Registros del tráfico que entra o sale del entorno. Incluyen origen/destino, puertos y protocolos.

**Ejemplo:**
Blocked inbound TCP connection from 203.0.113.5:443 to 192.168.1.100:3389

**Usos:**

- Detección de escaneos de red.
- Identificación de conexiones salientes a destinos sospechosos.
- Reconocimiento de patrones de ataque (p. ej. DDoS).

---

### 3. 🌐 Logs de Proxy / Web

Capturan navegación web, solicitudes HTTP/S, URLs y descargas.

**Ejemplo:**
192.168.1.15 - GET http://malicious-domain.com/index.php

**Usos:**

- Detectar comunicación con dominios maliciosos.
- Monitorear intentos de phishing o malware web.
- Analizar actividad inusual del usuario.

---

### 4. 🛡️ Logs de Antivirus / EDR

Registros de detección, bloqueo, cuarentena o remediación.

**Ejemplo:**
Trojan:Win32/Emotet detected and removed Process: C:\Users\user\Downloads\invoice.exe


**Importancia:**

- Validar infecciones confirmadas.
- Correlacionar eventos con otros logs (red, sistema).
- Confirmar intentos de ejecución o persistencia.

---

### 5. 🌍 Logs de Servidores Web (Apache / Nginx)

#### Apache Access Log (`/var/log/apache2/access.log`)
192.168.1.10 - - [06/Apr/2025:12:01:02 +0000] "GET /admin.php HTTP/1.1" 200


#### Nginx Access Log (`/var/log/nginx/access.log`)
192.168.1.10 - - [06/Apr/2025:12:01:02 +0000] "POST /login HTTP/1.1" 403

**Usos:**

- Detección de fuerza bruta o fuzzing.
- Identificación de escaneo de rutas y directorios.
- Rastreo de vectores de ataque web.

---

## 📚 Terminología Clave

| Término              | Definición                                                                 |
|----------------------|----------------------------------------------------------------------------|
| **Event ID**         | Identificador de evento en Windows Event Logs.                            |
| **Syslog**           | Protocolo estándar de logs para sistemas Unix/Linux.                      |
| **IOC (Indicator of Compromise)** | Evidencia de posible intrusión.                          |
| **FQDN**             | Nombre de dominio completamente calificado.                               |
| **False Positive**   | Alerta incorrecta, sin amenaza real.                                       |
| **Log Rotation**     | Gestión del tamaño de logs para evitar saturación.                        |

---

## 🧪 Ejemplo Visual: Caso de Fuerza Bruta por SSH

### 🔍 Logs detectados:

**auth.log**
Failed password for invalid user admin from 192.168.0.50 port 55844 ssh2


**fail2ban.log**
Ban 192.168.0.50 after 5 failed attempts


**Alerta en el SIEM**
SSH Brute Force Detected - Source IP: 192.168.0.50

### 🧩 Análisis del Blue Team:

- Verificar si la IP aparece en otros eventos del entorno.
- Buscar intentos exitosos posteriores.
- Correlacionar con logs de otros dispositivos.
- Aplicar contramedidas:
  - Bloqueo de IP.
  - Notificación automática.
  - Revisión de accesos al sistema.

---

## ✅ Buenas Prácticas en el Manejo de Logs

- Habilitar logs detallados en todos los sistemas críticos.
- Centralizar logs mediante un **SIEM** (como Wazuh, ELK).
- Configurar **rotación de logs** y retención segura.
- Validar la integridad de los archivos de logs (hashes, firmas).
- Automatizar alertas ante patrones conocidos.
- Capacitar al equipo en análisis de eventos y respuesta rápida.
