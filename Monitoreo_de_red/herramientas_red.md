# Herramientas de Análisis de Red

Este documento forma parte del repositorio de **Threat Hunting** y tiene como objetivo presentar las principales herramientas utilizadas para el análisis de tráfico de red, tanto gráficas como de línea de comandos. Estas herramientas permiten inspeccionar paquetes, analizar flujos y detectar posibles amenazas.

---

## 🧰 Herramientas Gráficas

### 1. **Wireshark**

Wireshark es una herramienta de análisis de protocolos de red que permite capturar y examinar el tráfico en tiempo real.

- **Ventajas**:
  - Interfaz intuitiva.
  - Permite aplicar filtros personalizados.
  - Reconoce una gran cantidad de protocolos.

- **Uso básico**:
  1. Captura tráfico en una interfaz de red.
  2. Filtra paquetes con expresiones como:
     - `http`
     - `ip.addr == 192.168.1.10`
     - `tcp.port == 80`
  3. Analiza el contenido de los paquetes y reconstruye sesiones.

- **Ejemplo visual**:

  ![Wireshark Screenshot](https://www.wireshark.org/docs/wsug_html/images/ws-main.png)

---

### 2. **Miner**

Miner (también conocido como HELK Miner o Open Threat Research Miner) es una herramienta que permite visualizar y explorar datos de red en formato gráfico.

- **Ventajas**:
  - Integración con herramientas como HELK, Elasticsearch y Kibana.
  - Visualiza relaciones entre IPs, dominios y eventos.
  - Útil para análisis de amenazas persistentes avanzadas (APT).

- **Caso de uso**:
  - Visualizar la comunicación entre endpoints tras una campaña de phishing.
  - Correlacionar tráfico malicioso con indicadores de compromiso (IOCs).

---

## 🔧 Herramientas de Línea de Comandos

### 1. **tcpdump**

Herramienta poderosa para capturar y analizar tráfico directamente desde la terminal.

- **Comandos útiles**:
  - Capturar paquetes en una interfaz:
    ```bash
    sudo tcpdump -i eth0
    ```
  - Guardar la captura en un archivo:
    ```bash
    sudo tcpdump -i eth0 -w captura.pcap
    ```
  - Filtros:
    ```bash
    tcpdump port 80
    tcpdump src host 10.0.0.5
    tcpdump dst net 192.168.0.0/24
    ```

---

### 2. **iftop**

Muestra el uso del ancho de banda en tiempo real por dirección IP.

- **Ejemplo**:
  ```bash
  sudo iftop -i eth0
   ```
Muestra qué IPs están consumiendo más recursos en la red, lo cual puede alertar sobre conexiones sospechosas.

### 3. nload
Visualiza gráficamente el tráfico de red entrante y saliente en consola.
 ```bash
sudo nload
 ```
Útil para detectar picos repentinos de tráfico.

### 4. netstat
Permite ver conexiones activas, puertos en uso y programas vinculados a estas conexiones.

 ```bash
netstat -tuln
 ```
Opcionalmente, puedes usar:
 ```bash
netstat -ano | grep :80
 ```
### 🔍 Filtros y Comandos Útiles en Linux para Análisis de Red
Comando	Descripción

  -netstat -tulnp	Muestra puertos abiertos y servicios asociados.
  
  -lsof -i	Lista procesos que usan la red.
  
  -ss -tulwn	Alternativa moderna a netstat.
  
  -arp -a	Muestra la tabla ARP de la red local.
  
  -ping, traceroute	Diagnóstico básico de conectividad.
  
  -whois, dig, nslookup	Recolección de información sobre dominios e IPs.
  
## 🧠 Casos de Uso y Aplicación en Threat Hunting
### Caso 1: Exfiltración de Datos
  -Se detecta un pico de tráfico de salida con nload.

  -Se analiza con tcpdump y Wireshark.

  -Se identifica un ZIP cifrado saliendo hacia una IP extranjera.

  -Con whois se determina que la IP pertenece a un proveedor sospechoso.

## Caso 2: Detección de Beaconing
Con iftop se detecta comunicación constante hacia una IP externa cada 5 segundos.

Wireshark revela solicitudes HTTP vacías o repetidas.

Se sospecha de C2 (comando y control) y se investigan procesos con lsof -i.
