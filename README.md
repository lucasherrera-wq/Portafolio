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
