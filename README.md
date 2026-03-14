# Exploratory Data Analysis: Healthcare Dataset
Enlace a la hoja de Google Sheet donde se ha desarrollado el proyecto: https://docs.google.com/spreadsheets/d/1YlkAGp_jmGMB55m60qCLuJaTVmIjpnRUZk-DdRO3dYY/edit?usp=sharing 

Archivo con los datos originales: https://docs.google.com/spreadsheets/d/1DdoVmMMPMtk_OtI5UN8-fdcJU4jueCuhzblGT4lCyok/edit?usp=sharing 
1. ## **Descripción del proyecto**

Este proyecto realiza un **Análisis Exploratorio de Datos (EDA)** sobre un dataset sanitario disponible en Kaggle: [https://www.kaggle.com/datasets/prasad22/healthcare-dataset](https://www.kaggle.com/datasets/prasad22/healthcare-dataset)

El dataset contiene información sobre pacientes hospitalizados, incluyendo características demográficas, condiciones médicas, duración de hospitalización, hospitales, medicación y costes médicos.

El dataset incluye aproximadamente **50.000 registros de pacientes** y **15 variables** relacionadas con información clínica y administrativa.

El objetivo del proyecto es:

* Comprender la estructura del dataset  
* Realizar un proceso de **limpieza y preparación de datos**  
* Explorar patrones relacionados con **costes hospitalarios, duración de estancias médicas y enfermedades**  
* Generar métricas que permitan analizar el comportamiento de los datos

El análisis se centra en **identificar anomalías, crear nuevas variables y analizar relaciones entre variables clínicas y económicas**.

El dataset utilizado es **sintético**, es decir, los datos han sido generados artificialmente para fines educativos y de práctica en análisis de datos.

2. ## **Estructura del proyecto**

El proyecto se organiza de la siguiente manera:

project/  
│  
├── data/  
│   └── healthcare\_dataset.csv        \# Dataset original descargado de Kaggle  
│  
├── eda/  
**│   └── hospital\_analysis.xlsx        \# Archivo con el análisis exploratorio en Google Sheets**  
│  
├── README.**md**                         \# Descripción del proyecto

3. ## **Instalación y requisitos**

Este proyecto se ha desarrollado utilizando herramientas de análisis de datos accesibles sin programación.

**Herramientas utilizadas:**

* Google Sheets  
* Tablas dinámicas  
* Funciones de limpieza y transformación de datos  
* Macros (automatización de procesos repetitivos)  
* Análisis Exploratorio de Datos (EDA)  
* Visualización de datos mediante **dashboard interactivo en Google Sheets**


4. ## **Proceso de limpieza y preparación de datos**

Durante el proceso de análisis exploratorio se realizaron diversas tareas de **data cleaning** para asegurar la calidad del dataset.

1) ### **Corrección del formato de Billing Amount**

Se detectó un problema de formato en la variable **Billing Amount**.  
Los valores aparecían extremadamente altos debido a una interpretación incorrecta de los separadores decimales al importar el CSV en Google Sheets.

El dataset original utilizaba formato inglés: 18856.2813059781

Sin embargo, Google Sheets interpretó los puntos como separadores de miles, generando valores incorrectos como: 18.856.281.305.978.100

Para corregirlo se realizó:

* Eliminación de separadores incorrectos  
* Conversión a formato numérico  
* Reescalado de los valores

2) **Normalización de nombres de pacientes**

Se detectaron inconsistencias en el formato de nombres (mayúsculas, minúsculas y espacios). Se utilizó la función: \=NOMPROPIO(ESPACIOS(A2)) para:

* Eliminar espacios innecesarios  
* Estandarizar el formato de mayúsculas.

3) **Eliminación de duplicados**

Se comprobó la existencia de registros duplicados mediante:

* Formato condicional y las fórmulas:  
  \=FILTER(Tabla\_1;[CONTAR.SI](http://CONTAR.SI)(Tabla\_1\[Name\];Tabla\_1\[Name\])\>1)  
  \=CONTAR.SI($A$2:$A;$A2)\>1   
* Funciones de filtrado.

Finalmente se eliminaron las filas duplicadas considerando la coincidencia en todas las columnas relevantes.

4) **Tratamiento de valores faltantes**

Se verificó la existencia de valores nulos utilizando:

* Estadísticas de columna  
* Filtrado de valores vacíos

No se encontraron **datos faltantes** en el dataset.

5) **Identificación de valores anómalos**

Se detectaron **96 valores negativos** en la variable **Billing Amount**. Para detectarlos se creó una nueva hoja y se utilizó la fórmula: \=CONTAR.SI(Tabla\_1\[Billing Amount\];"\<0")

Dado que los costes hospitalarios no pueden ser negativos, estos registros se consideraron anomalías y se eliminaron del dataset.

Estos valores representaban aproximadamente el 0,19% de los datos (96 / 50.000), por lo que su eliminación no afecta significativamente al análisis.

6) **Revisión de tipos de datos**

Se verificó que cada variable tuviera el formato adecuado:

| Variable | Tipo |
| ----- | ----- |
| Age | Numérico |
| Billing Amount | Numérico |
| Date of Admission | Fecha |
| Discharge Date | Fecha |
| Room Number | Numérico |

7) **Creación de nuevas variables**

Durante el análisis se generaron nuevas variables para facilitar el estudio del dataset.

- ### **Duración de hospitalización**

Se creó la variable: Días hospitalizado \= Fecha alta \- Fecha admisión

Esta métrica permite analizar la duración de las estancias médicas.

\-    **Coste por día hospitalizado**

Se generó una métrica adicional: Billing per Day \= Billing Amount / Días hospitalizado

Esta variable permite comparar el coste hospitalario ajustado por duración de estancia.

**5\. Proceso de análisis de datos**

Durante el proceso de análisis se construyó un **dashboard** que permite visualizar las principales métricas del dataset.

El dashboard incluye:

* Número total de pacientes

* Facturación hospitalaria total

* Coste medio por paciente

* Coste medio por día hospitalizado

* Distribución de pacientes por condición médica

* Distribución por tipo de admisión

* Distribución de medicación

* Distribución de costes hospitalarios por rangos

Este dashboard se construyó utilizando **tablas dinámicas y gráficos** con el objetivo de facilitar la exploración visual del dataset y detectar patrones en los datos.

Las visualizaciones permiten analizar de forma rápida:

* La distribución de enfermedades

* La duración de las estancias hospitalarias

* La relación entre costes médicos y condiciones clínicas

Además, se implementaron **macros con botones interactivos** que permiten cambiar entre distintas vistas del análisis, pacientes y billing amount (coste hospitalario), mejorando la navegación dentro del dashboard.

## **6\. Resultados y conclusiones**

El análisis exploratorio permitió identificar varios patrones relevantes en el dataset.

1) ### **Distribución de pacientes**

El dataset contiene **49.904 pacientes** con una distribución prácticamente equilibrada por género:

* Mujeres: **24.957**

* Hombres: **24.947**

Esto indica que el dataset no presenta sesgos significativos en la variable género.

2) **Distribución por condición médica**

Las condiciones médicas presentan una distribución muy similar en número de pacientes:

| Condición | Pacientes |
| ----- | ----- |
| Arthritis | 8430 |
| Asthma | 8254 |
| Cancer | 8278 |
| Diabetes | 8366 |
| Hypertension | 8301 |
| Obesity | 8275 |

Esto sugiere que el dataset fue generado de forma **balanceada entre enfermedades**, lo que facilita las comparaciones entre grupos.

3) **Coste hospitalario**

El coste hospitalario registrado en el dataset es de **702.288.403,65 €.**

A partir de esta cifra se calculó el coste medio hospitalario por paciente, que se sitúa  en **14.073 €** por paciente.

Este KPI permite comprender el gasto medio asociado a cada ingreso hospitalario dentro del dataset.

El análisis del **coste medio diario por condición médica** muestra valores relativamente similares entre enfermedades, situándose aproximadamente entre **1.760 € y 1.915 € por día hospitalizado.**

Se puede ver que las enfermedades con mayor coste diario medio son:

* **Diabetes**

* **Obesity**

* **Hypertension**

Mientras que **Asthma** presenta el coste medio diario más bajo.

4) **Duración de hospitalización**

El análisis de la duración de estancia muestra que la mayoría de los pacientes se concentran entre **1 y 30 días de hospitalización**

La distribución de días hospitalizados es bastante homogénea entre las diferentes condiciones médicas, sin diferencias extremas entre enfermedades.

5) **Medicación**

Las medicaciones analizadas presentan una distribución bastante equilibrada entre pacientes:

| Medicación | Pacientes |
| ----- | ----- |
| Aspirin | 9971 |
| Ibuprofen | 9986 |
| Lipitor | 10013 |
| Paracetamol | 9961 |
| Penicillin | 9973 |

Esto indica que las medicaciones se distribuyen de forma relativamente uniforme entre los pacientes del dataset.

6) **Tipo de admisión**

Las admisiones hospitalarias se distribuyen en tres categorías:

* Elective

* Emergency

* Urgent

Los valores son similares entre ellas, lo que sugiere que el dataset simula distintos tipos de ingreso hospitalario de forma equilibrada.

7) **Distribución de coste hospitalario**

El análisis del coste hospitalario agrupado muestra que la mayoría de los casos se concentran en rangos de entre **0 € y 30.000 €**

A medida que aumenta el coste hospitalario, el número de casos disminuye progresivamente, mostrando una distribución decreciente típica en costes sanitarios.

## **7\. Próximos Pasos**

Como continuación del proyecto se podrían explorar varias líneas de análisis adicionales.

### **Análisis estadístico**

* Estudiar nuevas correlaciones entre variables como **edad, duración de hospitalización y coste médico.**  
* Aplicar técnicas de análisis estadístico para identificar patrones más complejos.

**Análisis predictivo**

El dataset podría utilizarse para desarrollar modelos predictivos orientados a:

* Estimar **coste hospitalario esperado.**  
* Predecir **duración de hospitalización.**  
* Analizar probabilidades de distintos tipos de admisión.

**Análisis de eficiencia hospitalaria**

Una posible extensión del proyecto sería analizar métricas como:

* Coste por día hospitalizado

* Duración media de estancias

* Distribución de recursos médicos.

## **8\. Contribuciones**

Las contribuciones a este proyecto son bienvenidas. Si deseas mejorar el análisis, proponer nuevas visualizaciones, optimizar el proceso de limpieza de datos o añadir nuevas métricas, puedes hacerlo mediante sugerencias o mejoras sobre el proyecto.

## **9\. Autores**

La autora del proyecto es Isabel García Guillén.

Este proyecto fue desarrollado como parte de un ejercicio de **Análisis Exploratorio de Datos (EDA)** utilizando herramientas de análisis accesibles como **Google Sheets, tablas dinámicas, macros y visualización mediante dashboard**.

