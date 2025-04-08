# Correlación de Eventos y Técnicas Forenses en Threat Hunting

## ¿Por qué correlacionar?
En entornos complejos, los eventos maliciosos rara vez son obvios. Un solo intento de inicio de sesión fallido o un nuevo proceso ejecutado por powershell.exe pueden parecer inofensivos… hasta que se conectan con otra actividad que ocurre minutos antes o después.
Correlacionar eventos es encontrar el hilo conductor entre piezas sueltas del rompecabezas.

## Caso práctico: ¿Ataque o coincidencia?
Imagina que ves esto en los logs:

Inicio de sesión exitoso desde una IP extranjera.

A los pocos minutos, creación de una nueva cuenta de usuario con privilegios administrativos.

Poco después, ejecución de rundll32.exe en el mismo host.

Separados, estos eventos podrían pasar como algo “normal” (especialmente si nadie los supervisa activamente).
Pero si los correlacionas temporalmente y por hostname, el patrón es claro: movimiento lateral + persistencia + ejecución de código.

💡 Insight clave: Lo que no parece una amenaza cuando se analiza en silos, se convierte en una alerta crítica cuando se ve como parte de una cadena.

## La correlación puede hacerse de varias maneras:

Por tiempo: Eventos que ocurren en un intervalo pequeño, relacionados por usuario, IP o host.

Por contexto: Mismo usuario que inicia sesión y luego ejecuta comandos sospechosos.

Por dependencia: Un proceso inicia otro, y ese segundo genera conexiones salientes.

### Ejemplo en Graylog

```Graylog
source:winlogbeat AND (EventID:4624 OR EventID:4720) AND host:server01
````
Esta consulta busca inicios de sesión y creación de cuentas en un mismo host. Es un punto de partida para la correlación manual.

## Entra la parte forense 🧬
Correlacionar te dice qué pasó. El análisis forense te dice cómo pasó y qué dejó atrás.
Aquí es donde entran herramientas especializadas:

Volatility: Análisis de memoria RAM. Te dice qué procesos estaban en ejecución, qué conexiones había y qué DLLs estaban cargadas.

Plaso / log2timeline: Reconstrucción de líneas de tiempo de actividad en el sistema, útil para rastrear desde la ejecución de malware hasta cambios en archivos.

Autopsy: Suite forense completa que permite examinar discos, extraer metadatos, y detectar patrones como acceso a documentos o recuperación de archivos eliminados.

🧠 Dato importante: La memoria no miente. Aunque un atacante borre logs del sistema, los procesos y conexiones quedan en la RAM por un tiempo. Ahí es donde entra Volatility.

## ¿Y qué papel juegan YARA y Sigma?
YARA te permite definir firmas basadas en patrones binarios o cadenas en archivos/memoria.
Sigma, por otro lado, te permite definir condiciones específicas en logs para detectar comportamientos sospechosos.

✅ Ejemplo de regla Sigma: Detectar ejecución de whoami.exe por usuarios sin privilegios elevados.

yaml
````yaml
detection:
   selection:
  
    Image: 'C:\\Windows\\System32\\whoami.exe'
    User: '!Administrador'
    
  condition: selection
 ```` 
Estas reglas se pueden convertir automáticamente al lenguaje de tu SIEM (Splunk, Graylog, Elastic, etc.), permitiendo detección automatizada basada en lo aprendido durante el análisis.


## Bonus: Ciclo real de hunting + forense
Detectas un inicio de sesión fuera del horario habitual.

Correlacionas con logs de procesos: ves ejecución de cmd.exe.

Extraes una imagen de memoria y con Volatility descubres que hubo carga de un archivo x.exe desde C:\\Temp.

Corres YARA sobre el binario y descubres que es un backdoor conocido.

Mapear los eventos a MITRE ATT&CK te muestra que el atacante usó T1059 (Command and Scripting Interpreter), T1078 (Valid Accounts) y T1547 (Boot or Logon Autostart).

🎯 Resultado: Construiste una narrativa completa del ataque.

## Cierre
Correlacionar eventos y aplicar técnicas forenses es lo que convierte a un analista en cazador. No se trata solo de ver qué pasó, sino de entender por qué, cómo y con qué fin.

Un buen hunter sabe que los logs no cuentan la historia completa hasta que los unes con intención y contexto.
