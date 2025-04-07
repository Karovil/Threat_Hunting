# 🧪 Ejemplo Práctico: Uso de un EDR en un Proceso de Threat Hunting

---

## 🧠 Contexto del Caso

Imagina que eres parte del equipo **Blue Team** de una empresa financiera.  
El **Blue Team** es el encargado de **la defensa activa de la infraestructura TI**, lo que incluye monitorear, detectar y responder a incidentes de seguridad.

Recientemente, se ha recibido una alerta desde el EDR (por ejemplo, Wazuh o CrowdStrike) informando sobre **actividad sospechosa en un endpoint crítico**.

---

## 🎯 Objetivos del Threat Hunting

El proceso de **Threat Hunting** (caza de amenazas) busca **identificar amenazas avanzadas** que han evadido las defensas tradicionales como antivirus o firewalls.

Objetivos de este caso:

- Determinar si la alerta corresponde a una amenaza real o falso positivo.
- Identificar el alcance del incidente (otros usuarios, máquinas afectadas).
- Aplicar medidas de contención inmediatas.
- Documentar el incidente y reforzar los controles preventivos.

---

## 🔍 Fase 1: Detección Inicial

El EDR genera una alerta con la siguiente información:

- **Proceso detectado:** `powershell.exe`
- **Argumentos sospechosos:** `-enc JAB...` (cadena en Base64)
- **Usuario:** `usuario-finanzas01`
- **IP:** `192.168.10.23`
- **Hora:** `03:24 AM`

Esto puede indicar un intento de ejecución de **PowerShell ofuscado**, una técnica común en malware fileless.

---

## 🔬 Fase 2: Análisis con el EDR

Se realiza una investigación usando las capacidades del EDR:

- **Árbol de procesos:**  
  Identificar si `powershell.exe` fue lanzado por otro proceso (p. ej. `explorer.exe` o `outlook.exe`), y si generó procesos hijos.

- **Consultas de integridad de archivos:**  
  Buscar archivos modificados en:
  - `%APPDATA%`
  - `%TEMP%`
  - Claves del registro sospechosas

- **Reglas YARA / Coincidencia con IOCs:**  
  Comparar el comportamiento con firmas de malware conocidas.

- **Persistencia:**  
  Verificar si se crearon mecanismos de persistencia como:
  - Tareas programadas
  - Servicios nuevos
  - Claves en `HKCU\\Software\\Microsoft\\Windows\\CurrentVersion\\Run`

---

## 🧯 Fase 3: Respuesta

Acciones tomadas desde la consola del EDR:

- 🛑 **Aislamiento del endpoint** para evitar propagación lateral.
- 📁 **Recolección de artefactos**:
  - Dump de memoria
  - Logs de eventos
  - Archivos sospechosos
- 📄 **Snapshot del sistema** (estado del equipo en ese momento).
- 👤 **Cambio de contraseña** del usuario comprometido.

---

## 📈 Fase 4: Lecciones y Recomendaciones

- Crear una **regla de detección** para alertar cuando se use PowerShell con el argumento `-enc`.
- **Restringir PowerShell** solo para usuarios administradores.
- **Actualizar IOCs** y firmas del EDR periódicamente.
- Hacer un **barrido completo de la red** para detectar otros endpoints con actividad similar.

---

## 📌 Herramientas Complementarias

Además del EDR, pueden usarse herramientas de apoyo como:

- **Sysmon:** Para monitorear procesos y conexiones en Windows.
- **ELK Stack:** Para centralizar logs y correlacionar eventos.
- **Osquery:** Consultas SQL sobre el estado del sistema (procesos, puertos, servicios, etc).

