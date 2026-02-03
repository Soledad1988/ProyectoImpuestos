📊 Documentación – Pipeline de Recaudación (Análisis Mensual y Anual)
1. Objetivo del proyecto

El objetivo de este análisis es construir un dataset consolidado de recaudación impositiva que permita:

Analizar la recaudación mensual por impuesto

Analizar la recaudación anual agregada

Unificar múltiples archivos Excel heterogéneos en una sola tabla base

Dejar el dataset listo para análisis exploratorio, visualización o uso en Power BI

El período analizado abarca desde 2020 hasta 2025.

2. Estructura de los datos de origen

Los datos se encuentran organizados en el sistema de archivos de la siguiente manera:

recaudacion/
│
├── 2020/
│   ├── 2020_enero.xls
│   ├── 2020_febrero.xls
│   └── ...
│
├── 2021/
│   ├── 2021_enero.xlsx
│   └── ...
│
└── 2025/


Características principales de los archivos:

Un archivo por mes

Formatos mixtos: .xls y .xlsx

Estructura no homogénea (cantidad de columnas variable)

Filas iniciales no relevantes (encabezados descriptivos)

Columnas de interés:

Concepto / Impuesto

Recaudación monetaria

3. Estrategia general del pipeline

Se implementó un pipeline en Python + pandas con enfoque modular y reutilizable:

Lectura iterativa de archivos mensuales por año

Normalización de columnas

Detección dinámica de columnas relevantes

Limpieza y estandarización

Agregado de metadatos temporales

Consolidación histórica (2020–2025)

┌──────────────────────────┐
│   Carpetas por año       │
│   recaudacion/           │
│   ├── 2020/              │
│   ├── 2021/              │
│   ├── 2022/              │
│   ├── 2023/              │
│   ├── 2024/              │
│   └── 2025/              │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│ Iteración por año        │
│ procesar_recaudacion_    │
│ historica()              │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│ Iteración por archivos   │
│ mensuales (.xls/.xlsx)  │
│ procesar_recaudacion_   │
│ por_anio()               │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│ Lectura Excel            │
│ read_excel(skiprows=12) │
│ + logs de control        │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│ Limpieza y normalización │
│ - nombres columnas       │
│ - selección columnas     │
│ - nulos                  │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│ Enriquecimiento temporal │
│ + año                    │
│ + mes                    │
│ + nombre de mes          │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│ Concatenación            │
│ mensual → anual → total  │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│ df_base                  │
│ Dataset final            │
│ (mensual + anual)        │
└─────────────┬────────────┘
              │
              ▼
┌──────────────────────────┐
│ Exportación CSV          │
│ Power BI / Análisis      │
└──────────────────────────┘


4. Función: procesamiento por año

La función procesar_recaudacion_por_anio se encarga de:

Recorrer todos los archivos Excel dentro de una carpeta anual

Leer cada archivo con pandas.read_excel

Limpiar y normalizar los datos

Agregar columnas de contexto temporal

Tareas clave realizadas:

Se ignoran archivos que no sean Excel

Se eliminan filas sin concepto de impuesto

Se reemplazan valores nulos de recaudación por 0

Se agregan columnas:

anio

mes

mes_nombre

Cada archivo mensual genera un DataFrame limpio que luego es concatenado a nivel anual.

5. Logs de control y validación

Durante la ejecución del pipeline se imprimen mensajes de control como:

leyendo: 2020_abril.xls
filas leídas: (52, 8)


Estos mensajes cumplen una función de debug y trazabilidad, indicando:

Qué archivo se está procesando

Si el archivo fue leído correctamente

La estructura original del Excel (filas, columnas)

⚠️ Estos mensajes no representan el DataFrame final, sino estados intermedios del proceso.

6. Función: procesamiento histórico (todos los años)

La función procesar_recaudacion_historica:

Recorre los años definidos (2020–2025)

Verifica la existencia de cada carpeta anual

Ejecuta el pipeline anual

Concatena todos los años en un único DataFrame base

El resultado final es el DataFrame:

df_base

7. Dataset final (df_base)

El DataFrame consolidado contiene información a nivel mensual, con la siguiente estructura:

Columna	Descripción
impuesto	Nombre del impuesto
recaudacion	Monto recaudado
anio	Año
mes	Número de mes
mes_nombre	Nombre del mes

Este dataset permite:

Agregaciones mensuales

Agregaciones anuales

Comparaciones interanuales

Análisis por impuesto y período

8. Preparación para análisis posterior

A partir de df_base se pueden construir fácilmente:

Tablas anuales (groupby(anio))

Series temporales mensuales

Visualizaciones

Exportes a CSV o conexión directa a Power BI

9. Conclusión

El pipeline implementado garantiza:

Reproducibilidad

Escalabilidad (agregar nuevos años/meses)

Robustez ante cambios de estructura en los Excel

Separación clara entre ingesta, limpieza y análisis

Este enfoque permite trabajar con datos públicos heterogéneos de manera confiable y profesional.