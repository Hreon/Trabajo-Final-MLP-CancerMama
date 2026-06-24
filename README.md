# Clasificación de tumores mamarios con un Perceptrón Multicapa

Proyecto del curso **Agentes Inteligentes / Análisis y Visualización de Datos** (USIL).
Equipo **«Monos»**: Ryan Patrick Medina Torres · Fabian Felipe Roncal Falconi · Sergio Martin Sanchez Balvin · Alexis Ivan Villegas Sulca.

Clasifica tumores mamarios como **malignos** o **benignos** sobre el conjunto público
*Breast Cancer Wisconsin (Diagnostic)* (569 muestras, 30 características) usando una
**Red Neuronal Artificial (Perceptrón Multicapa)** y un modelo base de comparación
(regresión logística).

## Requisitos

- Python 3.10 o superior.

## Instalación

```bash
pip install -r requirements.txt
```

## Ejecución

Desde la carpeta `codigo/`:

```bash
python main.py
```

Esto entrena el modelo, imprime las métricas en consola y genera las figuras
(matriz de confusión, curva ROC y curva de pérdida) en la carpeta `figuras/`.

## Pruebas

```bash
python tests/test_pipeline.py
# o, si tienes pytest instalado:
python -m pytest -q
```

## Estructura del proyecto

```
codigo/
├── main.py                 # punto de entrada
├── requirements.txt        # dependencias
├── README.md
├── src/
│   ├── data_loader.py      # carga del dataset
│   ├── preprocessor.py     # estandarización + split estratificado
│   ├── strategies.py       # patrón Strategy: MLP y regresión logística
│   ├── model_factory.py    # patrón Factory: creación de modelos
│   ├── evaluator.py        # métricas y figuras
│   └── pipeline.py         # patrón Facade: orquesta el flujo
└── tests/
    └── test_pipeline.py    # prueba mínima
```

## Patrones de diseño aplicados

- **Strategy** — los clasificadores (`MLPStrategy`, `LogisticStrategy`) comparten la
  interfaz `ClassifierStrategy` y son intercambiables.
- **Factory** — `ModelFactory.create("mlp" | "logistic")` centraliza su creación.
- **Facade** — `Pipeline.run()` ofrece una interfaz simple sobre todo el subsistema.

## Resultados de referencia

| Métrica | MLP | Regresión Logística |
|---------|-----|---------------------|
| Exactitud (prueba) | ~95.6 % | ~98.2 % |
| Sensibilidad (recall) | ~94.4 % | — |
| Valor F1 | ~96.5 % | — |
| AUC (ROC) | ~0.994 | — |
| Validación cruzada (5-fold) | ~97.9 % ± 0.9 % | — |

> Los valores pueden variar ligeramente según la versión de las librerías.
