# 🧠 Módulo 3: Metodologías y Frameworks de Threat Hunting

El Threat Hunting es una disciplina avanzada de ciberseguridad que se enfoca en la **búsqueda proactiva** de amenazas que han evadido las defensas tradicionales como antivirus, firewalls y sistemas de detección de intrusos (IDS). Este módulo detalla las metodologías utilizadas para realizar hunting estructurado y profesional.

---

## 🎯 Objetivos del Módulo

- Comprender el ciclo de vida del threat hunting.
- Aplicar metodologías basadas en hipótesis.
- Utilizar frameworks de modelado de ataques para cazar amenazas de forma efectiva.
- Integrar inteligencia de amenazas y telemetría.
- Documentar hallazgos y generar detecciones reutilizables.

---

## 🔍 Fundamentos del Threat Hunting

A diferencia de un SOC reactivo, el threat hunter **no espera alertas**. Parte de la premisa de que un atacante ya se encuentra en el sistema, y busca evidencias que confirmen o refuten esa hipótesis.

### 🧠 Mentalidad del Hunter:

- Analítica e inquisitiva.
- Familiaridad con el entorno de red y endpoints.
- Capacidad de correlacionar datos entre múltiples fuentes.
- Conocimiento de TTPs utilizados por APTs.

---

## 🧪 Ciclo de Vida del Threat Hunting

1. **Formular la hipótesis**  
   Basada en inteligencia de amenazas, comportamiento sospechoso, análisis de logs, etc.

2. **Planificar el hunt**  
   Elegir qué sistemas, logs y herramientas serán analizados.

3. **Ejecutar queries y análisis**  
   Usar herramientas como ELK, Graylog, Splunk, Velociraptor, osquery, Sigma, etc.

4. **Identificar patrones sospechosos**  
   Comportamientos como acceso fuera de horario, uso de herramientas administrativas inusuales, tráfico anómalo, etc.

5. **Validar y documentar hallazgos**  
   Confirmar actividad maliciosa o ajustar la hipótesis.

6. **Retroalimentar las defensas**  
   Crear reglas de detección (SIEM, EDR, IDS) o controles preventivos.

---

## 🛠️ Principales Frameworks de Apoyo

### 🔹 MITRE ATT&CK

📘 **Adversarial Tactics, Techniques and Common Knowledge**  
Una base de conocimiento que mapea las tácticas y técnicas utilizadas por los adversarios en el mundo real.

#### Beneficios:
- Permite generar hipótesis por técnica.
- Ayuda a mapear cobertura de detecciones.
- Es útil para comparar la madurez del SOC y establecer prioridades.

🔗 https://attack.mitre.org/

---

### 🔹 Cyber Kill Chain

Desarrollado por Lockheed Martin, organiza el ataque en 7 fases secuenciales, útil para interceptar al atacante en fases tempranas.

| Fase | Descripción |
|------|-------------|
| Reconocimiento | Recolección de información del objetivo |
| Armamento | Creación del malware/exploit |
| Entrega | Envío del malware al objetivo |
| Explotación | Ejecución del payload |
| Instalación | Persistencia del malware |
| C2 | Comunicación con el atacante |
| Acción | Robo, destrucción, manipulación de datos |

🔗 https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html

---

### 🔹 Diamond Model

Modelo de análisis de intrusiones que considera cuatro nodos clave: **Adversary**, **Infrastructure**, **Capability** y **Victim**. Muy útil para relacionar campañas, APTs y ataques dirigidos.

---

## 🧩 Tipos de Hipótesis en Threat Hunting

- **Basadas en amenazas conocidas**: “Se ha detectado actividad de APT29 en entornos similares, ¿estamos expuestos?”
- **Basadas en comportamientos anómalos**: “Hemos visto uso de PowerShell con argumentos sospechosos en horarios inusuales.”
- **Basadas en gaps de visibilidad**: “No tenemos cobertura sobre registros DNS internos. ¿Hay exfiltración de datos vía DNS tunneling?”

---

## ⚒️ Herramientas Comunes en el Hunting

| Herramienta | Uso |
|------------|-----|
| Velociraptor | DFIR y queries forenses |
| Splunk / Graylog | Correlación y análisis de logs |
| Sigma | Lenguaje común para reglas de detección |
| Osquery | Inspección de sistemas con SQL |
| Wireshark / Zeek | Análisis de tráfico |
| ELK Stack | Telemetría y dashboards |
| YARA | Identificación de malware |

---

## 📈 Métricas de Éxito en Threat Hunting

- Nuevas detecciones desarrolladas.
- Tiempo medio para validar hipótesis (MTTH).
- Casos de uso añadidos al SIEM.
- Número de hipótesis investigadas por ciclo.
- Tiempo promedio para identificar actividad maliciosa (MTTI).

---

## 📘 Recursos Recomendados

- [The Threat Hunter Playbook](https://github.com/ThreatHuntingProject/ThreatHunter-Playbook)
- [Hunting EL Framework](https://posts.specterops.io/hunting-el-framework-4aee2f1d2f2e)
- [MITRE D3FEND (defensivo)](https://d3fend.mitre.org/)
- [Detection Engineering](https://detectionengineering.net/)
- [Purple Teaming Tools](https://github.com/topics/purple-teaming)

---

## ✅ Conclusión

El threat hunting no es magia, es método. Invertir en esta práctica mejora significativamente la detección temprana de amenazas, fortalece la postura defensiva y promueve la mejora continua. Frameworks como MITRE ATT&CK y la Kill Chain son pilares esenciales para darle estructura y enfoque al hunting.

---

📂 *Volver al [README principal](../README.md)*
