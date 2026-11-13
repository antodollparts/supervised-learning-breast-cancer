# Comparación de algoritmos de aprendizaje supervisado: KNN, SVM y MLP

Práctica de clasificación de tumores de mama (benignos vs. malignos) que implementa y compara tres algoritmos de aprendizaje supervisado sobre un mismo conjunto de datos y una misma división de entrenamiento y prueba.

# Comparación de algoritmos de aprendizaje supervisado: KNN, SVM y MLP

Práctica de clasificación de tumores de mama (benignos vs. malignos) que implementa y compara tres algoritmos de aprendizaje supervisado sobre un mismo conjunto de datos y una misma división de entrenamiento y prueba.

## Objetivo

Comprender las diferencias entre K-Nearest Neighbors (KNN), Support Vector Machine (SVM) y una red neuronal artificial (MLP), evaluar su rendimiento y determinar cuál ofrece mejores resultados para un problema de clasificación médica.

## Dataset

**Breast Cancer Wisconsin (Diagnostic)** — archivos `wdbc.data` y `wdbc.names`.

| Característica | Valor |
|---|---|
| Registros | 569 |
| Variables predictoras | 30 (10 medidas del núcleo celular × media, error estándar y peor valor) |
| Variable objetivo | `diagnosis` |
| Clases | Benigno (B): 357 · Maligno (M): 212 |
| Valores nulos | 0 |

La columna `id` se descarta por no aportar información predictiva. Para el modelado, la clase **Maligno** se codifica como `1` (clase positiva) y **Benigno** como `0`.

## Metodología

1. **Carga y exploración:** inspección de registros, variables, balance de clases y valores nulos.
2. **Separación** de características (`X`) y variable objetivo (`y`).
3. **División** 80 % entrenamiento / 20 % prueba, con `random_state=42` y estratificación por clase. La misma división se usa para los tres modelos.
4. **Preprocesamiento:** estandarización con `StandardScaler`, ajustado únicamente con los datos de entrenamiento para evitar fuga de información.
5. **Entrenamiento** de los tres modelos con búsqueda de hiperparámetros (`GridSearchCV`, validación cruzada de 5 pliegues):
   - KNN: número de vecinos y tipo de ponderación.
   - SVM: parámetro `C`, kernel y `gamma`.
   - MLP: arquitectura de capas ocultas, función de activación y regularización `alpha`.
6. **Evaluación** sobre el mismo conjunto de prueba con exactitud, precisión, exhaustividad, F1-score y matriz de confusión.
7. **Comparación** mediante tabla y gráficas, e interpretación de resultados.

## Resultados

> Completar con los valores obtenidos en el notebook.

| Modelo | Accuracy | Precision | Recall | F1-score | Falsos positivos | Falsos negativos |
|---|---|---|---|---|---|---|
| KNN | 0.9386 | 0.973 | 0.8571 | 0.9114 | 1 | 6 |
| SVM | 0.9737 | 1.000 | 0.9286 | 0.9630 | 0 | 3 |
| MLP | 0.9737 | 1.000 | 0.9286 | 0.9630 | 0 | 3 |

## Conclusiones

- **Mejor rendimiento:** SVM y MLP empataron (accuracy 0.9737, F1 0.9630) y acertaron 111 de 114 casos. KNN quedó por debajo (accuracy 0.9386).
- **Más errores:** KNN, con 7 errores, de los cuales 6 fueron falsos negativos (tumores malignos clasificados como benignos). Su recall de la clase maligna fue de 0.8571.
- **Diferencias de comportamiento:** KNN no entrena un modelo, solo compara cada caso con sus vecinos más cercanos, y es sensible a la escala de los datos. SVM busca la frontera de margen máximo y es estable en datasets pequeños. MLP aprende patrones no lineales, pero depende de la inicialización y de más hiperparámetros.
- **Elección del modelo:** en diagnóstico médico la exactitud no basta: un falso negativo retrasa el tratamiento de un paciente con cáncer, así que se prioriza el recall de la clase maligna. SVM y MLP tienen la mayor exactitud y también el menor número de falsos negativos (3). Elegimos **SVM** porque, con el mismo desempeño, necesita menos hiperparámetros y no depende de la inicialización aleatoria. Ningún modelo eliminó por completo los falsos negativos, así que en un uso real convendría ajustar el umbral de decisión para aumentar el recall.

## Estructura del repositorio

```
.
├── notebook.ipynb      # Notebook de Google Colab con la práctica completa
├── data/
│   ├── wdbc.data
│   └── wdbc.names
└── README.md
```

## Cómo ejecutar

1. Abrir `notebook.ipynb` en [Google Colab](https://colab.research.google.com/).
2. Subir `wdbc.data` y `wdbc.names` al panel de archivos (o ajustar la ruta si se monta Google Drive).
3. Ejecutar: `Entorno de ejecución → Ejecutar todo`.

## Tecnologías

Python · pandas · NumPy · scikit-learn · matplotlib · seaborn · Google Colab

## Integrantes del Equipo

* **Antonella Junco** - [@antodollparts](https://github.com/antodollparts/)
* **Amerika Carbajal** - [@Amerikita](https://github.com/Amerikita)
* **Victor Canché** - [@usuario3](https://github.com/victor332-af)
* **Diego Alexander** - [@DiegoMarin025](https://github.com/DiegoMarin025)
* **Leobardo Mex** -[@YondaimeMex](https://github.com/YondaimeMex)
