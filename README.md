# MCDI504 - Machine Learning I - Grupo 2

Repositorio de las evaluaciones formativas y sumativas de Machine Learning I.
El proyecto documenta el análisis de datos, la preparación metodológica, el
entrenamiento y la evaluación de modelos supervisados mediante notebooks
reproducibles.

## Integrantes

- Enzo Pinilla
- Claudio Alarcón
- Luis Rodrigo Espinoza

## Fase 1 - Definición y orientación de la situación

La primera fase utiliza el dataset Iris para definir y justificar un problema
de clasificación supervisada multiclase.

- Variable objetivo: `Species`.
- Variables predictoras: `Sepal.Length`, `Sepal.Width`, `Petal.Length` y
  `Petal.Width`.
- Actividades principales: definición del problema, análisis exploratorio,
  evaluación de calidad de datos y preparación metodológica.
- En esta fase no se entrenan modelos de Machine Learning.

Entregables:

- Notebook: [`notebooks/F1_Definicion.ipynb`](notebooks/F1_Definicion.ipynb)
- Informe: [`docs/MCDI504_S1_1_GRUPO2.pdf`](docs/MCDI504_S1_1_GRUPO2.pdf)

## Fase 2 - Modelos de regresión supervisada

La segunda fase trabaja con el dataset California Housing de scikit-learn. El
objetivo es predecir `MedHouseVal`, que representa el valor mediano de las
viviendas de cada distrito censal en cientos de miles de dólares.

El análisis considera ocho variables socioeconómicas y geográficas:
`MedInc`, `HouseAge`, `AveRooms`, `AveBedrms`, `Population`, `AveOccup`,
`Latitude` y `Longitude`.

Se implementaron tres modelos obligatorios:

- Regresión Lineal Simple, utilizando `MedInc` como predictor.
- Árbol de Decisión para regresión, con profundidad seleccionada mediante una
  partición de validación interna.
- Red Neuronal MLP, entrenada con las variables estandarizadas.

Además, se incorporaron como análisis complementarios una Regresión Lineal
Multivariable y un Random Forest Regressor.

### Resultados principales

Las métricas se calcularon sobre el mismo conjunto de prueba, correspondiente
al 20 % de los datos y generado con `random_state=42`.

| Modelo | Tipo | RMSE | R2 de prueba |
|---|---|---:|---:|
| Random Forest | Complementario | 0.503 | 0.807 |
| Red Neuronal MLP | Obligatorio | 0.549 | 0.770 |
| Árbol de Decisión | Obligatorio | 0.644 | 0.683 |
| Regresión Lineal Multivariable | Complementario | 0.746 | 0.576 |
| Regresión Lineal Simple | Obligatorio | 0.842 | 0.459 |

La Red Neuronal MLP obtuvo el mejor desempeño entre los modelos obligatorios.
Random Forest alcanzó el mejor resultado global, aunque presentó una brecha
mayor entre entrenamiento y prueba. Los resultados muestran que las relaciones
entre las características de los distritos y el valor de las viviendas no son
puramente lineales.

Entregables:

- Notebook: [`notebooks/F2_Regresion.ipynb`](notebooks/F2_Regresion.ipynb)
- Informe: [`docs/MCDI504_S2_1_GRUPO2.pdf`](docs/MCDI504_S2_1_GRUPO2.pdf)

## Fase 3 - Modelos de clasificación supervisada

La tercera fase trabaja con el dataset Titanic para abordar un problema de
clasificación binaria: predecir supervivencia (`Survived`). Se implementaron
modelos obligatorios y comparativos para evaluar distintas estrategias
supervisadas.

Modelos implementados:

- K-Nearest Neighbors (`KNeighborsClassifier`)
- Árbol de Decisión (`DecisionTreeClassifier`)
- Support Vector Machine (`SVC`)
- Naive Bayes Gaussiano (`GaussianNB`)

Métricas utilizadas: exactitud (accuracy), precisión, recall, F1-score y
matriz de confusión. Las figuras y tablas se generan al ejecutar el notebook
completo con la semilla fija para reproducibilidad.

Entregables:

- Notebook: [`notebooks/F3_Clasificacion.ipynb`](notebooks/F3_Clasificacion.ipynb)
- Informe: [`docs/MCDI504_S3_ENTREGABLE_GRUPO2.pdf`](docs/MCDI504_S3_ENTREGABLE_GRUPO2.pdf)

## Entrega integrada - Regresión y redes neuronales

La entrega final integra las Fases 2 y 3 utilizando el dataset Titanic para dos
objetivos predictivos diferentes:

- **Regresión:** estimar la tarifa pagada (`fare`) mediante Regresión Lineal
  Múltiple, Árbol de Decisión, Random Forest y SVR. El ajuste de SVR se realiza
  con `GridSearchCV` y validación cruzada de cinco particiones.
- **Clasificación:** predecir la supervivencia (`survived`) mediante redes
  neuronales MLP con una, dos y tres capas ocultas.

En la ejecución reproducida, el SVR ajustado obtuvo el mejor resultado de
regresión (`RMSE=25.304`, `R²=0.5862`). La MLP de tres capas presentó el mejor
balance preliminar de clasificación (`Accuracy=0.8268`, `Recall=0.7568` y
`F1-score=0.7832`).

Entregables:

- Notebook: [`notebooks/F3_RedesNeuronales.ipynb`](notebooks/F3_RedesNeuronales.ipynb)
- Informe final: [`docs/MCDI504_F3_S03_grupo2.pdf`](docs/MCDI504_F3_S03_grupo2.pdf)

## Fase 4 - Evaluación y validación del modelo

La cuarta fase evalúa las tres arquitecturas MLP de la entrega anterior sobre
el dataset Titanic. Se utiliza una partición Hold-Out 80/20 estratificada para
comparar accuracy, precision, recall, F1-score y matrices de confusión. Además,
el MLP de una capa oculta se valida con `StratifiedKFold(k=5)` para reportar el
promedio y la variabilidad de las métricas entre folds.

El preprocesamiento se mantiene dentro de un `Pipeline` con
`ColumnTransformer`: la imputación, la codificación y el escalamiento se
ajustan únicamente con datos de entrenamiento y vuelven a ajustarse dentro de
cada fold. La ejecución reproducida utiliza `RANDOM_STATE = 42`.

Resultados Hold-Out reproducidos:

| Modelo | Accuracy | Precision | Recall | F1-score |
|---|---:|---:|---:|---:|
| MLP 1 capa oculta | 0.7821 | 0.7679 | 0.6232 | 0.6880 |
| MLP 2 capas ocultas | 0.8156 | 0.7903 | 0.7101 | 0.7481 |
| MLP 3 capas ocultas | 0.8045 | 0.7931 | 0.6667 | 0.7244 |

La validación K-Fold del MLP de una capa obtiene accuracy promedio de 0.8258
con desviación estándar de 0.0312, y F1-score promedio de 0.7563 con desviación
estándar de 0.0458. Las advertencias de convergencia quedan registradas como
limitación del experimento.

Entregables:

- Notebook ejecutado: [`notebooks/F4_Evaluacion_Sumativa.ipynb`](notebooks/F4_Evaluacion_Sumativa.ipynb)
- Informe final: [`docs/MCDI504_S4_2_GRUPO2-2.pdf`](docs/MCDI504_S4_2_GRUPO2-2.pdf)
- Dataset local: [`data/titanic.csv`](data/titanic.csv)
- Documentación del dataset: [`data/README_datos.md`](data/README_datos.md)
- Figuras: `figures/fase4_evaluacion/`

## Estructura del repositorio

```text
docs/
    MCDI504_S1_1_GRUPO2.pdf
    MCDI504_S2_1_GRUPO2.pdf
    MCDI504_S3_ENTREGABLE_GRUPO2.pdf
    MCDI504_F3_S03_grupo2.pdf
    MCDI504_S4_2_GRUPO2-2.pdf

data/
    README_datos.md
    titanic.csv

figures/
    fase1_definicion/
        Figuras generadas por F1_Definicion.ipynb
    fase2_regresion/
        Figuras generadas por F2_Regresion.ipynb
    fase3_clasificacion/
        Figuras generadas por F3_Clasificacion.ipynb
    fase3_redes_neuronales/
        Figuras generadas por F3_RedesNeuronales.ipynb
    fase4_evaluacion/
        Figuras generadas por F4_Evaluacion_Sumativa.ipynb

notebooks/
    F1_Definicion.ipynb
    F2_Regresion.ipynb
    F3_Clasificacion.ipynb
    F3_RedesNeuronales.ipynb
    F4_Evaluacion_Sumativa.ipynb

requirements.txt
```

Los notebooks F1, F2, F3 y F4 muestran cada gráfico en pantalla con `plt.show()` y,
antes de mostrarlo, guardan una copia PNG con `plt.savefig()` en su subcarpeta
correspondiente de `figures/`. Las subcarpetas se crean automáticamente al
ejecutar las celdas iniciales de cada notebook.

## Configuración del entorno

Se recomienda utilizar Python 3.10 o una versión compatible con las
dependencias del proyecto.

### macOS o Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m ipykernel install --user --name mcdi504-ml1 --display-name "Python (MCDI504 ML1)"
jupyter lab
```

### Windows PowerShell

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
python -m ipykernel install --user --name mcdi504-ml1 --display-name "Python (MCDI504 ML1)"
jupyter lab
```

Después de abrir Jupyter, seleccionar el kernel `Python (MCDI504 ML1)` y
ejecutar el notebook correspondiente mediante **Restart Kernel and Run All**.

## Reproducibilidad

Los notebooks de las Fases 2, 3 y 4 utilizan una semilla única
(`RANDOM_STATE = 42`) en las particiones y en los modelos con componentes
aleatorios. El escalamiento se ajusta exclusivamente con los datos de
entrenamiento para evitar fuga de información. Las tablas, métricas y figuras
se generan al ejecutar cada notebook completo.

## Principales tecnologías

- Python y JupyterLab
- pandas y NumPy
- Matplotlib y seaborn
- scikit-learn
- SciPy
