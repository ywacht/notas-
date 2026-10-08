	Un **SIEM** (_Security Information and Event Management_) es una plataforma que recolecta, centraliza y analiza los registros (logs) y eventos de seguridad de todos los sistemas de una organización, para detectar amenazas en tiempo real y facilitar la respuesta a incidentes.

## Qué hace

	- **Recolección de logs:** reúne datos de firewalls, servidores, endpoints, antivirus, aplicaciones, routers, servicios en la nube, etc.
	- **Normalización:** convierte formatos distintos de logs a uno común para poder compararlos.
	- **Correlación de eventos:** relaciona eventos aparentemente aislados para detectar patrones de ataque. Por ejemplo, 50 intentos de login fallidos seguidos de uno exitoso desde otro país.
	- **Alertas:** avisa al equipo de seguridad (SOC) cuando se cumple una regla o se detecta una anomalía.
	- **Dashboards y reportes:** visualización del estado de seguridad y reportes de cumplimiento (ISO 27001, PCI-DSS, etc.).
	- **Análisis forense:** permite investigar qué pasó después de un incidente porque conserva el historial de eventos.

## Su nombre viene de dos funciones

	- **SIM** (gestión de información de seguridad): almacenamiento y análisis de logs a largo plazo.
	- **SEM** (gestión de eventos de seguridad): monitoreo y alertas en tiempo real.

**Herramientas conocidas**

- **Splunk**
- **IBM QRadar**
- **Microsoft Sentinel**
- **Elastic Security (ELK)**
- **Wazuh** (open source, muy usado para aprender)
- **Graylog** (open source)

	**Ejemplo práctico**

	Un atacante intenta entrar por fuerza bruta a un servidor. El SIEM recibe los logs de autenticación, detecta decenas de fallos en poco tiempo desde la misma IP, genera una alerta y el analista del SOC puede bloquear esa IP y revisar si hubo acceso exitoso.

	Si quieres practicar, Wazuh o el stack ELK se pueden montar en una máquina virtual o directamente en Linux para ver cómo funciona un SIEM de forma real.

	: BlackArch tiene más de 2,800 herramientas, pero casi todas son **ofensivas** (pentesting, redes, forense, ingeniería inversa, etc.). Para SIEM en específico hay poco, porque no es su enfoque.

	- **Wazuh, Splunk, QRadar, Sentinel:** no son parte de BlackArch. Wazuh se instala desde el AUR o con sus propios repos.
	- **ELK (Elasticsearch, Logstash, Kibana):** están en los repos de Arch o en el AUR, no en BlackArch.
	- **Graylog:** tampoco está en BlackArch, se instala aparte.

Lo que sí hay en BlackArch relacionado con el lado defensivo o de análisis:

	- **Forense:** volatility, autopsy, binwalk, foremost, etc.
	- **Análisis de red:** wireshark, tcpdump, ettercap, etc.
	- **Detección de intrusos y análisis de tráfico:** algunas herramientas tipo IDS/sniffers.

	Para ver qué hay exactamente, puedes usar los grupos de BlackArch:

bash

```bash
pacman -Sg | grep blackarch          # lista todos los grupos
pacman -Sg blackarch-defensive       # herramientas defensivas
pacman -Sg blackarch-forensic        # herramientas forenses
pacman -Ss <nombre>                  # buscar una herramienta concreta
```

	Si lo que quieres es practicar con un SIEM, lo más práctico es instalar **Wazuh** o **ELK** aparte (en una VM o con Docker) y usar las herramientas de BlackArch para generar ataques de prueba, como fuerza bruta con hydra o escaneos con nmap. Así ves cómo el SIEM detecta lo que tú mismo provocas.
	
### Atributos del Sistema

(Es la descripción de las cuatro funciones clave de un SIEM, justo lo que vimos antes.)

**Agregación**  
Recolección masiva y centralizada de datos y bitácoras (syslog, SNMP).

**Correlación**  
Conexión analítica de eventos aparentemente aislados para detectar patrones maliciosos.

**Alertamiento**  
Notificaciones automáticas y en tiempo real basadas en reglas de seguridad predefinidas.

**Retención**  
Almacenamiento inmutable a largo plazo para auditorías de cumplimiento y análisis forense.

**Mis comentarios**

- **Agregación:** _syslog_ es el protocolo estándar para enviar logs desde servidores, firewalls y equipos de red. _SNMP_ se usa sobre todo para monitorear dispositivos de red (switches, routers), y puede mandar _traps_ (avisos de eventos). Por eso un SIEM necesita **normalizar**: cada fuente habla en un formato distinto.
- **Correlación:** es lo que distingue a un SIEM de un simple almacén de logs. Un solo login fallido no dice nada, pero 50 fallos seguidos y luego un acceso exitoso desde otro país sí es un patrón.
- **Alertamiento:** "reglas predefinidas" significa que la calidad de las alertas depende de qué tan bien estén afinadas las reglas. Reglas malas generan muchos **falsos positivos** y el analista termina ignorando las alertas (_alert fatigue_).
- **Retención:** "inmutable" quiere decir que los logs no se pueden alterar ni borrar, lo cual es clave porque un atacante suele intentar borrar sus huellas. Los periodos de retención suelen venir de normativas como PCI-DSS o ISO 27001.

### Diapositiva 2: ¿Qué son las Amenazas?

_(Título superior: "Premium Tactical Briefing")_

"Una amenaza cibernética es cualquier evento potencial, ya sea malicioso o accidental, que busca explotar una vulnerabilidad (en sistemas, redes o factor humano) para comprometer la confidencialidad, integridad o disponibilidad de los activos de la organización."

El diagrama muestra flechas rojas (amenazas) apuntando hacia un círculo central azul "Activos de la organización", con la etiqueta "Vulnerabilidad" señalando el punto por donde entran.

**Mis comentarios**

- La definición menciona la **tríada CIA**: Confidencialidad, Integridad y Disponibilidad. Es la base de casi todo en ciberseguridad y es muy probable que la pregunten en examen.
- Distingue bien tres conceptos que suelen confundirse:
    - **Activo:** lo que se quiere proteger (datos, servidores, personas).
    - **Vulnerabilidad:** una debilidad (software sin parchar, contraseña débil, un empleado sin capacitación).
    - **Amenaza:** lo que puede explotar esa debilidad.
    - Cuando una amenaza explota una vulnerabilidad se materializa el **riesgo**.
- La diapositiva dice "malicioso o accidental": una amenaza no siempre es un hacker. Un empleado que borra una base de datos por error o un desastre natural también cuentan.
- En el diagrama, las flechas rojas no cruzan el círculo punteado en todos lados, solo donde hay vulnerabilidad. Es una forma visual de entender que sin vulnerabilidad, la amenaza no logra comprometer el activo.