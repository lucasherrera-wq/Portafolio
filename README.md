### **Etapa 2: Reducción de Dimensionalidad con PCA**

El dataset contiene múltiples variables macroeconómicas, demográficas y sociales, por lo que se aplicará Análisis de Componentes Principales (`PCA`) con el objetivo de reducir la dimensionalidad y capturar los principales patrones subyacentes en los datos.

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
