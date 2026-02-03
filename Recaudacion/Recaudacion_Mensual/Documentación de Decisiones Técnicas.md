1. ¿Por qué un pipeline modular?

Decisión: separar el procesamiento en funciones reutilizables.

✔️ Permite:

Escalar a nuevos años sin tocar código

Depurar errores por etapa

Reutilizar lógica en otros proyectos

📌 Funciones clave:

procesar_recaudacion_por_anio

procesar_recaudacion_historica

2. Lectura flexible de archivos Excel

Decisión: aceptar .xls y .xlsx indistintamente.

✔️ Motivo:

Los datos históricos no son homogéneos

Pandas puede manejar ambos formatos

if archivo.endswith((".xls", ".xlsx")):

3. Uso de skiprows

Decisión: omitir filas iniciales no estructuradas.

✔️ Motivo:

Los archivos contienen encabezados descriptivos

La tabla útil comienza luego de varias filas

📌 Esto evita limpieza manual posterior.

4. Detección dinámica de columnas

Decisión: no hardcodear nombres de columnas.

✔️ Motivo:

Los nombres cambian entre archivos/años

Algunos dicen “concepto”, otros “impuesto”, otros “detalle”

✔️ Estrategia:

Buscar columnas por palabras clave

Usar fallback si no se detecta ninguna

Esto hace al pipeline robusto ante cambios.

5. Normalización temprana de datos

Decisión: limpiar antes de concatenar.

✔️ Incluye:

Normalizar nombres de columnas

Eliminar filas sin impuesto

Reemplazar nulos en recaudación por 0

📌 Resultado:

Dataset consistente

Sin valores problemáticos para agregaciones

6. Enriquecimiento temporal explícito

Decisión: agregar anio, mes y mes_nombre como columnas.

✔️ Motivo:

Facilita análisis temporal

Evita depender del nombre del archivo

Ideal para Power BI y visualizaciones

7. Logs de control durante la ejecución

Decisión: usar prints informativos.

Ejemplo:

leyendo: 2020_abril.xls
filas leídas: (52, 8)


✔️ Beneficios:

Detectar archivos corruptos

Identificar estructuras atípicas

Auditar el pipeline sin frenar la ejecución

📌 Importante: no forman parte del dataset, solo debugging.

8. Un solo dataset base (df_base)

Decisión: trabajar con una tabla “larga” (long format).

✔️ Ventajas:

Ideal para BI

Fácil de agregar por mes o año

Flexible para distintos análisis

Ejemplo de agregación posterior:

df_base.groupby(["anio", "mes"])["recaudacion"].sum()

9. Exportación en CSV UTF-8

Decisión: exportar en CSV con utf-8-sig.

✔️ Motivo:

Compatible con Excel y Power BI

Evita problemas de encoding

🧠 Conclusión técnica

El pipeline fue diseñado para:

Manejar datos reales y desprolijos

Escalar en el tiempo

Ser entendible, auditado y reproducible

Separar claramente ingestión, limpieza y análisis

Esto ya es nivel proyecto profesional, no ejercicio.

Si querés, próximos pasos posibles:

📊 diagrama visual (estilo draw.io / mermaid)

🧪 validación de totales oficiales

⭐ modelo estrella para Power BI

🧾 versión resumida “para portfolio”

Decime cómo seguimos y lo llevamos al siguiente nivel 🚀