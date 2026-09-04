enfoques de inteligencia artificial


---
## Clasificasion de los enfoques 
la literaturaa clasica de la inteligencia artificial define el diseno de un sistema inteligente basandoinos en dos tensiones fundamentales 

filidelidad humana frente a  relacionalidad matematicaa 

procesos de pensamiento frente a comportamiento obserbable 

---
## PENSAR COMO HUMANO

1. DEFINICION Enfoque congnitivo que busca replicar la funcionalidad exacta del pensamiento humano en modelos computacionales
2. OBJETIVO: determinado como piensqa los humanos para construir maquinas con procesos internos equivalentes .
3. METODOS DE VALIDACION :introduccion experimentcion pscologicos y modelado cognitivo .  



## Actuar como Humanos (Test de Turing)

1. **Definición:** Enfoque que busca que las máquinas exhiban un comportamiento inteligente indistinguible del de un humano ante un observador externo, sin importar cómo se logre internamente ese comportamiento.
2. **Objetivo:** Crear máquinas que realicen acciones que, si las hiciera un humano, requerirían inteligencia (Test de Turing de Alan Turing, 1950).
3. **Disciplinas necesarias:**
    - Procesamiento de lenguaje natural (para comunicarse)
    - Representación del conocimiento (para almacenar lo que sabe o escucha)
    - Razonamiento automático (para responder preguntas y sacar conclusiones)
    - Aprendizaje automático (para adaptarse a nuevas circunstancias)
    - Visión artificial y robótica (para el Test de Turing total, que añade percepción y manipulación de objetos)


## Pensar Racionalmente (Leyes del pensamiento)

1. **Definición:** Enfoque basado en la lógica formal, que busca que las máquinas razonen de manera correcta siguiendo reglas lógicas explícitas ("leyes del pensamiento"), independientemente de si eso imita o no al pensamiento humano.
2. **Objetivo:** Usar la lógica (silogismos, lógica proposicional y de predicados) para representar el conocimiento y derivar conclusiones correctas mediante procesos de inferencia formal.
3. **Limitaciones históricas:**
    - Es muy difícil traducir el conocimiento informal (del mundo real) a términos lógicos formales, especialmente cuando hay incertidumbre.
    - Resolver un problema "en principio" (con lógica) es distinto de resolverlo "en la práctica": muchos problemas se vuelven intratables computacionalmente al crecer el número de variables o hechos (explosión combinatoria).
    - No maneja bien el conocimiento incierto o probabilístico, típico de situaciones reales.
## Actuar Racionalmente (Agente Racional)

1. **Definición:** Enfoque que define la inteligencia artificial como el diseño de agentes racionales: sistemas que actúan de forma que logran el mejor resultado esperado (o el mejor resultado esperado dada la incertidumbre) según sus percepciones y el conocimiento disponible.
2. **Objetivo:** Construir agentes que, a partir de lo que perciben del entorno, elijan siempre la acción que maximice el logro de sus metas u objetivos, sin necesidad de replicar el pensamiento humano ni seguir estrictamente leyes lógicas formales.
3. **Ventajas / características principales:**
    - Es más general que el enfoque de "leyes del pensamiento", porque la racionalidad correcta no siempre depende de una inferencia lógica correcta (a veces no hay una acción "provablemente correcta" y aun así hay que actuar).
    - Es más susceptible al desarrollo científico riguroso que los enfoques basados en el comportamiento o el pensamiento humano, ya que el estándar de racionalidad está definido con claridad matemática.
    - Permite incorporar razonamiento lógico como una herramienta más (no la única) al servicio de la acción racional, junto con otras capacidades como el aprendizaje o la percepción.


|                     | Pensar como humanos       | Actuar como humano    | Pensar racionalment             | Actuar Racionalmente  |
| ------------------- | ------------------------- | --------------------- | ------------------------------- | --------------------- |
| objetivo            | replica cognicion         | emular comportamiento | Logica irrefutable              | maximissar utilidad   |
| Base teorica        | Psicologia y neurociencia | prueba de turing      | filosofia y silogismo           | teoria de la decision |
| Principal ventaja   | cercania biologica        | Enfoque empirico      | exactitud demostable            | optimisasion fexible  |
| Limitacioness Clave | Cerebro incompensable     | engano superficial    | intractibilidad e incertidumbre | Costa computacional   |
### Resumen y Conclusiones

A lo largo de la historia de la Inteligencia Artificial, los cuatro enfoques presentados han organizado el campo en torno a dos grandes tensiones:

- **Fidelidad humana vs. racionalidad matemática:** ¿queremos que la máquina piense/actúe _como un humano_, o que piense/actúe de forma _ideal según la lógica o la utilidad_?
- **Procesos internos vs. comportamiento observable:** ¿nos importa _cómo_ razona el sistema por dentro, o solo _qué resultados_ produce hacia afuera?

De la combinación de estas dos tensiones surgen los cuatro enfoques:

||Fidelidad humana|Racionalidad matemática|
|---|---|---|
|**Procesos internos (pensar)**|Pensar como humanos|Pensar racionalmente|
|**Comportamiento (actuar)**|Actuar como humanos|Actuar racionalmente|

**Conclusiones principales:**

1. Los enfoques centrados en **imitar al humano** (pensar y actuar como humanos) son valiosos para entender la cognición y crear sistemas que se comuniquen naturalmente con las personas, pero dependen de la psicología, son difíciles de validar científicamente y están limitados por lo que aún no comprendemos del cerebro.
2. Los enfoques basados en **leyes del pensamiento** aportan rigor lógico y demostrabilidad, pero chocan con la dificultad de formalizar el conocimiento del mundo real y con la explosión combinatoria al escalar los problemas.
3. El enfoque de **agente racional** es, en la práctica, el que domina la IA moderna: es más general que la lógica pura (permite actuar incluso sin certeza absoluta), es más flexible que imitar al humano (no exige replicar sus errores o limitaciones), y se presta mejor al desarrollo científico riguroso gracias a la teoría de la decisión.
4. En síntesis, la evolución del campo ha ido desplazándose progresivamente **de la imitación humana hacia la racionalidad como agente**, usando la lógica y el aprendizaje como herramientas —no como fines en sí mismos— al servicio de tomar la mejor decisión posible dado el entorno y la información disponible.
