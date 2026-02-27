# Modelo de Credit Scoring: Predicción de Riesgo Crediticio

Resumen Ejecutivo
Este proyecto desarrolla un modelo de Machine Learning diseñado para automatizar y optimizar la evaluación de riesgo crediticio en una cartera de clientes minoristas. El objetivo principal es predecir la probabilidad de incumplimiento (default) de un préstamo, permitiendo a la entidad financiera reducir la pérdida esperada y mejorar la rentabilidad de su cartera.

---

Datos y Preparación (Feature Engineering)
Se procesó un dataset histórico de más de 32.000 solicitudes de crédito. El pipeline de datos incluyó:
* Limpieza y tratamiento de nulos: Imputación de valores faltantes en tasas de interés y antigüedad laboral utilizando la mediana para evitar distorsiones por outliers.
* Filtros lógicos de negocio: Eliminación de registros atípicos o errores de carga sistémica (ej. antigüedades laborales superiores a la edad biológica).
* Transformación de variables: Aplicación de One-Hot Encoding a variables categóricas (estado de vivienda, propósito del préstamo) con la técnica drop_first para evitar la multicolinealidad perfecta.
* Escalado: Estandarización de variables continuas (StandardScaler) para homogeneizar el peso matemático de atributos como el ingreso anual y la edad.

---

Modelado Predictivo y Calibración
Se implementó un algoritmo de Regresión Logística. Durante el análisis inicial se detectó un fuerte desbalanceo de clases, lo que generaba un modelo excesivamente optimista.

* Estrategia de mitigación: Se aplicó una penalización matemática (class_weight='balanced') para priorizar la detección de la clase minoritaria (deudores).
* Resultado: La sensibilidad (Recall) para la detección de deudores aumentó del 56% al 78%.
* Métrica global: El modelo alcanzó un ROC-AUC de 0.87, demostrando una alta capacidad de discriminación entre perfiles de riesgo.

---

Impacto Comercial
La calibración del modelo permitió captar a más de 300 deudores adicionales en el conjunto de prueba que el modelo original habría dejado pasar. En un entorno real, esta optimización representa un ahorro directo de millones en capital no recuperado, justificando el trade-off de rechazar marginalmente a algunos clientes dudosos.

---

Feature Importance
La explicabilidad del modelo reveló los principales drivers de riesgo:
* Ratio Deuda/Ingreso (DTI): Es el factor de riesgo más determinante. Altos porcentajes de endeudamiento empujan fuertemente al default.
* Tenencia de vivienda: Los clientes que alquilan (RENT) presentan un riesgo significativamente mayor, mientras que ser propietario (OWN) actúa como un fuerte escudo protector.
* Propósito del préstamo: Los créditos destinados a negocios/emprendimientos (Venture) mostraron un mejor comportamiento de pago en comparación con otros destinos.

---

Herramientas Utilizadas
* Lenguaje: Python
* Manipulación de Datos: Pandas, NumPy
* Machine Learning: Scikit-Learn
* Visualización: Matplotlib, Seaborn
