etapa-1

## **Predicción del Nivel de PIB utilizando Datos del Banco Mundial**

#### **Propósito del Proyecto**
Este proyecto tiene como objetivo diseñar y evaluar un modelo de clasificación capaz de predecir el Nivel de Producto Interno Bruto (PIB) de diversas naciones. Utilizando indicadores macroeconómicos, demográficos y sociales provenientes de las bases de datos abiertas del Banco Mundial, el análisis busca identificar qué factores (salud, educación, infraestructura, etc.) tienen mayor peso en la categorización económica de un país.

El enfoque principal es transformar datos crudos en inteligencia accionable, optimizando la complejidad del modelo mediante técnicas avanzadas de reducción de dimensionalidad.

### **Estructura del Proyecto**
El desarrollo se divide en tres fases críticas, gestionadas mediante un sistema de control de versiones robusto:

1. Ingeniería de Datos y Análisis Exploratorio (EDA)

- Extracción: Obtención de datos reales desde el World Bank API.
 main

- Limpieza: Tratamiento de valores nulos mediante criterios de umbral y técnicas de imputación por mediana.

- Normalización: Estandarización de variables para asegurar la integridad estadística.

2. Optimización de Dimensiones (PCA)
- Aplicación de Análisis de Componentes Principales (PCA) para mitigar el fenómeno de la "maldición de la dimensionalidad".

- Análisis de la varianza explicada para conservar entre el 70% y 90% de la información original, garantizando un modelo parsimonioso y eficiente.

3. Modelado Predictivo
- Implementación de algoritmos de clasificación para asignar niveles de PIB.

- Evaluación de métricas de desempeño para validar la precisión de las predicciones.

- Otras observaciones relevantes.


### **Flujo de Trabajo y Control de Versiones**
Para garantizar la trazabilidad y el orden del proyecto, se ha implementado una estrategia de ramificación (branching):

- `main`: Rama principal que consolida la versión estable y final del código.

- `etapa-1`: Foco en la limpieza, imputación y análisis inicial de datos.

- `etapa-2 `: Foco en la transformación matemática y reducción de variables (PCA).

etapa-1
- Discretizar la variable dependiente `NY.GDP.MKTP.PP.KD` de aceurdo con la siguiente indicación.

    ```python
    df_wb_raw['NY.GDP.MKTP.PP.KD'] = pd.qcut(df_wb_raw['NY.GDP.MKTP.PP.KD'], q=5, labels=['Low', 'Medium-Low', 'Medium', 'Medium-High', 'High'])

    ```

- Enviar a Github a la rama 1 el notebook ejecutado en esta etapa.

    **Nota**: Debe describir de manera clara y ordenada los pasos realizados durante el desarrollo del proyecto, incorporando una breve justificación para cada uno de ellos, de modo que se expliciten las decisiones adoptadas y su coherencia con los objetivos planteados.

    Esta indicación es válida para todas las etapas del proyecto.


#### **Documentación de los pasos y las decisiones metodológicas.**

1. **Identificación y Manejo de Valores Faltantes**

El primer paso consistió en diagnosticar la integridad del dataset mediante el cálculo de valores nulos.

- Diagnóstico: Se generó un resumen detallado con el conteo y porcentaje de nulos por columna.


- Criterio de Exclusión: Se estableció un umbral del 15%. Aquellas variables que superaban este porcentaje de ausencia de datos fueron eliminadas, ya que la imputación en estos niveles podría introducir sesgos significativos.



- Imputación: Para las columnas numéricas que se mantuvieron, se utilizó la mediana como medida de tendencia central para rellenar los valores faltantes. Se eligió la mediana por su robustez frente a posibles valores atípicos (outliers).

2. **Definición de la Variable Objetivo**

Se identificó la columna `NY.GDP.MKTP.PP.KD ` como el indicador clave del Producto Interno Bruto (PIB).

- Renombrado: Se renombró a `PIB_Level` para facilitar su identificación como la variable objetivo categórica del modelo de clasificación.



- Verificación: Se confirmó que el tipo de dato fuera numérico antes de proceder a cualquier transformación posterior.


3. **Estandarización de Nombres de Columnas**

Para asegurar la compatibilidad con librerías de Python y mejorar la legibilidad del código:

- Se convirtieron todos los encabezados a minúsculas.



- Se reemplazaron los puntos (`.`) por guiones bajos (`_`).




- Se excluyeron de este proceso las columnas de control: country, year y `PIB_Level`.


4. **Análisis Exploratorio Visual (EDA)**

Se realizaron visualizaciones para entender la distribución y naturaleza de los datos limpios.



- Distribución de Categorías: Se utilizó un gráfico de barras (`seaborn`) para observar el balance de las clases en `PIB_Level`. Esto es crucial para identificar si existe un desbalance de clases que pueda afectar el entrenamiento de los modelos de clasificación.

- Visualización Geográfica: Mediante Plotly Express, se generó un mapa coroplético utilizando los códigos ISO-3 de los países. Esto permitió validar la cobertura geográfica del dataset y observar patrones espaciales en la distribución del nivel de PIB a nivel global.

5. Resumen Estadístico

- Finalmente, se ejecutó un `describe().transpose()`para obtener una visión general de las escalas, medias y desviaciones estándar de las variables resultantes, confirmando que los datos están listos para la etapa de Estandarización y PCA.


- `etapa-3`: Foco en el entrenamiento de modelos y resultados finales.
- main
