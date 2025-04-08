# Casos Reales Recientes de Threat Hunting

Estos casos representan situaciones reales donde el threat hunting fue clave para detectar amenazas avanzadas que habían evadido controles automatizados. Analizamos su contexto, técnicas utilizadas y lecciones aprendidas.

---

## 🧠 Caso 1: SUNBURST - Ataque a la cadena de suministro de SolarWinds (2020)

### 🧩 Descripción
Los atacantes comprometieron el sistema de compilación de SolarWinds, inyectando un backdoor llamado **SUNBURST** en actualizaciones del software **Orion**, ampliamente utilizado en redes empresariales y gubernamentales.

### 🧰 Técnicas y tácticas (según MITRE ATT&CK):
- **T1195.002**: Compromiso de la cadena de suministro.
- **T1071.001**: Comunicación C2 a través de HTTPS.
- **T1557.001**: Escucha de credenciales (LLMNR/NBT-NS Spoofing).
- **T1552.001**: Exfiltración de credenciales de memoria (Mimikatz).

### 🧠 Relevancia para Threat Hunting:
- El malware evadía EDRs y firmas conocidas.
- Solo se detectó gracias a análisis de tráfico de red e identidad inusual.
- Se usaron patrones de comportamiento como consultas DNS anómalas y conexiones persistentes desde sistemas de administración.

### 📘 Fuentes:
- FireEye, Microsoft, US-CERT, Volexity

---

## 🧠 Caso 2: Log4Shell (CVE-2021-44228)

### 🧩 Descripción
Una vulnerabilidad crítica en Apache Log4j permitía la ejecución remota de código (RCE) con una simple cadena enviada en cabeceras HTTP o campos de usuario.

### 🧰 Técnicas y tácticas:
- **T1190**: Explotación de vulnerabilidades en aplicaciones públicas.
- **T1059.001**: Comandos vía intérprete de comandos.
- **T1105**: Descarga de herramientas maliciosas desde dominios temporales.
- **T1027**: Evasión mediante cifrado y ofuscación.

### 🧠 Relevancia para Threat Hunting:
- Antes de las firmas, hunters identificaron patrones de payloads en logs HTTP (JNDI:ldap://...).
- Permite construir reglas Sigma para búsqueda retroactiva en logs históricos.
- Se descubrió uso de Log4Shell para ejecutar Monero miners y establecer reverse shells.

### 📘 Fuentes:
- LunaSec, Cloudflare, Elastic Security, SANS

---

## 🧠 Caso 3: APT29 / Nobelium – Compromiso de Microsoft Exchange & Azure AD

### 🧩 Descripción
APT29 (grupo asociado al gobierno ruso) realizó campañas de spear phishing y uso de credenciales válidas para acceder a entornos de Microsoft Exchange, Azure y SharePoint.

### 🧰 Técnicas y tácticas:
- **T1078**: Uso de cuentas válidas (con MFA y sin MFA).
- **T1071.004**: Uso de protocolos estándar (HTTPS, IMAP) para C2.
- **T1041**: Exfiltración de datos vía canales cifrados.
- **T1210**: Explotación de servicios remotos.

### 🧠 Relevancia para Threat Hunting:
- Actividad detectada revisando flujos de red desde endpoints no privilegiados accediendo a APIs administrativas.
- Se utilizaron técnicas como impersonación de tokens OAuth y uso de certificados autofirmados.
- Se identificaron conexiones sospechosas entre endpoints internos y recursos en la nube fuera de horas laborales.

### 📘 Fuentes:
- Microsoft Threat Intelligence, Mandiant, Volexity

---

## 🧠 Caso Extra: Hafnium – Ataques masivos a Microsoft Exchange (2021)

### 🧩 Descripción
El grupo chino Hafnium explotó múltiples vulnerabilidades en Microsoft Exchange on-premise, logrando ejecución remota, persistencia y exfiltración de correos.

### 🧰 Técnicas y tácticas:
- **T1190**: Explotación de vulnerabilidades (ProxyLogon).
- **T1059.001**: PowerShell para despliegue de webshells.
- **T1505.003**: Instalación de webshells en servidores IIS.
- **T1003**: Dumping de LSASS y extracción de hashes.

### 🧠 Relevancia para Threat Hunting:
- Muchos servidores quedaron comprometidos antes de los parches.
- Threat hunters detectaron procesos anómalos (w3wp.exe ejecutando cmd.exe) y creación de archivos ASPX en carpetas no estándar.
- Se identificaron patrones de tráfico hacia IPs chinas desde Exchange sin precedentes.

### 📘 Fuentes:
- Microsoft, RiskIQ, Palo Alto Unit42

---

## 🧾 Conclusión

Los casos analizados demuestran que el threat hunting no es un lujo, sino una **necesidad estratégica** frente a amenazas avanzadas. Las técnicas usadas por los atacantes son cada vez más sofisticadas, silenciosas y adaptativas. Solo mediante análisis humano proactivo y contextualizado es posible detectarlas antes de que el daño sea irreversible.
