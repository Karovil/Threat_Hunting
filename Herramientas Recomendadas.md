# 🛠️ Herramientas Recomendadas para Threat Hunting

En un entorno de threat hunting, contar con herramientas adecuadas es fundamental para recolectar evidencia, analizar comportamientos, detectar anomalías y validar hipótesis. A continuación, se describen las herramientas más relevantes, su propósito principal, y ejemplos básicos de uso.

### 🔍 Splunk / ELK Stack / Graylog
Estas plataformas SIEM (Security Information and Event Management) permiten la recolección centralizada de logs, su análisis y la generación de visualizaciones y alertas. Son fundamentales para detectar patrones y correlacionar eventos sospechosos.

**Splunk**: Plataforma comercial con alto rendimiento. Utiliza su propio lenguaje de consultas SPL para búsquedas complejas.

**ELK Stack**: Solución open source compuesta por Elasticsearch, Logstash y Kibana. Logstash ingiere y transforma datos, Elasticsearch los indexa, y Kibana los visualiza.

**Graylog**: SIEM más ligero y versátil, ideal para entornos pequeños o medianos. Usa Lucene DSL para sus consultas.

**Ejemplo básico en Splunk:**
```spl
index=windows EventCode=4625 | stats count by Account_Name, host
```
Esta consulta muestra la cantidad de intentos fallidos de inicio de sesión agrupados por cuenta y equipo.

---

### 🌐 Wireshark / TCPdump
Estas herramientas permiten la captura y análisis del tráfico de red. Son esenciales para identificar comunicaciones sospechosas, conexiones a servidores de comando y control (C2), o patrones de exfiltración de datos.

**Wireshark**: Herramienta gráfica para visualizar tráfico de red con filtros muy precisos. Permite ver protocolos, payloads y secuencias.

**TCPdump**: Alternativa por línea de comandos. Es más rápida para recolección en servidores o scripting automatizado.

**Ejemplo básico con TCPdump:**
```bash
tcpdump -i eth0 host 192.168.1.5 and port 443
```
Captura tráfico HTTPS entre una IP específica y el host local.

---

### 🧪 Velociraptor / KAPE
Herramientas de análisis forense que permiten recolectar artefactos desde endpoints, esenciales para investigaciones post-intrusión.

**Velociraptor**: Framework que ejecuta consultas en vivo (VQL) sobre endpoints para recolectar procesos activos, archivos modificados, conexiones, etc. Ideal para hunting distribuido.

**KAPE**: Herramienta para recolectar artefactos forenses de forma rápida. Automatiza la extracción de registros, prefetch, historiales y claves del sistema.

**Ejemplo básico con Velociraptor:**
Desde la consola web, seleccionar un host y ejecutar la consulta `Windows.System.Prefetch`

---

### 🔐 Sigma / YARA
Estas herramientas definen patrones de comportamiento para detección de amenazas.

**Sigma**: Lenguaje agnóstico para detección en logs. Una regla Sigma puede convertirse para Splunk, Elastic o Graylog.

**YARA**: Define reglas para buscar patrones en archivos o memoria (strings, hashes, estructuras específicas). Ideal para detección de malware.

**Ejemplo básico de regla Sigma:**
```yaml
detection:
  selection:
    CommandLine|contains: 'whoami'
    Image: 'cmd.exe'
  condition: selection
```

**Ejemplo básico de YARA:**
```yara
rule ExampleRule {
  strings:
    $a = "malicious.exe"
  condition:
    $a
}
```

---

### 🧾 OSQuery
Convierte el sistema operativo en una base de datos SQL. Permite hacer auditorías en tiempo real, detectar configuraciones anómalas o procesos activos sospechosos.

**Ejemplo básico:**
```sql
SELECT name, pid, path FROM processes WHERE name='cmd.exe';
```
Retorna información sobre el proceso cmd.exe si se está ejecutando en el sistema.

---

### 👾 DeimosC2
Plataforma de Command & Control (C2) utilizada en entornos de laboratorio para emular técnicas adversarias y evaluar capacidades de detección.

Se usa para:
- Simular persistencia.
- Ejecutar cargas maliciosas.
- Observar comunicación de malware en red (beaconing).

**Ejemplo básico:**
- Crear payload desde la interfaz web.
- Ejecutarlo en una máquina virtual.
- Observar qué artefactos genera y cómo responde el SIEM.

---

### 🧠 Autopsy / FTK Imager
Herramientas de análisis de disco para investigaciones forenses profundas.

**Autopsy**: Interfaz gráfica para examinar discos. Muestra archivos borrados, artefactos, historial de uso, claves del registro, etc.

**FTK Imager**: Permite montar discos, visualizar estructuras, y crear imágenes forenses sin alterar evidencia.

**Ejemplo básico:**
- Cargar imagen de disco.
- Navegar artefactos.
- Extraer archivos borrados para análisis.

---

### 🧬 Volatility
Framework para análisis de memoria RAM. Extrae información de sistemas en ejecución incluso si ya fueron apagados.

**Uso común:**
- Identificar procesos activos en RAM.
- Ver conexiones de red.
- Detectar DLLs inyectadas o rootkits.

**Ejemplo básico:**
```bash
volatility -f memoria.raw --profile=Win10x64_18362 pslist
```
Lista los procesos activos en el volcado de memoria.

---

Estas herramientas son esenciales para cubrir todo el ciclo del threat hunting, desde la detección hasta el análisis forense. Su dominio permite identificar amenazas avanzadas, validar compromisos y fortalecer la seguridad del entorno.

