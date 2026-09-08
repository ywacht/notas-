---
materia: Inteligencia Artificial
unidad: Aprendizaje Automático
tipo: concepto
fecha: 2026-09-04
tags:
  - IA
  - MachineLearning
  - Conceptos
---
#flashcards o #fichas
# Generalización, Sobreajuste y Subajuste

---

## 1. Generalización
> **Concepto:** Capacidad matemática de un modelo predictivo para mantener su rendimiento y precisión al procesar datos nuevos, invisibles y no utilizados durante la fase de entrenamiento.

### Fichas de Repaso (Spaced Repetition)
¿Qué es la generalización en Machine Learning?:: Capacidad de un modelo predictivo para mantener su rendimiento y precisión al procesar datos nuevos e invisibles.
<!--SR:!2026-09-18,11,270-->

---

## 2. Sobreajuste (Overfitting)
> **Definición:** Fenómeno estadístico donde un modelo aprende no solo la señal subyacente, sino también el ruido y las fluctuaciones aleatorias de los datos de entrenamiento.

* **Efecto:** Rendimiento casi perfecto en el entrenamiento, pero degradación severa en inferencia con datos nuevos.
* **Causa teórica:** Alta complejidad del modelo en relación con la cantidad y diversidad de los datos disponibles.

### Fichas de Repaso (Spaced Repetition)
¿Qué es el sobreajuste (Overfitting)?:: Fenómeno donde el modelo aprende la señal subyacente, el ruido y las fluctuaciones aleatorias del conjunto de entrenamiento.
<!--SR:!2026-09-19,12,270-->
Efecto del sobreajuste en inferencia:: Rendimiento casi perfecto en entrenamiento, pero degradación severa con datos nuevos.
<!--SR:!2026-09-19,12,270-->
¿Cuál es la causa teórica del sobreajuste?:: Alta complejidad del modelo en relación con los datos disponibles.
<!--SR:!2026-09-17,10,270-->

---

## 3. Subajuste (Underfitting)
> **Definición:** Incapacidad del modelo para capturar la estructura subyacente y los patrones de los datos, resultando en un desempeño deficiente.

* **Efecto:** Altas tasas de error tanto en la fase de entrenamiento como en la de prueba.

### Fichas de Repaso (Spaced Repetition)
¿Qué es el subajuste (Underfitting)?:: Incapacidad del modelo para capturar la estructura subyacente y patrones de los datos.
<!--SR:!2026-09-17,10,270-->
Efecto del subajuste en entrenamiento y prueba:: Altas tasas de error en ambas fases (entrenamiento y prueba).
<!--SR:!2026-09-10,2,250-->

---

## Resumen Comparativo

| Concepto | Rendimiento en Entrenamiento | Rendimiento en Prueba | Causa Principal |
| :--- | :--- | :--- | :--- |
| **Generalización** | Alto | Alto | Complejidad y datos balanceados |
| **Sobreajuste** | Casi perfecto | Muy bajo | Modelo demasiado complejo / Ruido |
| **Subajuste** | Bajo | Bajo | Modelo demasiado simple |

