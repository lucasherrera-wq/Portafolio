### **Etapa 3:  Implementación y Comparación de Modelos de Clasificación**

Esta fase final constituye el núcleo analítico del proyecto, donde se valida la utilidad de las etapas previas mediante la experimentación con algoritmos de Machine Learning. El objetivo principal es determinar cómo influye la reducción de dimensionalidad (PCA) en la capacidad predictiva de los modelos.

El proyecto concluye con un análisis crítico que contrasta ambos enfoques. Se evalúa el equilibrio entre la interpretabilidad (entender las variables originales), la eficiencia (menor costo computacional con PCA) y la eficacia (precisión final de la clasificación del PIB)

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
