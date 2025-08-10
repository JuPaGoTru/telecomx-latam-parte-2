# Proyecto de Predicción de Cancelación de Clientes (Churn) - Telecom X

## Descripción  
Este proyecto tiene como objetivo analizar y predecir la cancelación de clientes (*churn*) en la empresa de telefonía Telecom X. Se utilizan técnicas de machine learning para identificar patrones y factores clave que influyen en la cancelación, así como para construir modelos predictivos que permitan anticipar qué clientes están en riesgo.

---

## Contenido del Proyecto

- **Preprocesamiento:**  
  - Tratamiento de valores faltantes y categóricos.  
  - Ingeniería de características.  
  - Balanceo de clases usando SMOTE para manejar el desbalance entre clientes que cancelan y los que no.

- **Modelado:**  
  - Regresión Logística  
  - Random Forest  
  Ambos modelos se entrenan con y sin aplicación de SMOTE para evaluar el impacto del balanceo en el rendimiento.

- **Evaluación:**  
  - Métricas: Accuracy, Precisión, Recall, F1-score.  
  - Análisis de matriz de confusión.  
  - Interpretación de variables importantes para entender qué factores influyen más en la cancelación.

- **Estrategias de Retención:**  
  Basadas en los hallazgos, se proponen recomendaciones para reducir churn.

---

## Estructura del Repositorio
  - 📊 TelecomX_LATAM_Parte_2.ipynb # Análisis exploratorio (EDA), visualizaciones y conclusiones
  - 📄 README.md # Este archivo
  - 📄 informe.md # Informe final


---

## Requisitos

- Python 3.8+  
- Librerías principales:  
  - pandas  
  - numpy  
  - scikit-learn  
  - imblearn (para SMOTE)  
  - matplotlib / seaborn (para visualización)  

---

## Resultados Clave
- La Regresión Logística con SMOTE maximiza la detección de clientes en riesgo (mejor recall), ideal para estrategias de retención proactivas.

- Los factores más importantes incluyen: tipo de contrato, tiempo como cliente, método de pago, cargos mensuales y servicios contratados (como soporte técnico y seguridad online).

- Se proponen acciones concretas como incentivos para contratos anuales, facilidades para pagos automáticos y mejora en la oferta de servicios.

--- 

## 🧠 Modelos de Machine Learning

### 🔹 Regresión Logística

![Coeficientes - Regresión Logística](img/Coeficientes_Regresion_logistica%20(SMOTE).png)

### 🔹 Random Forest

![Coeficientes - Random Forest](img/Coeficientes_Random_forest%20(SMOTE).png)
