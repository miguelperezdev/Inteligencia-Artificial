# Inteligencia-Artificial

![Python](https://img.shields.io/badge/python-3.13-3776AB?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-notebook-F37626?logo=jupyter&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.9-F7931E?logo=scikitlearn&logoColor=white)

Repositorio de la materia de **Inteligencia Artificial**: teoría comentada, ejemplos resueltos y prácticas de *Machine Learning* con Python y `scikit-learn`, organizadas por semana.

Cada tema vive en su propia carpeta con dos subcarpetas: `notebooks/` (material de clase y prácticas) y `data/` (datasets en local).

---

## Contenido

### [`Semana07_SVM/`](./Semana07_SVM) — Máquinas de Vectores de Soporte

| Notebook | Contenido |
|---|---|
| `0_SVM_theory_examples_v2.ipynb` | Teoría completa de SVM: margen máximo, vectores de soporte, parámetro `C`, producto punto, *kernel trick*, kernels polinómico y RBF, SVR, y **6 ejercicios resueltos** con código y explicación. |
| `1_SVM-sklearn.ipynb` | SVM con `scikit-learn` sobre datos artificiales: kernel lineal y polinómico, fronteras de decisión. |
| `2_SVM_Exercises.ipynb` | Ejercicios guiados de SVM (experimentos con distintos kernels sobre `dataset1/2/3`). |
| `Ejercicio_cancer.ipynb` | Práctica: clasificación de cáncer de mama con SVM (`sklearn.datasets.load_breast_cancer`). |

**Datos** (`Semana07_SVM/data/`): cuatro archivos `.data` en formato CSV sin encabezado (`x1, x2, etiqueta`), uno de ellos con partición `train`/`test`.

### [`Semana07_Arboles/`](./Semana07_Arboles) — Árboles de decisión y ensambles

| Notebook | Contenido |
|---|---|
| `00_intro_arboles.ipynb` | Guía de trabajo: teoría de árboles, criterios de división (Gini, entropía) e implementación del algoritmo paso a paso. |
| `01_Arboles_Churn-STUD.ipynb` | Práctica de *churn* en telefonía móvil: entendimiento de datos, árbol, evaluación, poda (overfitting) y ensambles. **Plantilla para completar** (`-STUD`). |
| `02_DSML_Ch8_Trees.ipynb` | Notas y ejemplos del capítulo de árboles del libro de referencia del curso. |
| `03_Practica_Decision_Trees.ipynb` | Práctica de *Decision Trees* con dataset de diabetes (cargado desde Kaggle). |
| `04_Random_Forest.ipynb` | Random Forest: teoría, hiperparámetros y prácticas con Iris y Car Evaluation. |
| `DecStump-Ejemplo.ipynb` | *Decision Stump*: árbol de profundidad 1 como caso base de boosting. |
| `DecisionTrees_sklearn.ipynb` | Árbol de decisión con `scikit-learn`, incluyendo EDA previa. |
| `Interactive_Decision_Tree.ipynb` | Árbol de decisión interactivo *(crédito: Michael Pyrcz, University of Texas at Austin — [GeostatsGuy](https://github.com/GeostatsGuy))*; incluye widget interactivo y dataset `unconv_MV`. |

**Datos** (`Semana07_Arboles/data/`): `01-churn.csv` (20 000 registros, separador `;`), `car_evaluation.csv` (1 728 registros, sin encabezado) y `unconv_MV.csv` (1 000 registros).

---

## Estructura del repositorio

```text
Inteligencia-Artificial/
├── README.md
├── requirements.txt          # dependencias congeladas
├── .gitignore
├── Semana07_SVM/
│   ├── notebooks/            # teoría, ejemplos y prácticas de SVM
│   └── data/                 # datasets (.data) usados por los notebooks
└── Semana07_Arboles/
    ├── notebooks/            # árboles de decisión, Random Forest, ensambles
    └── data/                 # datasets (.csv) usados por los notebooks
```

**Convenciones:**

- Los notebooks se numeran en orden de trabajo (`00_`, `01_`, `02_`, …).
- Los que terminan en **`-STUD`** son plantillas sin resolver para completar en clase.
- Los notebooks que se guardan **con salidas** muestran los resultados ya ejecutados (gráficas y tablas incluidas), de modo que se pueden leer sin levantar el entorno.
- Las rutas de datos son relativas a la carpeta del notebook (`../data/archivo.csv`), porque el kernel arranca en la carpeta donde vive el `.ipynb`.

---

## Requisitos

- **Python 3.13** (probado con `3.13.5`; debe funcionar también con 3.10 o superior).
- **Visual Studio Code** con las extensiones **Python** (`ms-python.python`), **Pylance** (`ms-python.vscode.pylance`) y **Jupyter** (`ms-toolsai.jupyter`).
- Alternativa: JupyterLab o el clásico Jupyter Notebook.

---

## Puesta en marcha

### 1. Crear el entorno

Abre la raíz del repositorio en VS Code (**File > Open Folder**) y en la terminal integrada:

```bash
python3 --version
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

El entorno `.venv` es local y **no se sube a Git** (ya está en el `.gitignore`).

### 2. Registrar el kernel de Jupyter

Usa un nombre único por proyecto para no mezclarlo con otros repositorios:

```bash
python -m ipykernel install --user --name ia-inteligencia-artificial --display-name "Python (IA)"
```

### 3. Seleccionar intérprete **y** kernel

En VS Code ambos selectores deben apuntar a `.venv`:

1. `Ctrl+Shift+P` → **Python: Select Interpreter** → el que termina en `.venv/bin/python`.
2. Al abrir el `.ipynb`, en el selector superior derecho → **Python (IA)**.
3. Reinicia el kernel y ejecuta las celdas.

> ⚠️ Seleccionar el intérprete **no siempre** cambia el kernel del notebook. Si uno apunta a `.venv` y el otro a Conda `base` o al Python del sistema, aparecerá `ModuleNotFoundError` aunque el paquete esté instalado.

Comprueba el entorno desde una celda:

```python
import sys
print(sys.executable)   # debe incluir .venv/bin/python

import numpy, sklearn
print(numpy.__version__, sklearn.__version__)
```

Si falta un paquete:

```bash
source .venv/bin/activate
python -m pip install <paquete>
```

Evita instalar paquetes con `sudo` o en el Python global del sistema, y **no reutilices `.venv` entre proyectos**.

### 4. En cada sesión nueva

```bash
source .venv/bin/activate
```

---

## Trabajando con Git

- **Antes de commitear**, revisa que el notebook abra sin errores y que las salidas sean las esperadas.
- Los diffs de `.ipynb` en JSON son difíciles de leer; instala [`nbdime`](https://nbdime.readthedocs.io/) para diffs y merges legibles:

```bash
source .venv/bin/activate
python -m pip install nbdime
nbdime config-git --enable
```

- Los `.zip` del material original están ignorados: la data y los notebooks ya viven descomprimidos en cada carpeta.

---

## Material y créditos

Este repositorio reúne **material académico de las clases** de Inteligencia Artificial (apuntes, ejemplos y prácticas), junto con notebooks de terceros debidamente identificados (`Interactive_Decision_Tree.ipynb`).

**El repositorio no se publica con licencia abierta.** Si quieres usar, copiar o modificar su contenido, pide permiso previamente.

---

## Referencias

- Cortes, C., & Vapnik, V. (1995). *Support-vector networks*. Machine Learning.
- Bishop, C. M. (2006). *Pattern Recognition and Machine Learning*, Cap. 7.
- Documentación de [scikit-learn](https://scikit-learn.org/stable/modules/svm.html).
