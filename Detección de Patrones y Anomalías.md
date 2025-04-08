# Detección de Patrones y Anomalías en Threat Hunting

## ¿Qué es una anomalía y por qué es tan poderosa?

Una anomalía es, en pocas palabras, **un comportamiento que no encaja con lo esperado**.  
En un entorno corporativo bien monitoreado, la mayoría de las acciones siguen un patrón: usuarios acceden a ciertas horas, desde ciertos lugares, ejecutan ciertas herramientas. Cuando algo rompe ese patrón, las alarmas deben activarse.

> Detección basada en anomalías = la capacidad de ver lo que no encaja, incluso si no sabíamos que debíamos buscarlo.

## ¿Qué tipos de anomalías buscamos?

El análisis de anomalías busca identificar desviaciones significativas del comportamiento base. Estas pueden clasificarse en:

- **Anomalías temporales:** como autenticaciones fuera del horario laboral habitual.
- **Anomalías contextuales:** por ejemplo, un usuario de finanzas ejecutando `powershell.exe`.
- **Anomalías estructurales:** uso de herramientas legítimas para propósitos maliciosos (LOLbins como `certutil.exe`, `rundll32.exe`, `wmic`).
- **Anomalías de red:** conexiones recurrentes a dominios no resueltos, beaconing periódico, tráfico hacia direcciones IP no autorizadas.

## ¿Cómo las detectamos?

Hay dos grandes aproximaciones:

### 1. Basada en reglas

Podemos definir lo que consideramos “normal” y marcar como sospechoso lo que se sale de ese rango.

**Ejemplo en Sigma:**

```yaml
detection:
  selection:
    Image: 'C:\\Windows\\System32\\cmd.exe'
    CommandLine|contains: 'whoami'
    User|endswith: '$'
  condition: selection
````

Esta regla busca la ejecución del comando whoami desde cuentas de servicio, lo cual no es habitual.

#

## 2. Basada en comportamiento (ML y UEBA)
Las plataformas modernas integran User and Entity Behavior Analytics (UEBA), que construyen un modelo base por usuario, host o grupo.
Luego analizan su comportamiento en el tiempo para detectar desvíos, sin necesidad de reglas explícitas.

## Ejemplo práctico:
El usuario juan.garcia siempre inicia sesión desde Colombia entre las 8 a.m. y 6 p.m.
Un día inicia sesión a las 2 a.m. desde una IP de Europa del Este y luego accede a una carpeta que nunca había usado.

🔎 Resultado: El sistema lo marca como una anomalía contextual y geográfica.

#

## Herramientas y técnicas que potencian esta detección
Machine Learning no supervisado: clustering, aislamiento de bosque (isolation forest), autoencoders para detectar desvíos sin entrenamiento previo.

Visualización de patrones: uso de histogramas, mapas de calor, series temporales y gráficos de dispersión para observar outliers.

Comparación de baseline histórico: comparar el día actual contra comportamiento de los últimos 30 días por usuario o sistema.

🧠 Nota: Lo importante no es detectar una anomalía cualquiera, sino una anomalía relevante, que indique una amenaza real.

## Patrones que delatan amenazas
Algunos de los patrones más comunes en hunting incluyen:

Picos anormales en la creación de procesos en un host silencioso.

Cambios súbitos en la configuración de red.

Transferencia de archivos inusuales a destinos externos.

Usuarios ejecutando comandos administrativos sin historial previo.

Tráfico repetitivo a IPs sin resolución DNS: típico de malware con C2.

#

## Cierre
La detección basada en patrones y anomalías no depende de firmas conocidas ni de alertas preconfiguradas.
Es una estrategia inteligente y adaptativa que permite detectar amenazas incluso cuando no sabemos qué estamos buscando.

Las mejores herramientas de defensa no siempre son las que más alertan, sino las que mejor entienden el comportamiento de nuestro entorno.
