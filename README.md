# Recuperación de Información

Prácticas de Recuperación de Información sobre el corpus de libros del Proyecto Gutenberg. El repositorio reúne tres notebooks que recorren, de forma progresiva, el preprocesamiento de texto, la indexación, la búsqueda booleana, la representación vectorial y el ranking de documentos.

## Estructura del proyecto

```
InformationRetrieval/
├── README.md
├── .gitignore
└── notebooks/
    ├── 01_revml.ipynb
    ├── 02_booleansearch.ipynb
    ├── 03_vectorsearch.ipynb
    └── epub/                 # corpus de Gutenberg (no versionado)
        └── <id>/pg<id>.txt
```

## Notebooks

### `01_revml.ipynb` — Repaso práctico de Machine Learning

Repasa los fundamentos de Machine Learning antes de entrar en Recuperación de Información.

- Explora el dataset Iris y presenta una tabla y un gráfico de distribución de clases.
- Compara siete clasificadores (Naive Bayes, regresión logística, SVM lineal, árbol, Random Forest, Gradient Boosting y MLP) con particiones de entrenamiento, validación y prueba.
- Usa escalamiento ajustado solo con entrenamiento, matrices de confusión y análisis de errores.
- Compara modelos de regresión sobre el dataset Diabetes (lineal, Ridge, Lasso, kNN, árbol, Random Forest, Gradient Boosting y MLP) con MAE, RMSE y R², gráficos de valores reales frente a predicciones y residuos.
- Analiza el efecto de la regularización en Ridge y Lasso y responde preguntas de interpretación.

### `02_booleansearch.ipynb` — Procesamiento de texto, recuperación secuencial e indexación

Implementa y compara dos mecanismos de recuperación sobre libros de Project Gutenberg.

- **Parte A (corpus pequeño):** carga los 18 documentos de Gutenberg incluidos en NLTK, define una configuración de normalización y tokenización, implementa búsqueda secuencial con dos lazos anidados y mide tiempos con 30 repeticiones.
- Construye un índice invertido, inspecciona listas de postings y calcula la frecuencia documental (DF) de varios términos.
- Implementa consultas booleanas con `AND`, `OR`, `NOT` y paréntesis.
- **Parte B (corpus grande):** trabaja con los archivos `pg*.txt` de `notebooks/epub/`, deduplica por título y autor, toma una muestra reproducible de 1.000 documentos (`random_state=42`) y repite las búsquedas secuenciales y con índice.
- **Parte C:** analiza la escalabilidad con subconjuntos de 50, 100, 250, 500 y 1.000 documentos, ajusta funciones de tiempo por mínimos cuadrados y compara los dos métodos.

### `03_vectorsearch.ipynb` — Búsqueda vectorial con TF-IDF y BM25

Construye representaciones vectoriales y rankings sobre el corpus `epub`, reutilizando el preprocesamiento y la muestra de la práctica 02.

- Recupera y revisa el corpus: tabla de **identificador, título y número de términos únicos**, número de documentos, tamaño del vocabulario y longitudes mínima, media y máxima.
- Implementa explícitamente TF, DF, IDF y los seis pesos TF-IDF (TF `raw`, `log`, `augmented` × IDF clásica y `+1`).
- Construye la matriz documento-término TF-IDF en formato disperso y la verifica contra `TfidfVectorizer` (máxima diferencia absoluta `0.0`).
- Define cuatro consultas, construye sus vectores con el vocabulario y los IDF del corpus y calcula la similitud coseno mediante producto punto y normas, comparándola con `sklearn.metrics.pairwise.cosine_similarity`.
- Presenta el top-5 de cada consulta con identificador, título, puntuación y fragmento del texto original.
- Implementa BM25, explica sus componentes (`k1`, `b`, IDF y normalización por longitud) y compara sus rankings con los de TF-IDF.

## Corpus `notebooks/epub/`

La carpeta `notebooks/epub/` contiene 78.145 archivos `pg*.txt` descargados del Proyecto Gutenberg (unos 28 GB). Por su tamaño **no se versiona**: está incluida en `.gitignore`. Los notebooks 02 y 03 la leen directamente desde disco, deduplican por título y autor y trabajan con una muestra aleatoria reproducible de 1.000 documentos para que los experimentos sean tratables en memoria. Cada documento conserva su identificador original de Gutenberg.

## Requisitos

- Python 3.10 o superior.
- `numpy`, `pandas`, `scipy`, `scikit-learn`, `matplotlib`, `nltk` y `jupyter`.

Instalación sugerida:

```bash
pip install numpy pandas scipy scikit-learn matplotlib nltk jupyter
```

## Cómo ejecutar

Desde la raíz del proyecto:

```bash
jupyter notebook notebooks/03_vectorsearch.ipynb
```

Los notebooks 02 y 03 buscan la carpeta `epub` tanto en el directorio de trabajo como en `notebooks/epub`, por lo que pueden ejecutarse desde la raíz del proyecto o desde la carpeta `notebooks/`. La primera ejecución del notebook 03 tarda alrededor de un minuto porque lee y tokeniza los 1.000 documentos; las siguientes celdas trabajan con la representación dispersa ya construida.

## Autor

- Jairo Angulo
