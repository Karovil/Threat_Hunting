# Fundamentos y Conceptos Clave de Ciberseguridad

## 📄 Tabla de Contenidos
<!-- TOC -->
- [Introducción](#introducción)
  - [¿Qué es?](#Qué-es)
  - [Cómo funciona](#Cómo-funciona)
- [⚔️ Tácticas y Técnicas](#️tácticas-y-técnicas)
- [TTPs (Tactics, Techniques, and Procedures)](#ttps-tactics-techniques-and-procedures)
- [Living off the Land (LotL)](#living-off-the-land-lotl)
- [Initial Access](#initial-access)
- [Privilege Escalation](#privilege-escalation)
- [Lateral Movement](#lateral-movement)
- [🧩 Indicadores y Artefactos](#-indicadores-y-artefactos)
- [📦 Herramientas y Frameworks](#-herramientas-y-frameworks)
- [📈 Análisis y Detección](#-análisis-y-detección)
- [🌐 Principios de Redes y Sistemas](#-principios-de-redes-y-sistemas)
  - [🧠 Fundamentos de Redes](#-fundamentos-de-redes)
  - [🧩 Fundamentos de Sistemas](#-fundamentos-de-sistemas)
  - [🧠 Conocimientos Básicos en Arquitectura de Redes, Protocolos y Seguridad de Sistemas](#-conocimientos-básicos-en-arquitectura-de-redes-protocolos-y-seguridad-de-sistemas)
<!-- /TOC -->
---

## Introducción
Threat hunting o también conocido como “caza de amenazas cibernéticas”, se ha vuelto una pieza cada vez más vital para las organizaciones. Este mecanismo surge con el propósito de encontrar intrusiones y también para la prevención de estos.

- ¿Qué es?
  
Es un proceso centrado en el análisis humano y del software en la búsqueda de actividades anormales en los activos de la organización.

- Cómo funciona
  
Este al igual que un cazador de la antigüedad, hay que hacer reconocimiento del lugar donde se encuentra la presa. Por esta razón, el proceso del hunter es analizar el sistema, conocerlo a profundidad, e identificar las actividades anormales.
Este hunter tiene las herramientas e instrumentos necesarios para hacer un debido procedimiento, ellos aparecen al ya haber pasado un ataque o mientras está pasando.
La cacería de amenazas cibernéticas se caracteriza por su proactividad. No es tan solo un detector de amenazas pasivo como un SIEM (Security Information and Event Management) tradicional. 
En lo que se centran es en adelantarse a las amenazas. Usa mecanismos de predicción, detección y respuesta.
Estos hunters deben hacer hipótesis para así hallar un propósito al ataque y deducir que quería el atacante y como prevenir futuros ataques.


## ⚔️Tácticas y Técnicas
### TTPs (Tactics, Techniques, and Procedures)

Patrón de comportamiento del adversario y/o descripción de cómo actúa un adversario en un ataque.

- **Tactics**: Objetivos de alto nivel (exfiltración de datos).
- **Techniques**: Métodos usados para lograr esos objetivos (keylogging).
- **Procedures**: Implementación específica del atacante (uso de PowerShell con scripts personalizados para una organización como tal).

### Living off the Land (LotL)
Uso de herramientas legítimas del sistema operativo (como PowerShell, WMIC, RDP) para llevar a cabo actividades maliciosas sin levantar sospechas ni hacer uso de malware externos.

### Initial Access
Primera forma en la que un atacante ingresa a un sistema o red: phishing, explotación de vulnerabilidad, uso de credenciales filtradas.

## Privilege Escalation

Técnicas utilizadas por el atacante para obtener mayores permisos, como pasar de usuario estándar a administrador/root.

## Lateral Movement

Desplazamiento entre sistemas dentro de una red una vez comprometido un punto inicial, para expandir control o acceder a activos más valiosos.

## 🧩 Indicadores y Artefactos

- **IOC (Indicators of Compromise)**: Evidencias como IPs maliciosas, hashes, dominios sospechosos.
- **IOA (Indicators of Attack)**: Actividad en curso o preparación de ataque (creación de procesos anómalos, conexiones inusuales).
- **Hash**: Huella digital única de un archivo (MD5, SHA1, SHA256).
- **Persistence Mechanism**: Métodos para mantener acceso tras reinicios (tareas programadas, backdoors, claves de registro).

## 📦 Herramientas y Frameworks

- **[MITRE ATT&CK](https://attack.mitre.org/)**: Base de datos abierta para clasificar tácticas y técnicas de ataque.
- **Sigma Rules**: Reglas de detección que se adaptan a diferentes SIEMs.
- **YARA**: Reglas para identificar archivos maliciosos.

```yara
rule Malware_By_Hash {
    meta:
        description = "Detecta archivo por hash conocido"
        hash = "e99a18c428cb38d5f260853678922e03"

    condition:
        filesize < 1MB and
        sha256 == "e99a18c428cb38d5f260853678922e03"
}
```

- **Sysmon**: Herramienta de Microsoft para registrar eventos detallados del sistema.
- **Velociraptor**: Plataforma para respuesta forense y threat hunting en endpoints.

## 📈 Análisis y Detección

- **Event Correlation**: Unir eventos de distintas fuentes para identificar patrones.
- **False Positive**: Detección errónea que no representa una amenaza.
- **Noise vs Signal**: Separar datos irrelevantes de actividad sospechosa.
- **Dwell Time**: Tiempo entre intrusión y detección.

## 🌐 Principios de Redes y Sistemas

Conocer redes y sistemas es clave para threat hunting: ayuda a detectar configuraciones débiles, técnicas de ataque y permite reaccionar proactivamente.

### 🧠 Fundamentos de Redes

#### 🏗️1. Modelos de Referencia

- **Modelo OSI**: 7 capas (Física, Enlace, Red, Transporte, Sesión, Presentación, Aplicación).
- **Modelo TCP/IP**: 4 capas (Acceso a red, Internet, Transporte, Aplicación).

#### 📡2. Protocolos Clave

- **TCP**: Conexión fiable (HTTP, FTP).
- **UDP**: Sin conexión, más rápido (DNS, streaming).
- **HTTP/HTTPS**: Transferencia de páginas web (HTTPS cifrado).
- **DNS**: Resuelve nombres de dominio.
- **ICMP**: Diagnóstico (ping), también usado para covert channels.

#### 🔌3. Topologías y Dispositivos

- **Switches, Routers, Firewalls**: Infraestructura crítica.
- **Proxy**: Intermediario entre cliente y servidor.
- **DMZ**: Zona expuesta para servicios públicos.

### 🧩 Fundamentos de Sistemas

#### 💻 1. Sistemas Operativos

- **Windows**: Entorno empresarial, con PowerShell y Active Directory.
- **Linux**: Servidores, usa bash y estructura diferente de permisos.

#### 👥 2. Gestión de Usuarios y Permisos

- **Autenticación**: Verifica identidad (contraseñas, 2FA).
- **Autorización**: Control de acciones (lectura, escritura).
- **Mínimos Privilegios**: Solo los accesos necesarios.

#### ⚙️ 3. Procesos, Servicios y Registro

- **Procesos**: Programas en ejecución (malware puede camuflarse).
- **Servicios**: En segundo plano (antivirus, red).
- **Logs**: Registro clave para análisis (inicio sesión, errores).

#### 🔐 4. Hardening y Supervisión

- **Hardening**: Asegurar el sistema (desactivar servicios innecesarios, actualizaciones).
- **Monitoreo**: SIEMs, EDRs, Sysmon.

### 🧠 Conocimientos Básicos en Arquitectura de Redes, Protocolos y Seguridad de Sistemas

#### 🏗️ Arquitectura de Redes

- **Topologías**: Estrella, malla, jerárquica.
- **Segmentación**: Aislar zonas por nivel de confianza.
- **Dispositivos**: Switches, routers, firewalls, NAT, IDS/IPS.

#### 📡 Protocolos de Comunicación

- **TCP/IP, DNS, HTTP/HTTPS, ICMP**: Reglas de comunicación que permiten identificar tráfico malicioso.

#### 🔐 Seguridad de Sistemas

- **Autenticación y Autorización**
- **Logs de eventos**
- **Monitoreo de procesos y servicios**
- **Persistencia y Actualizaciones**
- **Gestión de usuarios y privilegios**

---

## 🧩 Relación con Threat Hunting

Un hunter debe:

- Reconocer configuraciones débiles.
- Analizar tráfico y protocolos.
- Revisar logs de sistemas.
- Identificar brechas por mala configuración.
