# 🚀 Mi Viaje Construyendo un Simulador Financiero de Alta Fidelidad

Como científico de datos, mi mayor frustración siempre ha sido la misma: la escasez de datos que reflejen la verdadera complejidad de un negocio. Un `dataset` no es una simple tabla; es el eco de miles de decisiones, estrategias, políticas de riesgo y comportamientos humanos. Con esa frustración como punto de partida, me embarqué en la misión de no solo "generar datos", sino de construir un **gemelo digital** del proceso de originación de créditos en la industria automotriz.

Este repositorio contiene el resultado de esa misión: un motor de simulación dinámico y orientado a objetivos, que produce un `dataset` listo para ser explotado con modelos analíticos y de Machine Learning avanzados. Este no es solo un script, es un laboratorio para entender el riesgo.

---
## 🧠 El Desafío: El Abismo entre los Datos Aleatorios y la Realidad

Todo gran proyecto de Data Science comienza con datos. Sin embargo, en la industria financiera, los datos reales son un activo protegido y complejo. La alternativa, generar datos sintéticos, a menudo fracasa al no capturar las sutilezas que definen la realidad de un negocio:

* Un cliente no es solo un sueldo; es un **arquetipo de comportamiento**.
* Una venta no es solo un monto; es el resultado de **políticas de precios y campañas comerciales** que cambian con el tiempo.
* Un portafolio de créditos no es una muestra aleatoria; es el resultado de un **proceso de aprobación y rechazo** que filtra activamente a los solicitantes.

Este simulador fue diseñado para cruzar ese abismo.

---
## 💡 La Arquitectura: Ordenando el Caos del Mundo Real

Para simular un sistema complejo, la primera regla es no programar el caos. Es necesario ordenarlo en estructuras lógicas que representen las distintas capas del negocio. Mi enfoque se basó en tres componentes principales:

### 1. La Constitución (`Config` Class)
Decidí centralizar absolutamente todas las reglas de negocio, precios, políticas y parámetros en una única clase `Config`. Este es el "cerebro" estático de nuestro universo simulado. Contiene desde las listas de precios de cada año hasta los perfiles psicológicos de los clientes. Hacerlo así permite que cualquier experto de negocio pueda leer y validar la lógica sin necesidad de ser un programador, y hace que ajustar el modelo sea increíblemente sencillo.

### 2. La Fábrica (`GeneradorMotorCo` Class)
Esta es nuestra línea de ensamblaje. Es un motor que toma las reglas de la "Constitución" (`Config`) y las aplica secuencialmente para construir cada "historia": una solicitud de crédito. No genera un cliente y un crédito al azar; simula el proceso paso a paso, desde la evaluación inicial del cliente hasta el cálculo final de la cuota.

### 3. El Director de Orquesta (`generar_dataset_por_kpi`)
Aquí es donde la simulación cobra vida. Descubrí que generar un número fijo de registros no era suficiente. Por eso, implementé un bucle inteligente que actúa como un director de negocio: genera operaciones en lotes hasta que la cartera final de créditos **aprobados** cumple con un KPI estratégico (entre 60% y 65% de operaciones financiadas). Esto asegura que el `dataset` final no sea solo una colección de datos, sino un portafolio realista.

---
## ✨ Lógica de Negocio de Alta Fidelidad: Una Inmersión Profunda

Lo que realmente da valor a este simulador son las capas de conocimiento de la industria y las finanzas que hemos programado.

### El Cliente No Es un Promedio: La Magia de los Arquetipos
En lugar de asumir que todos en una comuna tienen ingresos similares, diseñé un sistema de **arquetipos de comportamiento** para crear perfiles de clientes diversos y realistas:

* **Patrimonio Consolidado:** Alta renta, alto score. El cliente ideal.
* **Profesional Endeudado:** Alta renta, pero score castigado. Refleja a quienes viven por encima de sus posibilidades.
* **Clase Media Estable:** Renta sólida y buen score. La columna vertebral del negocio.
* **Clase Media Emergente:** Renta más baja y score más riesgoso. El aspirante.

### El Embudo de Riesgo: Un Proceso de Rechazo Multi-Etapa
Un crédito no se aprueba o rechaza en un solo paso. Implementé un embudo de evaluación que imita el proceso de *underwriting* real, donde los clientes pueden ser rechazados por:

1.  **Causas Judiciales** (rechazo estocástico).
2.  **Mal Comportamiento Financiero** (vinculado a un score crediticio muy bajo).
3.  **Antigüedad Laboral Insuficiente** (menos de 12 meses).
4.  **Carga Financiera Excesiva** (si la cuota supera el 33% de la renta - DTI).

### El Mercado Manda: Precios y Políticas Dinámicas
El sistema está anclado a la realidad del mercado:

* **Precios y Line-up Reales:** Utiliza listas de precios estáticas y diferenciadas para 2024 y 2025, actualizando el catálogo de vehículos para descontinuar modelos y añadir nuevos según la fecha.
* **Tasas de Mercado:** Asigna tasas de interés basadas en un sistema de períodos y probabilidades de mercado, incluyendo tasas preferenciales para vehículos de gama alta.
* **Estructura de Compra:** Genera una mezcla realista de compras al **Contado (~35%)** y con **Financiamiento (~65%)**.
* **Condiciones de Financiamiento:** Las opciones de pie (% de entrada) cambian en el tiempo, ampliándose a partir de abril de 2025.

### Estructura Comercial y Geográfica
Simula una red de concesionarios con perfiles de venta diferenciados ('alto valor' vs. 'alto volumen'), lo que influye en la mezcla de modelos vendidos en cada sucursal.

### Prediciendo el Futuro: La Columna `FUTURO_DEFAULT`
Para que este `dataset` sea útil para Machine Learning, cada operación aprobada incluye una "variable objetivo" (`FUTURO_DEFAULT`). Es una **"profecía" simulada** que nos dice si ese crédito terminará o no en impago. Se calcula con un modelo de *Probability of Default (PD)* que considera el score, la carga financiera, el desempleo y un **"bono de confianza"** para clientes antiguos de la marca.

---
## 🛠️ ¿Cómo Ejecutar el Simulador?

El proyecto está contenido en un único script de Python, diseñado para ser ejecutado fácilmente en Google Colab.

1.  Abre Google Colab y crea un nuevo cuaderno.
2.  Copia el código completo del archivo `.py`.
3.  Pégalo en una celda del cuaderno.
4.  Ejecuta la celda. El script instalará las dependencias, ejecutará la simulación hasta alcanzar el KPI y guardará el resultado.

---
## 📊 El Resultado: `dataset.xlsx`

El archivo de Excel de salida es un completo activo de datos con dos pestañas:

* **`Dataset_Completo`:** Incluye **todas** las operaciones generadas, tanto 'Aprobadas' como 'Rechazadas'. Es ideal para analizar tasas de aprobación y los motivos de rechazo.
* **`Solo_Aprobados`:** Un subconjunto que representa la cartera final de clientes, listo para ser usado en modelos de propensión, segmentación o análisis de portafolio.

#### Columnas clave que encontrarás:
* `ESTADO` ('Aprobado', 'Rechazado'), `MOTIVO_RECHAZO`
* `TIPO_COMPRA` ('Contado', 'Financiado')
* `CLIENTE_ARQUETIPO`, `CLIENTE_RENTA`, `CLIENTE_SCORE`, `CLIENTE_ANTIGUO_MARCA`
* `PLAZO_MESES`, `TASA_MENSUAL`, `PIE_PORCENTAJE`, `MONTO_CAPITAL`
* `FUTURO_DEFAULT` (la variable objetivo para modelos de riesgo).

---
## 🔭 La Visión a Futuro: Fase 2

Este proyecto representa la **Fase 1**. La visión completa se materializa en la **Fase 2**: **Simulación de la Evolución del Crédito en el Tiempo.**

El siguiente gran paso, implementado en un script separado, es tomar este `dataset` y proyectar la vida de cada crédito mes a mes, simulando:

* **Comportamiento de Pago Mensual:** Si el cliente paga, se atrasa o cae en default.
* **Depreciación del Vehículo:** Cálculo del valor del auto a lo largo del tiempo.
* **Decisión de Renovación:** Simulación de la decisión del cliente al final de los créditos con opción de renovación.
