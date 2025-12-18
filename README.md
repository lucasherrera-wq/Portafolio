 etapa-3
### **Etapa 3:  Implementación y Comparación de Modelos de Clasificación**

Esta fase final constituye el núcleo analítico del proyecto, donde se valida la utilidad de las etapas previas mediante la experimentación con algoritmos de Machine Learning. El objetivo principal es determinar cómo influye la reducción de dimensionalidad (PCA) en la capacidad predictiva de los modelos.

El proyecto concluye con un análisis crítico que contrasta ambos enfoques. Se evalúa el equilibrio entre la interpretabilidad (entender las variables originales), la eficiencia (menor costo computacional con PCA) y la eficacia (precisión final de la clasificación del PIB)

**Justificación de los Modelos**

- k-Nearest Neighbors (`KNN`): Es un modelo no paramétrico que clasifica basado en la proximidad. En este contexto, asume que países con indicadores macroeconómicos similares (puntos cercanos en el espacio multidimensional) deberían pertenecer al mismo nivel de PIB. Es ideal para detectar grupos naturales de desarrollo.

- Random Forest Classifier: Es más complejo. Al usar todas las variables originales, este modelo buscará interacciones complejas entre indicadores (por ejemplo, cómo se relacionan la salud y la educación con el PIB) sin necesidad de transformaciones previas.

#### **Comaparación de Resultados**

**Accuracy**

- KNN: 0.425
- KNN PCA: 0.25

- Random Forest Original: 0.725
- Random Forest PCA: 0.3

**F1-Score**

- KNN: 0.4141
- KNN PCA: 0.2484

- Random Forest Original: 0.7167
- Random Forest PCA: 0.3256

**Discusión de Resultados**

En este proyecto, observamos que el uso de PCA tuvo efectos opuestos según el algoritmo:

Con K-Nearest Neighbors el rendimiento del modelo decayó significativamente, pasando de un 0.425 a un 0.25 en accuracy. Esto sugiere que, al reducir el dataset a solo 5 componentes, se perdió la resolución espacial necesaria para que el algoritmo identifique correctamente la vecindad de los datos. En KNN, la distancia euclidiana es fundamental; al comprimir 38 variables en 5, las distancias entre países de diferentes categorías se volvieron ambiguas, provocando clasificaciones erróneas.

Random Forest perdió su capacidad predictiva al pasar al espacio de 5 componentes, y esto se debe a que el algoritmo de Random Forest fundamenta su eficacia en la diversidad y la abundancia de datos. Al ser un modelo basado en la construcción de múltiples árboles de decisión, necesita un espectro amplio de variables para explorar diferentes combinaciones y detectar patrones complejos que no son visibles a simple vista. Al limitar el espacio a pocos componentes, se restringe la "visión" del modelo, obligándolo a generalizar en exceso y eliminando la riqueza informativa que le permite ser preciso.

**Conclusión Metodológica**

Para este dataset del Banco Mundial, la reducción de dimensionalidad mediante PCA no resultó en una mejora para los modelos probados. El algoritmo de KNN mostró ser altamente sensible a la pérdida de información dimensional, lo que invalida el uso de solo 5 componentes para este método. En conclusión, si se busca la máxima precisión posible en la clasificación del nivel de PIB, el Random Forest con el dataset original (67 variables) sigue siendo la mejor opción estratégica, ya que preserva la complejidad necesaria para capturar las disparidades económicas globales.

#### **Documentación de los pasos y las decisiones metodológicas.**


1. **Justificación de Modelos Seleccionados.**

Para garantizar una evaluación robusta, se seleccionaron dos algoritmos con naturalezas matemáticas y lógicas distintas:

- k-Nearest Neighbors (`kNN`): Se eligió como un modelo basado en instancias y proximidad. Su lógica reside en que países con perfiles macroeconómicos similares (puntos cercanos en el espacio vectorial) deberían pertenecer al mismo nivel de PIB. Es un modelo que no asume una distribución previa de los datos, pero es altamente sensible a la escala y a la cantidad de variables.

- Random Forest Classifier: Se eligió por su capacidad para capturar interacciones complejas y no lineales entre variables sin requerir supuestos de normalidad.


2. **Metodología de Entrenamiento.**

- Se aplicó una partición de datos 80/20 para entrenamiento y prueba, utilizando una estratificación (`stratify=y`). Esto garantiza que todas las categorías de PIB_Level (`desde Low hasta High`) estén representadas proporcionalmente tanto en el entrenamiento como en la validación, evitando que el modelo se sesgue hacia las clases más frecuentes.

3. **Discusión de Resultados y Hallazgos Clave.**

- Para realizar las comparaciones, utilizamos las metricas `Accuracy` y `F1-Score`

- En el dataset original, kNN obtuvo un Accuracy de 0.4250. Este rendimiento moderado se debe a la "maldición de la dimensionalidad", ya que al tener tantas variables (67), el concepto de "distancia" se vuelve difuso, como mencionamos anteriormente este modelo es sensible a la escala y a la cantidad de variables.

- El Random Forest sufrió una caída similar en su desempeño (`de 0.72 a 0.30`) al cambiar a PCA. Esto sugiere que el algoritmo depende de las variables originales crudas para identificar los puntos de corte óptimos en sus árboles de decisión; al licuar la información en componentes abstractos, se pierden las fronteras de decisión locales que el modelo aprovecha.

 etapa-2
### **Etapa 2: Reducción de Dimensionalidad con PCA**

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
 main


 etapa-2
- Seleccionar únicamente variables numéricas y estandarizarlas previamente.
- Aplicar `PCA` y analizar la varianza explicada por cada componente.
- Elegir el número de componentes necesarias para explicar entre 70% y 90% de la varianza total, justificando brevemente dicha elección.
- Construir un nuevo DataFrame que contenga las componentes seleccionadas, el cual será utilizado como insumo para los modelos de clasificación posteriores.
- Documentar de forma clara los pasos realizados y las decisiones metodológicas adoptadas.

**Justificación Metodológica**
Se seleccionaron 5 componentes principales.
Esta elección nos permite reducir la dimensionalidad de 38 a 5 variables,
manteniendo el 74.66% de la información original (varianza).
Esto asegura una simplificación del modelo sin una pérdida significativa de capacidad predictiva,
cumpliendo con el principio de parsimonia para evitar el sobreajuste.

#### **Documentación de los pasos y las decisiones metodológicas.** (Etapa 2)

1. Para la estandarización utilizamos `StandarScaler` debido a las variables macroeconómicas tienen escalas muy distintas (Por ejemplo, porcentajes vs. valores en millones), ya que PCA es sensible a estas diferencias.

2. Selección por Porcentaje Acumulado de Varianza Explicada: Se seleccionaron 5 componentes principales basándose en el criterio de Porcentaje Acumulado, estableciendo un umbral de retención de información superior al 70%.

3. Aunque para alcanzar un nivel de varianza del 90% se requerirían 10 componentes, la selección de 5 dimensiones logra capturar el 74.66% de la varianza total. En el análisis de indicadores macroeconómicos, este porcentaje se considera suficiente para representar la estructura subyacente de los datos sin incurrir en una excesiva complejidad dimensional. Esta decisión equilibra la representatividad estadística con el principio de parsimonia, garantizando que los modelos de clasificación de la Etapa 3 utilicen variables ortogonales de alta densidad informativa, filtrando componentes menores que aportan una ganancia marginal de varianza a cambio de un mayor riesgo de ruido.

- `etapa-3`: Foco en el entrenamiento de modelos y resultados finales.
- main
 main
 main
