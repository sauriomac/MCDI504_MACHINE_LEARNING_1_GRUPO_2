# Dataset Titanic

El dataset Titanic es distribuido mediante
[`seaborn-data`](https://github.com/mwaskom/seaborn-data) y está disponible en
Python a través de `sns.load_dataset("titanic")`.

Este repositorio incluye una copia local en [`titanic.csv`](titanic.csv) para
garantizar la reproducibilidad y permitir que los notebooks se ejecuten sin
conexión a Internet. El archivo contiene 891 observaciones y 15 columnas.

`F4_Evaluacion_Sumativa.ipynb` intenta primero leer
`data/titanic.csv`. Solamente cuando el archivo local no está disponible
utiliza como respaldo el CSV público de `seaborn-data`.

Titanic corresponde al conjunto de datos utilizado durante las fases previas
del caso ABP. No se presenta como un dataset exigido específicamente por la
rúbrica; se documenta para identificar su procedencia y mantener la
trazabilidad del proyecto.
