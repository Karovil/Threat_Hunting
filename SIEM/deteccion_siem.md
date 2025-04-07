# 🛡️ Detección de Amenazas con SIEM

---

## ❓ ¿Cómo detecta amenazas un SIEM?

Un **SIEM (Security Information and Event Management)** utiliza correlación de eventos y análisis de logs para identificar actividades sospechosas o maliciosas dentro de un entorno TI.  

La detección puede hacerse:

- En **tiempo real**
- O mediante **análisis retrospectivo** de registros

---

## 🔍 ¿Qué analiza un SIEM?

El SIEM evalúa grandes volúmenes de datos en busca de:

- Actividades anómalas
- Indicadores de Compromiso (IoCs)
- Comportamientos maliciosos (por reglas o IA)
- Coincidencias con firmas conocidas

---

## 🧠 Métodos de Detección

### 🔎 Basada en Reglas (Detección por Firma)

Se configuran **reglas predefinidas o personalizadas** para detectar patrones específicos.

**Ejemplos:**

- Más de 5 intentos de inicio de sesión fallidos desde una misma IP en 1 minuto.
- Acceso a servidores fuera del horario laboral.

**✅ Ventajas:**  
- Alta precisión  
- Baja latencia  

**⚠️ Desventajas:**  
- No detecta amenazas desconocidas (zero-day)

---

### 🧠 Basada en Comportamiento (UEBA)

**UEBA** = User and Entity Behavior Analytics

Utiliza machine learning para detectar **comportamientos fuera de lo común**, incluso si no hay reglas definidas.

**Ejemplos:**

- Un usuario que siempre accede desde Colombia ahora inicia sesión desde Rusia.
- Un empleado descarga 10 GB de datos inesperadamente.

**✅ Ventajas:**  
- Detecta amenazas avanzadas y desconocidas

**⚠️ Desventajas:**  
- Puede generar falsos positivos

---

## 📋 Ejemplos de Reglas de Detección

### 🛡️ Fuerza Bruta (Brute Force Login)

- **Evento:** Múltiples intentos fallidos de autenticación  
- **Condición:** > 5 fallos por el mismo usuario en 1 minuto  
- **Acción:** Generar alerta y bloquear IP temporalmente

---

### 🎯 Movimiento Lateral

- **Evento:** Múltiples conexiones RDP desde una IP hacia distintos hosts  
- **Condición:** > 3 hosts en 10 minutos  
- **Acción:** Alerta crítica + aislamiento del host

---

### 🌐 Beaconing (C2)

- **Evento:** Conexiones repetidas a una misma IP externa a intervalos regulares  
- **Condición:** Una conexión cada X segundos  
- **Acción:** Alertar y bloquear tráfico saliente

---

## 🧩 Priorización de Alertas

Los SIEM permiten clasificar alertas según su nivel de severidad:

| Nivel | Descripción |
|-------|-------------|
| 🔴 **Crítica** | Indicador claro de compromiso (explotación, exfiltración) |
| 🟠 **Alta**     | Comportamiento sospechoso que requiere atención inmediata |
| 🟡 **Media**    | Posibles falsos positivos, pero relevantes |
| 🟢 **Baja**     | Informativa, sin riesgo inmediato |

Los analistas priorizan en función de estas categorías.

---

## 🔧 Herramientas de Apoyo

- **MITRE ATT&CK**: Framework de tácticas y técnicas de adversarios.
- **YARA**: Reglas para detección en archivos o logs.
- **IOC Feeds**: Listas de hashes, dominios, IPs o URLs maliciosas.

---

## 🧪 Casos Prácticos

### 📁 Caso 1: Exfiltración de Datos

- Se detecta una transferencia anómala de archivos hacia una IP no autorizada.
- El acceso fue precedido por login con credenciales comprometidas.

**✅ Resultado:**  
Alerta crítica + respuesta inmediata

---

### 🔓 Caso 2: Uso de Cuentas Dormidas

- Cuenta de empleado inactivo se usa a las 3 a.m. desde otra geolocalización.
- Actividad fuera de perfil habitual del usuario.

**✅ Resultado:**  
Bloqueo automático + investigación forense

---

