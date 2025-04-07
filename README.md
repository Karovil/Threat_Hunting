Introduccion al Threat Hunting
El Threat Hunting es la busqueda proactiva de amenazas en una red que han eludido las soluciones de seguridad tradicionales. A diferencia de la deteccion reactiva, el hunting implica analizar sistemas y eventos en busca de indicadores de compromiso (IoCs) o tacticas, tecnicas y procedimientos (TTPs) utilizados por atacantes.

1. Recopilacion y Analisis de Datos

Recoleccion de Datos
Fuentes principales:
- Logs de sistemas operativos (eventos de Windows, syslog en Linux)
- Firewalls y sistemas de prevencion de intrusos (IPS)
- Sistemas EDR/XDR
- SIEMs (ej: Splunk, Graylog, ELK)
- NetFlow y capturas de red (PCAPs)
- Servidores DNS y proxies

Estrategias clave:
- Cobertura amplia y completa: recoger logs de todos los endpoints y dispositivos perimetrales.
- Agregacion centralizada: usar un SIEM para centralizar la informacion.
- Enriquecimiento: anadir contexto como geolocalizacion de IPs, reputacion de dominios, etc.

Normalizacion de Datos
Proceso de transformar datos heterogeneos en un formato comun para su analisis.
Ejemplo:
Fuente | Campo original | Campo normalizado
-------|----------------|------------------
Syslog | src_ip         | source.ip
Windows| IpAddress      | source.ip

Formatos comunes: CEF, LEEF, Elastic Common Schema (ECS).

Analisis de Datos
- Analisis exploratorio: identificar valores atipicos y comportamientos inusuales.
- Analisis de series temporales: identificar variaciones a lo largo del tiempo.
- Dashboards y visualizacion: usar Kibana, Grafana o Splunk para representar datos de forma visual.

2. Correlacion de Eventos y Tecnicas Forenses

Correlacion de Eventos
Permite unir multiples eventos relacionados para identificar actividad maliciosa compleja.
Ejemplo:
1. Inicio de sesion exitoso desde una IP extranjera.
2. Elevacion de privilegios.
3. Creacion de cuenta administrativa.
4. Descarga de herramientas sospechosas.

Tecnicas:
- Reglas de correlacion en SIEMs.
- Sigma/YARA rules para patrones en logs y archivos.
- MITRE ATT&CK Mapping: alinear eventos con tecnicas conocidas.

Tecnicas Forenses
- Volcados de memoria.
- Analisis de disco.
- Timeline forensics (Plaso, log2timeline).
- Analisis de registros (accesos, errores del sistema).

3. Deteccion de Patrones y Anomalias

Identificacion de Comportamientos Anomalos
Tipos de anomalias:
- Tiempo: accesos fuera de horario.
- Volumen: transferencia inusual de datos.
- Contexto: accesos a recursos no habituales.

Tecnicas:
- UEBA.
- Machine learning.
- Scripting personalizado (Python, Bash).

Identificacion de Patrones Maliciosos
- Nombres de procesos comunes (cmd.exe, whoami).
- Comportamiento de malware (rundll32, regsvr32).
- Comunicacion con dominios de C2.
- Secuencia de tecnicas segun MITRE ATT&CK.

Herramientas Recomendadas
Herramienta       | Uso principal
------------------|-----------------------------
Splunk/ELK/Graylog| Agregacion y visualizacion
Wireshark/TCPdump | Captura y analisis de trafico
Velociraptor/KAPE | Recoleccion forense
Sigma/YARA        | Reglas de deteccion
OSQuery           | Consultas del sistema
DeimosC2          | Emulacion de amenazas

