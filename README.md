# Análisis de Evasión de Clientes (Churn) - Telecom X
**Descripción del Proyecto**

Telecom X, una empresa del sector telecomunicaciones, ha enfrentado un creciente índice de cancelación de contratos por parte de sus clientes. Con el objetivo de comprender las causas detrás de este fenómeno, se realizó un análisis exploratorio de datos seguido por la construcción y evaluación de modelos predictivos que permitan anticipar la cancelación de clientes (churn).

El objetivo final del análisis es identificar qué factores están más relacionados con la cancelación, con el fin de ayudar a la empresa a diseñar estrategias de retención más efectivas.

## Estructura del Proyecto
Este proyecto fue desarrollado en Google Colab utilizando las siguientes bibliotecas:

- import pandas as pd
- import numpy as np
- import matplotlib.pyplot as plt
- import seaborn as sns
- from sklearn.model_selection import train_test_split
- from sklearn.ensemble import RandomForestClassifier
- from sklearn.linear_model import LogisticRegression
- from sklearn.preprocessing import StandardScaler
- from sklearn.pipeline import Pipeline
- from sklearn.metrics import (accuracy_score, precision_score, recall_score, f1_score, confusion_matrix, classification_report)
- from IPython.display import display

### ⚙️ ¿Cómo Ejecutar el Análisis?

- Extraer el .csv adjunto, en el entorno del proyecto en Google Colab.
- Cargar el dataset original (df).
- Ejecutar las celdas en orden para seguir todas las etapas:

### 🧹 Limpieza y Transformación de Datos

- Se eliminaron columnas irrelevantes como clienteID.
- Se trataron valores faltantes.
- Se codificaron variables categóricas:
  - Variables binarias como Genero, Pareja, AdultoMayor se codificaron como 0 y 1.
  - La variable objetivo Cancelacion fue codificada como 0 = “Sí se fue” y 1 = “No se fue”.
  - Otras variables categóricas se transformaron mediante One-Hot Encoding.
  - Se creó la variable PagoDiario dividiendo PagoMensual por 30.

## Análisis Exploratorio

- La proporción de cancelación fue de aproximadamente 27% (cancelaron) frente a 73% (se quedaron).
- Se evaluaron las correlaciones de las variables con la variable objetivo Cancelacion.
- Variables más correlacionadas positivamente con la cancelación:

    SeguridadOnline_No
    SoporteTecnico_No
    ServicioInternet_FibraOptica
    MetodoPago_ElectronicCheck
    RespaldoOnline_No
    PagoMensual
    Variables correlacionadas negativamente:
    TipoContrato_TwoYear
    MesesContrato
    SoporteTecnico_Si
    SeguridadOnline_Si

## Modelos Predictivos

Se desarrollaron y compararon dos modelos de clasificación:
**1. Random Forest (sin normalización)**
Accuracy: 77%
F1 Score: 0.53 (para clientes que se cancelan)
Buen rendimiento general, pero con menor recall en detectar cancelaciones.

**2. Regresión Logística (con normalización)**
Accuracy: 75%
F1 Score: 0.61 (para clientes que se cancelan)
Mejor recall que Random Forest, lo que lo hace más útil en detección de clientes que se van.

Ambos modelos fueron evaluados en los datos de prueba (30% del total), después de ser entrenados con los datos de entrenamiento (70%).

## Importancia de Variables
**Regresión Logística (Coeficientes)**
Las variables con mayor influencia negativa (protegen contra la cancelación):

    TipoContrato_TwoYear
    TipoContrato_OneYear
    SoporteTecnico_Si
    MesesContrato

Las variables que aumentan la probabilidad de cancelación:

    MetodoPago_ElectronicCheck
    ServicioInternet_FibraOptica
    SeguridadOnline_No

**Random Forest (Importancia de características)**

Las variables más importantes fueron:

    PagoAcumulado
    PagoMensual
    MesesContrato
    SoporteTecnico_No
    SeguridadOnline_No

## Conclusiones

- Los clientes con contratos más largos (One Year, Two Year) y más tiempo en la empresa (MesesContrato) tienen una menor tasa de cancelación.
- Los clientes con servicios como Soporte Técnico y Seguridad Online están más fidelizados.
- El pago mensual alto y el uso de Fibra Óptica se asocian a una mayor cancelación, posiblemente por percepción de bajo valor o mala experiencia.
- El método de pago Electronic Check se asocia fuertemente con la evasión.
- La cancelación suele ocurrir dentro de los primeros 10 meses, lo que sugiere un período crítico de retención en el primer año.
