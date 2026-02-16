# 🛡️ Detección de Fraude en Transacciones Financieras | IEEE-CIS

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![XGBoost](https://img.shields.io/badge/Model-XGBoost-orange.svg)](https://xgboost.readthedocs.io/)
[![DuckDB](https://img.shields.io/badge/Data_Engine-DuckDB-yellow.svg)](https://duckdb.org/)
[![Kaggle](https://img.shields.io/badge/Dataset-Kaggle-blue.svg)](https://www.kaggle.com/competitions/ieee-fraud-detection/data)

## 📝 Resumen Ejecutivo
Este repositorio presenta un sistema de detección de fraude transaccional de **grado bancario**. A diferencia de los modelos académicos, este pipeline implementa ingeniería de variables de **Velocity**, manejo de desbalanceo de clases mediante `scale_pos_weight` y validación de riesgo a través de la **Estadística KS** y el **Coeficiente Gini**.

## 📂 Dataset
El modelo utiliza los datos de la competencia **IEEE-CIS Fraud Detection**. 
Puedes acceder y descargar los archivos directamente desde Kaggle:

🔗 [IEEE-CIS Fraud Detection Dataset](https://www.kaggle.com/competitions/ieee-fraud-detection/data)

> **Nota:** El dataset se compone de dos tablas principales (`train_transaction` y `train_identity`) que fueron unidas mediante el `TransactionID`.

## 🚀 Key Highlights
- **Ingeniería de Datos High-Performance:** Uso de **DuckDB** para procesar millones de registros y calcular métricas de frecuencia (Velocity) en milisegundos.
- **Métricas de Riesgo:** Logro de un **KS de 0.45** (Modelo Muy Fuerte) y un **Gini de 0.59**.
- **Explicabilidad:** Implementación de **SHAP** para eliminar el efecto "caja negra" y entender los disparadores del fraude.

---

## 🔍 Análisis Criminalístico (EDA)
El análisis reveló patrones de ataque específicos que el modelo aprendió a identificar:
- **La Ventana de Riesgo:** Se detectó una anomalía matutina (07:00 - 10:00 AM) donde la probabilidad de fraude se triplica.
- **Comportamiento del Monto:** Los estafadores utilizan montos redondeados para "testear" tarjetas, lo que se convirtió en nuestra variable más predictiva: `is_round_amount`.

<img width="1000" height="466" alt="image" src="https://github.com/user-attachments/assets/1d804580-edaf-4be1-b559-23c49cc65dac" />


---

## 🧠 Modelado y Validación de Riesgo

### Estrategia de Entrenamiento
Para evitar el **Data Leakage**, se utilizó un **Time-based Split (80/20)**, asegurando que el modelo se entrene con el pasado para predecir el futuro, tal como sucede en un banco real.

### Performance del Modelo
| Métrica | Resultado | Valor de Negocio |
| :--- | :--- | :--- |
| **Gini** | **0.59** | Alta capacidad de discriminación entre clientes. |
| **KS Stat** | **0.45** | Supera el estándar de la industria (0.40). |
| **Punto de Corte** | **0.4474** | Umbral óptimo para maximizar el ahorro económico. |

<img width="750" height="543" alt="image" src="https://github.com/user-attachments/assets/45e4f25b-0c11-49b0-a462-7961542129d4" />


### Matriz de Confusión (Impacto Operativo)
Con el umbral de **0.4474**, el modelo logra atrapar el **~73% del fraude** detectado en el set de prueba.

<img width="587" height="453" alt="image" src="https://github.com/user-attachments/assets/fbbb118b-5ea4-4c4f-9c31-a98a7ebb432b" />

---


## 🧪 Explicabilidad con SHAP
El modelo basa sus decisiones en patrones lógicos y auditables:
1. **`is_round_amount`**: Principal factor de riesgo.
2. **`amt_to_mean_card1`**: Identifica desviaciones súbitas del gasto habitual del cliente.
3. **`card1_cnt`**: La historia transaccional reduce el score de riesgo (Factor de Confianza).

<img width="670" height="440" alt="image" src="https://github.com/user-attachments/assets/7371e223-0a38-44b5-9bef-ab64e5c94ff1" />


---

## 🛠️ Estructura del Proyecto
- `notebooks/Detección de Fraude(XBoost).ipynb`: Procesamiento masivo de datos; Entrenamiento, KS, Gini y SHAP; Matriz de Confusión

---
