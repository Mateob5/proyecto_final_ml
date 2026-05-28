<div align="center">
  <img src="banner.png" alt="Banner Optimización de Campañas de Marketing Bancario" width="100%">
</div>

# Optimización de Campañas de Marketing Bancario

**Materia:** Aprendizaje de Máquina  
**Profesor:** Gustavo Garzón Ph.D.  
**Autor:** Jeronimo Andres Mateo Bazán Rojas  
**Fecha:** 5 de Mayo de 2026

**Video:** <a href="https://www.youtube.com/watch?v=F3i_26kWzdo">Link Video</a>

---

## 📄 Descripción del Proyecto
Este repositorio contiene el análisis y modelado predictivo sobre el dataset **Bank Marketing** (proveniente del UCI Repository, con 45.211 registros). El objetivo principal es evaluar y optimizar campañas de marketing telefónico de un banco portugués, prediciendo si un cliente suscribirá o no un depósito a plazo fijo.

El proyecto abarca todo el flujo de trabajo de Machine Learning, desde la exploración y limpieza de datos hasta la comparación exhaustiva de modelos de aprendizaje supervisado, no supervisado y redes neuronales profundas (Deep Learning).

---

## 📊 Características del Dataset
* **Enlace de origen:** [UCI Bank Marketing Dataset](https://archive.ics.uci.edu/dataset/222/bank+marketing)
* **Preprocesamiento y Limpieza:** Se eliminaron las variables `default` (por exceso de valores nulos) y `duration`. Esta última se descartó estratégicamente para evitar fuga de datos (*data leakage*), ya que la duración de la llamada es una variable que no se conocería en un entorno de producción real antes de ejecutar el contacto.
* **Desbalance de Clases:** Se identificó un desbalance severo en la variable objetivo (88.73% de "No" frente a 11.27% de "Sí").
* **Transformación:** Se aplicó One-Hot Encoding para convertir las características categóricas en binarias y se utilizó particionado estratificado (80% entrenamiento / 20% prueba) para mantener la proporción de las clases.

---

## 🛠 Modelos Implementados

### 1. Aprendizaje Supervisado (Modelos Clásicos)
Se entrenaron y validaron mediante Cross-Validation (con k=5) los siguientes algoritmos:
* **Decision Tree Classifier:** Se exploraron profundidades de 2 a 10, encontrando el punto de generalización óptimo en `max_depth=5`, logrando un *accuracy* del ~90.3%.
* **Random Forest Classifier:** Configurado con `n_estimators=10`, alcanzó un *accuracy* cercano al 89%. A través del análisis de importancia de características (*Feature Importance*), se determinó que `age` (edad), `euribor3m` (tasa de interés) y `campaign` (número de contactos) son las variables más determinantes para la predicción.
* **Support Vector Machine (SVM):** Implementado con escalado previo (StandardScaler). Se evaluaron kernels lineales, polinómicos y radiales, destacando el kernel RBF con un *accuracy* del ~90%.

### 2. Deep Learning (Perceptrón Multicapa - MLP)
Se diseñaron tres arquitecturas de redes neuronales, configuradas con optimizador Adam, función de pérdida *binary crossentropy* y mecanismos para evitar sobreajuste como *Dropout* y *Early Stopping*:
* **Arquitectura 1:** 3 capas ocultas densas (64, 128, 128 neuronas).
* **Arquitectura 2:** 6 capas ocultas densas (64, 64, 128, 128, 256, 256 neuronas).
* **Arquitectura 3:** 10 capas ocultas densas (todas estructuradas con 128 neuronas).

A través de entrenamientos de hasta 50 épocas, las arquitecturas convergieron consistentemente en métricas de validación alrededor del 88% de *accuracy*.

### 3. Aprendizaje No Supervisado
Para explorar la estructura inherente de los datos se implementó:
* **Reducción de Dimensionalidad (PCA):** Demostró la complejidad del espacio original, ya que los dos primeros componentes principales (PC1 y PC2) explicaron únicamente el 14.7% de la varianza total.
* **Clustering:**
    * **K-Means:** Aplicando el Método del Codo sobre el espacio bidimensional de PCA, se identificó k=4 como el número óptimo de clústeres.
    * **DBSCAN:** Se trazó un gráfico de K-Distancias (K-Distance graph) fijando un valor de `eps=0.08` para aislar muestras ruidosas e identificar formaciones de clústeres densos.

---

## 🏆 Resultados y Conclusiones Principales
* Las **técnicas clásicas**, específicamente los Árboles de Decisión y las Máquinas de Vectores de Soporte, demostraron ser las de mejor rendimiento para esta naturaleza tabular, superando la barrera del 90% de exactitud y generalizando mejor que las aproximaciones profundas.
* Desde un punto de vista de negocio, el **Decision Tree Classifier** no solo es el modelo más robusto aquí, sino el más valioso: ofrece la transparencia e interpretabilidad clave requerida por las unidades de marketing para entender los motivadores detrás del comportamiento del cliente.

---
*Nota: Proyecto elaborado enteramente en Google Colab. El cuaderno principal adjunto incluye gráficos de dispersión de clústeres, evolución de accuracy/loss por épocas y matrices de correlación integrales de las variables.*
