### 🧠 Módulo 3: Metodologías y Frameworks de Threat Hunting

Este módulo aborda las principales metodologías y frameworks utilizados en el proceso de Threat Hunting. Su objetivo es guiar a los analistas en la detección proactiva de amenazas mediante un enfoque sistemático y basado en hipótesis.

---

#### 🧩 ¿Qué es una metodología de Threat Hunting?

Las metodologías en Threat Hunting proporcionan una estructura para identificar, investigar y mitigar amenazas que evaden las defensas tradicionales. Estas metodologías combinan el conocimiento de las amenazas, la experiencia del analista y el uso de herramientas avanzadas para descubrir actividades maliciosas ocultas.

---

#### 🧪 Planteamiento de hipótesis

El Threat Hunting se basa en el **planteamiento de hipótesis**, es decir, suposiciones razonables sobre posibles ataques basadas en:

- Inteligencia de amenazas (Threat Intelligence)
- Resultados de investigaciones previas
- Comportamientos anómalos en los logs
- Frameworks como MITRE ATT&CK

> Ejemplo: "Es posible que un atacante esté utilizando cuentas legítimas para moverse lateralmente en la red sin ser detectado."

---

#### ⚙️ Frameworks clave utilizados

##### 1. MITRE ATT&CK
- Base de datos de TTPs (Técnicas, Tácticas y Procedimientos) usados por actores maliciosos.
- Clasifica comportamientos de ataque como ejecución, persistencia, movimiento lateral, evasión de defensas, etc.
- Es útil para identificar **qué** buscar y **cómo** correlacionar eventos.

[🔗 Ver MITRE ATT&CK](https://attack.mitre.org/)

##### 2. Cyber Kill Chain (Lockheed Martin)
- Modelo de 7 etapas que describe la secuencia típica de un ciberataque.
- Sirve para detectar y detener ataques en fases tempranas.

Etapas:
1. Reconocimiento
2. Armamento
3. Entrega
4. Explotación
5. Instalación
6. Comando y Control (C2)
7. Acciones sobre objetivos

##### 3. Diamond Model of Intrusion Analysis
- Analiza un incidente considerando cuatro elementos clave: adversario, víctima, infraestructura y capacidad.
- Permite ver patrones y relaciones entre múltiples incidentes.

---

#### 🛠️ Ciclo del Threat Hunting

1. **Preparación**: definir hipótesis y seleccionar fuentes de datos.
2. **Recolección y análisis**: usar herramientas como SIEM, EDR y scripts personalizados.
3. **Detección de patrones**: correlacionar eventos y detectar comportamientos sospechosos.
4. **Respuesta**: documentar hallazgos, generar alertas y mejorar reglas de detección.
5. **Retroalimentación**: refinar hipótesis futuras y actualizar procedimientos.

---

#### 📌 Beneficios de seguir una metodología

- Aumenta la efectividad y consistencia del hunting.
- Permite detectar amenazas avanzadas (APT) que evaden detección tradicional.
- Fomenta la mejora continua y la madurez del equipo de ciberseguridad.

---

#### 💬 Frase para reflexionar

> “Threat hunting no se trata de buscar algo que ya sabés que está ahí… se trata de encontrar lo que aún no sabés que existe.” — Analista desconocido pero sabio 😄

---

