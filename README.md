Modelo de Credit Scoring: Predicción de Riesgo Crediticio

Resumen Ejecutivo
Este proyecto desarrolla un modelo de Machine Learning diseñado para automatizar y optimizar la evaluiacion de riesgo crediticio en una cartera de clientes minoristas. El objetivo principal es predecir la probabilidad de incumplimiento (default) de un prestamo, permitiendo a la entidad financiera reducir la perdida esperada y mejorar la rentabilidad de su cartera.

Datos y Reparacion (Feature Engineering)
Se procesó un dataset histórico de mas de 32.000 solicitudes de crédito. El pipeline de datos incluyó:
-Limpieza y Tratamiento de Nulos: Imputacion de valores faltantes en tasas de interés y antiguedad laboral utilizando la mediana para evitar distorsiones por outliers.
-Filtros Logicos de Negocio: Eliminacion de registros atípicos o errores de carga sistémica (ej. antiguedades laborales superiores a la edad biologica).
-Transformacion de Variables: Aplicacion de One-Hot Encoding a variables categoricas (estado de vivienda, proposito del préstamo) con técnica 'drop_first' para evitar la multicolinealidad perfecta en los cálculos matriciales. 
-Escalado: Estandarizacion de variables continuas ('StandardScaler') para homogeneizar el peso matematico de atributos como el ingreso anual y la edad.

Modelado Predictivo y Calibracion
Se implemento un algoritmo de Regresion Logistica. Durante el analisis inicial, se detectó un fuerte desbalanceo de clases (tipico en carteras de credito sanas), lo que generaba un modelo excesivamente optimista. 

Estrategia de Mitigacion: Se aplico una penalizacion matematica ('class_weight='balanced'') para priorizar la deteccion de la clase minoritaria (deudores).
-Resultado: La sensibilidad (Recall) para la deteccion de deudores aumentó drásticamente del 56% al 78%.
-Métrica Global: El modelo alcanzó un ROC-AUC de 0.87, demostrando una alta capacidad de discriminacion entre buenos y malos perfiles de riesgo.

Impacto Comercial
La calibracion del modelo permitio atrapar a mas de 300 deudores adicionales en el conjunto de prueba que el modelo oroginal habría dejado pasar. En un entorno real, esta optimizacion representa un ahorro directo de millones en capital no recuperado, justificando ampliamente el trade-off de rechazar marginalmente a algunos clientes dudosos.

Feature Importance
La explicabilidad del modelo reveló los principales drivers de riesgo para la toma de descisiones:
-Ratio Deuda/Ingreso (DTI): Es el factor de riesgo más determinante. Altos porcentajes de endeudamiento sobre el ajuste empujan fuertemente al default, confirmando empíricamente las reglas de suscripción tradicionales.
-Tenencia de Vivienda: Los clientes que alquilan ('RENT') presentan un riesgo significativamente mayor debido a la carga de sus costos fijos, mientras que ser propietario ('OWN') actúa como un fuerte escudo protector contra el incumplimento.
-Propósito del Préstamo: Paradojicamente, los créditos destinados a negocios/emprendimientos (Venture) mostraron un mejor comportamiento de pago en comparacion con otros destinos, sugiriendo un perfil de cliente orientado a la generación de rentabilidad.

Herramientas Utilizadas
Lenguaje: Python
Manipulacion de Datos: Pandas, Numpy
Machine Learning: Scikit-Learn
Visualización: Matplotlib, Seaborn
