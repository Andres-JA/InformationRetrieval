# Recuperación de Información

Prácticas de Recuperación de Información sobre el corpus del Proyecto Gutenberg: preprocesamiento, indexación, búsqueda booleana, representación vectorial y ranking con TF-IDF y BM25.

## Estructura

```
InformationRetrieval/
├── README.md
├── .gitignore
└── notebooks/
    ├── 01_revml.ipynb
    ├── 02_booleansearch.ipynb
    ├── 03_vectorsearch.ipynb
    ├── 04_bm25.ipynb
    └── epub/                 # corpus de Gutenberg (no versionado)
        └── <id>/pg<id>.txt
```

## Notebooks

### `01_revml.ipynb` — Repaso de Machine Learning

- Iris: análisis exploratorio y comparación de siete clasificadores con escalado, validación y matrices de confusión.
- Diabetes: comparación de modelos de regresión con MAE, RMSE y R², y análisis del efecto de Ridge y Lasso.

### `02_booleansearch.ipynb` — Procesamiento, búsqueda secuencial e indexación

- Corpus NLTK (18 libros): normalización, tokenización, búsqueda secuencial e índice invertido.
- Consultas booleanas con `AND`, `OR`, `NOT` y paréntesis.
- Corpus `epub`: deduplicación, muestra reproducible de 1.000 documentos y comparación de tiempos entre búsqueda secuencial e indexada.
- Análisis de escalabilidad con 50, 100, 250, 500 y 1.000 documentos.

### `03_vectorsearch.ipynb` — Búsqueda vectorial con TF-IDF

- Cálculo de TF, DF, IDF y los seis pesos TF-IDF.
- Matriz documento-término dispersa, verificada contra `TfidfVectorizer`.
- Similitud coseno y presentación del top-5 por consulta.
- Introducción a BM25 y comparación de sus rankings con TF-IDF.

### `04_bm25.ipynb` — BM25

- Implementación de BM25 (`k1=1.2`, `b=0.75`) y comparación con TF-IDF + coseno en ocho consultas.
- Intersección de los top-10, tamaño de las listas y primer resultado de cada método.
- Análisis del aporte de cada término (`|d|`, `f(t,d)`, `df(t)`) y efecto de los parámetros `k1` y `b`.

## Corpus `notebooks/epub/`

Contiene 78.145 archivos `pg*.txt` del Proyecto Gutenberg (unos 28 GB). Por su tamaño **no se versiona** y está incluido en `.gitignore`. Los notebooks 02–04 deduplican por título y autor y trabajan con una muestra aleatoria reproducible de 1.000 documentos (`random_state=42`), conservando el identificador original de cada libro.

## Requisitos

- Python 3.10 o superior.
- `numpy`, `pandas`, `scipy`, `scikit-learn`, `matplotlib`, `nltk` y `jupyter`.

```bash
pip install numpy pandas scipy scikit-learn matplotlib nltk jupyter
```

## Ejecución

Desde la raíz del proyecto:

```bash
jupyter notebook notebooks/04_bm25.ipynb
```

Los notebooks buscan la carpeta `epub` en el directorio de trabajo o en `notebooks/epub`, por lo que pueden ejecutarse desde la raíz o desde `notebooks/`. La primera ejecución de los notebooks 03 y 04 tarda alrededor de un minuto porque lee y tokeniza los 1.000 documentos.

## Autor

- Jairo Angulo
