# Challenge_Telecom_X_2

# Análisis de Predicción de Cancelación de Clientes (Churn)

## Propósito del Análisis

El objetivo principal de este proyecto es analizar los datos de clientes para predecir su posible cancelación (churn). Mediante la identificación de los factores más relevantes que influyen en la decisión de un cliente de dejar el servicio, buscamos desarrollar modelos predictivos que permitan anticipar el churn y así implementar estrategias de retención efectivas.

## Estructura del Proyecto

El proyecto se organiza de la siguiente manera:

-   `Telecom_Xparte2_Latam.ipynb`: Cuaderno principal de Google Colab que contiene todo el código para la carga, limpieza, preprocesamiento, análisis exploratorio, modelado y evaluación de los datos.
-   `df_normalizado.csv`: Archivo CSV con los datos de clientes utilizados para el análisis.
-   Carpeta de Visualizaciones (Opcional): Si se generan visualizaciones adicionales y se guardan como archivos de imagen.

## Proceso de Preparación de Datos

La preparación de los datos incluyó las siguientes etapas:

1.  **Carga y Limpieza de Datos:** Se cargó el archivo `df_normalizado.csv` en un DataFrame de pandas. Se eliminaron columnas irrelevantes para la predicción, como el identificador único de cliente (`customerID`).
2.  **Clasificación de Variables:** Las variables fueron clasificadas en categóricas (tipo `object`) y numéricas (tipo `float64`, `int64`, `bool`) para aplicar el preprocesamiento adecuado.
3.  **Codificación de Variables Categóricas:** Las variables categóricas fueron transformadas a formato numérico utilizando One-Hot Encoding (`pd.get_dummies`) para hacerlas compatibles con los algoritmos de machine learning. Se eliminó la primera categoría de cada variable codificada (`drop_first=True`) para evitar la multicolinealidad.
4.  **Manejo del Desbalance de Clases:** Se calculó la proporción de clientes que cancelaron y los que no, identificando un desbalance significativo. Para abordar esto, se aplicó la técnica SMOTE (Synthetic Minority Over-sampling Technique) al conjunto de entrenamiento para generar ejemplos sintéticos de la clase minoritaria ('Churn') y balancear las clases.
5.  **División de Datos:** El conjunto de datos fue dividido en conjuntos de entrenamiento y prueba (`train_test_split`) para evaluar el rendimiento de los modelos en datos no vistos. La división se realizó antes de aplicar SMOTE para evitar la fuga de datos del conjunto de prueba al entrenamiento. Se utilizó estratificación (`stratify=y`) para mantener la proporción de clases en ambos conjuntos.
6.  **Escalado de Datos:** Para los modelos que requieren normalización (como Regresión Logística), las características de los conjuntos de entrenamiento (balanceado) y prueba fueron estandarizadas utilizando `StandardScaler`.

## Justificaciones para las Decisiones de Modelado

Se entrenaron dos tipos de modelos para predecir la cancelación:

-   **Regresión Logística:** Se eligió por ser un modelo lineal simple y eficaz para problemas de clasificación binaria. Requiere normalización de los datos para un rendimiento óptimo.
-   **Random Forest:** Se seleccionó por ser un modelo basado en árboles que no es sensible a la escala de los datos y suele ofrecer buen rendimiento.

La decisión de entrenar ambos tipos de modelos nos permite comparar su desempeño y entender cómo la normalización impacta en los resultados.

## Análisis Exploratorio de Datos (EDA) - Insights Clave

Durante el EDA, se obtuvieron los siguientes hallazgos:

-   Se confirmó el desbalance de clases en la variable objetivo 'Churn'.
-   La visualización de la matriz de correlación mostró la relación entre las variables numéricas y la cancelación.
-   Los gráficos (boxplots y scatter plots) revelaron que los clientes que cancelaron tienden a tener un `tenure` (tiempo de contrato) más corto y `Charges.Total` (gasto total) más bajos.

## Instrucciones para Ejecutar el Cuaderno

Para ejecutar el cuaderno `Telecom_Xparte2_Latam.ipynb`, sigue estos pasos:

1.  Abre el cuaderno en Google Colab.
2.  Asegúrate de que el archivo `df_normalizado.csv` se encuentre en la ruta `/content/` en el entorno de Colab. Puedes subirlo si es necesario.
3.  Instala las bibliotecas necesarias ejecutando las siguientes celdas de código:
