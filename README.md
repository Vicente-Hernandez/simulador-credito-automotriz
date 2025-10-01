# simulador-credito-automotriz
Motor de simulación en Python para la generación de datasets sintéticos de origen de crédito automotriz, basado en arquetipos de cliente y reglas de negocio reales.


# 🚀 Simulador Avanzado de Datos Financieros para Crédito Automotriz

Este proyecto es una solución de alta fidelidad para uno de los desafíos más críticos en Data Science: la ausencia de datos realistas para el entrenamiento de modelos. En lugar de depender de datasets limitados, hemos construido una "fábrica" de datos sintéticos que genera un portafolio de créditos automotrices, no basado en simple aleatoriedad, sino en un ecosistema de reglas de negocio, políticas de riesgo y arquetipos de cliente interconectados.

El resultado es un motor de simulación dinámico y orientado a objetivos, que produce un dataset listo para ser explotado con modelos analíticos y de Machine Learning avanzados.

---
## 🧠 El Desafío: El Abismo entre los Datos Aleatorios y la Realidad

Todo gran proyecto de Data Science comienza con datos. Sin embargo, en la industria financiera, los datos reales son un activo protegido y complejo. La alternativa, generar datos sintéticos, a menudo fracasa al no capturar las sutilezas que definen la realidad de un negocio:

* Un cliente no es solo un sueldo; es un **arquetipo de comportamiento**.
* Una venta no es solo un monto; es el resultado de **políticas de precios y campañas comerciales** que cambian con el tiempo.
* Un portafolio de créditos no es una muestra aleatoria; es el resultado de un **proceso de aprobación y rechazo** que filtra activamente a los solicitantes.

Este simulador fue diseñado para cruzar ese abismo.

---
## 💡 La Solución: Un Ecosistema de Negocio Simulado

Este motor de simulación no genera registros aislados; crea un universo de negocio coherente. Cada operación, ya sea aprobada o rechazada, es el producto de una cadena de decisiones lógicas que imitan el mundo real.

El sistema opera de forma dinámica hasta que la cartera de créditos resultante cumple con los KPIs estratégicos del negocio, asegurando que el dataset final no solo sea rico, sino también representativo.

---
## ✨ Lógica de Negocio de Alta Fidelidad

Este motor se distingue por la profundidad y el realismo de sus reglas de negocio:

* **Precios y Line-up Reales:** Utiliza **listas de precios estáticas y diferenciadas para 2024 y 2025**, actualizando el catálogo de vehículos para descontinuar modelos y añadir nuevos según la fecha de la operación, reflejando el ciclo de vida comercial de los productos.

* **Segmentación Avanzada por Arquetipos:** Los clientes no se generan a partir de promedios geográficos. Se simulan basados en **4 arquetipos de comportamiento** ("Patrimonio Consolidado", "Profesional Endeudado", etc.), cada uno con su propia distribución de renta, score crediticio y probabilidad de ser un cliente recurrente.

* **Modelo de Riesgo Multi-Etapa:** Simula un embudo de aprobación realista. Los clientes son evaluados y pueden ser rechazados en etapas tempranas por:
    1.  **Causas Judiciales** (rechazo estocástico).
    2.  **Mal Comportamiento Financiero** (vinculado a un score crediticio muy bajo).
    3.  **Antigüedad Laboral Insuficiente** (menos de 12 meses).
    4.  **Carga Financiera Excesiva** (si la cuota supera el 33% de la renta).

* **Políticas Comerciales Dinámicas:**
    * **Tasas de Mercado:** Asigna tasas de interés basadas en un sistema de períodos (con cambios en abril de 2025) y probabilidades de mercado, incluyendo tasas preferenciales para vehículos de gama alta.
    * **Estructura de Compra:** Genera una mezcla realista de compras al **Contado (35%)** y con **Financiamiento (65%)**.
    * **Condiciones de Financiamiento:** Las opciones de pie (% de entrada) cambian en el tiempo, ampliándose a partir de abril de 2025.

* **Estructura Comercial y Geográfica:** Simula una red de concesionarios con perfiles de venta diferenciados ('alto valor' vs. 'alto volumen'), lo que influye en la mezcla de modelos vendidos en cada sucursal.

* **Generación Orientada a KPI:** El simulador no se detiene al generar un número fijo de registros. Opera en un **bucle inteligente** hasta que el dataset de operaciones **aprobadas** alcanza un objetivo de negocio real: una cartera con entre 60% y 65% de operaciones financiadas.

* **Modelo Predictivo Integrado:** Cada operación aprobada incluye una variable objetivo (`FUTURO_DEFAULT`). Esta "profecía" se calcula con un modelo logístico que considera el score, la carga financiera, el entorno macroeconómico y un **"bono de confianza"** para clientes antiguos de la marca.

---
## 🛠️ ¿Cómo Ejecutar el Simulador?

El proyecto está contenido en un único script de Python, diseñado para ser ejecutado fácilmente en Google Colab.

1.  **Abre Google Colab** y crea un nuevo cuaderno.
2.  **Copia el código** completo del archivo `.py`.
3.  **Pégalo** en una celda del cuaderno.
4.  **Ejecuta la celda.** El script instalará las dependencias, ejecutará la simulación hasta alcanzar el KPI y guardará el resultado.

---
## 📊 El Resultado: `dataset.xlsx`

El archivo de Excel de salida es un completo activo de datos con dos pestañas:

1.  **`Dataset_Completo`:** Incluye **todas** las operaciones generadas, tanto 'Aprobadas' como 'Rechazadas'. Es ideal para analizar tasas de aprobación, efectividad de las políticas de riesgo y los motivos de rechazo.
2.  **`Solo_Aprobados`:** Un subconjunto que representa la cartera final de clientes, listo para ser usado en modelos de propensión, segmentación o análisis de portafolio.

Columnas clave que encontrarás:
* `ESTADO` ('Aprobado', 'Rechazado'), `MOTIVO_RECHAZO`
* `TIPO_COMPRA` ('Contado', 'Financiado')
* `CLIENTE_ARQUETIPO`, `CLIENTE_RENTA`, `CLIENTE_SCORE`, `CLIENTE_ANTIGUO_MARCA`
* `PLAZO_MESES`, `TASA_MENSUAL`, `PIE_PORCENTAJE`, `MONTO_CAPITAL`
* `FUTURO_DEFAULT` (la variable objetivo para modelos de riesgo).

---
## 🔭 La Visión a Futuro: Fase 2

Este proyecto representa la **Fase 1**, la creación de una base de datos de origen de créditos. La visión completa del proyecto se materializa en la **Fase 2**:

**Simulación de la Evolución del Crédito en el Tiempo.**

El siguiente gran paso es tomar este dataset y proyectar la vida de cada crédito mes a mes, simulando:
* **Comportamiento de Pago Mensual:** Si el cliente paga, se atrasa o cae en default.
* **Depreciación del Vehículo:** Cálculo del valor del auto a lo largo del tiempo.
* **Decisión de Renovación:** Simulación de la decisión del cliente al final de los créditos con opción de renovación.
