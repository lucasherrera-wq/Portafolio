## **Predicción del Nivel de PIB utilizando Datos del Banco Mundial**

#### **Propósito del Proyecto**
Este proyecto tiene como objetivo diseñar y evaluar un modelo de clasificación capaz de predecir el Nivel de Producto Interno Bruto (PIB) de diversas naciones. Utilizando indicadores macroeconómicos, demográficos y sociales provenientes de las bases de datos abiertas del Banco Mundial, el análisis busca identificar qué factores (salud, educación, infraestructura, etc.) tienen mayor peso en la categorización económica de un país.

El enfoque principal es transformar datos crudos en inteligencia accionable, optimizando la complejidad del modelo mediante técnicas avanzadas de reducción de dimensionalidad.

### **Estructura del Proyecto**
El desarrollo se divide en tres fases críticas, gestionadas mediante un sistema de control de versiones robusto:

1. Ingeniería de Datos y Análisis Exploratorio (EDA)

- Extracción: Obtención de datos reales desde el World Bank API.

- Limpieza: Tratamiento de valores nulos mediante criterios de umbral y técnicas de imputación por mediana.

- Normalización: Estandarización de variables para asegurar la integridad estadística.

2. Optimización de Dimensiones (PCA)
- Aplicación de Análisis de Componentes Principales (PCA) para mitigar el fenómeno de la "maldición de la dimensionalidad".

- Análisis de la varianza explicada para conservar entre el 70% y 90% de la información original, garantizando un modelo parsimonioso y eficiente.

3. Modelado Predictivo
- Implementación de algoritmos de clasificación para asignar niveles de PIB.

- Evaluación de métricas de desempeño para validar la precisión de las predicciones.


### **Flujo de Trabajo y Control de Versiones**
Para garantizar la trazabilidad y el orden del proyecto, se ha implementado una estrategia de ramificación (branching):

- `main`: Rama principal que consolida la versión estable y final del código.

- `etapa-1`: Foco en la limpieza, imputación y análisis inicial de datos.

- `etapa-2 `: Foco en la transformación matemática y reducción de variables (PCA).

- `etapa-3`: Foco en el entrenamiento de modelos y resultados finales.
