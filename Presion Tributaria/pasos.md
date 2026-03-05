# Análisis del Producto Interno Bruto (PIB) 2020–2025

## Exploración inicial de los datos

En primer lugar se realizó una exploración inicial del conjunto de datos correspondiente al Producto Interno Bruto (PIB).  
Este paso permitió observar la estructura de la serie, identificar los tipos de datos presentes y verificar la existencia de registros anuales y trimestrales.

La exploración inicial facilita comprender cómo se encuentra organizado el dataset antes de aplicar transformaciones o filtros.

---

## Limpieza y selección de la información relevante

Posteriormente se realizó un proceso de limpieza de los datos con el objetivo de aislar únicamente la información necesaria para el análisis.

En particular se seleccionaron los registros correspondientes a los **totales anuales del PIB**, eliminando otras observaciones que no resultaban relevantes para el estudio.

Luego se extrajo el **año desde el índice del dataset**, permitiendo trabajar con una estructura más clara y adecuada para el análisis temporal.

---

## Filtrado del período de estudio

Una vez preparada la serie de datos se filtró el período comprendido entre **2020 y 2024**, con el objetivo de concentrar el análisis en los años recientes de la economía argentina.

Este filtrado permite trabajar con un subconjunto de datos más manejable y directamente vinculado con el objetivo del análisis.

---

## Incorporación de los datos de 2025

El dataset original contiene información trimestral para el año 2025.  
Para incorporar este año al análisis se realizó un cálculo agregando los trimestres disponibles, obteniendo así una estimación del PIB para ese período.

De esta manera se logró extender la serie temporal hasta **2025**, permitiendo observar la evolución más reciente de la actividad económica.

---

## Reorganización del dataset

Luego se reorganizó la información en una estructura de **DataFrame**, conformada por dos variables principales:

- **Año**
- **Producto Interno Bruto (PIB)**

Esta estructura facilita el análisis posterior y permite utilizar la información en distintos tipos de visualizaciones.

---

## Verificación de tipos de datos

Antes de realizar gráficos o cálculos adicionales se verificó que los valores del dataset se encontraran en formato numérico.  
Este paso es importante para evitar errores durante el análisis y asegurar que los datos puedan utilizarse correctamente en operaciones estadísticas.

---

## Visualización de la evolución del PIB

Finalmente se construyó un gráfico para representar la evolución del Producto Interno Bruto durante el período analizado.

La visualización permite observar de manera clara las variaciones en el nivel de actividad económica entre los distintos años, facilitando la interpretación de la tendencia general del PIB.

---

## Importancia para el análisis de presión tributaria

El análisis del PIB constituye un paso fundamental para el estudio de la **presión tributaria**, ya que este indicador se calcula como la relación entre la recaudación impositiva y el tamaño de la economía.

Por lo tanto, contar con una serie del PIB correctamente estructurada permite posteriormente integrar la información de **recaudación tributaria** y calcular el nivel de carga impositiva en relación con la actividad económica.