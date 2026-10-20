# EcoGrid AI: módulos y tecnologías

Oct 15, 2026 · @al

## Visión y alcance

EcoGrid AI mide el consumo eléctrico, predice picos de demanda y desconecta cargas de forma automática; para la semana 12 debe funcionar de punta a punta en una versión mínima, aunque sea con datos simulados.

**Versión mínima (MVP), lo que sí o sí debe funcionar:**

1. Dos ESP32 con sensor de corriente/voltaje (PZEM-004T o ACS712+ZMPT101B) midiendo un circuito real, más un simulador en software que completa el volumen de datos y genera picos y fallas controladas.
2. Una API que recibe esas lecturas y las guarda en una base no relacional en la nube.
3. Un dashboard web que muestra el consumo en tiempo real y el historial.
4. Un modelo de IA que clasifica patrones de consumo y predice picos de demanda.
5. Un clasificador de texto que lee bitácoras de fallas y asigna una severidad (baja, media, alta).
6. Una regla de desconexión automática: si se predice un pico, el sistema apaga una carga (simulada en pantalla).
7. Monitoreo de seguridad con Syslog y SNMP, probado contra un ataque DoS.

**Extras, solo si sobra tiempo:** app móvil, algoritmo genético para optimizar, alertas por correo o Telegram, roles de usuario (administrador y operador), modo residencial e industrial.

**Decisión clave para mañana:** sí hay hardware real: dos ESP32 con sensores de energía. Van a medir un circuito real y el simulador en software completa el resto del volumen de datos (picos, fallas, más "medidores"). Eso da algo físico que mostrar en la exposición sin depender de muchos sensores reales.

## Arquitectura general

[embed: node/f5dc8013-c876]

Las lecturas entran por la API y se guardan en la nube; el Motor de IA las lee, predice picos y clasifica las bitácoras de fallas; el Control de cargas apaga lo necesario y el dashboard lo muestra, mientras Syslog y SNMP vigilan cada pieza.

## Módulos de la app

Son 9 módulos y cada uno tiene dueño natural según la materia que lleva; la columna final dice cómo saber que ya está terminado.

|   |   |   |   |   |
|---|---|---|---|---|
|#|Módulo|Qué hace|Materia|Listo cuando|
|1|Medidores (IoT + simulador)|Dos ESP32 miden un circuito real; el simulador en software completa el resto del volumen y genera picos y fallas|Fundamentos de IA + Bases de Datos|Los ESP32 reportan datos reales y el script llena el volumen|
|2|API de ingesta y consulta|Recibe lecturas, las valida y las ofrece al dashboard y a los modelos|Bases de Datos en la Nube|Dos rutas funcionando: guardar y consultar|
|3|Base de datos en la nube|Guarda las series de tiempo de forma masiva|Bases de Datos en la Nube|Miles de lecturas guardadas y consultables|
|4|Modelos de consumo|Clasifica patrones (redes neuronales, KNN, SVM, K-Means/SOM), predice picos y se optimiza con algoritmo genético|Fundamentos de IA|Predice un pico con una métrica medible|
|5|Minería de texto|Lee bitácoras y reportes de fallas y clasifica su severidad; reporta exactitud y F1-score|Minería de Texto|Clasificador entrenado y métricas en tabla|
|6|Control de cargas|Si se predice un pico, decide qué carga apagar y lo ejecuta|IA + DSM|Una carga simulada se apaga sola|
|7|Dashboard web|Muestra consumo en tiempo real, historial, alertas y estado de cargas|Desarrollo de Software|Gráfica en vivo y botón manual de desconexión|
|8|Seguridad y monitoreo|Recolecta eventos con Syslog y SNMP y resiste un ataque DoS|Seguridad Informática|Ataque simulado detectado y bloqueado|
|9|Documentación del proyecto|Justificación social, recursos y costos, y manual de uso en inglés con imperativos|Formulación de Proyectos + Inglés VI|Documento de costos y manual en PDF|

## Tecnologías por parte

La descripción del proyecto dice "plataforma web y nube", así que la web es obligatoria y la app móvil es un extra. La recomendación busca un solo lenguaje (Python) en la parte de datos e IA para que los dos grupos se entiendan. Antes de votar, revisen los planes gratuitos vigentes de cada servicio en la nube.

|   |   |   |   |
|---|---|---|---|
|Parte|Opciones|Recomendada|Por qué|
|Dashboard web|HTML + JavaScript con Chart.js · React · Vue · Flutter Web|Angular con Chart.js o ngx-charts (el equipo de DSM ya lo domina)|Aprovecha lo que el equipo ya sabe hacer; menos tiempo de curva de aprendizaje|
|App móvil (extra)|PWA (la misma web instalable) · Flutter · Kotlin (Android nativo)|Ionic con Angular, reutilizando los componentes del dashboard|Comparte código con el dashboard web; el equipo ya conoce Angular/Ionic|
|API|Flask · FastAPI · Node + Express · Django REST|Flask (ya decidido por el equipo)|Ya elegido; Python, igual que el equipo de IA|
|Tiempo real|Consultar cada pocos segundos · WebSockets · MQTT|Consultar cada pocos segundos; WebSockets si sobra tiempo|Lo más simple que se ve "en vivo"|
|Base en la nube|MongoDB Atlas · Firebase Firestore · InfluxDB Cloud · DynamoDB|MongoDB Atlas, o InfluxDB si quieren series de tiempo nativas|Cumple lo de repositorio no relacional|
|Simulador de medidores|2 ESP32 + PZEM-004T o ACS712/ZMPT101B, enviando por WiFi (HTTP POST o MQTT) · resto generado por el script de Python|ESP32 + PZEM-004T (hardware real), script Python para el resto|El ESP32 manda datos reales y el script llena el resto del volumen|
|Datos de entrenamiento|Datos simulados · dataset UCI de consumo en hogares · mezcla de ambos|Mezcla de ambos|Los reales dan realismo, los simulados dan picos controlados|
|Modelos de consumo|scikit-learn · TensorFlow/Keras · PyTorch · MiniSom (SOM)|scikit-learn para KNN, SVM y K-Means; Keras para la red neuronal; MiniSom para el SOM|Cubre todos los algoritmos del documento|
|Algoritmo genético|PyGAD · DEAP · implementación propia|PyGAD o propia|Optimiza hiperparámetros o el orden de desconexión|
|Minería de texto|TF-IDF con scikit-learn · NLTK · spaCy · BERT en español (BETO)|TF-IDF con SVM como base; BETO como mejora si hay tiempo|Primero algo que funcione, luego lo vistoso|
|Registro de eventos|rsyslog · syslog-ng · Wazuh|rsyslog|Es el estándar de Syslog en Linux|
|Monitoreo SNMP|net-snmp (snmpd) · Zabbix · LibreNMS · Grafana|net-snmp con Zabbix o Grafana para ver los datos|Muestra la red en pantalla para la exposición|
|Control de versiones|GitHub · GitLab|GitHub con ramas e issues|Se ve quién hizo qué|
|Tareas del equipo|GitHub Projects · Trello · Notion|GitHub Projects|Todo queda junto al código|

## Ciberseguridad con BlackArch

El documento pide "monitoreo continuo con Syslog y SNMP, asegurando la infraestructura contra ataques DoS". Con BlackArch ya instalado, el plan es: 1) montar el monitoreo, 2) simular el ataque desde la propia máquina con BlackArch, 3) mostrar que el sistema lo detecta.

1. **Monitoreo:** configurar `rsyslog` en el servidor o contenedor para centralizar logs, y `net-snmp` (`snmpd`) para exponer métricas de uso de red; ver todo junto en Zabbix o Grafana.
2. **Prueba de ataque:** usar herramientas de BlackArch como `hping3` o `slowloris` para simular un DoS controlado contra la API, solo en el entorno de pruebas del equipo, nunca contra un servicio ajeno.
3. **Evidencia para la materia:** capturas de los logs mostrando el pico de tráfico y, si da tiempo, una regla simple que bloquee o limite peticiones (rate limiting).

## Reparto sugerido y decisiones para votar mañana

**Propuesta de equipos (3 IA + 2 DSM):**

- **Equipo Datos e IA (3 de IA):** simulador de medidores, modelos de consumo, minería de texto. Uno de los tres puede apoyar en Formulación de Proyectos.
- **Equipo Plataforma (2 de DSM, incluyendo a quien ya sabe de APIs):** API de ingesta, base en la nube, dashboard web, control de cargas.
- **Seguridad y documentación:** se reparten entre ambos equipos porque cruzan todo el proyecto; sugerir que una persona sea responsable de que no se quede sin hacer, sin que tenga que hacerlo sola.

**Lo que hay que decidir en la reunión de mañana (1 hora):**

1. Confirmar el alcance mínimo (MVP) de la sección de Visión.
2. Asignar nombre a cada módulo de la tabla de Módulos.
3. Elegir una opción de cada fila de la tabla de Tecnologías (votar donde haya dudas).
4. Acordar la regla de uso de IA: se puede usar para acelerar, pero cada quien debe poder explicar y defender su parte.
5. Fijar fecha de entrega semanal (ej. todos los viernes) y dónde se sube el avance (GitHub).

Las 2 horas de la tarde se usan para dejar el entorno listo: crear el repositorio en GitHub, las cuentas de los servicios en la nube elegidos y el primer commit.

## Explicación a fondo de cada módulo y sus partes

Cada módulo tiene un dueño que arma la parte central, y una o dos sub-tareas reales para los compañeros de apoyo (no solo observar).

### 1. Medidores (IoT + simulador)

Dos ESP32 con sensor de corriente/voltaje miden un circuito real y mandan sus lecturas por WiFi. Un script en Python genera el resto del volumen de datos (más "medidores" simulados) y mete picos y fallas a propósito, para que haya algo que predecir y que clasificar más adelante.

- **Parte 1 — Hardware:** armar y programar los dos ESP32 (conexión del sensor, código que lee y envía por WiFi).
- **Parte 2 — Simulador:** script en Python que genera lecturas falsas con picos y fallas controladas.
- **Parte 3 — Dataset de apoyo:** integrar el dataset de consumo de hogares de UCI como fuente adicional de realismo.

### 2. API de ingesta y consulta

Recibe las lecturas de los ESP32 y del simulador, las valida y las guarda. También responde cuando el dashboard o los modelos piden datos (histórico, última lectura, etc.).

- **Parte 1 — Rutas de guardado:** recibir y validar lecturas nuevas (POST).
- **Parte 2 — Rutas de consulta:** histórico, filtros por fecha, última lectura (GET).

### 3. Base de datos en la nube

Guarda todas las lecturas como series de tiempo, en una base no relacional (MongoDB Atlas o similar), para que se puedan consultar miles de registros rápido.

- **Parte 1 — Esquema y colecciones:** cómo se guarda cada lectura (medidor, fecha, kWh, voltaje, corriente).
- **Parte 2 — Conexión y pruebas de carga:** conectar la API a la base y probar que aguanta muchas lecturas seguidas.

### 4. Modelos de consumo (IA)

Clasifica patrones de consumo y predice picos de demanda. Usa aprendizaje supervisado (red neuronal, KNN o SVM) para predecir, y no supervisado (K-Means o SOM) para agrupar patrones parecidos; un algoritmo genético ajusta los parámetros del modelo.

- **Parte 1 — Modelo principal:** entrenar el modelo que predice picos de demanda.
- **Parte 2 — Agrupamiento:** K-Means o SOM para encontrar grupos de consumo parecidos.
- **Parte 3 — Algoritmo genético:** optimizar parámetros del modelo o el orden de desconexión.

### 5. Minería de texto

Lee las bitácoras de mantenimiento y reportes de fallas (texto libre) y clasifica qué tan grave es cada incidente: baja, media o alta. Es el documento técnico de 5 puntos que ya les pidieron.

- **Parte 1 — Corpus y preprocesamiento:** redactar y limpiar 100-150 reportes de ejemplo, etiquetados por severidad.
- **Parte 2 — Vectorización y clasificador:** convertir el texto a números (TF-IDF) y entrenar el modelo que clasifica.
- **Parte 3 — Métricas y reporte:** calcular accuracy, F1-score y falsos positivos, y armar el documento de 5 puntos.

### 6. Control de cargas

Si el modelo predice un pico, decide qué carga apagar (simulada en pantalla) para evitarlo. Conecta la predicción de picos con una acción real sobre el sistema.

- **Parte 1 — Lógica de decisión:** reglas de qué apagar y cuándo, según la predicción.
- **Parte 2 — Botón manual:** que alguien pueda forzar la desconexión desde el dashboard.

### 7. Dashboard web

Muestra el consumo en tiempo real, el historial, las alertas de picos o fallas, y el estado de las cargas. Es lo que se ve en la presentación.

- **Parte 1 — Gráfica en tiempo real:** consumo actual e histórico (Angular + Chart.js).
- **Parte 2 — Alertas e historial:** lista de picos detectados, fallas clasificadas y estado de cada carga.

### 8. Seguridad y monitoreo

Vigila que la infraestructura del proyecto no se caiga por un ataque. Recolecta eventos con Syslog y SNMP, y se prueba con un ataque DoS simulado desde BlackArch.

- **Parte 1 — Monitoreo:** configurar rsyslog y net-snmp, ver los datos en Zabbix o Grafana.
- **Parte 2 — Prueba de ataque:** simular un DoS controlado y mostrar que se detecta (y, si da tiempo, que se bloquea).

### 9. Documentación del proyecto

El respaldo escrito: justificación social del proyecto, gestión de recursos y costos (Formulación de Proyectos), y el manual de uso en inglés con imperativos (Inglés VI).

- **Parte 1 — Justificación y recursos:** por qué el proyecto es socialmente responsable, qué recursos necesita y cuánto cuesta.
- **Parte 2 — Manual en inglés:** guía de uso del sistema con instrucciones (afirmativas y negativas).

## Orden de tareas y dependencias

Las 20 tareas se acomodan en 4 fases. Dentro de cada fase se pueden hacer en paralelo; entre fases hay dependencia real, no se puede saltar una.

[embed: node/b5f02af9-9c51]

|      |                                |                                                                                                                       |                                      |                                               |
| ---- | ------------------------------ | --------------------------------------------------------------------------------------------------------------------- | ------------------------------------ | --------------------------------------------- |
| Fase | Tarea                          | Qué hacer específicamente                                                                                             | Herramienta                          | Depende de                                    |
| F1   | ESP32: hardware (1.1)          | Conectar el sensor PZEM-004T (o ACS712+ZMPT101B) a cada ESP32, programar lectura y envío por WiFi cada pocos segundos | Arduino IDE / PlatformIO + PZEM-004T | —                                             |
| F1   | Simulador Python (1.2)         | Script que genera lecturas falsas con picos y fallas aleatorias, mismo formato que los ESP32                          | Python                               | —                                             |
| F1   | Esquema BD (3.1)               | Definir cómo se guarda cada lectura: medidor, fecha, kWh, voltaje, corriente, origen                                  | MongoDB Atlas                        | —                                             |
| F1   | Corpus bitácoras (5.1)         | Redactar 100-150 reportes de falla de ejemplo, etiquetados con severidad                                              | Hoja de cálculo / CSV                | —                                             |
| F1   | Monitoreo Syslog/SNMP (8.1)    | Instalar rsyslog y net-snmp; conectar a Zabbix o Grafana                                                              | rsyslog + net-snmp + Grafana         | —                                             |
| F1   | Doc: justificación (9.1)       | Justificación social, recursos y estimación de costos                                                                 | Word / Google Docs                   | —                                             |
| F2   | API: guardado (2.1)            | Endpoint POST que recibe una lectura (ESP32 o simulador) y la guarda en la base                                       | Flask                                | Esquema BD (3.1)                              |
| F2   | Conexión BD (3.2)              | Conectar Flask a MongoDB Atlas y probar que aguanta muchas lecturas seguidas                                          | Flask + MongoDB Atlas                | Esquema BD (3.1), API guardado (2.1)          |
| F2   | Vectorización texto (5.2)      | Convertir el corpus a vectores TF-IDF y entrenar el clasificador de severidad                                         | scikit-learn (TF-IDF + SVM)          | Corpus (5.1)                                  |
| F2   | API: consulta (2.2)            | Endpoints GET para histórico, filtros por fecha y última lectura                                                      | Flask                                | Conexión BD (3.2)                             |
| F3   | Modelo predicción (4.1)        | Entrenar el modelo que predice picos de demanda a partir del histórico                                                | scikit-learn / Keras                 | API consulta (2.2)                            |
| F3   | Agrupamiento K-Means/SOM (4.2) | Agrupar patrones de consumo parecidos                                                                                 | scikit-learn (K-Means) + MiniSom     | API consulta (2.2)                            |
| F3   | Métricas minería texto (5.3)   | Calcular accuracy, F1-score y falsos positivos; armar el documento técnico de 5 puntos                                | scikit-learn (metrics)               | Clasificador (5.2)                            |
| F3   | Dashboard: gráfica (7.1)       | Gráfica de consumo en tiempo real e histórico                                                                         | Angular + Chart.js                   | API consulta (2.2)                            |
| F3   | Prueba de ataque DoS (8.2)     | Simular un DoS controlado contra la API desde BlackArch y verificar que se detecta en los logs                        | hping3 / slowloris (BlackArch)       | Monitoreo (8.1), API guardado (2.1)           |
| F4   | Algoritmo genético (4.3)       | Optimizar los parámetros del modelo de predicción o el orden de desconexión de cargas                                 | PyGAD                                | Modelo predicción (4.1)                       |
| F4   | Control cargas: lógica (6.1)   | Reglas de qué carga apagar cuando se predice un pico o se detecta una falla grave                                     | Flask (lógica en la API)             | Modelo predicción (4.1), Métricas texto (5.3) |
| F4   | Control cargas: botón (6.2)    | Botón en el dashboard que fuerza la desconexión manual                                                                | Angular                              | Dashboard gráfica (7.1), Lógica (6.1)         |
| F4   | Dashboard: alertas (7.2)       | Lista de picos, fallas clasificadas y estado de cada carga                                                            | Angular                              | Lógica control cargas (6.1)                   |
| F4   | Manual en inglés (9.2)         | Guía de uso del sistema con imperativos (afirmativos y negativos)                                                     | Word / Google Docs                   | Sistema funcionando (todo lo anterior)        |
