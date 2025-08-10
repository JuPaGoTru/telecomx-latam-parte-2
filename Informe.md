# Informe de Modelado de Churn de Clientes

## 1. Introducción  
El objetivo de este análisis es identificar los factores que más influyen en la cancelación de clientes (*churn*) y evaluar diferentes modelos de machine learning para predecir este comportamiento. Se probaron **Regresión Logística** y **Random Forest**, tanto en su forma original como aplicando la técnica de sobremuestreo **SMOTE** para balancear la clase minoritaria.

## 2. Modelos Evaluados y Rendimiento

| Modelo                         | Accuracy | Precisión | Recall  | F1-score | Observaciones Clave |
|-------------------------------|----------|-----------|---------|----------|---------------------|
| Regresión Logística            | 0.7965   | 0.6362    | 0.5455  | 0.5873   | Buen equilibrio general, mejor precisión que recall. |
| Random Forest                  | 0.7761   | 0.5961    | 0.4866  | 0.5358   | Ligera caída en recall respecto a la regresión logística. |
| Regresión Logística + SMOTE    | 0.7487   | 0.5176    | 0.7879  | 0.6247   | Mayor recall, captura más casos de churn a costa de precisión. |
| Random Forest + SMOTE          | 0.7686   | 0.5706    | 0.5187  | 0.5434   | Rendimiento balanceado, sin mejoras significativas con SMOTE. |

**Conclusiones sobre el rendimiento:**  
- **Mejor precisión:** Regresión Logística sin SMOTE.  
- **Mejor recall:** Regresión Logística con SMOTE.  
- **Modelo más equilibrado para negocio:** depende del objetivo; si se busca **minimizar pérdidas** (detectar la mayor cantidad posible de clientes en riesgo), la Regresión Logística con SMOTE es preferible, aunque implique más falsos positivos.

## 3. Principales Factores que Influyen en la Cancelación

### 3.1 Variables más importantes en la **Regresión Logística con SMOTE**  
A partir de los coeficientes absolutos más altos, se identificaron las siguientes variables con mayor impacto:

| Variable                             | Coeficiente | Interpretación                                                       |
|------------------------------------|-------------|--------------------------------------------------------------------|
| InternetService_No                  | -0.912      | No tener servicio de internet reduce la probabilidad de churn.    |
| InternetService_Fiber optic         | 0.846       | Tener internet fibra óptica aumenta riesgo de cancelación.         |
| Contract_Month-to-month             | 0.723       | Contratos mensuales aumentan significativamente el churn.          |
| Contract_Two year                  | -0.721      | Contratos de dos años reducen notablemente el churn.               |
| PaperlessBilling                   | 0.510       | Facturación sin papel se asocia a mayor churn.                      |
| TechSupport                       | -0.460      | Contar con soporte técnico reduce la probabilidad de churn.        |
| StreamingTV                       | 0.363       | Tener servicio de streaming TV incrementa el riesgo.               |
| OnlineSecurity                    | -0.329      | Seguridad online está relacionada con menor churn.                 |
| PaymentMethod_Electronic check    | 0.326       | Pago con cheque electrónico aumenta probabilidad de cancelación.   |
| StreamingMovies                   | 0.249       | Servicio de streaming de películas incrementa el riesgo.           |

**Interpretación:**  
Variables relacionadas con el tipo de contrato, servicios contratados y método de pago tienen un peso fuerte en la probabilidad de churn. La ausencia de internet o servicios de soporte reduce la cancelación, mientras que ciertos servicios adicionales y facturación sin papel la aumentan.

---

### 3.2 Variables más importantes en el **Random Forest con SMOTE**

| Variable                         | Importancia | Interpretación                                                  |
|---------------------------------|-------------|-----------------------------------------------------------------|
| tenure                          | 0.153       | Tiempo como cliente es la variable con mayor peso.              |
| Charges.Monthly                 | 0.112       | Cargos mensuales altos están asociados a mayor churn.           |
| Cuentas_Diarias                | 0.110       | Nuevas métricas diarias también influyen en la predicción.      |
| Contract_Month-to-month        | 0.110       | Contratos mensuales con impacto alto en churn.                   |
| PaymentMethod_Electronic check | 0.084       | Pago con cheque electrónico aumenta la probabilidad de churn.   |
| Contract_Two year              | 0.048       | Contrato de dos años reduce churn.                               |
| PaperlessBilling              | 0.043       | Facturación sin papel tiene efecto positivo en churn.            |
| Partner                       | 0.033       | Estado de pareja tiene impacto menor pero presente.              |
| TechSupport                  | 0.031       | Soporte técnico reduce el churn.                                 |
| InternetService_Fiber optic   | 0.031       | Fibra óptica aumenta la probabilidad de cancelación.             |

**Interpretación:**  
El Random Forest destaca el tiempo de permanencia y los cargos mensuales como las variables clave, junto con el contrato y método de pago, similar a la regresión logística. Además, métricas diarias específicas como `Cuentas_Diarias` emergen como variables relevantes.

---

## 4. Matrices de Confusión y Análisis  
- Sin SMOTE, ambos modelos tienden a **subestimar** la clase churn, reflejado en un recall moderado.  
- Con SMOTE, se aumenta la detección de churn (mayor recall), pero se incrementan los falsos positivos (menor precisión).  
- Para un caso de negocio donde es más costoso perder un cliente que contactar a un no-churn, **el aumento de recall es deseable**.

## 5. Estrategias de Retención Propuestas  
Basadas en los factores identificados:

1. **Fidelización temprana**  
   - Implementar programas de bienvenida y beneficios exclusivos para clientes en los primeros 6 meses.  
2. **Incentivar contratos anuales**  
   - Ofrecer descuentos o beneficios exclusivos para clientes que cambien de mensual a anual.  
3. **Optimizar precios y paquetes**  
   - Revisar tarifas para clientes con cargos altos y ofrecer paquetes personalizados.  
4. **Promover servicios complementarios**  
   - Incluir soporte técnico y seguridad online como parte de planes estándar para aumentar el valor percibido.  
5. **Facilitar pagos automáticos**  
   - Incentivar la adopción de métodos de pago recurrentes con descuentos pequeños o beneficios adicionales.  
6. **Revisar facturación sin papel**  
   - Aunque es conveniente, podría asociarse a mayor churn; analizar comunicación y experiencia de usuario en este canal.  
7. **Ajustar oferta de servicios de streaming**  
   - Evaluar el impacto de servicios como Streaming TV y Movies, optimizando su valor para reducir cancelaciones.

## 6. Conclusión  
La Regresión Logística con SMOTE se presenta como la mejor opción cuando el objetivo principal es **maximizar la detección de clientes en riesgo**, a pesar de su menor precisión. Sin embargo, si se busca un modelo más conservador en cuanto a falsos positivos, la Regresión Logística sin SMOTE es preferible. Las variables clave identificadas permiten focalizar estrategias concretas para reducir churn, mejorando retención y satisfacción.
