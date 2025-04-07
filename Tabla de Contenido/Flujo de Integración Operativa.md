# 🧠 Punto 2: Flujo de Integración Operativa — Threat Hunting + Respuesta a Incidentes

Este flujo muestra cómo debería funcionar una organización moderna en términos de detección, análisis y respuesta frente a amenazas. No son procesos separados, sino que se interconectan en tiempo real, permitiendo actuar de forma rápida, precisa y colaborativa.

---

## 🧩 Etapas del Flujo y Roles

| Etapa | Actividad de **Threat Hunting** | Actividad de **IR (Incident Response)** |
|-------|-------------------------------|----------------------|

---

### 🔍 1. Recolección

- **Threat Hunting**:
  - Recoge información desde múltiples fuentes: logs de red, endpoints, sistemas de autenticación, SIEM, EDR, etc.
  - Analiza datos históricos y en tiempo real buscando patrones inusuales.

- **IR**:
  - Monitorea alertas generadas por las herramientas de seguridad.
  - Comienza validación si se detecta una alerta crítica.

🔧 *Ejemplo*: El hunter analiza logs DNS buscando dominios maliciosos; IR revisa alertas por inicios de sesión anómalos.

---

### 🧠 2. Hipótesis

- **Threat Hunting**:
  - Formula hipótesis basadas en TTPs o IOCs.
  - Se basa en inteligencia de amenazas o tendencias conocidas.

- **IR**:
  - Puede investigar eventos relacionados mientras espera confirmación del hunter.

🔧 *Ejemplo*: Hunter sospecha de un ataque Golden Ticket por comportamiento anómalo en Kerberos.

---

### 🚨 3. Detección

- **Threat Hunting**:
  - Encuentra actividad sospechosa que no ha sido alertada automáticamente.
  - Presenta evidencia suficiente para escalar.

- **IR**:
  - Valida si se trata de un incidente real.
  - Inicia análisis forense si es necesario.

🔧 *Ejemplo*: Hunter detecta conexión a una IP de comando y control; IR confirma el incidente.

---

### 📢 4. Comunicación

- **Threat Hunting**:
  - Entrega un informe técnico con evidencia, contexto e impacto.
  - Comunica al equipo de IR para actuar.

- **IR**:
  - Activa playbooks específicos según el tipo de amenaza.
  - Asigna tareas al equipo de respuesta.

🔧 *Ejemplo*: Se informa sobre uso de PowerShell malicioso; IR activa playbook de ejecución remota.

---

### 🤝 5. Coordinación

- **Threat Hunting**:
  - Apoya en el análisis técnico y búsqueda de otros vectores.
  - Ayuda a identificar el alcance del ataque.

- **IR**:
  - Contiene y erradica la amenaza (aislar equipos, cerrar accesos).
  - Continúa con acciones de respuesta.

🔧 *Ejemplo*: IR aísla máquina infectada; hunter busca si hay más sistemas comprometidos.

---

### 📄 6. Documentación

- **Threat Hunting**:
  - Registra hallazgos, hipótesis, patrones y resultados.
  - Mejora futuras búsquedas con base en lo aprendido.

- **IR**:
  - Documenta el incidente, acciones tomadas, línea de tiempo e impacto.
  - Extrae lecciones aprendidas.

🔧 *Ejemplo*: Se documenta vulnerabilidad en RDP sin MFA y se marca como hallazgo crítico.

---

### 📈 7. Mejora Continua

- **Threat Hunting**:
  - Refina queries, ajusta hipótesis, agrega nuevos IOCs al SIEM.
  - Crea nuevos casos de uso para futuras búsquedas.

- **IR**:
  - Actualiza políticas, reglas de firewall/EDR/SIEM.
  - Mejora playbooks y procesos de respuesta.

🔧 *Ejemplo*: Tras ataque con `certutil`, se crean reglas para detectar su uso no autorizado.

---

## 🧪 Conclusión

Cuando hunting e IR trabajan en sincronía:

- Se detectan amenazas más rápido.
- Se responde con mayor precisión.
- Se aprende y mejora constantemente.

Esta integración es clave para instituciones como el **SENA**, que buscan adaptarse a un entorno digital en constante evolución.
