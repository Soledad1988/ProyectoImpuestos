📊 Proyecto Integrado
Presión tributaria e informalidad laboral en Argentina (2020–2025)
1. Objetivo del proyecto

El presente trabajo tiene como objetivo analizar la evolución de la presión tributaria y su relación con variables socioeconómicas y laborales, particularmente la informalidad del empleo, en el período 2020–2025.

El foco se centra en comprender:

El impacto del shock de la pandemia en 2020.

La dinámica posterior del empleo formal e informal.

La relación entre presión tributaria y estructura laboral.

2. Fuentes de datos

Se utilizaron las siguientes fuentes oficiales:

Datos de empleo formal e informal provenientes de la Encuesta Permanente de Hogares (EPH) publicada por el Instituto Nacional de Estadística y Censos.

Datos de Producto Interno Bruto (PBI) anual.

Datos de recaudación tributaria anual (IVA, Ganancias y Total).

3. Limpieza y transformación de datos
3.1. Construcción de la variable de informalidad

Se extrajo la fila correspondiente a “Sin descuento jubilatorio (informal)”.

Se eliminaron columnas no numéricas y separadores vacíos.

Se reconstruyó la estructura temporal trimestral.

Se calculó el promedio anual para obtener una tasa anual de informalidad.

Se construyó la tasa de empleo formal como:

tasa_empleo_formal =100 − tasa_informalidad

3.2. Transformación de datos de recaudación

Los datos de recaudación estaban en formato largo (long format), por lo que:

Se realizó un pivot para obtener formato ancho (wide format).

Se generaron las variables:

recaudacion_total

recaudacion_iva

recaudacion_ganancias

3.3. Integración de bases

Se realizó un merge por la variable anio entre:

PBI

Recaudación

Variables laborales

Se construyó así un dataset maestro consolidado 2020–2025.

4. Construcción de variables derivadas

Se calcularon:

4.1 Presión tributaria

presion_tributaria= (recaudacion_total / pib_total) * 100
	​
4.2 Variaciones interanuales

Se calcularon tasas de variación porcentual para:

Presión tributaria

Informalidad laboral

5. Análisis realizado
5.1 Análisis descriptivo

Se analizaron:

Evolución del empleo formal e informal.

Evolución del PBI.

Evolución de la presión tributaria.

Se identificó el efecto shock en 2020, donde la informalidad cae artificialmente debido a la salida de trabajadores del mercado laboral durante la pandemia.

5.2 Análisis comparativo por período

Se creó una variable categórica:

“Shock Pandemia (2020)”

“Post-pandemia (2021–2025)”

Se compararon promedios entre períodos para evaluar cambios estructurales.

5.3 Análisis de correlación

Se calculó la matriz de correlación entre:

Presión tributaria

Tasa de empleo formal

Tasa de informalidad

PBI

Este análisis permitió evaluar la fuerza y dirección de las relaciones.

5.4 Elasticidad simple

Se estimó la elasticidad aproximada de la informalidad respecto a la presión tributaria utilizando variaciones porcentuales.

Esto permitió evaluar la sensibilidad del empleo informal ante cambios en la carga tributaria.

5.5 Análisis gráfico

Se generaron:

Series temporales comparadas.

Gráficos de dispersión.

Línea de tendencia con ajuste lineal.

Comparaciones estructurales entre años.

6. Principales hallazgos preliminares

En 2020 se observa una caída abrupta de la formalidad laboral producto del shock pandémico.

La presión tributaria no necesariamente se mueve en la misma magnitud que la estructura laboral.

La relación entre presión tributaria e informalidad no es puramente lineal.

Factores macroeconómicos (actividad económica, inflación, composición impositiva) pueden influir significativamente.

7. Limitaciones del análisis

Muestra reducida (6 años).

Posible efecto nominal por inflación.

No se incluyen variables de control adicionales.

2025 contiene información parcial (tres trimestres promedio).

8. Conclusión

El análisis integrado permite observar que la relación entre presión tributaria e informalidad laboral es compleja y está mediada por shocks macroeconómicos y ciclos económicos.

El período 2020–2025 muestra que:

El shock pandémico generó distorsiones temporales.

La recuperación posterior no implicó necesariamente una mejora estructural sostenida.

La presión tributaria debe analizarse en conjunto con el contexto macroeconómico para comprender su impacto real sobre el mercado laboral.