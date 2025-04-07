# Herramientas para el Análisis de Logs

El análisis de logs es una pieza clave en el Threat Hunting. A través de los registros generados por sistemas, redes, aplicaciones y dispositivos, es posible identificar patrones sospechosos, correlacionar eventos y detectar amenazas antes de que se materialicen.

Para ello, se utilizan herramientas que permiten visualizar, filtrar, interpretar y correlacionar grandes volúmenes de datos. Estas herramientas ayudan a detectar comportamientos anómalos y posibles ataques en curso.

---

## 🧰 Herramientas Principales

### 1. **Wireshark**

**¿Qué es?**  
Wireshark es un analizador de tráfico de red (packet sniffer) de código abierto. Captura paquetes en tiempo real y permite analizarlos detalladamente.

**¿Para qué sirve en Threat Hunting?**
- Detectar conexiones sospechosas.
- Identificar transferencias de datos no autorizadas.
- Analizar patrones de comunicación entre dispositivos.

**Caso de uso:**  
Supón que detectas tráfico constante hacia una IP desconocida en un horario inusual. Con Wireshark puedes:
- Capturar el tráfico en tiempo real.
- Filtrar por dirección IP o protocolo.
- Inspeccionar si hay exfiltración de información o un canal de C2 (Command and Control).

**Visual:**  
``` bash
tcp.port == 443 and ip.dst == 192.168.1.50
```
Este filtro muestra el tráfico HTTPS hacia un servidor específico.

---

## 🔧 Comandos Útiles para Análisis de Logs en Linux

Los entornos Linux suelen generar muchos registros ubicados en `/var/log/`. Analizar estos archivos directamente desde consola con comandos eficientes es una habilidad clave para el Blue Team y los Threat Hunters.

A continuación, te muestro comandos prácticos y filtros comunes para revisar logs:

---

### 📄 1. Ver los últimos registros de un archivo
``` bash
tail -n 100 /var/log/auth.log
```
Muestra las últimas 100 líneas del archivo auth.log, donde se registran eventos de autenticación.

🔍 2. Buscar intentos fallidos de login
``` bash
grep "Failed password" /var/log/auth.log
```
Filtra los intentos fallidos de autenticación. Muy útil para detectar ataques de fuerza bruta.

🧑‍💻 3. Buscar accesos de un usuario específico
``` bash
grep "carolina" /var/log/auth.log
``` 
Muestra todos los eventos relacionados con el usuario carolina.

🌍 4. Ver conexiones SSH entrantes
``` bash
grep "Accepted" /var/log/auth.log | grep "ssh"
``` 
Filtra los logins exitosos vía SSH.

📅 5. Filtrar por fecha y hora
``` bash
awk '$0 ~ /Apr 06 10:/' /var/log/auth.log
``` 
Muestra todos los eventos registrados a las 10:00 AM del 6 de abril.

🕵️‍♀️ 6. Buscar intentos de acceso desde una IP específica
``` bash
grep "192.168.1.20" /var/log/auth.log
``` 
Permite saber si una IP ha interactuado con el sistema.

🔁 7. Analizar logs con más contexto
``` bash
grep -C 3 "Failed password" /var/log/auth.log
``` 
Incluye 3 líneas antes y después del evento, dando más contexto sobre lo ocurrido.

📦 8. Contar la cantidad de intentos fallidos
``` bash
grep "Failed password" /var/log/auth.log | wc -l
```
Devuelve el número total de intentos fallidos registrados.

🧮 9. Listar IPs con más intentos fallidos
``` bash
grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}' | sort | uniq -c | sort -nr | head
``` 
Este comando muestra las IPs que más veces intentaron ingresar de forma incorrecta. Ideal para identificar fuentes de ataque.

🪓 10. Extraer solo la IP de eventos de login fallido
``` bash
grep "Failed password" /var/log/auth.log | awk '{print $(NF-3)}'
``` 
Extrae únicamente la IP que aparece al final de los logs de intentos fallidos.

✅ Tips para aplicar estos comandos
Los logs suelen estar comprimidos (.gz): usa zgrep en lugar de grep para buscarlos sin descomprimir.

Puedes combinar comandos con | (pipes) para obtener resultados más específicos.

Automatiza tareas con scripts en bash o integraciones con cron para revisiones periódicas.

### 2. **Miner (dentro de HELK, Open Threat Hunter, etc.)**

**¿Qué es?**  
Miner es una herramienta utilizada para automatizar la adquisición y enriquecimiento de inteligencia de amenazas (Threat Intelligence). Se integra comúnmente en plataformas como HELK (Hunting ELK).

**¿Para qué sirve?**
- Enriquecer los logs con información de IOCs (Indicators of Compromise).
- Automatizar la búsqueda de amenazas en los datos recolectados.
- Priorizar eventos según su criticidad y contexto externo.

**Caso de uso:**  
Supón que tu SIEM recolectó varios intentos de conexión saliente hacia dominios sospechosos. Miner puede verificar esos dominios contra fuentes de inteligencia y etiquetarlos como:
- Maliciosos
- Potencialmente peligrosos
- Benignos

Esto ayuda a enfocar los esfuerzos del analista en las amenazas reales.

**Ejemplo Visual:**
| Indicador       | Tipo      | Estado          | Fuente de Inteligencia |
|-----------------|-----------|------------------|--------------------------|
| 185.244.25.10   | IP        | Maliciosa        | AbuseIPDB                |
| evilcorp.com    | Dominio   | Sospechoso       | VirusTotal               |
| d41d8cd9...     | Hash MD5  | Conocido Malware | MISP                     |

---

### 3. **Elastic Stack (ELK)**

**¿Qué es?**  
Conjunto de herramientas que incluye:
- **Elasticsearch**: motor de búsqueda y análisis.
- **Logstash**: ingesta y transformación de logs.
- **Kibana**: visualización de datos.

**¿Para qué sirve?**
- Centralizar y correlacionar grandes cantidades de eventos.
- Crear dashboards visuales que permiten identificar patrones anómalos.
- Automatizar alertas y búsquedas programadas.

**Ejemplo de visualización:**
- Gráficos de barras para intentos de login fallidos por hora.
- Mapa de conexiones SSH entrantes por país.
- Top 10 IPs con más alertas generadas.

---

## 🖼️ Ejemplos Visuales

### 📊 Gráfico de Análisis de Eventos por Severidad
| Severidad | Cantidad de Eventos |
|-----------|---------------------|
| Alta      | 23                  |
| Media     | 102                 |
| Baja      | 350                 |

---

### 🌐 Conexiones HTTP Sospechosas
timestamp src_ip dst_ip user_agent 2025-04-05 22:14:33 10.0.0.23 142.250.180.3 curl/7.64.1 2025-04-05 22:15:01 10.0.0.23 185.244.25.10 python-requests/2.25.1

yaml
Copiar
Editar

---

### 🧠 Correlación de Logs con Miner
| Indicador       | Tipo      | Estado          | Fuente de Inteligencia |
|-----------------|-----------|------------------|--------------------------|
| 185.244.25.10   | IP        | Maliciosa        | AbuseIPDB                |
| evilcorp.com    | Dominio   | Sospechoso       | VirusTotal               |
| d41d8cd9...     | Hash MD5  | Conocido Malware | MISP                     |

---

## 🔎 Casos de Uso Relevantes

- **Análisis de comportamiento**: detectar patrones como accesos a horas no laborales o desde ubicaciones inusuales.
- **Reconocimiento de movimientos laterales**: visualizar cómo un atacante se mueve lateralmente en la red.
- **Identificación de herramientas usadas por el atacante**: por ejemplo, si se observa el user-agent de una herramienta como `sqlmap`.
- **Detección de beaconing**: comunicaciones repetitivas a intervalos constantes, común en malware que intenta comunicarse con un servidor de C2.

---
## 🔎 Sysmon + Winlogbeat

### ¿Qué es Sysmon?

**Sysmon (System Monitor)** es una herramienta de Microsoft Sysinternals que genera logs detallados sobre:

- Creación de procesos.
- Cambios en el registro.
- Conexiones de red.
- Cargas de DLL.
- Manipulación de memoria.

### ¿Qué es Winlogbeat?

**Winlogbeat** es un agente ligero que envía logs de eventos de Windows (incluidos los de Sysmon) a una plataforma como ELK o Wazuh.

### Ejemplo:

- Sysmon detecta que el proceso `notepad.exe` está lanzando `powershell.exe` con una cadena codificada en base64.
- Winlogbeat envía esta información al SIEM → se genera una alerta → se investiga el proceso.

---

## ⛏️ LogMiner

**LogMiner** es una utilidad de Oracle Database que permite examinar los archivos de redo log y archivelog, útiles para la **auditoría forense** en bases de datos.

### ¿Qué permite hacer?

- Ver qué transacciones se han ejecutado.
- Determinar quién hizo qué cambios en la base de datos.
- Rastrear actividades sospechosas en entornos con base de datos crítica.

### Uso típico en ciberseguridad:

- Analizar actividad SQL inusual (borrado masivo de datos, accesos a tablas críticas).
- Determinar el origen de una modificación en la base de datos tras un incidente.

---

## 📦 OSQuery

**OSQuery** convierte el sistema operativo en una base de datos que permite hacer consultas SQL para extraer información.

### ¿Qué permite?

- Ver procesos activos, módulos cargados, puertos abiertos, usuarios conectados.
- Crear consultas recurrentes y automatizar auditorías de seguridad.
- Detectar cambios en archivos, instalación de software no autorizado, etc.

---

## 📁 Otras herramientas complementarias

| Herramienta       | Descripción breve                                                 |
|-------------------|--------------------------------------------------------------------|
| **Auditd**        | Sistema de auditoría de Linux que registra eventos del kernel.     |
| **NxLog**         | Recolector de logs multiplataforma, muy configurable.              |
| **Graylog**       | SIEM open source con enfoque en búsquedas rápidas y paneles.       |
| **Fluentd**       | Recolector de logs con soporte para múltiples formatos y destinos. |

---

## 🔐 Rol del Blue Team

El **Blue Team** utiliza estas herramientas para:

- Mantener una visibilidad detallada de todo lo que ocurre en los endpoints y la red.
- Correlacionar eventos para descubrir ataques en curso o amenazas persistentes.
- Responder rápidamente a incidentes detectados mediante las alertas generadas.
- Establecer una línea base de comportamiento para detectar desviaciones.

---
## 📌 Recomendaciones para el uso efectivo

- Crear dashboards personalizados según el rol (SOC, Threat Hunter, CISO).
- Combinar múltiples fuentes de logs: red, endpoint, nube, DNS, proxy.
- Automatizar el enriquecimiento de logs con IOCs.
- Aplicar filtros y alertas en tiempo real según comportamiento.

---

