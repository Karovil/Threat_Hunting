# Recopilación y Análisis de Datos

🔍 Recopilación y Análisis de Datos en Operaciones de Threat Hunting
Introducción
Todo proceso efectivo de threat hunting comienza con una sola pregunta: ¿Qué tan bien conocemos lo que ocurre en nuestra red?
Para responder a eso, necesitamos datos. Pero no cualquier tipo de datos, sino aquellos que puedan aportar contexto, detectar comportamientos y permitir correlaciones profundas.

¿Qué datos necesitamos y de dónde los sacamos?
En una red moderna, los datos de seguridad pueden venir de múltiples capas. Necesitamos recolectar desde registros del sistema (como logs de Windows o Syslog de Linux), hasta eventos de red, autenticaciones, uso de aplicaciones y señales de los endpoints.

🧠 Ejemplo real:
Un atacante logra acceso inicial por RDP y empieza a moverse lateralmente. Si solo recolectas logs del firewall, te perderás toda la actividad interna. Pero si recolectas eventos de autenticación fallida (EventID 4625), logs del EDR y tráfico lateral (SMB, WinRM), la historia cambia completamente.

Cómo hacer que los datos "hablen el mismo idioma"
Cada sistema tiene su forma de generar logs. Un intento fallido de login en Windows no se parece en nada a uno en Linux. Para analizarlos todos juntos, necesitamos convertirlos a un formato común. A esto lo llamamos normalización.

Se usan herramientas como:

- Logstash o Fluentd, para transformar los datos entrantes.

- Elastic Common Schema (ECS), para darles una estructura común.

- Graylog pipelines o Cribl, para enriquecer eventos antes de analizarlos.

💡 Dato curioso: ECS no solo define los campos (source.ip, event.outcome, etc.), sino que su estructura permite consultas cruzadas sobre fuentes distintas, como correlacionar logs de proxy con actividad en endpoints.

¿Qué hacemos con todos esos datos?
Una vez los logs están centralizados y normalizados, comienza la verdadera caza. Aquí aplicamos análisis desde distintos ángulos:

Análisis temporal: Detectamos patrones que se repiten a ciertas horas o días (por ejemplo, actividad fuera del horario laboral).

Análisis conductual: ¿Ese usuario suele iniciar sesión en ese servidor? ¿Desde esa IP? ¿Con ese proceso?

Análisis estructural: Evaluamos cambios no autorizados, procesos inusuales, DLLs cargadas que no corresponden, etc.

Casos reales que se pueden detectar
Un usuario que normalmente accede de 8 a 17, de repente inicia sesión a las 3 a.m.

Se ejecuta powershell.exe sin argumentos en un host sin tareas automatizadas.

Un endpoint sin antivirus genera tráfico DNS inusual hacia dominios que no existen.

✅ Todos estos comportamientos pueden no levantar alertas en un sistema tradicional, pero sí aparecer en un proceso de hunting bien planteado.

Herramientas clave (resumen con aplicación práctica)
Wazuh: Recopila logs, analiza en tiempo real, genera alertas. Ideal para ver integridad de archivos, registros de sistema, y comportamientos sospechosos por agentes en los endpoints.

Graylog: Potente analizador de logs con filtros y consultas personalizadas. Útil para crear dashboards de actividad sospechosa y filtrar eventos por patrón (por ejemplo, buscar procesos anómalos como whoami.exe en usuarios que no deberían ejecutarlos).

Elastic Stack: Elasticsearch permite búsquedas a gran escala; Logstash transforma; Kibana visualiza. Su combinación permite detectar tendencias y visualizar relaciones entre eventos.

Splunk: Robusto y escalable. Permite búsquedas como:

spl
Copiar
Editar
index=windows EventCode=4672 user!="Administrador"
Eso detectaría privilegios especiales asignados a usuarios inesperados.

MITRE ATT&CK + Sigma: Uno da el mapa de cómo atacan los adversarios (tácticas, técnicas, procedimientos); el otro te permite traducir esas técnicas en reglas detectables en tu entorno.

Ejercicio sugerido
Objetivo: Detectar un posible movimiento lateral basado en autenticaciones sospechosas.

Pasos:

Filtra todos los logs con EventID 4624 (logins exitosos).

Busca usuarios que normalmente acceden desde ciertos hosts, conectándose desde otros nuevos.

Cruza la información con eventos de cmd.exe ejecutado tras el login.

Pregunta clave: ¿Hay alguna coincidencia entre autenticaciones inusuales y ejecución de comandos administrativos?

Cierre
El hunting no es una herramienta, ni una tecnología: es una mentalidad.
Se basa en la suposición de que el enemigo ya está dentro y nos corresponde encontrarlo.

Por eso, la recopilación y análisis de datos no puede ser un proceso pasivo. Requiere conocimiento técnico, inteligencia contextual y creatividad para conectar eventos dispersos y ver la historia completa detrás de ellos.
