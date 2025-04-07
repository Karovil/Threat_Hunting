# Fundamentos y Conceptos Clave de Ciberseguridad

## 📄 Tabla de Contenidos
<!-- TOC -->
- [Introducción](https://github.com/Karovil/Threat_Hunting/blob/M%C3%B3dulo-2-Fundamentos-y-Conceptos-Clave-de-Ciberseguridad-Terminolog%C3%ADa-esencial-adversarios%2C-TTPs%2C-IOCs%2C-entre-otros/README.md)
  - [¿Qué es?](https://github.com/Karovil/Threat_Hunting/blob/M%C3%B3dulo-2-Fundamentos-y-Conceptos-Clave-de-Ciberseguridad-Terminolog%C3%ADa-esencial-adversarios%2C-TTPs%2C-IOCs%2C-entre-otros/README.md)
  - [Cómo funciona](https://github.com/Karovil/Threat_Hunting/blob/M%C3%B3dulo-2-Fundamentos-y-Conceptos-Clave-de-Ciberseguridad-Terminolog%C3%ADa-esencial-adversarios%2C-TTPs%2C-IOCs%2C-entre-otros/README.md)
    
- [⚔️ Tácticas y Técnicas](#️tácticas-y-técnicas)
  - [TTPs (Tactics, Techniques, and Procedures)](#ttps-tactics-techniques-and-procedures)
  - [Living off the Land (LotL)](#living-off-the-land-lotl)
  - [Initial Access](#initial-access)
  - [Privilege Escalation](#privilege-escalation)
  - [Lateral Movement](#lateral-movement)
    
- [🔐 Indicadores y Artefactos](#-indicadores-y-artefactos)
  - [IOC](#-indicadores-y-artefactos)
  - [IOA](#-indicadores-y-artefactos)
  - [Hash](#-indicadores-y-artefactos)
  - [Persistence Mechanism](#-indicadores-y-artefactos)
    
- [📦 Herramientas y Frameworks](#-herramientas-y-frameworks)
  - [MITRE ATT&CK](#-herramientas-y-frameworks)
  - [Sigma Rules](#-herramientas-y-frameworks)
  - [YARA](#-herramientas-y-frameworks)
  - [Sysmon](#-herramientas-y-frameworks)
  - [Velociraptor](#-herramientas-y-frameworks)
    
- [🧱 Análisis y Detección](#-análisis-y-detección)
  - [Event Correlation](#-análisis-y-detección)
  - [False Positive](#-análisis-y-detección)
  - [Noise vs Signal](#-análisis-y-detección)
  - [Dwell Time](#-análisis-y-detección)


- [🌐 Principios de Redes y Sistemas](#-principios-de-redes-y-sistemas)
- [📡 Fundamentos de Redes](#-fundamentos-de-redes)
  - [Modelos de Referencia](#-fundamentos-de-redes)
  - [Protocolos Clave](#-fundamentos-de-redes)
  - [Topologías y Dispositivos](#-fundamentos-de-redes)
    
- [🧩 Fundamentos de Sistemas](#-fundamentos-de-sistemas)
  - [Sistemas Operativos](#-fundamentos-de-sistemas)
  - [Gestión de Usuarios y Permisos](#-fundamentos-de-sistemas)
  - [Procesos, Servicios y Registro](#-fundamentos-de-sistemas)
  - [Hardening y Supervisión](#-fundamentos-de-sistemas)
  
- [🏗️ Conocimientos Básicos en Arquitectura de Redes, Protocolos y Seguridad de Sistemas](#-conocimientos-básicos-en-arquitectura-de-redes-protocolos-y-seguridad-de-sistemas)
  - [Arquitectura de Redes](#-conocimientos-básicos-en-arquitectura-de-redes-protocolos-y-seguridad-de-sistemas)
  - [Elementos clave](#-conocimientos-básicos-en-arquitectura-de-redes-protocolos-y-seguridad-de-sistemas)
  - [Diseño seguro](#-conocimientos-básicos-en-arquitectura-de-redes-protocolos-y-seguridad-de-sistemas)
  - [Protocolos de Comunicación](#-conocimientos-básicos-en-arquitectura-de-redes-protocolos-y-seguridad-de-sistemas)
  - [Protocolos comunes](#-conocimientos-básicos-en-arquitectura-de-redes-protocolos-y-seguridad-de-sistemas)
  - [Seguridad de Sistemas](#-conocimientos-básicos-en-arquitectura-de-redes-protocolos-y-seguridad-de-sistemas)
  - [Conceptos fundamentales](#-conocimientos-básicos-en-arquitectura-de-redes-protocolos-y-seguridad-de-sistemas)
    
- [🧠 Relación con Threat Hunting](#-Relación-con-Threat-Hunting)
<!-- /TOC -->
---

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

- **MITRE ATT&CK**: Base de datos abierta para clasificar tácticas y técnicas de ataque.
  ```>https://attack.mitre.org/```
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

El deber de un hunter es:

- Reconocer configuraciones débiles.
- Analizar tráfico y protocolos.
- Revisar logs de sistemas.
- Identificar brechas por mala configuración.
