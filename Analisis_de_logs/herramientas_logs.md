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
tcp.port == 443 and ip.dst == 192.168.1.50

yaml
Copiar
Editar
Este filtro muestra el tráfico HTTPS hacia un servidor específico.

---

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

## 📌 Recomendaciones para el uso efectivo

- Crear dashboards personalizados según el rol (SOC, Threat Hunter, CISO).
- Combinar múltiples fuentes de logs: red, endpoint, nube, DNS, proxy.
- Automatizar el enriquecimiento de logs con IOCs.
- Aplicar filtros y alertas en tiempo real según comportamiento.

---

