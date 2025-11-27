Predicción Trimestral de la Tasa de Natalidad en el Perú
Comparación de Modelos de Machine Learning a Nivel Departamental

Este repositorio contiene el desarrollo completo del proyecto de modelado predictivo orientado a estimar la tasa de natalidad trimestral en el Perú utilizando técnicas de Machine Learning y datos oficiales del Registro de Nacidos Vivos (2015–2025). El enfoque incorpora análisis espacio-temporal, ingeniería de características, validación temporal y comparación de algoritmos.

1. Descripción General

La tasa de natalidad peruana ha mostrado una tendencia decreciente durante la última década, con marcadas diferencias entre departamentos. Para apoyar el análisis demográfico y la toma de decisiones en salud, educación y planificación territorial, este proyecto desarrolla un sistema predictivo que integra datos sociodemográficos, geográficos y temporales en un panel trimestral departamental.

El modelo con mejor desempeño fue XGBoost, alcanzando un R² de 0.91 en el conjunto de prueba. Además, el análisis de importancia de variables evidencia que las características temporales y geográficas explican más del 90% del poder predictivo.

2. Objetivos del Proyecto

Objetivo general
Desarrollar y comparar modelos de Machine Learning para predecir la tasa de natalidad trimestral a nivel departamental en el Perú.

Objetivos específicos

Procesar y transformar datos individuales de nacimientos, construyendo un panel trimestral departamental.

Implementar modelos considerando la estructura temporal de las series.

Evaluar el desempeño mediante métricas estandarizadas y validación temporal.

Identificar las variables con mayor influencia predictiva en el modelo de mejor desempeño.

3. Datos Utilizados

Los datos provienen de fuentes oficiales públicas:

3.1. Registros de Nacidos Vivos (2015–2025)

Dataset con más de 4.7 millones de registros individuales, con características de:

Madre (edad, educación, estado civil).

Recién nacido.

Atención del parto.

Ubicación geográfica mediante código Ubigeo.

3.2. Catálogo de Ubigeo del INEI

Utilizado para asignar cada nacimiento a su departamento correspondiente.

3.3. Proyecciones de Población Departamental

Datos anuales del INEI utilizados para generar poblaciones trimestrales mediante interpolación lineal.

4. Proceso de Preprocesamiento

El pipeline completo incluyó:

Limpieza de registros:

Eliminación de duplicados.

Conversión y normalización de valores especiales.

Tratamiento de valores ignorados o inválidos.

Eliminación de variables no relevantes.

Integración geográfica:

Unión por código Ubigeo.

Asignación de departamento.

Ingeniería de características:

Cálculo de estadísticas de edad materna.

Promedios de historia reproductiva.

Proporciones de categorías agregadas (educación, estado civil, financiador, tipo de atención).

Creación de variables temporales: lag1, lag4, ma4.

Construcción del panel trimestral departamental:

Agregación por año, trimestre y departamento.

Incorporación de población trimestral.

Cálculo de la tasa de natalidad por 1000 habitantes.

5. Modelos Implementados

Se compararon cinco algoritmos representativos de distintos paradigmas:

Regresión Lineal

K-Nearest Neighbors (k=5 y k=10)

Árbol de Decisión (max_depth=6)

Random Forest (100 árboles, max_depth=6)

XGBoost (mejor desempeño)

Todos los modelos se evaluaron con validación cruzada temporal (TimeSeriesSplit, 5 folds) para respetar la estructura cronológica.

6. Resultados Principales
6.1. Validación Cruzada Temporal (promedio)

XGBoost: R² = 0.8632, MAE = 0.1955

Random Forest: R² = 0.8493, MAE = 0.2107

Árbol de Decisión: R² = 0.7118, MAE = 0.2715

Regresión Lineal: R² = 0.7309, MAE = 0.2737

KNN (k=5): R² = 0.7027, MAE = 0.2892

6.2. Evaluación en el Conjunto de Prueba (2024–2025)

Modelo final (XGBoost con parámetros ajustados):

R²: 0.9107

RMSE: 0.2144

MAE: 0.1618

El modelo mostró alta capacidad de generalización y estabilidad.

7. Importancia de Variables

El análisis de importancia del modelo XGBoost reveló:

Categoría Temporal: 53.08 %

Categoría Geográfica: 38.77 %

Atención de salud: 2.83 %

Educación: 1.52 %

Edad materna: 1.04 %

Factores reproductivos: 0.99 %

Las variables lag1, lag4 y ma4 fueron las más influyentes, evidenciando un fuerte componente de inercia temporal en la natalidad.

8. Exclusión del Período COVID-19

Se realizaron experimentos comparando modelos entrenados con y sin datos correspondientes al período COVID-19 (2020–2021T2).
La exclusión de este período mejoró todas las métricas, demostrando que dichos valores representan eventos atípicos que introducen ruido y reducen la capacidad de generalización.
