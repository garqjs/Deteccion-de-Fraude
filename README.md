# Prediccion-de-Riesgo-de-Credito

📝 Descripción del Proyecto
Este proyecto desarrolla un sistema de clasificación binaria para predecir la probabilidad de que un solicitante de crédito incurra en impago (default). Utilizando el dataset de Home Credit, se integraron múltiples fuentes de datos para construir un perfil de riesgo integral, permitiendo una toma de decisiones basada en evidencia estadística.

📈 Impacto de Negocio
El modelo no solo busca precisión técnica, sino rentabilidad financiera. Se implementó un análisis de optimización de umbral (threshold tuning) para equilibrar el costo de los Falsos Negativos (créditos impagados) frente al costo de oportunidad de los Falsos Positivos (créditos rechazados a buenos clientes).

🛠️ Tech Stack & Metodología
Lenguaje: Python.
Librerías: Pandas, NumPy, Scikit-learn (Logistic Regression), Seaborn, Matplotlib.
Ingeniería de Datos: Unión de tablas relacionales (application, bureau, previous_application), tratamiento de nulos y One-Hot Encoding.
Optimización: Escalado de variables y auditoría de dimensionalidad.

🧬 Pipeline del Proyecto
1. Exploratory Data Analysis (EDA)
Análisis de correlación con el Target para identificar los principales factores de riesgo (ej. Edad del cliente, historial de créditos previos). Implementación de mapas de calor y distribuciones de densidad.

2. Feature Engineering
Creación de variables sintéticas como la relación deuda/ingreso y métricas agregadas del historial crediticio externo (Bureau).

3. Entrenamiento y Evaluación
Modelo: Regresión Logística con regularización.

Métricas: Foco en AUC-ROC para medir la capacidad de discriminación del modelo.

Análisis por Deciles: Segmentación de la población por probabilidad de riesgo para validar la consistencia del modelo.

4. Simulación "What-If"
Creación de un "Cliente Base" para realizar simulaciones de riesgo ante cambios en variables específicas, demostrando la sensibilidad y estabilidad del modelo.

📊 Resultados Clave
AUC-ROC Score:

<img width="702" height="548" alt="image" src="https://github.com/user-attachments/assets/9a23b10e-7d64-4595-b2ce-b114fc3b8070" />


**Insights:**

🔍 Interpretación de Factores de Riesgo vs. Protección

La gráfica muestra cómo cada variable empuja la probabilidad de impago hacia arriba (Riesgo) o hacia abajo (Protección). La magnitud (largo de la barra) indica qué tan fuerte es ese impacto.

1. 🚩 Factores de Riesgo (Barras Rojas / Coeficientes Positivos)
Estas variables aumentan la probabilidad de que el cliente caiga en default.

FLAG_EMP_PHONE y DAYS_EMPLOYED: Son los predictores más fuertes. Indican que la situación laboral (o la forma en que se valida) es el mayor determinante de riesgo. Curiosamente, en este dataset, a menudo un valor alto en DAYS_EMPLOYED (si no está normalizado) puede actuar como un proxy de inestabilidad o falta de datos.

AMT_CREDIT: A mayor monto de crédito solicitado, mayor es el riesgo percibido por el modelo. Esto es lógico: deudas más grandes son más difíciles de servir.

2. 🛡️ Factores de Protección (Barras Verdes / Coeficientes Negativos)
Estas variables disminuyen la probabilidad de impago; son indicadores de un cliente "sano".

AMT_GOODS_PRICE: Es el factor de protección más fuerte. Indica que cuando el crédito está respaldado por un bien de alto valor, el cliente tiene más incentivos para pagar.

EXT_SOURCE_1, 2 y 3: Estas son puntuaciones de crédito externas. El hecho de que tengan coeficientes negativos importantes confirma que estas fuentes externas son vitales para validar la solvencia del cliente.

PREV_RATE_INTEREST_PRIVILEGED_mean: Sugiere que clientes que han tenido tasas preferenciales en el pasado tienden a ser mejores pagadores.

<img width="1271" height="709" alt="image" src="https://github.com/user-attachments/assets/54a6fbc5-ab49-4c11-b6cd-cde900b694a8" />




Optimización Económica: El ajuste del umbral de decisión permitió una reducción proyectada en pérdidas por impago en comparación con el modelo base.

--- Análisis Económico ---

Utilidad Proyectada SIN modelo: $63,426,000.00

Utilidad Proyectada CON modelo: $61,806,000.00

Impacto Económico del Modelo:  $-1,620,000.00

Evaluación con Umbral Estricto (0.3):

--- Análisis Económico ---

Utilidad Proyectada SIN modelo: $63,426,000.00

Utilidad Proyectada CON modelo: $33,598,000.00

Impacto Económico del Modelo:  $-29,828,000.00



📁 Estructura del Repositorio
notebooks/: Google Colab con el análisis paso a paso.

data/: (Opcional) Enlace al dataset original o muestra de datos.

src/: Scripts de limpieza y modelado.

README.md: Descripción del proyecto.
