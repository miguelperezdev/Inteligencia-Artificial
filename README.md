# Inteligencia-Artificial

## Preparar VS Code para Python y Jupyter

Esta guía configura un entorno independiente para este repositorio. No es necesario iniciar Anaconda Navigator ni abrir Jupyter en el navegador.

### Requisitos

- Python 3 instalado.
- Visual Studio Code.
- Extensiones de VS Code: **Python** (`ms-python.python`), **Pylance** (`ms-python.vscode-pylance`) y **Jupyter** (`ms-toolsai.jupyter`).

Instala las extensiones desde el panel **Extensions** de VS Code si aún no aparecen instaladas.

### Crear el entorno para un repositorio

Abre la carpeta raíz del repositorio en VS Code con **File > Open Folder**. Abre una terminal integrada y ejecuta estos comandos en Linux:

```bash
python3 --version
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

El entorno `.venv` es local a este proyecto y no debe subirse a Git. Añade `.venv/` al `.gitignore` de cada repositorio. Si un repositorio nuevo todavía no tiene `requirements.txt`, créalo con las librerías que necesite, por ejemplo:

```text
ipykernel
jupyter
numpy
pandas
matplotlib
seaborn
scipy
scikit-learn
```

Después de instalar los paquetes, registra el entorno como kernel de Jupyter. Usa un nombre único para cada proyecto:

```bash
python -m ipykernel install --user --name ia-mi-proyecto --display-name "Python (IA - mi proyecto)"
```

### Seleccionar Python y el kernel

En VS Code, ambos selectores deben apuntar al entorno `.venv`:

1. Abre la paleta de comandos con `Ctrl+Shift+P`, ejecuta **Python: Select Interpreter** y selecciona el intérprete que termina en `.venv/bin/python`.
2. Abre el archivo `.ipynb`. En el selector de kernel de la esquina superior derecha, elige **Python (IA - mi proyecto)** (o el nombre que registraste).
3. Reinicia el kernel y ejecuta las celdas.

Seleccionar el intérprete de Python no siempre cambia el kernel del notebook. Si uno apunta a `.venv` y el otro a Conda `base` o al Python del sistema, el notebook puede mostrar `ModuleNotFoundError` aunque el paquete ya esté instalado en `.venv`.

Comprueba el intérprete desde una celda del notebook:

```python
import sys
print(sys.executable)

import numpy as np
print(np.__version__)
```

La ruta impresa debe incluir `.venv/bin/python`. Si `numpy` no se importa, instala el paquete en el mismo entorno seleccionado y reinicia el kernel:

```bash
source .venv/bin/activate
python -m pip install numpy
```

También puedes instalar todas las dependencias declaradas con `python -m pip install -r requirements.txt`. Evita instalar paquetes con `sudo` o en el Python global del sistema.

### Usar el entorno en otra sesión

Cada vez que abras una terminal nueva para este repositorio, activa el entorno antes de instalar o ejecutar comandos Python:

```bash
source .venv/bin/activate
```

Para un repositorio nuevo, repite la creación del entorno y la selección del intérprete/kernel. No reutilices `.venv` entre proyectos: cada repositorio debe tener sus propias dependencias.
