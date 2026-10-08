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
	
	
### Amenaza 1 : inyeccion SQL

	una vulnerabilidad critica donde un atacante interfiere con las consultas que una app realiza a su base de datos . permite la manipulación o extracción no autorizada de datos confidenciales al insertar comandos maliciosos dentro de campos de entrada de texto que la app asume como seguros.

### Vulnerando la autenticación
	paso 1 : el atacante ingresa la cadena or "1" = 1 en el campo contraseña  
	paso 2 : El servidor web procesa la entrada sin validar ni sonetizarla 
	paso 3: La base de datos evalua la condicion como verdadera para todos los usarios
	Impacto: el sistema concede acceso administrativo al atacante sin requerir una credencial valida 


### Amenaza 2 : Cross site Scripting 

	Conocido como xss es un ataque de inyeccion donde scripts maliciosos se insertan en sitios web benignos y de confianza . a diferencoa de SQLi , el objetivo aqui no es el servidor , si no el navegador del usuario final explotando la confianza que el usuario tiene en el sitio .


