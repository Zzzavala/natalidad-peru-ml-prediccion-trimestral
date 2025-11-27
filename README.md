# Predicción Trimestral de la Tasa de Natalidad en el Perú
## Comparación de Modelos de Machine Learning a Nivel Departamental

Este repositorio contiene el desarrollo completo del proyecto orientado a predecir la tasa de natalidad trimestral en el Perú utilizando modelos de Machine Learning aplicados a datos oficiales del Registro de Nacidos Vivos (2015–2025). El sistema integra análisis espacio-temporal, ingeniería de características y validación temporal.

---

## 1. Descripción General

La tasa de natalidad peruana presenta una tendencia descendente con fuertes diferencias entre departamentos. Este proyecto desarrolla un modelo predictivo capaz de capturar estas variaciones mediante un panel trimestral departamental construido a partir de millones de registros individuales.

El modelo XGBoost obtuvo el mejor desempeño, alcanzando un R² de 0.91 en el conjunto de prueba, indicando una excelente capacidad de generalización.

---

## 2. Objetivos del Proyecto

### Objetivo general
Desarrollar y comparar modelos de Machine Learning para predecir la tasa de natalidad trimestral a nivel departamental en el Perú.

### Objetivos específicos
- Procesar y transformar datos individuales de nacimientos para formar un panel trimestral departamental.
- Implementar modelos de predicción respetando la secuencia temporal.
- Evaluar y comparar el desempeño mediante métricas estandarizadas (R², MAE, RMSE).
- Identificar las variables con mayor influencia predictiva.

---

## 3. Datos Utilizados

### 3.1. Registros de Nacidos Vivos (2015–2025)
Más de 4.7 millones de registros con información sociodemográfica, de salud y ubicación geográfica.

### 3.2. Catálogo de Ubigeo del INEI
Utilizado para asignación correcta del departamento de cada nacimiento.

### 3.3. Proyecciones de Población Departamental
Datos anuales del INEI usados para estimar población trimestral mediante interpolación.

---

## 4. Proceso de Preprocesamiento

El pipeline incluyó:

### 4.1. Limpieza de datos
- Eliminación de duplicados.
- Normalización de valores especiales.
- Conversión de valores inválidos.
- Eliminación de campos no relevantes.

### 4.2. Integración geográfica
- Unión por código Ubigeo.
- Identificación del departamento correspondiente.

### 4.3. Ingeniería de características
- Estadísticas de edad materna.
- Promedios de variables reproductivas.
- Proporciones de categorías agrupadas.
- Variables temporales: lag1, lag4, MA4.

### 4.4. Construcción del panel trimestral
- Agregación por año, trimestre y departamento.
- Incorporación de población trimestral.
- Cálculo de tasa de natalidad por 1000 habitantes.

---

## 5. Modelos Implementados

Se evaluaron cinco algoritmos:

- Regresión Lineal
- K-Nearest Neighbors (k = 5 y k = 10)
- Árbol de Decisión (profundidad máxima = 6)
- Random Forest (100 árboles)
- XGBoost (modelo de mejor desempeño)

Todos evaluados mediante validación cruzada temporal (TimeSeriesSplit, 5 folds).

---

## 6. Resultados Principales

### 6.1. Validación Cruzada Temporal (promedio)

| Modelo             | R²      | MAE     | RMSE    |
|-------------------|---------|---------|---------|
| XGBoost           | 0.8632  | 0.1955  | 0.2593  |
| Random Forest     | 0.8493  | 0.2107  | 0.2747  |
| Árbol de Decisión | 0.7118  | 0.2715  | 0.3606  |
| Regresión Lineal  | 0.7309  | 0.2737  | 0.3527  |
| KNN (k = 5)       | 0.7027  | 0.2892  | 0.3636  |

### 6.2. Desempeño en el Conjunto de Prueba (2024–2025)

Modelo final (XGBoost ajustado):

- **R²:** 0.9107
- **RMSE:** 0.2144
- **MAE:** 0.1618

El modelo mostró buena generalización y consistencia entre validación y prueba.

---

## 7. Importancia de Variables

### Importancia acumulada por categoría
- **Temporal:** 53.08 %
- **Geográfica:** 38.77 %
- **Atención de salud:** 2.83 %
- **Educación:** 1.52 %
- **Edad materna:** 1.04 %
- **Reproductivo:** 0.99 %

Las variables temporales lag1, lag4 y MA4 fueron las más influyentes.

---

## 8. Exclusión del Período COVID-19

Se compararon modelos entrenados con y sin los datos de 2020–2021T2.  
La exclusión del período COVID mejoró todas las métricas, debido a comportamientos atípicos durante la pandemia.

---

## 9. Conclusiones

- Los modelos basados en árboles superaron ampliamente a los lineales.
- XGBoost alcanzó el mejor desempeño, capturando patrones no lineales y dependencias temporales.
- Las variables temporales y geográficas explicaron más del 90 % del poder predictivo.
- La exclusión del período COVID mejoró la estabilidad del modelo.

---

## 10. Autores

Proyecto desarrollado por el Grupo 08:

- John Arzapalo
- Ariana Burga
- Ricardo Lara
- Luis Miranda
- Alessandro Santé
- Juan Zavala
