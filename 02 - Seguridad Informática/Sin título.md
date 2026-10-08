---

tags:

- ciberseguridad
- SIEM
- amenazas fecha: 2026-10-08 materia: Ciberseguridad

---

# SIEM y Amenazas

> [!NOTE] <!--easygit-callout:original=abstract,collapse=--> Resumen Un [[SIEM]] (_Security Information and Event Management_) centraliza y analiza logs y eventos de seguridad para detectar amenazas en tiempo real. Una [[Amenaza]] es cualquier evento potencial que busca explotar una [[Vulnerabilidad]] para comprometer la [[Tríada CIA]] de los activos.

---

## 1. Atributos del Sistema (SIEM)

Las cuatro funciones clave de un SIEM.

### Agregación

> [!quote] Diapositiva Recolección masiva y centralizada de datos y bitácoras (syslog, SNMP).

- **syslog** es el protocolo estándar para enviar logs desde servidores, firewalls y equipos de red.
- **SNMP** se usa sobre todo para monitorear dispositivos de red (switches, routers) y puede mandar _traps_ (avisos de eventos).
- Por eso un SIEM necesita **normalizar**: cada fuente habla en un formato distinto.

### Correlación

> [!quote] Diapositiva Conexión analítica de eventos aparentemente aislados para detectar patrones maliciosos.

- Es lo que distingue a un SIEM de un simple almacén de logs.
- Un solo login fallido no dice nada, pero 50 fallos seguidos y luego un acceso exitoso desde otro país sí es un patrón.

### Alertamiento

> [!quote] Diapositiva Notificaciones automáticas y en tiempo real basadas en reglas de seguridad predefinidas.

- La calidad de las alertas depende de qué tan bien estén afinadas las reglas.
- Reglas malas generan muchos **falsos positivos** y el analista termina ignorando las alertas (_alert fatigue_).

### Retención

> [!quote] Diapositiva Almacenamiento inmutable a largo plazo para auditorías de cumplimiento y análisis forense.

- **Inmutable** = los logs no se pueden alterar ni borrar. Es clave porque un atacante suele intentar borrar sus huellas.
- Los periodos de retención suelen venir de normativas como **PCI-DSS** o **ISO 27001**.

---

## 2. ¿Qué son las Amenazas?

_(Título superior de la diapositiva: "Premium Tactical Briefing")_

> [!quote] Definición (diapositiva) Una amenaza cibernética es cualquier evento potencial, ya sea malicioso o accidental, que busca explotar una vulnerabilidad (en sistemas, redes o factor humano) para comprometer la confidencialidad, integridad o disponibilidad de los activos de la organización.

**Diagrama:** flechas rojas (amenazas) apuntan hacia un círculo central azul "Activos de la organización". La etiqueta "Vulnerabilidad" señala el punto por donde entran.

### Tríada CIA

> [!IMPORTANT] <!--easygit-callout:original=important,collapse=--> Posible pregunta de examen La definición menciona la **tríada CIA**, base de casi todo en ciberseguridad.

|Letra|Principio|Significa|
|---|---|---|
|**C**|Confidencialidad|Solo accede quien debe|
|**I**|Integridad|Los datos no se alteran sin autorización|
|**A**|Disponibilidad|Los sistemas y datos están accesibles cuando se necesitan|

### Conceptos que se confunden

|Concepto|Qué es|Ejemplo|
|---|---|---|
|**Activo**|Lo que se quiere proteger|Datos, servidores, personas|
|**Vulnerabilidad**|Una debilidad|Software sin parchar, contraseña débil, empleado sin capacitación|
|**Amenaza**|Lo que puede explotar esa debilidad|Atacante, malware, error humano|
|**Riesgo**|Se materializa cuando una amenaza explota una vulnerabilidad|Fuga de datos, caída del servicio|

> [!TIP] <!--easygit-callout:original=tip,collapse=--> Notas
> 
> - "Malicioso o accidental": una amenaza no siempre es un hacker. Un empleado que borra una base de datos por error o un desastre natural también cuentan.
> - En el diagrama, las flechas no cruzan el círculo punteado en todos lados, solo donde hay vulnerabilidad. **Sin vulnerabilidad, la amenaza no logra comprometer el activo.**

---

## Relacionado

- [[SIEM]]
- [[Tríada CIA]]
- [[Wazuh]] / [[ELK Stack]] (para practicar un SIEM)