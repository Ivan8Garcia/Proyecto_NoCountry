# ✈️ Flight On Time  
### Predicción de Retrasos en Vuelos

## 📌 Descripción del Proyecto
**Flight On Time** es un sistema predictivo que estima si un vuelo despegará puntual o con retraso, utilizando información histórica de vuelos a partir de una base de datos y variables operativas disponibles antes del despegue..

Este repositorio contiene en análisis realizado por el equipo de **Data Science**, correspondiente a un **MVP** eficiente para probarse en producción por el equipo de Backend.

El sistema fue desarrollado como parte de la **Hackathon Alura-No Country** para el **grupo G8**.

---

## 🎯 Situación problema
Los retrasos en vuelos generan:
- Insatisfacción en los pasajeros,
- Costos operativos para las aerolíneas,
- Problemas logísticos en aeropuertos (conexiones perdidas, reprogramaciones).

La solución del sistema busca **anticipar el riesgo de retraso** antes de la salida del vuelo, apoyando la toma de decisiones operativas.

---

## 🧠 Objetivo del Proyecto
Desarrollar un modelo de *Machine Learning* capaz de predecir si un vuelo presentará un **retraso mayor a 15 minutos en su salida**, utilizando la información disponible antes del despegue.

---

## 📊 Dataset
- **Fuente:** Dataset público con un histórico de vuelos (2019–2023)
- **Enlace:** https://www.kaggle.com/datasets/patrickzel/flight-delay-and-cancellation-dataset-2019-2023?resource=download

### ⚙️ Estrategia de carga de datos
Para evitar sobrecarga de memoria y optimizar el análisis del modelo, se realizó la carga de la información, seleccionando las **8 columnas más relevantes** para el desarrollo del reto:

| Variable     | Descripción                                   |
|--------------|-----------------------------------------------|
| FL_DATE      | Fecha del vuelo                               |
| AIRLINE      | Aerolínea                                     |
| ORIGIN       | Aeropuerto de origen                          |
| DEP_TIME     | Hora de salida programada                     |
| DEP_DELAY    | Retraso del vuelo en minutos                  |
| TAXI_OUT     | Tiempo de rodaje previo al despegue           |
| DISTANCE     | Distancia del vuelo                           |
| CANCELLED    | Indicador de cancelación                      |

---

## 🧹 Limpieza y Preparación de Datos
Se aplicaron las siguientes etapas de limpieza:
- Eliminación de vuelos cancelados,
- Eliminación de registros con valores críticos faltantes, nulos o duplicados.

Este proceso permitió evitar problemas de memoria en Google Colab, analizando únicamente la información relevante del Dataset para que el modelo se pueda entrenar con datos completos de vuelo.

El resultado final fue de: **2.920.860 registros de vuelos** para el entrenamiento.

---

## 🛠️ Variables
Se definió la variable objetivo como **RETRASADO** bajo los siguientes criterios:
- **1:** → vuelo con más de 15 minutos de retraso en el despegue  
- **0:** → vuelo puntual  

El dataset presenta un desbalance natural, reflejando el comportamiento real del sistema aéreo.

A partir de la información de los vuelos, se generaron las siguientes variables clave para analizar los patrones en la predicción de retrasos de los vuelos:
- `DEP_HOUR`: hora de salida,
- `DAY_OF_WEEK`: día de la semana (0 = lunes, 6 = domingo),
- `IS_WEEKEND`: indicador de fin de semana.

---

## 📈 Análisis Exploratorio de Datos (EDA)
El análisis exploratorio permitió identificar patrones relevantes como:
- Mayor riesgo de retraso en determinadas horas del día,
- Diferencias en el comportamiento según el día de la semana,
- Comportamientos diferenciados entre aerolíneas y países.

---

## 🤖 Modelado
Se entrenó un modelo basado en el algoritmo **Random Forest Classifier**, seleccionado por su precisión predictiva y control del sobreajuste en la muestra de datos.

### Las variables seleccionadas para el modelo, que representan factores operativos reales y se encuentran disponibles antes del despegue, fueron:
- `DEP_HOUR`
- `DAY_OF_WEEK`
- `IS_WEEKEND`
- `DISTANCE`
- `TAXI_OUT`
- `AIRLINE`

El modelo final logra identificar aproximadamente el **64 % de los vuelos retrasados**.

---

## 🔍 Explicabilidad del Modelo
El análisis de las variables en el modelo muestra que la **hora de salida (DEP_HOUR)** es el factor más influyente en la predicción de retrasos en los vuelos, seguida de la **distancia del vuelo**.

---

## 🔌 Integración y Validación con Backend
El proyecto fue entrenado en **scikit-learn** y almacenado en formato **PKL**.  
Para su consumo en backend, se realizó una conversión del modelo al formato **ONNX**, destinada a probarse en entornos de producción.

### 🔄 Equivalencia entre modelo PKL y ONNX
Se validó que ambos formatos representan el mismo flujo lógico. El modelo ONNX es una traducción directa del pipeline de scikit-learn, manteniendo la lógica de predicción.

---

## 📦 Entregables para Producción
- `flight_delay_model_backend.pkl`  
  → Modelo original con pipeline completo usado en Python

- `flight_delay_model.onnx`  
  → Modelo compatible para consumo desde backend

---

## 🚀 Cómo Ejecutar el Notebook
1. Abrir el notebook en **Google Colab** o **Jupyter Notebook**.
2. Ejecutar las celdas en orden.
3. Al finalizar, se generarán los archivos del modelo para backend.

---

## 🔮 Future Work -Líneas de mejora consideradas:
- Incorporación de variables meteorológicas para análisis,
- Optimización adicional del uso de memoria,
- Calibración de probabilidades del modelo.

---

## 👥 Equipo
Proyecto desarrollado para la **Hackatón G8 Alura-No Country** por un equipo multidisciplinario de **Data Science** y **Backend**.  
**Grupo H12-25-L Equipo 24**

---

## ✅ Estado del Proyecto
✔ MVP funcional  
✔ Modelo entrenado y evaluado  
✔ Modelo validado para consumo vía API en producción

---

## 👥 Equipo
Proyecto desarrollado como parte del Hackathon de Alura Latam (Oracle).

Equipo: H12-25-L-Equipo 24 - FlightOnTime

---
